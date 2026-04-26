# ADR 0001 — Arquitectura de marca: BaW como paraguas + edificios con marca propia

## Estado

**Accepted** — Mayo 2026

---

## Contexto

BaW opera en un espacio donde conviven al menos tres tipos de audiencia con relaciones distintas con la marca:

1. **Operadores B2B** (property managers, desarrolladores): compran BaW OS como plataforma de software. Su relación es con BaW como empresa de tecnología.
2. **Propietarios de edificios**: invierten en un edificio que opera con BaW. Su relación es con BaW como operador y con el nombre del edificio como activo patrimonial.
3. **Huéspedes e inquilinos**: viven o se hospedan en el edificio. Su relación es con el edificio, no con la tecnología que lo opera.

La pregunta inicial que surgió en el desarrollo del sistema de marca fue: ¿debería existir una sola voz de marca o voces diferenciadas por contexto?

El Brand System v2 (en `/references/claude-design-v1/Brand System v2.html`) exploró una arquitectura de tres voces: SaaS (operador B2B), Real Estate (edificios) y Hospitality (huéspedes). En revisión con el founder, esa estructura resultó innecesariamente compleja y no refleja la forma en que el negocio opera ni cómo escala.

ZXY Ventures, el holding, debe permanecer invisible al mercado. No es una marca de cara al cliente.

---

## Decisión

Se adopta una **arquitectura de marca de dos capas**, no de tres voces:

**Capa 1 — BaW (paraguas)**

Marca única que cubre el software (BaW OS) y la promesa de operación. Es la marca que se vende, se comunica y se construye ante operadores, propietarios e inversores. No se fragmenta en sub-voces.

**Capa 2 — Edificios con marca propia (powered by BaW)**

Cada edificio operado por BaW mantiene su propia identidad de marca. BaW aparece como endorsement discreto, no como marca dominante en la experiencia del huésped o inquilino.

La relación entre capas:

```
BaW (software + operación) ──► BaW OS (producto)
                           ──► Edificios (cada uno con marca propia)
                                 └─ "powered by BaW" (endorsement)
```

ZXY Ventures no tiene presencia pública. Es invisible al mercado.

### Reglas de aplicación

- Cuando el usuario es **operador o propietario**: BaW domina la comunicación.
- Cuando el usuario es **huésped o inquilino**: la marca del edificio domina; BaW queda como endorsement opcional.
- BaW OS **puede convivir con marcas de edificios ya establecidas** sin requerir que adopten la identidad visual de BaW.

---

## Consecuencias

**Positivas:**

- Simplifica el sistema de marca: una sola marca que construir y defender.
- Permite que los edificios sean activos patrimoniales con identidad propia, aumentando su valor para los propietarios.
- Elimina la fricción de explicar la relación entre "BaW el software" y "BaW la marca del edificio".
- Escala naturalmente: cada edificio nuevo mantiene su identidad; BaW crece como marca B2B sin fragmentarse.

**Negativas / trade-offs:**

- El endorsement "powered by BaW" tiene menor visibilidad que si BaW dominara la experiencia del huésped.
- Construir brand awareness con el consumidor final (huéspedes) es más lento.
- Requiere disciplina operativa para no mezclar identidades en materiales que llegan a audiencias distintas.

**Decisiones derivadas:**

- Cada edificio necesitará su propio brief de marca cuando sea relevante.
- BaW Mateos 809 es el primer caso de coexistencia — sirve como referencia para futuros edificios.
- El endorsement mark "powered by BaW" requiere vectorización propia (pendiente).

---

## Alternativas consideradas

**Alternativa A — Tres voces (SaaS + Real Estate + Hospitality):**
Explorada en Brand System v2. Descartada porque: (1) BaW no es tres empresas distintas, (2) requiere mantener tres sistemas de voz activos con recursos limitados, (3) los edificios no son una "voz de BaW" — son entidades con marca propia.

**Alternativa B — Una sola marca monolítica (BaW en todo):**
Descartada porque: (1) los huéspedes no necesitan saber que viven en un edificio "con software de BaW", (2) los edificios premium tienen valor en su identidad propia, (3) limitaría la capacidad de BaW OS de convivir con marcas establecidas.

**Alternativa C — Holding visible (ZXY como marca paraguas):**
Descartada porque: (1) ZXY no tiene relevancia para el cliente final, (2) complica innecesariamente el pitch B2B, (3) no hay beneficio de visibilidad del holding para ninguna audiencia.
