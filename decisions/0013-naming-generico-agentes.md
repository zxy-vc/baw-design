# 0013 — Naming genérico descriptivo de agentes (provisional)

**Fecha**: 2026-04-26
**Estado**: Accepted (provisional, revisar tras benchmark)
**Autor**: Fran Durán
**Decisión**: Adoptar nombres genéricos descriptivos para los agentes de BaW OS en producto y comunicación externa ("Agente de Cobranza", "Agente de Mantenimiento", "Agente de Comunicaciones", etc.). Los nombres propios trabajados en la fase de exploración (Eco / Trazo / Pulso / Brisa / Rumbo / Alcance / Sello, y la propuesta paralela Central / Caja / Obra / Voz / Plaza / Mira / Acta) se preservan como **etiquetas internas** y se evaluarán formalmente cuando se haga el benchmark de agentes comerciales.

---

## Contexto

En la Fase 0 (exploración estratégica) se trabajaron dos nomenclaturas para los 7 agentes principales:

**Set "OpenClaw" (presentado en Source of Truth v0.1):**
Eco, Trazo, Pulso, Brisa, Rumbo, Alcance, Sello.

**Set "alterno" (propuesta Hugo):**
Central, Caja, Obra, Voz, Plaza, Mira, Acta.

Ambos sets son **nombres propios poéticos**, alineados con la marca BaW. Tienen ventajas (memorables, brandeables, defendibles legalmente) y costos importantes en la fase actual:

1. **Confusión interna y externa** — un nuevo cliente (Mateos hoy, otros mañana) necesita aprender un vocabulario nuevo antes de entender qué hace cada agente.
2. **Acoplamiento a la marca antes de validar funcionalidad** — si un agente cambia de scope (deja de existir, se fusiona, se separa), tendríamos que renombrar.
3. **Riesgo de copyright / colisión** — sin búsqueda formal de marca registrada en LATAM, puede haber colisiones (ej: "Pulso" como nombre de producto financiero ya existe).
4. **Falta de benchmark** — todavía no hemos estudiado cómo nombran los agentes los productos comerciales líderes (Anthropic, Salesforce Einstein, Microsoft Copilot, Glean, etc.). Decidir antes de ese estudio sería decidir a ciegas.

Cita literal de la decisión Fran (sesión abril 26, 2026):

> "si nos tendríamos que ir con nombres genéricos, descriptivos. Como agente de cobranza, agente de mantenimiento, etc."

## Decisión

### 1. En producto y comunicación externa

Usar nombres **genéricos descriptivos** en cualquier UI, copy, documentación pública, y onboarding:

| Etiqueta interna | Nombre en producto |
|---|---|
| Eco | Agente de Comunicaciones |
| Brisa | Agente de Leasing |
| Trazo | Agente de Mantenimiento |
| Pulso | Agente de Cobranza |
| Alcance | Agente de Owner Relations |
| Sello | Agente de Auditoría |
| Rumbo | Agente Orquestador (cuando exista) |

### 2. En documentos internos y artefactos de diseño

Las etiquetas internas (Eco / Trazo / Pulso / etc.) **se conservan** en:
- `baw-design/references/workflows-agentables.md`
- ADRs internos
- Discusiones de diseño y moodboards
- BRAND_FOUNDATIONS.md (sección de agentes — actualizar mostrando ambas)

Razón: las etiquetas son útiles para hablar de identidad visual del agente (color OKLCH, tono de voz, ilustración) sin tener que escribir "Agente de Cobranza" 50 veces. **Pero nunca llegan al usuario final.**

### 3. Identidad visual sigue trabajándose en paralelo

Cada agente conserva:
- Su color OKLCH (ver ADR 0005).
- Su tono de voz dentro del rango general de BaW.
- Su ilustración / símbolo (cuando se diseñe).

Lo que cambia es solo **cómo lo nombramos al usuario**.

### 4. Provisional — gatillo de revisión

Esta decisión es **provisional**. Se revisita cuando se cumpla **alguna de**:

- Termine el benchmark de naming de agentes comerciales (estudio formal de cómo nombran los 8-10 productos líderes con agentes en producción).
- BaW OS cierre Fase 1 (Mateos operando diariamente con ≥3 agentes activos).
- Aparezca un caso de uso comercial donde el nombre genérico se quede corto (ej: "Agente de Cobranza" colisiona con un producto del banco).

En la revisión se decide entre:
- (A) Mantener genérico permanentemente.
- (B) Adoptar nombres propios (uno de los sets, mezcla, o nuevos).
- (C) Sistema híbrido — nombre propio interno + nombre genérico en producto, indefinidamente.

### 5. Reglas de redacción

**Capitalización:** "Agente de Cobranza" (las dos palabras importantes en mayúscula). En español es nombre propio compuesto.

**En inglés (cuando aplique):** "Collections Agent". Mismo patrón.

**Forma corta aceptable** dentro de un mismo párrafo:
> "El Agente de Cobranza generó 14 cargos hoy. El agente identificó dos casos que requieren revisión humana."

Una vez introducido completo, "el agente" funciona como referencia.

---

## Consecuencias

**Positivas**
- Onboarding más rápido para clientes nuevos — entienden inmediatamente.
- Cero acoplamiento a una marca que todavía no validamos.
- Cero riesgo de colisión de marca registrada.
- Si en Fase 2 decidimos adoptar nombres propios, lo hacemos con datos de uso real.

**Negativas**
- Pierde diferenciación frente a competidores que sí usan nombres propios (ej: Einstein de Salesforce).
- Dificulta crear identidad emocional con el agente — más difícil que un usuario "se encariñe" con "Agente de Cobranza" que con "Pulso".
- Si en el futuro adoptamos nombres propios, hay un costo de migración (UI, docs, comunicación a clientes).

**Riesgos**
- Que la decisión "provisional" se vuelva permanente por inercia. Mitigación: el gatillo de revisión está ligado a hito objetivo (cierre de Fase 1), no a "cuando alguien se acuerde".

---

## Estado de implementación

- [ ] BRAND_FOUNDATIONS.md actualizado mostrando dualidad (etiqueta interna ↔ nombre producto). (pendiente Sprint 0)
- [ ] `references/workflows-agentables.md` ya usa esta convención. ✓ creado en este sprint.
- [ ] UI de baw-os (cuando se conecten agentes reales — Sprint 4 en adelante) usa nombre genérico.
- [ ] Página `/agents` reescrita o eliminada (hoy hardcodea Hugo/Alicia/Carmen como "agentes" que en realidad son humanos — tracked en auditoría baw-os, Sprint 1).

---

## Referencias

- Source of Truth v0.1 (Hugo, OpenClaw) — propuesta original Eco/Trazo/Pulso/...
- ADR 0001 — Arquitectura de marca
- ADR 0005 — Agent identity color
- `references/workflows-agentables.md` — lista canónica de agentes y dominios
