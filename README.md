# baw-design

> Sistema de marca y diseño de **BaW**. Source of truth para tipografía, color, logos, voz, principios y aplicaciones.

**Mantenido por:** Fran Duran (founder) · ZXY Ventures
**Estado:** Fase 0 — fundaciones
**Última actualización:** abril 2026

---

## Qué hay aquí

Este repo es la **fuente única de verdad** del sistema de marca y diseño de BaW. Todos los productos y aplicaciones BaW (empezando por `baw-os`) consumen tokens, lineamientos y assets desde aquí.

```
baw-design/
├── README.md                      ← estás aquí
├── BRAND_FOUNDATIONS.md           ← documento madre (léelo primero)
├── tokens/                        ← design tokens en CSS
│   ├── colors.css
│   ├── typography.css
│   ├── spacing.css
│   └── index.css                  ← entry point (importar este)
├── assets/
│   ├── logos/                     ← SVG, AI, PDF (cuando se vectoricen)
│   └── screenshots/               ← referencias visuales
├── references/
│   └── claude-design-v1/          ← exploraciones iniciales (read-only)
├── decisions/                     ← ADRs (Architecture Decision Records)
└── scripts/                       ← utilidades (cuando lleguen)
```

---

## Cuándo abrir este repo

| Quieres… | Vas a… |
|---|---|
| Entender la marca BaW | Leer `BRAND_FOUNDATIONS.md` |
| Cambiar un color, tipografía, espaciado | Editar `tokens/*.css` |
| Agregar el logo vectorizado | Subirlo a `assets/logos/` |
| Documentar una decisión estratégica | Crear un ADR en `decisions/` |
| Ver inspiración histórica | Abrir HTMLs en `references/claude-design-v1/` |

---

## Cómo se consume este repo desde otros proyectos

Este repo se incluye como **Git submodule** en cada app que lo necesita. Hoy: `baw-os`.

### Setup inicial en una app consumidora (solo una vez)

Desde la raíz de la app (ej. `~/Developer/zxy-ventures/baw-os`):

```bash
git submodule add git@github.com:zxy-ventures/baw-design.git design
git commit -m "chore: add baw-design as submodule"
```

Esto crea una carpeta `design/` que es un puntero a un commit específico de `baw-design`. La app consumidora elige cuándo actualizar.

### Importar tokens

En `globals.css` o equivalente:

```css
@import "../design/tokens/index.css";
```

O en JS/TS:

```ts
import "@/design/tokens/index.css";
```

### Aplicar modo claro/oscuro

Agregar la clase `.mode--light` o `.mode--dark` al `<html>` o un contenedor. Los tokens semánticos (`--bg`, `--surface`, `--text`, etc.) cambian automáticamente.

---

## Cómo subir cambios a `baw-design`

### Cambio pequeño (token, copy, doc)

```bash
cd ~/Developer/zxy-ventures/baw-design

# 1. Editar archivo en Cursor/VS Code
# 2. Verificar visualmente abriendo references/claude-design-v1/System Sheet.html

git add .
git commit -m "fix(typography): remove italic from display font"
git push origin main
```

### Cambio mediano o estructural (paleta, taxonomía de tokens, ruta de archivos)

```bash
cd ~/Developer/zxy-ventures/baw-design

git checkout -b refactor/new-brand-color
# editar archivos…
git add .
git commit -m "refactor(color): change brand hue from 266 to 240"
git push origin refactor/new-brand-color
# abrir Pull Request en GitHub, revisar, mergear
```

### Cambio estratégico (decisión de marca, principios, voz)

1. Crear ADR en `decisions/NNNN-titulo.md` antes de tocar código
2. Esperar criterio (si hay más de un stakeholder)
3. Aplicar cambios en `BRAND_FOUNDATIONS.md` y tokens
4. Commit con referencia al ADR: `git commit -m "feat(voice): adopt warmer tone (ADR-0007)"`

---

## Cómo bajar cambios a una app consumidora

Desde la app (ej. `baw-os`):

```bash
cd ~/Developer/zxy-ventures/baw-os

# Jalar la última versión del submodule
git submodule update --remote --merge design

# Verificar que funciona
npm run dev

# Si todo bien, commit el bump del submodule
git add design
git commit -m "chore: bump design submodule"
git push
```

El bump del submodule registra qué commit específico de `baw-design` está usando la app. Esto es **versionado de facto** — cada commit de la app sabe exactamente qué versión del sistema de diseño usa.

---

## Cómo revertir un cambio

```bash
cd ~/Developer/zxy-ventures/baw-design
git log --oneline -10                # ver historia reciente
git revert <commit-sha>               # revierte ese commit creando uno nuevo
git push
```

En la app consumidora, basta con `git submodule update --remote --merge design` para jalar la versión revertida.

---

## Dependencias externas

- **Fuentes:** Inter (rsms.me), IBM Plex Mono (Google Fonts), Instrument Serif (Google Fonts). Todas open source / libres.
- **Herramientas de diseño:**
  - Figma — diseño digital (UI, mocks, web)
  - Adobe Illustrator — logo master vectorial, signage, vehicular
  - Adobe InDesign — print complejo, papelería multi-página
- **Hosting de assets pesados:** TBD (probable: Vercel Blob o R2)

---

## Siguientes pasos (Fase 1)

- [ ] Vectorizar el logo BaW final (Figma o Illustrator)
- [ ] Subir variantes a `assets/logos/`
- [ ] Configurar `baw-os` como submodule consumer
- [ ] Aplicar tokens en una pantalla real de `baw-os`
- [ ] Crear `baw-landing` y aplicar el sistema
- [ ] Decidir paleta y voz de "powered by BaW" para edificios

---

## Convenciones

- **Commits:** Conventional Commits (`feat`, `fix`, `docs`, `refactor`, `chore`). Scope opcional: `(color)`, `(typography)`, `(voice)`, etc.
- **ADRs:** numeración incremental, formato `NNNN-titulo-en-kebab-case.md`
- **Branches:** `feat/`, `fix/`, `refactor/`, `docs/`
- **Idioma:** documentos en español; nombres de archivos, tokens y código en inglés.

---

## Licencia

Privado. © ZXY Ventures, 2026. Todos los derechos reservados.
