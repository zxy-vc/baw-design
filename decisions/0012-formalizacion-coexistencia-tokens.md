# 0012 — Formalización de la capa de compatibilidad HEX → OKLCH

**Fecha**: 2026-04-26
**Estado**: Accepted
**Autor**: Fran Durán
**Decisión**: Formalizar la capa de aliases que mapea los tokens legacy `--baw-*` (HEX) al sistema canónico OKLCH (`--brand-*`, `--agent-*`, neutrals semánticas), y declarar oficialmente cómo se borra cada alias.

> Este ADR **no introduce** la coexistencia. La coexistencia se decidió en el ADR 0011. Este documento formaliza la forma exacta en que la capa de compatibilidad existe en código y cuándo cada alias muere.

---

## Contexto

Después del ADR 0011 quedó habilitada la coexistencia, pero sin reglas operativas explícitas:

1. ¿Dónde vive físicamente el archivo de aliases?
2. ¿Cómo se sabe si un alias todavía se usa?
3. ¿Cuál es el criterio para borrar un alias?
4. ¿Qué pasa si alguien introduce un nuevo `--baw-*` por accidente?

Sin reglas, la "coexistencia gradual" se vuelve permanente. La deuda no se paga, se acumula.

## Decisión

### 1. La capa de compatibilidad vive en un solo archivo

```
baw-os/src/app/_compat-baw-tokens.css
```

Ese archivo:
- Importa los tokens canónicos desde el submodule (`@import "../../baw-design/tokens/index.css"`).
- Define `--baw-*` como **aliases** de los tokens canónicos correspondientes (`var(--brand-500)`, `var(--neutral-bg)`, etc.).
- Tiene un comentario por bloque indicando **fecha de adición** y **fecha esperada de borrado**.

Ejemplo:

```css
/* _compat-baw-tokens.css */
@import "../../baw-design/tokens/index.css";

:root {
  /* Added 2026-04-26 · Sunset target: 2026-08 (después de Sprint 6) */
  --baw-bg: var(--neutral-bg);
  --baw-surface: var(--neutral-surface);
  --baw-text: var(--neutral-text);
  --baw-primary: var(--brand-500);
  --baw-agent: var(--agent-500);
  /* ... */
}
```

### 2. Inventario público y vivo

Cada alias activo se registra en `baw-design/references/legacy-tokens-inventory.md` con:

| Alias | Mapea a | Usos en código (grep count) | Sunset target | Componentes pendientes |
|---|---|---|---|---|

El inventario se actualiza manualmente al cerrar sprint. Un script en `baw-design/scripts/` (futuro) puede automatizar el conteo.

### 3. Criterio de borrado

Un alias `--baw-X` se elimina cuando se cumplen **las tres** condiciones:

1. `grep -R "var(--baw-X)" baw-os/src` no devuelve resultados.
2. La PR que cierra el último uso pasa visual review (manual hoy, automatizado después).
3. Se actualiza el inventario para registrar el alias como **retired** con fecha.

Borrar un alias **antes** de cumplir las tres condiciones es bloqueante en code review.

### 4. Prohibición de nuevos `--baw-*`

A partir de este ADR, **introducir un nuevo `--baw-*` token es una regresión**. Para casos donde se necesite un token semántico nuevo (ej: `--brand-accent-soft`), el flujo es:

1. Agregar token canónico en `baw-design/tokens/`.
2. Consumirlo directamente desde el componente (sin alias `--baw-*`).
3. Si y solo si un componente legacy ya escrito con `--baw-*` lo necesita, agregar alias **temporal** con sunset explícito ≤ 1 sprint.

### 5. Naming canónico (sin alias)

Para componentes nuevos (Sprint 1 en adelante), está prohibido usar `--baw-*`. Solo tokens canónicos:

- Color marca → `var(--brand-*)`
- Color agente → `var(--agent-*)`
- Fondos / superficies / texto → tokens neutrals semánticos (`--neutral-bg`, `--neutral-surface`, `--neutral-text`, etc.).
- Estados (success / warning / danger) → tokens semánticos canónicos.

### 6. Migración sigue siendo componente por componente

Esta es **la regla del ADR 0011 reafirmada**: nunca un sweep masivo. Cada PR migra 1-3 componentes, valida visualmente, y registra cambios en inventario.

---

## Consecuencias

**Positivas**
- La coexistencia tiene fecha de muerte explícita por alias, no es indefinida.
- Inventario público hace visible la deuda — todos saben cuántos `--baw-*` quedan.
- Imposible introducir nueva deuda por descuido (queda bloqueante en review).
- Componentes nuevos nacen en el sistema canónico desde el día uno.

**Negativas**
- Mantener inventario es trabajo manual hasta que llegue el script.
- Code reviewers tienen que recordar la regla de prohibición de nuevos `--baw-*` (mitigado con linter futuro).

**Riesgos**
- Si nadie cierra sprints con migración real, los aliases sobreviven a sus sunset targets. Mitigación: cada sprint review revisa el inventario y mueve fechas o cierra deuda.

---

## Estado de implementación

- [x] Submodule `baw-design` conectado en `baw-os` (commit `bb4da45`).
- [ ] Archivo `_compat-baw-tokens.css` creado y sustituye bloque inline en `globals.css`. (pendiente Sprint 1)
- [ ] Inventario inicial publicado en `baw-design/references/legacy-tokens-inventory.md`. (pendiente Sprint 1)
- [ ] Primer componente migrado de `--baw-*` a canónico. (pendiente Sprint 1 — empezar por `AgentBadge` en `status.tsx`)

---

## Referencias

- ADR 0011 — Coexistencia gradual de tokens BaW
- ADR 0003 — Espacio de color OKLCH
- ADR 0004 — Brand hue 266
- ADR 0005 — Agent identity color
