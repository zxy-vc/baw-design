# ADR 0005 — Agent identity color separado (hue 300)

## Estado

**Accepted** — Mayo 2026

---

## Contexto

BaW OS es una plataforma donde humanos y agentes de IA conviven como actores de primera clase. En cualquier timeline de una unidad, en el audit log, en el approval hub, en las notificaciones — aparecen acciones realizadas por operadores humanos y acciones realizadas por agentes (Rumbo, Pulso, Trazo, Eco, Brisa, Alcance, Sello).

El operador necesita poder distinguir de un vistazo si una acción fue iniciada por un agente o por una persona. Esta distinción es crítica para:

1. **Accountability.** ¿Quién aprobó esto? ¿Fue una política automática o una decisión humana?
2. **Confianza.** El operador debe saber cuándo está leyendo el razonamiento de un agente vs. la nota de un compañero.
3. **Auditoría y compliance.** Los reguladores y los propietarios necesitan saber qué fue automatizado y qué fue manual.
4. **Calibración de autonomía.** Para decidir si un agente puede subir de L2 a L3, el operador necesita revisar el historial de acciones del agente — que debe ser escaneable.

La distinción visual puede hacerse con íconos, con labels de texto, con posición en la pantalla, o con color. El color es el mecanismo más rápido de escanear — los sistemas de mission control y NOC lo usan por esa razón. Pero el color no puede ser el único discriminador (accesibilidad: daltonismo rojo-verde afecta al 8% de los hombres).

El brand color (hue 266, indigo) ya está asignado a elementos interactivos y chrome del sistema. Usar el mismo hue para agentes y para elementos del sistema crearía confusión semántica.

---

## Decisión

**Las acciones y la presencia de agentes se señalizan con un violet diferenciado, hue 300 en OKLCH.**

Esta decisión establece dos colores con roles semánticos distintos y no intercambiables:

```
Hue 266 (indigo) → Brand BaW, chrome del sistema, acciones humanas primarias
Hue 300 (violet) → Identidad de agentes, acciones agénticas, agent badges
```

La separación de 34 hue-units en OKLCH es suficiente para que los dos colores sean perceptualmente distintos en cualquier tamaño, en dark y light mode.

### Escala del agent color (referencia)

Los valores exactos están en `/tokens/colors.css`. Ilustración del patrón:

```css
/* Ejemplo ilustrativo — valores exactos en tokens/colors.css */
--agent-100: oklch(97% 0.03 300);
--agent-200: oklch(93% 0.06 300);
--agent-300: oklch(87% 0.10 300);
--agent-400: oklch(78% 0.15 300);
--agent-500: oklch(65% 0.21 300);
--agent-600: oklch(52% 0.23 300);
--agent-700: oklch(42% 0.20 300);
--agent-800: oklch(32% 0.16 300);
--agent-900: oklch(22% 0.10 300);
```

### Aplicaciones del agent color

**Usar agent color (hue 300):**
- Badges de identificación de agentes (`[AGENT · PULSO]`)
- Bordes de tarjetas o filas en el agent activity feed
- Dot de estado en el agent status bar (globalmente visible en el top de la app)
- Indicador de "ejecutado por agente" en timelines y audit logs
- Background sutil en evidence packs y action receipts generados por agentes
- Avatares geométricos de los agentes en el fleet view

**No usar agent color:**
- En acciones o elementos iniciados por humanos
- Como color de énfasis genérico (podría confundirse con presencia de agente)
- En el brand chrome del sistema (sidebar, navigation, botones primarios — ese es el territorio del brand hue 266)
- Como color de estado semántico (no sustituye a los colores RAG)

### Distinción visual en timelines

El audit log unificado usa el agent color para señalizar acciones de agentes, azul para acciones humanas, y gris para eventos de sistema:

```
VIOLET  → [AGENT · ECO] 10:15  Clasificó mensaje entrante de Unit 812
AZUL    → [HUMAN · María R.] 10:22  Aprobó respuesta al inquilino
GRIS    → [SYSTEM] 10:22  Notificación enviada vía WhatsApp
VIOLET  → [AGENT · PULSO] 10:45  Emitió recordatorio de pago — Unit 302
```

El color va siempre acompañado del label de texto (`AGENT`, `HUMAN`, `SYSTEM`) — nunca el color solo, para cumplir con los requisitos de accesibilidad.

---

## Consecuencias

**Positivas:**

- El operador puede escanear el audit log o el timeline y saber en menos de un segundo si una acción fue iniciada por un agente o una persona — sin leer el texto completo.
- La distinción es sistemática: en cualquier superficie donde aparezca el agent color, el significado es el mismo.
- Los propietarios que auditan el sistema tienen un mecanismo visual claro para distinguir decisiones automatizadas de decisiones humanas.
- El sistema escala: si en el futuro hay más agentes (fuera del roster actual de 7), todos usan el mismo agent color — la identidad de agente como categoría es consistente.

**Negativas / trade-offs:**

- Introduce un tercer color "primario" en el sistema (brand + agent + RAG). Con el sistema semántico RAG esto suma 5 hues con significado propio. Requiere disciplina para no añadir más.
- El violet (hue 300) en algunas pantallas sRGB puede verse demasiado similar al brand indigo (hue 266) a tamaños muy pequeños. La regla de acompañar siempre con label de texto mitiga este riesgo.
- El daltonismo tipo tritanopia (raro, <0.01% de la población) afecta la percepción de azul-violeta. El label de texto cubre este caso.

**Impacto en la UI:**

- El componente `AgentBadge` en el código usa `--agent-600` (dark mode) o `--agent-500` (light mode) como background.
- El sidebar tiene un dot de estado del fleet de agentes que usa `--agent-500` cuando hay agentes activos.
- El agent activity feed tiene un left-border de `2px solid --agent-300` en cards de agente.

---

## Alternativas consideradas

**Alternativa A — No diferenciar agentes por color; usar solo íconos y labels:**
Descartada porque: los íconos requieren atención focada para escanear; el color permite escaneo periférico. En un audit log con 100+ eventos, el color es la única forma de leer el patrón de human vs. agent sin procesar cada línea.

**Alternativa B — Usar el mismo brand hue 266 para agentes:**
Descartada porque crearía ambigüedad semántica: ¿este elemento violeta es brand chrome o es un agente? La distinción brand/agent es un principio de diseño fundamental del sistema.

**Alternativa C — Verde para agentes:**
Descartada porque: el verde ya está reservado como color semántico de success/completed en el sistema RAG. Usar verde para agentes crearía conflicto ("¿verde significa que el agente está activo, o que la acción fue exitosa?").

**Alternativa D — Diferente ícono geométrico por agente sin unificación de color:**
Posible como complemento, no como alternativa. Los íconos individuales por agente (Rumbo, Pulso, etc.) pueden existir para identificar cuál agente específicamente, pero el color unificado identifica la categoría "agente" — son capas distintas de información.

**Alternativa E — Hue ~320 (pink/magenta):**
Considerado por mayor separación del brand. Descartado porque: (1) en muchos contextos culturales el pink tiene connotaciones no deseadas para software operativo B2B, (2) en dark mode el pink/magenta puede ser demasiado agresivo visualmente.
