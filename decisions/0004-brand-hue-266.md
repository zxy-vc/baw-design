# ADR 0004 — Brand hue 266 (electric indigo)

## Estado

**Accepted** — Mayo 2026

---

## Contexto

BaW OS necesita un color de marca que:

1. **Posicione el producto correctamente.** BaW OS es un sistema operativo técnico, confiable y premium para B2B. El color debe proyectar esas cualidades — no ser consumer-tech ni corporate-azul.

2. **Se diferencie de los referentes más cercanos.** Linear usa un azul-indigo (~hue 250-255). Stripe usa un morado-grape (~hue 272-280). Notion usa un azul estándar (~hue 210). El color de BaW debe ser reconocible como próximo a ese ecosistema pero distinguible.

3. **Funcione en ambos modos (dark y light).** El brand color debe verse como elemento de chrome activo en dark mode y como elemento interactivo en light mode, sin perder lectura ni contraste.

4. **Coexistir sin conflicto con el agent color (ADR 0005).** El brand color (acciones humanas, chrome del sistema) y el agent color (acciones de agentes) deben ser claramente distinguibles a simple vista. Si son demasiado similares, el sistema de atribución visual falla.

5. **Ser sharp, no suave.** Los colores de marca "suaves" (lavender, periwinkle, slate blue) son cálidos pero no proyectan la precisión técnica que BaW OS necesita. El brand color debe tener presencia.

---

## Decisión

**El brand hue de BaW es 266 en OKLCH — indigo eléctrico.**

En la nomenclatura OKLCH donde hue 0 = rojo, 120 = verde, 240 = azul, 266 se posiciona en el espacio entre azul-violeta y violeta:

```
Hue 240 — azul puro
Hue 250 — azul-indigo (Linear)
Hue 266 — indigo eléctrico (BaW) ← aquí
Hue 272 — indigo-morado
Hue 280 — morado (Stripe)
Hue 300 — violet (agent color de BaW)
```

### Valores de token en OKLCH (referencia)

Los valores exactos están en `/tokens/colors.css`. La escala del brand color sigue el patrón de 9 niveles (100–900) con la misma H y variando L y C:

```css
/* Ejemplo ilustrativo — valores exactos en tokens/colors.css */
--brand-100: oklch(97% 0.03 266);  /* tint más claro */
--brand-200: oklch(93% 0.06 266);
--brand-300: oklch(87% 0.10 266);
--brand-400: oklch(78% 0.15 266);
--brand-500: oklch(65% 0.21 266);  /* base — uso en light mode */
--brand-600: oklch(52% 0.24 266);  /* base — uso en dark mode */
--brand-700: oklch(42% 0.22 266);
--brand-800: oklch(32% 0.18 266);
--brand-900: oklch(22% 0.12 266);  /* shade más oscuro */
```

### Contextos de uso

**Usar brand color:**
- Botones primarios (CTA)
- Links activos y estados de focus
- Nav items activos en el sidebar
- Indicadores de selección
- Elementos de marca en marketing

**No usar brand color:**
- Señalizar acciones de agentes (ese rol corresponde al agent color, hue 300)
- Como background de área grande en dark mode (demasiado intenso)
- En texto de body copy (contraste insuficiente a valores medios)
- Mezclado con colores semánticos (RAG) para crear nuevos estados

---

## Consecuencias

**Positivas:**

- El posicionamiento hue 266 es distinguible de Linear (hue ~252) y de Stripe (hue ~278) pero está en el mismo espacio "técnico/premium" — señal clara de a qué categoría pertenece BaW.
- La separación de 34 hue-units con el agent color (hue 300) es suficiente para que sean perceptualmente distintos en todos los tamaños y contextos.
- El indigo eléctrico proyecta precisión técnica y confianza sin la frialdad del azul puro ni la calidez del morado consumer.
- En OKLCH, la escala de 9 niveles tiene pasos perceptualmente uniformes — se puede usar cualquier nivel y mantener la coherencia.

**Negativas / trade-offs:**

- La proximidad con Linear (hue 252) puede generar comparaciones en el mercado — "¿es como Linear pero para real estate?" Es un riesgo de posicionamiento que el diferenciador de producto (no el color) debe resolver.
- El indigo eléctrico es muy saturado en P3 — en monitores sRGB la saturación se reduce. Esto es una limitación del display, no del diseño, pero puede afectar la coherencia entre lo diseñado en Mac Pro y lo que ve un operador en un monitor sRGB antiguo.

**Impacto en otros sistemas:**

- El brand hue 266 es el valor H usado en toda la escala de brand tokens en `/tokens/colors.css`.
- Los estilos de focus, active y selected en componentes de UI usan derivados de esta escala.
- El marketing site usa la escala brand para CTAs y elementos de identidad.

---

## Alternativas consideradas

**Alternativa A — Azul puro (hue ~220-230):**
El "azul corporativo". Confiable pero genérico. Descartado porque: (1) es el default de demasiados productos SaaS, (2) no tiene el carácter técnico-premium que BaW OS necesita, (3) no se diferencia suficientemente de Salesforce, Oracle, SAP en el imaginario B2B.

**Alternativa B — Verde (hue ~140-160):**
Asociado a finanzas (Robinhood, success states). Descartado porque: (1) el verde está sobrecargado como color semántico (success/go en el sistema RAG), (2) no proyecta el carácter técnico-operativo de BaW OS.

**Alternativa C — Hue ~280 (morado tipo Stripe):**
Más cálido que indigo, asociado con Stripe. Descartado porque: (1) demasiada proximidad visual con Stripe en el imaginario de productos premium, (2) la separación con el agent color (hue 300) sería de solo 20 unidades — insuficiente para distinción visual confiable.

**Alternativa D — Negro / neutro sin brand color:**
El enfoque de Apple (usa grises y negro como color de marca). Descartado porque: (1) BaW OS necesita elementos interactivos claramente identificables en interfaces densas, (2) el negro funciona para hardware consumer, no para dashboards de operaciones donde la distinción de estados es crítica.

**Alternativa E — Rojo o naranja:**
Descartados porque: (1) rojo es color semántico de error/crítico en el sistema RAG, usarlo como brand color crearía conflicto semántico inmediato, (2) naranja es el color de warning — mismo problema.
