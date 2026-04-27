# 0014 — Resolución del nombre del primer edificio: Frontier Bay vs Pioneer Bay

**Fecha**: 2026-04-26
**Estado**: Accepted
**Autor**: Fran Durán
**Decisión**: El primer edificio operado por BaW (proyecto en Mateos 809P) se llama **Frontier Bay**.

---

## Contexto

Durante la Fase 0 aparecieron dos nombres en circulación para el primer edificio de la cartera BaW:

- **Frontier Bay** — nombre escrito en el Master Plan original y en los documentos de propiedad.
- **Pioneer Bay** — nombre que apareció en algunos documentos posteriores (Source of Truth v0.1, presentaciones internas).

Ambos nombres son **arquitectónicamente coherentes** con la línea editorial de los edificios BaW (palabras en inglés que evocan exploración, primera línea, descubrimiento). La ambigüedad genera tres problemas:

1. **Inconsistencia en comunicación** — distintas personas / documentos usan distinto nombre.
2. **Confusión legal** — los contratos, escrituras, y registros de propiedad usan **Frontier Bay**. Cualquier comunicación pública en otro nombre crea desalineación.
3. **Riesgo de SEO / branding** — si el edificio aparece bajo dos nombres, las búsquedas se dispersan, los reviews se dispersan, y la marca pierde fuerza.

La pregunta no es solo cosmética: define cómo se llama el activo en marketing, en BaW OS, en facturación, y en el ledger.

## Decisión

### 1. El nombre oficial es Frontier Bay

Razones:

- **Precedencia legal** — los contratos y la escritura de la propiedad usan "Frontier Bay". Cambiar el nombre comercial sin cambiar el legal genera complicaciones operativas.
- **Master Plan** — el documento estratégico original (Master Plan BaW) usa "Frontier Bay" desde la primera versión.
- **Coherencia editorial** — "Frontier" es ligeramente más rico semánticamente: evoca **frontera** (límite y posibilidad), no solo **pionero**. Encaja mejor con el posicionamiento BaW: vivienda en zonas de inflexión urbana.
- **Pioneer Bay** se queda como **etiqueta interna histórica** — no se usa en comunicación, pero se reconoce en documentos antiguos.

### 2. Convenciones de uso

| Contexto | Forma correcta |
|---|---|
| Comunicación pública | **Frontier Bay** |
| Marketing y web | **Frontier Bay** |
| BaW OS (UI) | **Frontier Bay** (sustituye cualquier "Mateos 809P" donde el contexto lo permita) |
| Documentos legales | **Frontier Bay** (ya consistente) |
| Dirección física complementaria | "Frontier Bay — Mateos 809, CDMX" |
| ID interno en BD | `frontier-bay` (slug) o el `propertyId` actual `mateos-809p` (mantener hasta migración planificada — ver más abajo) |

### 3. ID en base de datos — no se renombra hoy

El `propertyId` actual en código y BD es `mateos-809p`. **No se cambia en este momento** porque:

- 12 archivos hardcodean `ed4308c7-2bdb-46f2-be69-7c59674838e2` y `mateos-809p`.
- Renombrar requiere migración de datos + cambio en URL slugs + redirects.

Se programa migración del slug a `frontier-bay` para Sprint 4 o cuando se introduzca segundo edificio (lo que pase primero). Tracking en `MIGRATION_propertyId-slug.md` (a crear cuando arranque).

Mientras tanto:
- En UI mostrar **"Frontier Bay"** como label.
- En BD el slug sigue siendo `mateos-809p` (técnico).
- En logs y comunicación mantener nombre comercial.

### 4. Edificios futuros

La línea editorial **se confirma**: edificios BaW se nombran en inglés con palabras evocadoras de exploración / lugar / posibilidad. Próximos edificios siguen el patrón.

Ejemplos del Master Plan (no se eligen aquí, solo se referencian):
- Frontier Bay (este edificio).
- Cardinal Bay, Nimbus Bay, Halcyon Bay (candidatos del Master Plan).

La elección del nombre de cada edificio futuro se hace caso por caso; este ADR solo confirma **el patrón** y resuelve la ambigüedad histórica del primero.

---

## Consecuencias

**Positivas**
- Cero ambigüedad: una sola forma correcta.
- Alineación entre documentos legales, OS, marketing y comunicación.
- Línea editorial confirmada para edificios futuros.

**Negativas**
- Algunos documentos ya escritos con "Pioneer Bay" hay que actualizar. Mitigación: corrección oportunista — se actualiza cuando se toca el documento, no big-bang.

**Riesgos**
- Personas internas siguen usando "Pioneer Bay" por costumbre. Mitigación: corrección amable cada vez que aparezca, sin formalismos.

---

## Estado de implementación

- [ ] Source of Truth v0.1 (Notion) actualizado para usar "Frontier Bay". (pendiente — fuera de Sprint 0)
- [ ] BRAND_FOUNDATIONS.md actualizado donde mencione "Pioneer Bay". (pendiente Sprint 0)
- [ ] BaW OS — labels visibles muestran "Frontier Bay". (Sprint 1, parte del cleanup MVP)
- [ ] Plan de migración slug `mateos-809p` → `frontier-bay`. (Sprint 4 o cuando entre segundo edificio)

---

## Referencias

- Master Plan BaW (documento estratégico fundacional — Notion)
- Source of Truth v0.1 (Hugo / OpenClaw)
- ADR 0001 — Arquitectura de marca
- BRAND_FOUNDATIONS.md — capítulo de naming editorial
