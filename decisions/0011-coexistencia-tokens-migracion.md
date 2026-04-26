# 0011 — Coexistencia gradual de tokens BaW: legado HEX y canónico OKLCH

**Fecha**: 2026-04-26
**Estado**: Accepted
**Autor**: Fran Durán
**Decisión**: Coexistencia gradual de los tokens HEX legacy (`--baw-*`) y los tokens OKLCH canónicos (`--brand-*`, `--agent-*`) en `baw-os`. Migración componente por componente, no big-bang.

---

## Contexto

Al momento de conectar `baw-design` (sistema canónico) con `baw-os` (producto vivo), encontramos dos sistemas paralelos:

**Sistema legacy en `baw-os/src/app/globals.css`:**
- Variables `--baw-bg`, `--baw-surface`, `--baw-elevated`, `--baw-border`, `--baw-text`, `--baw-muted`, `--baw-faint`, `--baw-primary`, `--baw-agent`, `--baw-agent-subtle`, `--baw-success`, `--baw-warning`, `--baw-danger`
- Color space: HEX
- Convención: `--baw-{rol}`
- En producción, alimentando todos los componentes

**Sistema canónico en `baw-design/tokens/`:**
- Variables `--brand-50..950`, `--agent-50..950`, neutrals semánticas, tipografía, espaciado
- Color space: OKLCH (ver ADR 0003)
- Convención: `--{escala}-{step}`
- Sin uso real en producción todavía

Forzar reemplazo big-bang significaría reescribir toda la `globals.css` y tocar cada componente que dependa de `--baw-*`. Riesgo de regresión visual masivo, sin tests visuales automáticos.

## Decisión

### 1. Submodule

`baw-design` se conecta a `baw-os` como `git submodule` en `design/baw-design/` (carpeta `design/` permanece dedicada exclusivamente a ese submódulo).

### 2. Import al inicio de `globals.css`

```css
@import "../../design/baw-design/tokens/index.css";
@tailwind base;
@tailwind components;
@tailwind utilities;
```

Esto hace que las variables canónicas (`--brand-*`, `--agent-*`, etc.) estén disponibles en todo el árbol del DOM antes de que se procesen las clases de Tailwind y los `--baw-*` legacy.

### 3. Variables legacy permanecen sin cambio

Las definiciones existentes de `--baw-bg`, `--baw-primary`, etc. en `:root`, `html.light` y `aside[data-sidebar]` quedan intactas. Los componentes en producción siguen funcionando sin tocar nada.

### 4. Migración por componente

Cuando un componente entra al pipeline de actualización (por feature work, bug, o limpieza), se migra de `var(--baw-*)` a `var(--brand-*)` o equivalente canónico. Cada migración es un commit aislado, con visual diff manual.

### 5. Deprecation gradual

Cada `--baw-*` se considera deprecated desde la fecha de este ADR. No se introducen nuevos usos. Solo migración hacia afuera.

## Mapeo de tokens (referencia para migración)

| Legacy (`--baw-*`) | Canónico (`baw-design`) | Notas |
|---|---|---|
| `--baw-primary` | `--brand-500` | Hue 266 OKLCH |
| `--baw-agent` | `--agent-500` | Hue 300 OKLCH |
| `--baw-agent-subtle` | `--agent-100` con alpha | Reescribir como `oklch(... / 0.10)` |
| `--baw-bg` | `--neutral-950` (dark) / `--neutral-50` (light) | Confirmar contraste |
| `--baw-surface` | `--neutral-900` / `--neutral-100` | Idem |
| `--baw-elevated` | `--neutral-850` / `--neutral-150` | Idem |
| `--baw-border` | `--neutral-800` / `--neutral-200` | Idem |
| `--baw-text` | `--neutral-100` / `--neutral-900` | Idem |
| `--baw-muted` | `--neutral-400` / `--neutral-500` | Idem |
| `--baw-faint` | `--neutral-600` / `--neutral-400` | Idem |
| `--baw-success` | `--success-500` | A crear en baw-design |
| `--baw-warning` | `--warning-500` | A crear en baw-design |
| `--baw-danger` | `--danger-500` | A crear en baw-design |

⚠️ **Las escalas semánticas `success/warning/danger` en OKLCH aún no existen en `baw-design/tokens/colors.css`.** Hay que crearlas antes de migrar componentes que las consumen (`badge-paid`, `badge-late`, `badge-pending`, `btn-danger`).

## Consecuencias

### Positivas
- Cero downtime, cero regresión visual el día del submodule
- Permite trabajar en features de `baw-os` sin bloqueo
- Migración incremental, auditada, con commits chicos
- Los developers nuevos ven ambos sistemas y eligen el canónico para código nuevo

### Negativas
- Período de "doble verdad" donde existen dos sistemas vivos
- Riesgo de que la migración se estanque si no se prioriza
- Requiere disciplina: no introducir `--baw-*` nuevos
- El ADR es solo documentación; no hay enforcement automático

### Mitigación
- Lint rule futura: warn si código nuevo usa `--baw-*` (post-migración parcial)
- Tracking en `decisions/MIGRATION_STATUS.md` con conteo de usos de `--baw-*` que decrece con cada commit
- Al cerrar Fase 1, evaluar si la coexistencia debe terminar o continuar

## Criterio de cierre de coexistencia

La coexistencia termina cuando:
1. `grep -r "--baw-" baw-os/src/` retorna 0 resultados
2. Las definiciones de `--baw-*` se eliminan de `globals.css`
3. Se actualiza este ADR a estado "Superseded by ADR XXXX"

Estimación realista: 4-8 semanas si la migración se ataca como track paralelo a feature work, 12+ semanas si solo se hace cuando "toca el componente".

## Notas operativas

- **Branch protection**: cuando se establezca, agregar regla de que cambios a `globals.css` requieran revisión.
- **CI**: futuro check de uso de `--baw-*` con regex; reportar tendencia, no bloquear.
- **Documentación**: este ADR es la fuente de verdad. Cualquier comunicación interna sobre tokens debe referenciar este número (0011).
