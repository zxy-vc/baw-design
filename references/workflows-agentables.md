# Workflows agentables de BaW OS

> Catálogo canónico de procesos operativos que un agente puede ejecutar (con o sin aprobación humana) dentro de BaW OS.
> Fuente: trabajo conjunto Fran + Hugo + equipo OpenClaw, abril 2026.
> Esta es la **lista de referencia** para priorizar tiers, módulos MCP y orden de activación de agentes.

**Estado:** v1 — provisional. Se ajusta cuando termine el benchmark de naming y la fase de agent-readiness.

---

## Cómo leer este documento

- **Dominio:** familia funcional (6 dominios).
- **Workflow:** proceso concreto que un agente puede ejecutar.
- **Agente ancla:** el agente principal responsable. Otros agentes pueden colaborar.
- **Nota:** la nomenclatura "Eco / Trazo / Pulso / Brisa / Rumbo / Alcance / Sello" se usa aquí como **etiqueta de trabajo interna**. La decisión vigente (ADR 0013) es usar nombres genéricos descriptivos en el producto ("Agente de Cobranza", "Agente de Mantenimiento", etc.) hasta cerrar benchmark.

---

## Dominio 1 — Guest & Resident Comms

**Agente ancla:** Eco (Agente de Comunicaciones)
**Por qué primero:** WhatsApp intake es el dolor #1 reportado por Mateos.

| # | Workflow | Detalle operativo |
|---|---|---|
| 1.1 | Intake WhatsApp 24/7 | Recibir, clasificar y rutear mensajes entrantes (cobro, mantenimiento, contrato, leasing, otro). |
| 1.2 | Respuesta de primer contacto | Auto-responder con SLA, datos del residente y siguiente paso. |
| 1.3 | Confirmaciones de pago | Acuse recibo + recordatorio del próximo vencimiento. |
| 1.4 | Coordinación de visitas | Agendar / reagendar / cancelar visitas y recordatorios. |
| 1.5 | Encuestas post-servicio | Disparar NPS / CSAT al cerrar ticket de mantenimiento o contrato. |
| 1.6 | Anuncios masivos segmentados | Notificaciones por edificio / piso / tipo de unidad (corte de agua, junta, etc.). |

---

## Dominio 2 — Leasing & Revenue

**Agente ancla:** Brisa (Agente de Leasing)
**Por qué segundo:** dynamic pricing y conversión de leads tienen el ROI más claro.

| # | Workflow | Detalle operativo |
|---|---|---|
| 2.1 | Captura de leads multi-canal | Inmuebles24, Lamudi, Facebook, Instagram, WhatsApp directo. |
| 2.2 | Calificación inicial | Pre-screening: presupuesto, plazo, ocupantes, mascotas. |
| 2.3 | Agendado de visitas | Sincroniza calendario, envía ubicación y recordatorios. |
| 2.4 | Generación de cotización | Renta + depósito + ajustes por plazo / promociones vigentes. |
| 2.5 | Solicitud de aplicación | Envío de formulario, recolección de documentos. |
| 2.6 | Borrador de contrato | Pre-llenado con datos validados, listo para revisión legal. |
| 2.7 | Pricing dinámico | Recomendación de renta por unidad según ocupación, mercado y temporada. |

---

## Dominio 3 — Maintenance & Facilities

**Agente ancla:** Trazo (Agente de Mantenimiento)
**Por qué tercero:** ventaja estructural — el grafo de proveedores LATAM es difícil de replicar.

| # | Workflow | Detalle operativo |
|---|---|---|
| 3.1 | Triage de tickets | Clasificar urgencia, categoría, unidad afectada. |
| 3.2 | Match con proveedor | Seleccionar proveedor por especialidad, zona, historial, SLA. |
| 3.3 | Cotización y aprobación | Solicitar quote, ruta de aprobación según monto. |
| 3.4 | Coordinación de visita | Acceso, llaves, ventana horaria con residente. |
| 3.5 | Seguimiento de avance | Updates de estatus, fotos antes/después. |
| 3.6 | Cierre y validación | Confirmación residente + factura proveedor. |
| 3.7 | Mantenimiento preventivo | Calendario por equipo (bombas, elevadores, áreas comunes). |

---

## Dominio 4 — Collections, Finance & Compliance

**Agente ancla:** Pulso (Agente de Cobranza)
**Por qué cuarto:** CFDI / SAT es moat regulatorio LATAM.

| # | Workflow | Detalle operativo |
|---|---|---|
| 4.1 | Generación de cargos mensuales | Renta + servicios + ajustes contractuales. |
| 4.2 | Recordatorios escalonados | T-3, T-0, T+3, T+7 días por canal preferido. |
| 4.3 | Conciliación de pagos | Match transferencias / Stripe / depósitos contra cargos. |
| 4.4 | Emisión CFDI | Factura electrónica con FacturAPI, validación RFC. |
| 4.5 | Plan de pagos negociados | Estructurar parcialidades, registrar y dar seguimiento. |
| 4.6 | Reporte financiero mensual | Por edificio: ingresos, gastos, NOI, ocupación. |
| 4.7 | Ledger de cuentas por cobrar | Aging, riesgo, acciones recomendadas. |

---

## Dominio 5 — Owner Relations & Reporting

**Agente ancla:** Alcance (Agente de Owner Relations)

| # | Workflow | Detalle operativo |
|---|---|---|
| 5.1 | Reporte ejecutivo semanal | Resumen automático para Fran + owner: KPIs, alertas, decisiones pendientes. |
| 5.2 | Distribuciones a propietarios | Cálculo de neto a distribuir + comprobantes. |
| 5.3 | Comunicación de cambios materiales | Avisos sobre cambios de renta, gastos extraordinarios, derramas. |

---

## Dominio 6 — Governance, Audit & Exceptions

**Agente ancla:** Sello (Agente de Auditoría)

| # | Workflow | Detalle operativo |
|---|---|---|
| 6.1 | Audit trail de decisiones agentes | Log inmutable de toda acción agente con razonamiento. |
| 6.2 | Detección de excepciones | Alertar cuando un workflow cae fuera de tolerancia (monto, tiempo, frecuencia). |

---

## NO agentables (decisión humana obligatoria)

Procesos donde un agente puede preparar contexto, **pero la decisión y la ejecución son humanas**.

| # | Proceso | Por qué no se agentiza |
|---|---|---|
| N.1 | Desalojos legales | Requiere abogado, juzgado, riesgo reputacional alto. |
| N.2 | Negociación con inquilino difícil | Empatía, contexto humano, riesgo de escalada. |
| N.3 | Evaluación crediticia final | Decisión con sesgos legales, debe ser humana auditable. |
| N.4 | Remodelaciones mayores | Diseño, presupuesto > umbral, decisión de capital. |
| N.5 | Manejo de crisis | Inundación, incendio, fallecimiento — comunicación humana. |
| N.6 | Asambleas de condóminos | Política interna, votación, actas legales. |
| N.7 | Trato con autoridades locales | Inspecciones, permisos, multas — riesgo legal. |
| N.8 | Cierre de contrato con propietario | Decisión comercial estratégica, B2B. |

---

## Orden de activación de agentes (semanas 1-20)

| Semana | Agente | Workflows que activa |
|---|---|---|
| 1-3 | Eco (Comunicaciones) | 1.1, 1.2, 1.3 |
| 4-6 | Trazo (Mantenimiento) | 3.1, 3.2, 3.4 |
| 7-9 | Pulso (Cobranza) | 4.1, 4.2, 4.4 |
| 10-12 | Brisa (Leasing) | 2.1, 2.3, 2.4 |
| 13-15 | Rumbo (Orquestación) | conexiones cross-dominio |
| 16-18 | Alcance (Owner Relations) | 5.1, 5.2 |
| 19-20 | Sello (Auditoría) | 6.1, 6.2 |

> **Nota:** Rumbo no es un agente de dominio sino un orquestador. Aparece cuando ya hay ≥3 agentes operando para coordinar handoffs entre ellos.

---

## Cómo se conecta esto a la arquitectura técnica

Cada **dominio** corresponde a un **módulo MCP** en BaW OS (ver `references/mcp-first-architecture.md`):

| Dominio | Módulo MCP |
|---|---|
| 1. Guest & Resident Comms | `mcp-comms` |
| 2. Leasing & Revenue | `mcp-leasing` |
| 3. Maintenance & Facilities | `mcp-maintenance` |
| 4. Collections, Finance & Compliance | `mcp-finance` |
| 5. Owner Relations & Reporting | `mcp-owner` |
| 6. Governance, Audit & Exceptions | `mcp-audit` |

Un agente activa workflows **llamando tools del módulo MCP correspondiente**. Eso permite que el agente sea portable (Claude SDK hoy, OpenAI / LangGraph / OpenClaw mañana) sin reescribir la lógica de negocio.

---

## Referencias cruzadas

- ADR 0013 — Naming genérico de agentes
- `references/mcp-first-architecture.md` — cómo se exponen estos workflows como tools
- Source of Truth v0.1 (Hugo, OpenClaw) — estrategia y Definition of Done Fase 1
- Feature Board (Notion) — backlog de features a tier
