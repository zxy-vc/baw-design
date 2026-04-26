# ADR 0002 — Stack tipográfico: Inter + IBM Plex Mono + Instrument Serif

## Estado

**Accepted** — Mayo 2026

---

## Contexto

BaW OS necesita un sistema tipográfico que sirva tres contextos radicalmente distintos:

1. **Interfaz operativa densa** (operations dashboard, tablas de contratos, audit log): requiere máxima legibilidad a 12–14px, numerales tabulares alineados, distinción clara entre glifos similares (`1`, `l`, `I`; `0`, `O`).

2. **Datos técnicos e identidad de sistema** (IDs, timestamps, agent labels, terminales): requiere voz técnica que señale visualmente que este dato es exacto, inmutable, generado por el sistema.

3. **Momentos editoriales y marketing** (landing site, portadas de reportes para owners, onboarding): requiere calidez, calidad editorial, contraste con la voz operativa del producto.

Un sistema de un solo typeface no puede servir estos tres contextos sin comprometer alguno. Un sistema de más de tres typefaces introduce complejidad sin beneficio.

Las referencias visuales del producto (Linear, Stripe, Palantir) usan sistemas tipográficos con roles muy claros entre fuentes de UI, datos tabulares y display.

Los tokens de tipografía están en `/tokens/typography.css`. Los archivos de exploración en `/references/claude-design-v1/System Sheet.html` muestran la triada tipográfica ya aplicada.

---

## Decisión

Se adopta una **triada tipográfica con roles no intercambiables**:

### Inter — Voz del sistema

**Rol:** UI, navegación, body copy, labels, badges, cualquier texto operativo en el producto.

**Por qué:**
- x-height alta y glifos distintivos: legible a 12px en contextos densos
- `font-variant-numeric: tabular-nums` disponible nativamente
- Distinción clara entre `1`, `l`, `I` y entre `0`, `O` — crítico para un sistema que muestra muchos IDs y valores
- Variable font: cubre todos los pesos sin cargar múltiples archivos
- Diseñada explícitamente para pantallas — sin compromisos de legibilidad por adaptación de diseño impreso
- Licencia libre (SIL Open Font License)
- Usada por Linear, Vercel, Notion y otros referentes del ecosistema — señal de que el mercado objetivo la reconoce como "producto serio"

**Pesos usados:** 400 (regular), 500 (medium), 600 (semibold). No usar 700+ en interfaces operativas — reservar para marketing.

### IBM Plex Mono — Voz técnica

**Rol:** IDs de sistema, timestamps, datos tabulares de precisión, labels de categoría técnica en mayúsculas, terminales y audit logs en modo debug.

**Por qué:**
- Rol semántico claro: cuando aparece IBM Plex Mono, el usuario sabe que ese dato es técnico, exacto, generado por el sistema
- Diseñada por IBM para interfaces de datos e ingeniería — coherente con el posicionamiento de BaW OS
- Monospace verdadera: columnas de datos se alinean naturalmente
- Distinguible visualmente de Inter: contraste tipográfico claro, no sutil
- Compatible en peso y densidad óptica con Inter a los mismos tamaños de texto
- Candidata para el wordmark del logo (pendiente de confirmación)
- Licencia libre (SIL Open Font License)

**Pesos usados:** 400 (regular), 500 (medium). No usar italic en contextos operativos.

### Instrument Serif — Voz editorial

**Rol:** headlines en marketing site, portadas de reportes para propietarios, empty states celebratorios, momentos de onboarding con intención editorial.

**Por qué:**
- Contraste máximo con Inter: introduce calor humano donde el producto necesita pausa
- Diseñada para display — funciona bien a tamaños grandes (32px+)
- "Serif" señala editorial, confianza financiera, calidad — apropiado para comunicaciones hacia propietarios/inversionistas
- Coherente con el posicionamiento premium del producto sin caer en serif clásico corporativo
- Instrumento de narrativa, no de operación — su aparición es intencional y espaciada
- Licencia libre (SIL Open Font License)

**Pesos usados:** 400 (regular). No usar en body copy ni en interfaces operativas.

---

## Consecuencias

**Positivas:**

- Los tres typefaces tienen roles claros: un diseñador o desarrollador puede decidir cuál usar sin ambigüedad.
- La distinción visual entre voz del sistema (Inter), voz técnica (IBM Plex Mono) y voz editorial (Instrument Serif) comunica por sí misma la naturaleza del contenido.
- Instrument Serif como fuente de display permite que el marketing site se diferencia claramente de la interfaz del producto.
- Las tres fuentes son libres — sin costo de licencia ahora ni cuando escale.

**Negativas / trade-offs:**

- Tres typefaces tienen overhead de carga (aunque las tres son variable fonts optimizadas).
- Requiere disciplina: la tentación de usar Inter en todo o IBM Plex Mono fuera de su contexto debe resistirse activamente.
- Instrument Serif a pequeño tamaño no funciona — cualquier texto <24px debe ir en Inter.

**Configuración mínima en globals.css / tailwind:**

```css
:root {
  --font-sans:  'Inter', system-ui, sans-serif;
  --font-mono:  'IBM Plex Mono', 'Fira Code', monospace;
  --font-serif: 'Instrument Serif', Georgia, serif;
}

/* Global tabular nums — no negociable */
body {
  font-family: var(--font-sans);
  font-variant-numeric: tabular-nums;
}
```

---

## Alternativas consideradas

**Alternativa A — Un solo typeface (Inter en todo):**
Descartada porque: (1) Inter no tiene el carácter técnico suficiente para señalizar datos de sistema, (2) no hay contraste editorial para el marketing site, (3) el producto quedaría visualmente plano sin la diferenciación de voces.

**Alternativa B — Geist (Vercel) + Geist Mono:**
Considerada por proximidad con el ecosistema Next.js. Descartada porque: (1) Geist Mono tiene menos carácter técnico que IBM Plex Mono, (2) la asociación con Vercel/Next.js es demasiado directa para una plataforma que quiere identidad propia, (3) no hay opción serif en el sistema Geist.

**Alternativa C — Neue Haas Grotesk (similar a Helvetica) + mono + serif:**
Descartada porque: (1) requiere licencia comercial, (2) menos legible a tamaños pequeños que Inter en pantalla, (3) menos coherente con el ecosistema de productos de referencia (Linear, Vercel usan Inter o similares).

**Alternativa D — Berkeley Mono como voz técnica:**
Considerada por su carácter visual fuerte. Descartada porque: (1) requiere licencia comercial (~$75/dev), (2) IBM Plex Mono es más legible a 12px — crítico para tablas de datos, (3) Berkeley Mono es muy "developer-facing", menos apropiado para operadores no técnicos.
