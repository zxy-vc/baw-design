# ADR 0003 — OKLCH como espacio de color

## Estado

**Accepted** — Mayo 2026

---

## Contexto

El sistema de color de BaW OS necesita:

1. **Coherencia perceptual entre hues.** En hex o HSL, un amarillo con L:60 se percibe mucho más brillante que un morado con L:60. Esto produce paletas inconsistentes donde algunos colores "gritan" y otros "susurran" con el mismo valor nominal.

2. **Light y dark mode ambos de primera clase.** BaW OS no tiene un modo "principal" y un modo "opcional". Dark mode es el default para interfaces operativas; light mode es el default para portales. Ambos necesitan paletas diseñadas con la misma atención.

3. **Escalas predecibles.** Al generar una escala de grises o de un hue específico (para los 9 niveles de la escala de colores de marca), los pasos deben ser perceptualmente equidistantes. En HSL, los pasos no lo son.

4. **Soporte wide gamut.** Los monitores P3 (todos los Mac recientes, iPhones modernos) pueden mostrar colores más saturados que sRGB. OKLCH puede expresar esos colores; hex/HSL no.

5. **Compatibilidad con el ecosistema.** Linear, que es el referente visual más cercano de BaW OS, usa LCH para su sistema de color. Radix UI, la librería de componentes más usada en Next.js, también usa OKLCH. El navegador Chrome 111+, Firefox 116+, y Safari 16.4+ soportan `oklch()` nativamente.

El sistema de tokens en `/tokens/colors.css` ya usa OKLCH como formato principal.

---

## Decisión

**OKLCH es el espacio de color de trabajo para todo el sistema de marca de BaW.**

Todos los tokens de color en `/tokens/colors.css` se definen en formato `oklch(L C H)`. No se usan hex, HSL ni RGB como valores primarios — solo como fallback en contextos donde el soporte de OKLCH no está garantizado.

### Por qué OKLCH sobre alternativas

**Sobre hex (#rrggbb):**
Hex es un formato de serialización, no un modelo de color. No codifica ninguna relación perceptual. Diseñar en hex es diseñar a ciegas — no hay forma de predecir si dos colores con el mismo L perceptual tienen el mismo hex.

**Sobre HSL:**
HSL fue el primer intento de un modelo "entendible por humanos". Pero no es perceptualmente uniforme. El amarillo H:60 en HSL es mucho más brillante que el azul H:240 con el mismo S y L. Generar paletas de dark mode en HSL produce inconsistencias sistemáticas que solo se resuelven con ajustes manuales por hue.

**Sobre LCH (predecessor de OKLCH):**
LCH es el predecesor y tiene las mismas propiedades de uniformidad perceptual. OKLCH lo mejora en dos aspectos: (1) mejor comportamiento en extremos de C (chroma) alta, (2) mejor predicción de gamut P3. OKLCH es el estándar moderno.

**Sobre P3:**
P3 es un gamut (espacio de color), no un modelo de color. OKLCH puede especificar colores en P3 — son complementarios, no alternativos.

### Estrategia de modos

El dark mode no se genera invirtiendo la paleta de light mode. Se genera con una paleta independiente, definida en OKLCH, donde la elevación se comunica con diferencias en L (Lightness):

```
Dark mode:  L más alto = más elevado (surface sobre background)
Light mode: L más bajo = más elevado (surface más oscura sobre fondo más claro)
```

Esta estrategia, usada por Linear, produce dark y light modes que se sienten como versiones del mismo sistema, no como paletas distintas.

### Fallback strategy

Para contextos que aún no soportan `oklch()` (email clients, herramientas externas):

```css
/* Fallback para navegadores sin soporte OKLCH */
--brand: #4f46e5; /* hex aproximado */
--brand: oklch(52% 0.24 266); /* valor preciso */
```

Los valores hex en los tokens son aproximaciones calculadas del OKLCH correspondiente, no los valores primarios.

---

## Consecuencias

**Positivas:**

- Los modos light y dark se generan con lógica sistemática en lugar de ajustes manuales hue por hue.
- Las escalas de color son perceptualmente equidistantes — el paso de `--gray-3` a `--gray-4` se percibe igual que el de `--gray-7` a `--gray-8`.
- Los colores semánticos (brand, agent, RAG) tienen el mismo peso visual entre sí.
- Wide gamut disponible sin trabajo adicional cuando el contexto lo soporte.
- Coherente con el tooling moderno (Radix, shadcn, Tailwind v4 que usa OKLCH nativo).

**Negativas / trade-offs:**

- Los valores OKLCH no se "leen" intuitivamente: `oklch(52% 0.24 266)` no dice nada a alguien acostumbrado a hex.
- Las herramientas de diseño (Figma actual) tienen soporte parcial de OKLCH — los valores pueden no renderizarse exactamente igual. Cuando se use Figma como parte del workflow, se necesitará un plugin de conversión.
- Algunos email clients y herramientas externas no soportan `oklch()` — el fallback hex es obligatorio.
- CMYK para impresión requiere un paso de conversión adicional (los valores OKLCH no son directamente trasladables a CMYK).

**Herramientas recomendadas:**

- [oklch.com](https://oklch.com) — editor interactivo, generador de escalas, picker
- [bottosson.github.io/apps/colorpicker/](https://bottosson.github.io/apps/colorpicker/) — picker de Björn Ottosson (creador de Oklab)
- Conversión a hex para fallbacks: `node -e "require('culori').formatHex(require('culori').oklch({l: 0.52, c: 0.24, h: 266}))"`

---

## Alternativas consideradas

**Alternativa A — HSL + ajustes manuales para dark mode:**
La forma más común de manejar temas en CSS. Descartada porque: requiere decenas de ajustes manuales por hue, el dark mode resultante siempre tiene inconsistencias visuales que son difíciles de rastrear a una causa sistemática, y no escala bien al agregar nuevos colores.

**Alternativa B — P3 con hex sRGB como fallback:**
P3 es compatible pero no es un modelo de trabajo — es un gamut. No resuelve el problema de diseñar escalas coherentes. Descartada porque no es alternativa a OKLCH sino complementaria.

**Alternativa C — Sistema basado en Design Tokens con múltiples formatos (Style Dictionary en Fase 2):**
Esto sigue siendo el objetivo de Fase 2. En Fase 0, los tokens están en CSS puro. La decisión de OKLCH como espacio de color es independiente de la decisión de herramienta (Style Dictionary) — se puede adoptar OKLCH ahora y compilar a múltiples formatos más adelante.

**Alternativa D — Oklch solo para la paleta base, hex para tokens semánticos:**
Descartada porque parte del beneficio de OKLCH es la coherencia entre todos los colores del sistema. Si los tokens semánticos están en hex, la coherencia perceptual se pierde exactamente donde más importa.
