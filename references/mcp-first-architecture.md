# Arquitectura MCP-first aplicada a BaW OS

> Cómo construimos BaW OS para que los agentes (los nuestros y los de terceros como OpenClaw) puedan operar el producto sin acoplarse a un runtime de agentes en particular.

**Estado:** decisión vigente — abril 2026.
**Fuente:** decisión Fran (founder) + análisis técnico, validada con equipo OpenClaw.

---

## La idea en una frase

**Cada dominio operativo de BaW OS expone un servidor MCP. Los agentes — sea cual sea su runtime — se conectan a esos servidores para ejecutar trabajo real.**

Eso significa que la lógica de negocio (cobrar, agendar mantenimiento, generar CFDI, escribir contrato) **vive en BaW OS, no en el agente**. El agente solo razona y llama tools.

---

## Por qué MCP-first

### Problema que resuelve

Si construyes un agente que sabe cobrar rentas pero la lógica de cobranza está pegada al runtime de Claude SDK, cuando salga un mejor modelo (OpenAI, Gemini, llama local) o un cliente quiera traer su propio agente (OpenClaw), tienes que reescribir todo.

### Solución MCP

MCP (Model Context Protocol, abierto por Anthropic, adoptado por todos) es un protocolo estándar para que un agente descubra y llame tools de un servidor.

Si exponemos cada módulo de BaW OS como servidor MCP:
- El runtime del agente es **intercambiable**.
- La lógica de negocio es **dueña de BaW**, no del proveedor de modelos.
- Cualquier agente que hable MCP se puede conectar (los de OpenClaw, los de Anthropic, los nuestros).
- Auditoría natural: cada llamada MCP queda loggeada → audit trail (Sello).

### Costo

Mayor que pegar todo en un solo backend monolítico:
- Hay que diseñar **el contrato MCP** de cada módulo (qué tools expone, qué inputs, qué outputs).
- Hay que mantener **la capa de auth** (qué agente puede llamar qué tool, sobre qué propiedad).
- El primer mes es más lento que la opción "todo en Next API routes".

A 6 meses, paga. A 12 meses, no se entiende cómo se podría haber hecho de otra forma.

---

## Cómo se traduce en BaW OS

### Mapa módulo MCP ↔ dominio operativo

| Módulo MCP | Dominio | Workflows que ejecuta | Estado actual |
|---|---|---|---|
| `mcp-comms` | Guest & Resident Comms | 1.1 a 1.6 | por construir |
| `mcp-leasing` | Leasing & Revenue | 2.1 a 2.7 | por construir |
| `mcp-maintenance` | Maintenance & Facilities | 3.1 a 3.7 | parcial (`/maintenance` existe sin MCP) |
| `mcp-finance` | Collections, Finance & Compliance | 4.1 a 4.7 | parcial (FacturAPI conectado, falta MCP wrapper) |
| `mcp-owner` | Owner Relations & Reporting | 5.1 a 5.3 | por construir |
| `mcp-audit` | Governance, Audit & Exceptions | 6.1, 6.2 | por construir |

Ver lista completa en `references/workflows-agentables.md`.

### Anatomía de un módulo MCP

Cada módulo expone:

```
mcp-<dominio>/
├── server.ts           ← entry point MCP server
├── tools/              ← un archivo por tool expuesto
│   ├── createCharge.ts
│   ├── sendReminder.ts
│   └── reconcilePayment.ts
├── schemas/            ← JSON schemas de inputs/outputs
├── auth/               ← qué agente puede llamar qué tool
└── README.md           ← contrato del módulo
```

**Ejemplo concreto — `mcp-finance.createCharge`:**

```typescript
// Tool expuesto vía MCP
{
  name: "createCharge",
  description: "Genera un cargo mensual para una unidad arrendada",
  input_schema: {
    unitId: string,
    period: string,        // "2026-05"
    concepts: Array<{
      type: "rent" | "utility" | "fee",
      amount: number,
      description: string
    }>
  },
  output: {
    chargeId: string,
    total: number,
    dueDate: string,
    cfdiRequired: boolean
  }
}
```

El agente de cobranza no sabe nada de la base de datos. Solo sabe que existe el tool `createCharge`, lo llama, y BaW OS ejecuta la lógica (validar contrato vigente, calcular impuestos, escribir el ledger, etc.).

### Auth: quién puede llamar qué

Cada llamada MCP carga:
- **Identidad del agente** (firmada, expira).
- **Scope autorizado** (qué propiedades, qué tipo de operaciones, qué montos).
- **Razón de la llamada** (texto libre del agente — entra al audit trail).

Ejemplo: el "Agente de Cobranza" de Mateos 809P puede llamar `createCharge` solo sobre `propertyId = mateos-809p`, monto máximo por cargo $50,000 MXN, requiere co-firma humana > $20,000.

---

## Cómo se conectan los agentes

### Caso 1 — Agentes nativos BaW (Claude SDK, hoy)

```
┌─────────────────────────────┐
│  Agente de Cobranza         │
│  (Claude SDK, hosted BaW)   │
└────────────┬────────────────┘
             │ MCP
             ▼
┌─────────────────────────────┐
│  mcp-finance (BaW OS)       │
│  - createCharge             │
│  - sendReminder             │
│  - reconcilePayment         │
│  - emitCFDI                 │
└─────────────────────────────┘
```

### Caso 2 — Agentes de OpenClaw (cliente trae su propio agente)

```
┌─────────────────────────────┐
│  OpenClaw Agent             │
│  (runtime OpenClaw)         │
└────────────┬────────────────┘
             │ MCP (mismo protocolo)
             ▼
┌─────────────────────────────┐
│  mcp-finance (BaW OS)       │
└─────────────────────────────┘
```

**Diferencia:** ninguna desde el lado de BaW OS. Mismo contrato, mismo auth, mismo audit trail. La capa que cambia es solo el runtime del agente.

### Caso 3 — Agentes orquestados (multi-agente)

Cuando "Rumbo" (orquestador) coordina una decisión cross-dominio (ej: residente reporta fuga → ticket de mantenimiento + nota de crédito en cargo del mes):

```
┌───────────────────┐
│  Rumbo            │
│  (orquestador)    │
└────┬─────────┬────┘
     │ MCP     │ MCP
     ▼         ▼
┌─────────┐ ┌─────────────┐
│mcp-     │ │mcp-finance  │
│maint.   │ │             │
└─────────┘ └─────────────┘
```

Rumbo no tiene lógica de mantenimiento ni de cobranza. Solo razona sobre cuándo llamar cada tool de cada módulo.

---

## Decisiones derivadas

| Decisión | Implicación práctica |
|---|---|
| Lógica de negocio vive en módulos MCP | No metemos lógica en el agente. Si el agente desaparece, el módulo sigue siendo útil para la UI. |
| MCP es la única forma de que un agente escriba | UI puede llamar APIs Next directas; agentes solo entran por MCP. Eso simplifica auditoría. |
| Un módulo MCP = un dominio | No partimos por feature. Partimos por dominio operativo (los 6 dominios definidos). |
| MCP server vive dentro del repo `baw-os` | No es un microservicio aparte. Mismo deploy, misma DB, distinto entry point. |
| Auth MCP usa JWT firmado por BaW + scope explícito | No usamos credenciales largas. Cada sesión de agente tiene token de corta vida. |

---

## Qué NO es MCP-first

Aclaraciones útiles para evitar over-engineering:

- **No es microservicios.** Los módulos MCP viven en el mismo proceso que la app Next por ahora. Se separan solo si el costo de operación lo justifica.
- **No es serverless puro.** Un servidor MCP típicamente mantiene estado de sesión con el agente.
- **No reemplaza la API REST/Next** de la UI. La UI sigue llamando endpoints REST/server actions normales. MCP es para agentes.
- **No es agnóstico de modelo "from day one".** Hoy elegimos Claude SDK porque es el runtime más maduro para tool use. La portabilidad la garantiza el contrato MCP, no que cambiemos de modelo cada semana.

---

## Roadmap de adopción MCP

| Fase | Sprint(s) | Entregable |
|---|---|---|
| 0 — Foundations | Sprint 0-1 | ADRs, repo layout, auth model definido. |
| 1 — Primer módulo | Sprint 2-3 | `mcp-finance` con `createCharge`, `sendReminder`, `reconcilePayment`. Sin agente todavía — se prueba con cliente MCP de prueba. |
| 2 — Primer agente | Sprint 4 | Agente de Cobranza usa `mcp-finance`. Aprobación humana en cada acción. |
| 3 — Expansión | Sprint 5-6 | `mcp-comms`, `mcp-maintenance`. Agentes correspondientes. |
| 4 — Orquestación | Post-Fase 1 | `Rumbo` coordina ≥3 módulos. Multi-tenant. |

---

## Referencias

- [MCP spec oficial (Anthropic, abierto)](https://modelcontextprotocol.io)
- `references/workflows-agentables.md` — qué workflows expone cada módulo
- ADR 0013 — naming genérico de agentes (provisional)
- Source of Truth v0.1 (Hugo) — Definition of Done Fase 1
