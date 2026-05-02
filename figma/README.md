# Figma — BaW Design System

Archivo oficial de revisión visual:

https://www.figma.com/design/1sY3Gd9UUCY3nnFFFu5MxJ/BaW-OS-Design-system

## Rol de Figma

Figma es la mesa visual de decisión. Se usa para:

- comparar exploraciones de logo/mark/wordmark
- revisar paleta, tipografía y componentes
- comentar y aprobar dirección visual
- preparar referencias para colaboradores externos

Figma **no** es el source of truth técnico de producción.

## Source of truth

El repo `baw-design` manda para producción:

- `tokens/*.css` — tokens canónicos
- `assets/` — exports aprobados
- `BRAND_FOUNDATIONS.md` — fundamentos de marca/producto
- `decisions/` — ADRs de decisiones importantes
- `visual-review/` — galería navegable de revisión

## Workflow

```text
Figma = decisiones visuales
baw-design = assets/tokens/documentación aprobada
baw-os = implementación de producto
```

1. Se explora o comenta en Figma.
2. Fran aprueba una dirección visual.
3. Se exportan assets finales al repo.
4. Se actualizan tokens/documentación/ADRs.
5. `baw-os` consume la versión aprobada.

## Regla práctica

Si todavía está en discusión, vive en Figma o `references/`.
Si ya fue aprobado, vive en `assets/`, `tokens/`, `BRAND_FOUNDATIONS.md` o `decisions/`.
