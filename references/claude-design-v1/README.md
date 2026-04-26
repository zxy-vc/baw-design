# Claude Design v1 — Exploraciones iniciales

> **Read-only.** Este folder contiene los archivos originales generados por Claude Design (abril 2026) que sirvieron como punto de partida del sistema de diseño BaW. **No editar estos archivos.** Cualquier evolución se hace en `/tokens/`, `/BRAND_FOUNDATIONS.md` o `/assets/`.

## Origen

Generado en Claude (modo artifacts) usando como input el research interno `uploads/baw-os-design-research.pdf`. El research sintetiza cuatro investigaciones primarias sobre UX agent-native, command centers, colaboración humano-agente y tendencias agentic SaaS 2025–2026.

## Contenido

| Archivo | Qué contiene |
|---|---|
| `System Sheet.html` | **El más importante.** Hoja maestra con todos los tokens (colores OKLCH, tipografía, espaciados, radios, sombras), modos light/dark, identidad de agente, semánticos RAG. |
| `System Sheet-print.html` | Versión imprimible del System Sheet. |
| `Brand System v1.html` | Primera iteración del sistema de marca. |
| `Brand System v2.html` | Segunda iteración con 3 voces (SaaS / Real Estate / Hospitality). **Nota:** la arquitectura de 3 voces fue descartada — BaW arranca como marca paraguas + edificios con marca propia. Tomar de aquí solo la paleta y ejemplos visuales. |
| `Mark Final.html` | Iteraciones del símbolo (mark) finales. |
| `Mark Distinctive + Inside Badge.html` | Variantes con "inside badge" estilo Intel Inside. |
| `Mark Explorations.html` | Exploraciones de mark (early). |
| `Wordmark Explorations.html` | Exploraciones de wordmark (early). |
| `Wordmark Explorations v2.html` | Segunda iteración de wordmark. |
| `tweaks-panel.jsx` | Componente React reusable para un panel de ajustes en vivo (live tweak). Útil para iterar tokens en cualquiera de los HTMLs sin editar código. |
| `uploads/baw-os-design-research.pdf` | Research base (crítico para entender el porqué del producto). |
| `uploads/pasted-*.png` | Screenshots de referencia/inspiración usados por Claude. |

## Cómo abrir

Los HTMLs son autocontenidos: abánlos directamente en el navegador. No necesitan servidor.

```bash
open "System Sheet.html"
open "Brand System v2.html"
```

## Activar el panel de tweaks

En cualquier HTML que cargue React, abre la consola y ejecuta:

```js
window.postMessage({ type: '__activate_edit_mode' }, '*')
```

Ver el comentario en `tweaks-panel.jsx` para detalles.

## Por qué conservamos esto

Aunque ya no es source of truth, lo mantenemos versionado porque:
1. Documenta el punto de partida del sistema y las decisiones tempranas.
2. Sirve de referencia visual mientras el sistema productivo madura.
3. Permite comparar cómo evoluciona la marca (auditoría de marca).
