# BaW · Brand Foundations

> Documento madre del sistema de marca y diseño. Source of truth para identidad visual, posicionamiento de producto, principios de diseño y arquitectura de marca. Versión 1.0 — Mayo 2026.

---

## 0. Cómo usar este documento

### Quién lo edita y cuándo

Este documento es de edición restringida. Solo el founder (Fran Durán) puede proponer cambios. Cualquier modificación debe seguir el proceso:

1. Abrir un PR en el repo `baw-design` con la sección afectada
2. Documentar la razón del cambio en el mensaje de commit
3. Si el cambio implica una decisión arquitectónica, crear o actualizar el ADR correspondiente en `/decisions/`
4. Hacer merge solo después de validar el impacto downstream (tokens, componentes, copy)

### Qué es source of truth y qué no

| Artefacto | Source of truth | No es source of truth |
|---|---|---|
| Posicionamiento, principios, manifiesto | Este documento | Notion, slides, emails |
| Design tokens (color, tipo, spacing) | `/tokens/*.css` | Figma, Storybook, código inline |
| Componentes UI | `baw-os` repo (hasta que haya librería separada) | Bocetos, screenshots |
| ADRs (decisiones) | `/decisions/*.md` | Mensajes de Slack, conversaciones |
| Logo y wordmark | Cuando se vectorice: `/brand/logo/` | Los HTMLs de exploración actuales |

### Convenciones de estado

Cada sección lleva un marcador de estado:

- `[estable]` — decidido, no cambiar sin ADR
- `[en revisión]` — en proceso de validación, puede cambiar
- `[pendiente]` — no decidido aún, placeholder informado

### Relación con baw-os

Este repo (`baw-design`) se incluye como Git submodule en `baw-os`. Los tokens en `/tokens/*.css` se importan directamente en el proyecto Next.js. Ver README para instrucciones de setup del submodule.

---

## 1. Manifiesto

`[estable]`

### Por qué existe BaW

Un edificio residencial premium no debería funcionar como una empresa del siglo XX administrada con Excel, WhatsApp manual y un conserje que trabaja 12 horas. Debería funcionar como un sistema operativo: con estado visible, automatización trazable, excepciones que llegan al lugar correcto y personas que toman decisiones en lugar de perseguir datos.

Eso es lo que construimos.

BaW nació de operar un edificio real —Mateos 809— y descubrir que el software existente no estaba diseñado para el mundo donde los agentes de IA son actores de primera clase. Las plataformas de property management actuales son bases de datos CRUD con lógica de negocio cosida arriba. No son sistemas operativos. No están diseñadas para que humanos y agentes trabajen juntos.

La industria completa está lista para ser reescrita.

### La tesis en una línea

**BaW es el sistema operativo de un edificio.**

No un PMS con IA encima. No un chatbot de concierge. Un OS: donde los agentes monitorean, ejecutan y coordinan 24/7, y los humanos definen políticas, supervisan y atienden excepciones.

### Por qué "BaW"

BaW viene de **Break A Way** — tres significados en capas:

- **Break**: romper, abrir espacio, salir de lo establecido
- **Away**: automático, que opera cuando no estás
- **A Way**: un camino, una forma de resolver

La marca no grita. No tiene subtítulo corporativo. Opera en la misma frecuencia que el producto: confiada, técnica, discreta. El edificio que tiene BaW no necesita anunciarlo — se nota.

### Lo que no somos

- No somos un "property management system con IA integrada"
- No somos un chatbot de concierge
- No somos una app para inquilinos
- No somos un software genérico de back-office para PYMEs

---

## 2. Arquitectura de marca

`[estable]`

### El holding invisible

**ZXY Ventures** es la entidad legal que sostiene todo. No tiene presencia pública. No aparece en los materiales del cliente. Es la SAPI de CV que emite acciones internas, administra los ventures y permite spin-offs cuando un producto lo amerita.

**BaW es el venture de ZXY enfocado en operaciones inmobiliarias.** Opera con marca propia, independiente del holding.

### Las tres capas

```
ZXY Ventures (holding — invisible al mercado)
│
└── BaW (marca paraguas — operador de software y experiencia)
    │
    ├── BaW OS (producto software — el sistema operativo del edificio)
    │   └── Rumbo, Pulso, Trazo, Eco, Brisa, Alcance, Sello (agentes)
    │
    └── Edificios powered by BaW
        ├── BaW Mateos 809 (marca propia del edificio, operated by BaW)
        └── [futuros edificios con marca propia]
```

### Diagrama de relaciones de marca

```
┌─────────────────────────────────────────────────────────────────┐
│  ZXY Ventures                                    [invisible]    │
└─────────────────────────────────────────────────────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────┐
│  BaW                                         [marca paraguas]   │
│                                                                 │
│  "El sistema operativo de un edificio"                          │
│                                                                 │
│  ┌──────────────────────────┐   ┌───────────────────────────┐  │
│  │  BaW OS                  │   │  Edificios powered by BaW  │  │
│  │  [producto software B2B] │   │  [marca propia por edif.]  │  │
│  │                          │   │                            │  │
│  │  · Rumbo (ops)           │   │  · BaW Mateos 809          │  │
│  │  · Pulso (cobranza)      │   │  · [futuros]               │  │
│  │  · Trazo (mantenimiento) │   │                            │  │
│  │  · Eco (comms)           │   │  Endorsement mark:         │  │
│  │  · Brisa (leasing)       │   │  "powered by BaW"          │  │
│  │  · Alcance (inteligencia)│   │                            │  │
│  │  · Sello (compliance)    │   │                            │  │
│  └──────────────────────────┘   └───────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

### Reglas de coexistencia

La marca que domina cada superficie depende del rol del usuario:

| Superficie | Usuario | Marca dominante | Rol de BaW |
|---|---|---|---|
| UI de BaW OS | Operador / property manager | BaW OS | Principal |
| Owner portal | Propietario del edificio | BaW OS | Principal |
| Lobby / señalética | Huésped / inquilino | Nombre del edificio | Endorsement ("powered by BaW") |
| App de huésped | Huésped | Nombre del edificio | Secundario o invisible |
| Manual de huésped | Huésped | Nombre del edificio | Footnote opcional |
| Marketing B2B | Property managers, desarrolladores | BaW | Principal |
| Presentaciones a inversores | Inversionistas | BaW / ZXY según contexto | Según audiencia |

**Regla general:** cuando el usuario es un **operador** (property manager, dueño, staff), BaW domina. Cuando el usuario es el **huésped o inquilino**, la marca del edificio domina y BaW queda como endorsement discreto.

### BaW OS con marcas de edificios ya establecidas

BaW OS puede operar como sistema de fondo en edificios que ya tienen marca propia consolidada. En esos casos:

- BaW OS no aparece en materiales dirigidos a huéspedes o inquilinos
- El endorsement "powered by BaW" es opcional — decisión del operador
- En materiales B2B y presentaciones ante el propietario, BaW OS puede mencionarse como infraestructura

### Los 7 agentes de BaW OS — el roster

Los agentes son parte de la identidad de BaW OS. No son features ni módulos — son actores del sistema con identidad, rol y presencia visible en la interfaz. El sistema de naming sigue el tema **Caminos / Ways** — derivado de Break A Way:

| Agente | Rol | Significado | Narrativa |
|---|---|---|---|
| **RUMBO** | Operations Orchestrator | Dirección, curso | El que marca el rumbo de las operaciones. Coordina y delega entre agentes. |
| **PULSO** | Collections & Finance | Latido, ritmo | La cobranza tiene pulso: vencimientos, ciclos, ritmo mensual. "Tomar el pulso" = medir la salud financiera. |
| **TRAZO** | Maintenance & Facilities | Línea que marca un plan | Trazar la ruta de reparación. El plan de acción para cada incidencia. |
| **ECO** | Communications | Lo que resuena, llega a todos | El mensaje que va y vuelve. La señal que llega a todos los canales. WhatsApp-first. |
| **BRISA** | Leasing & Renewals | Corriente que atrae | Lo que atrae naturalmente. Movimiento suave que trae oportunidades y retiene inquilinos. |
| **ALCANCE** | Executive Intelligence | Visión, perspectiva, scope | "El alcance de la operación." Ve todo, mide todo. La visión completa para el propietario. |
| **SELLO** | Compliance & Audit | Lo que cierra, certifica | Sellar = cerrar con seguridad. CFDI, contratos, validación. Certifica y valida. |

**Test de conversación:**
- "Rumbo reasignó el caso de la 1807 a María"
- "Pulso envió los recordatorios de noviembre"
- "Trazo levantó 3 tickets de plomería"
- "Eco le mandó las instrucciones de check-in"
- "Brisa tiene 4 prospectos nuevos para el piso 12"
- "Alcance detectó que la ocupación bajó 2%"
- "Sello validó los CFDI de noviembre"

Escalabilidad del sistema: futuros agentes pueden nombrarse con el mismo patrón (Surco, Ronda, Puente, Faro) sin romper la coherencia del naming.

---

## 3. Posicionamiento de BaW OS

`[estable]`

### El cambio de paradigma

Jakob Nielsen lo articula con precisión: el usuario de software empresarial está dejando de ser **operador** para convertirse en **supervisor**. No conduce el coche; gestiona al chofer.

> *"Users are changing from doing the work (operating the UI) to supervising the work. The correct analogy is no longer driving a car; it is managing a chauffeur."*
> — Jakob Nielsen, UX Tigers

Para una plataforma de operaciones inmobiliarias, esta transición no es opcional. Los edificios tienen alto volumen de decisiones repetitivas con excepciones críticas, múltiples stakeholders con distintos niveles de delegación, y presión constante por operar 24/7 sin incrementar nómina proporcionalmente. Es exactamente donde los agentes agregan más valor.

El software de property management actual ignora esto. Son bases de datos CRUD con lógica de negocio —diseñadas para que los humanos hagan el trabajo, no para que lo supervisen. Eso está cambiando. BaW OS está diseñado desde el origen para el nuevo paradigma.

### Los tres hallazgos centrales

Estos tres hallazgos, documentados en el research interno (`baw-os-design-research.md`), articulan la tesis de producto:

**1. Humans supervise, agents operate.**

Los agentes monitorean cientos de variables; el humano revisa los tres que requieren juicio. El estado operativo ideal —"inbox zero" agéntico— debe diseñarse como primera clase, no como ausencia de alertas. La interfaz no es donde se hace el trabajo; es desde donde se supervisa.

*Implicación para BaW OS:* la vista default del sistema no muestra todo lo que está pasando. Muestra solo lo que requiere atención. Las operaciones que los agentes ejecutaron correctamente quedan en el audit log, no en la pantalla principal.

**2. Trust is a design output, not a tech output.**

Smashing Magazine lo sintetiza: *"Autonomy is an output of a technical system. Trustworthiness is an output of a design process."* La transparencia, el intent preview, el rationale explicado, el action receipt y la autonomy dial son los componentes de UX que convierten capacidad técnica en confianza operativa.

*Implicación para BaW OS:* cada acción consecuente del agente debe ir acompañada de: qué hizo, por qué, qué cambió, y cómo revertir. No como feature adicional — como comportamiento de fábrica.

**3. Interface as control plane.**

El trabajo real ocurre en la capa de agentes. La UI existe para configurar políticas, escalar excepciones, auditar y tomar control cuando se necesita. La interfaz de BaW OS es menos un "CRM de edificios" y más un sistema de mission control sobre un edificio que opera autónomamente.

*Implicación para BaW OS:* las pantallas se organizan por *qué necesita atención*, no por entidad de base de datos. Un operador no abre "Contratos" para revisar contratos; abre "Renovaciones en riesgo" para ver qué requiere acción.

### El modelo de triple capa (Nielsen)

Los sistemas agent-native maduros operan en tres capas. BaW OS las implementa explícitamente:

| Capa | Función | En BaW OS |
|---|---|---|
| **Intent Surface** | El usuario declara el outcome; el sistema infiere el contexto | `"Cobra los atrasos del edificio"` / `"Prepara la unidad 204 para check-in mañana"` |
| **Orchestration Surface** | Negociación entre intención y ejecución: plan, consent, receipts, conflictos | El **approval hub**, los flujos de excepción, el intent preview con `[Proceder] [Editar] [Hacerlo yo]` |
| **Direct Manipulation Surface** | La GUI tradicional persiste como fallback para edge cases, overrides y auditoría | Tablas, formularios y vistas clásicas — ahora para corrección y supervisión, no para operación cotidiana |

La capa de Orchestration es **la más crítica y la que más equipos ignoran**. En BaW OS, es el centro del diseño.

### Qué muere del SaaS tradicional

Seis patrones del SaaS tradicional están siendo desplazados. BaW OS los reemplaza desde el diseño:

| Patrón tradicional | Reemplazado por |
|---|---|
| Dashboard estático multi-widget | Interfaz exception-first + agent inbox |
| Formulario de entrada manual | Agentes leen intención y escriben datos; humanos confirman |
| Campana de notificaciones con volumen indiferenciado | Oversight inbox calibrado por tipo de acción requerida |
| Búsqueda por keywords | Síntesis: `"¿Por qué cayó la ocupación esta semana?"` |
| Pantallas CRUD como trabajo principal | Agentes escriben en el sistema de registro; humanos revisan |
| Automatizaciones rígidas tipo IFTTT | Agentes que perciben contexto y negocian excepciones |

> *"Business applications as we know them will collapse in the agent era. They are essentially CRUD databases with business logic that will migrate into the AI tier."*
> — Satya Nadella

### Modelos de confianza y delegación

El research identifica dos perfiles de usuario con estrategias de confianza distintas hacia los agentes:

- **Perfil conservador:** prefiere explicabilidad detallada y validación externa. Busca múltiples señales simultáneas. Quiere entender el razonamiento antes de aprobar.
- **Perfil pragmático:** confía por desempeño observado. Valora reliability y métricas de outcome. Se fatiga con explicabilidad excesiva.

BaW OS no debe construir una sola interfaz de confianza. Los owners conservadores y CFOs quieren ver el razonamiento. Los ops managers experimentados quieren ver el historial de aciertos. Ambos tienen razón. El autonomy dial, los tiers de disclosure (Nivel 1/2/3) y la configuración de umbrales por edificio sirven a los dos perfiles sin obligar a uno a operar como el otro.

### Flujos de escalamiento en BaW OS

Cinco tipos de escalamiento, todos diseñados como features de primera clase — no como estados de error:

| Tipo | Descripción | Ejemplo en BaW OS |
|---|---|---|
| **Clarificación** | El agente necesita información faltante | "El RFC del nuevo owner está incompleto; necesito actualizarlo para emitir el CFDI" |
| **Decisión** | Múltiples paths válidos, ninguno claramente mejor | "Tres ofertas de vendor de plomería para U-204; ¿priorizo precio, tiempo o rating?" |
| **Validación** | Riesgo alto requiere sign-off explícito | "Propongo waive del 50% del late fee a Sr. García; primer atraso en 18 meses" |
| **Contexto** | Situación sin precedente en la política | "Inquilino solicita extender lease 3 meses; no hay política previa para este tipo de unidad" |
| **Error** | Falla técnica o estado inconsistente | "API del banco timeout en cobro automático; ¿reintentar, manual, o flagged?" |

Tras un rechazo de acción, el comportamiento del agente es explícito: Abort / Reroute / Escalate. Nunca reintentar silenciosamente una acción rechazada. Esta regla no es negociable.

### La jerarquía ontológica del sistema

Los objetos de primera clase en BaW OS son:

```
Organización (empresa de property management / desarrolladora)
  └── Portfolio / Edificio
        └── Unidad
              ├── Contrato (lease, booking, ownership)
              ├── Reserva (si aplica)
              ├── Mantenimiento (tickets, historial)
              └── Transacciones financieras
```

Esta jerarquía se refleja en la navegación, en el audit log y en los reports. Los agentes leen y escriben en estos objetos; los humanos los revisan y corrigen. La integridad de los objetos (especialmente contratos y transacciones financieras) tiene protección adicional: toda escritura agéntica sobre estos objetos requiere atribución mínima (agent ID, confidence, human review status).

---

## 4. Principios de diseño

`[estable]`

Siete principios gobiernan todas las decisiones de diseño en BaW OS. Cada uno es accionable: genera una consecuencia concreta en el producto.

---

### 1. Humans supervise, agents operate

**El operador no hace el trabajo. Lo aprueba, lo configura y lo supervisa.**

La UI default está optimizada para supervisión. La ejecución ocurre en background y solo sube a la superficie cuando requiere juicio humano o cuando algo salió mal.

| Ejemplo en BaW OS | Anti-ejemplo |
|---|---|
| La pantalla de colecciones muestra el queue de acciones pendientes de aprobación, no la lista completa de contratos | Una tabla con todos los contratos y un botón "Enviar recordatorio" por fila |
| El dashboard de misión muestra "3 excepciones requieren tu atención" cuando todo va bien | Un muro de widgets con todas las métricas posibles del edificio |

---

### 2. Trust is a design output

**La confianza se construye con transparencia, no con marketing.**

Cada acción consecuente del agente va acompañada de: qué hizo, por qué, qué cambió en el mundo, y cómo revertirlo. No como detalle opcional — como comportamiento de fábrica. Los agentes no hacen cosas misteriosas.

| Ejemplo en BaW OS | Anti-ejemplo |
|---|---|
| Pulso envió 12 recordatorios de pago → receipt muestra: lista de inquilinos, monto, canal, razonamiento, ventana de undo | "Pulso completó la tarea" |
| Brisa rechazó a un prospecto → explicación: "Historial crediticio insuficiente según política del edificio" | El campo cambia de estado sin explicación |

---

### 3. Exception-first, not dashboard-first

**El estado operativo correcto es que los agentes trabajen sin interrupciones. La UI debe celebrar eso, no ocultarlo.**

Las excepciones surfacean. Las operaciones rutinarias quedan invisibles (en el audit log, accesibles pero no en primer plano). Una pantalla vacía de excepciones es éxito operativo, no una UI rota.

| Ejemplo en BaW OS | Anti-ejemplo |
|---|---|
| El operations dashboard muestra "Todo en orden — 0 excepciones esta mañana" como estado positivo | Una pantalla que solo existe cuando hay problemas; si no hay nada urgente, parece vacía |
| Los agentes activos se muestran como indicadores de salud del sistema, no como ruido | Notificaciones de cada paso que da cada agente, aunque todo sea normal |

---

### 4. Calibrated friction

**No toda fricción es mala. Los speed bumps antes de acciones irreversibles son un feature, no un bug.**

Las acciones con consecuencias grandes (corte de servicio, acción legal, transferencia de fondos, modificación de contrato) requieren confirmación explícita, independientemente del nivel de autonomía configurado. La fricción se calibra al riesgo.

Tres tiers de acción:

```
AUTO             → Ejecuta sin aprobación (reversible, bajo riesgo)
LOG              → Ejecuta y registra para revisión async
REQUIRE_APPROVAL → Bloquea hasta aprobación explícita (irreversible, financiero, bulk)
```

| Ejemplo en BaW OS | Anti-ejemplo |
|---|---|
| Corte de servicios: requiere aprobación con reason code, aunque el agente esté en nivel L4 | Un toggle de "automatización alta" que elimina todos los pasos de confirmación |
| Ajuste de precio >15%: el agente presenta el plan y espera go/no-go | El agente actualiza precios basado en market data sin notificar |

---

### 5. Explainable rationale

**Todo agente explica por qué.**

La fórmula: *"Porque definiste X, hice Y."* El razonamiento se ancla en políticas que el operador configuró, no en la lógica interna del modelo. El usuario puede challengear, editar la política y ver qué cambiaría.

Tres niveles de disclosure:

- **Nivel 1 (default):** qué hizo el agente — una línea
- **Nivel 2 (expandible):** por qué — 2-3 factores anclados en políticas del edificio
- **Nivel 3 (auditoría):** cómo — secuencia de pasos, datos utilizados, confidence score

| Ejemplo en BaW OS | Anti-ejemplo |
|---|---|
| "Porque la política del edificio dice que atrasos >30d van a cobranza extrajudicial, Pulso escaló el caso de Unidad 812" | "Pulso escaló el caso de Unidad 812" |
| Nivel 3 disponible para el auditor: timestamp, modelo utilizado, hash del prompt, confidence 94% | Reasoning disponible solo en modo debug para ingenieros |

---

### 6. Provenance + receipts

**Toda acción tiene trazabilidad nativa. No como feature de compliance — como comportamiento arquitectónico.**

Cada acción de agente y cada intervención humana es un evento de primera clase con atribución mínima: quién (agent ID o user ID), qué, cuándo, por qué, confidence score. El audit log es una superficie de UI, no un log de debug.

Los sistemas de registro (contratos, pagos, unidades) ganan importancia en la era agéntica, no la pierden. Son el núcleo estable que los agentes leen y escriben, y cuya integridad debe protegerse.

| Ejemplo en BaW OS | Anti-ejemplo |
|---|---|
| Timeline de Unidad 304 muestra: qué hicieron los agentes, qué aprobaron los humanos, qué cambió | Un historial de "última modificación" sin autoría |
| Action receipt de Pulso: 47 recordatorios enviados, hora, canal, inquilinos, ventana de undo (30 min) | "Tarea completada" |

---

### 7. Multi-stakeholder by default

**Un edificio tiene al menos cinco tipos de usuario. El sistema los sirve a todos sin comprometer la experiencia de ninguno.**

Propietario, operador (property manager), staff (conserje, housekeeping), inquilino y huésped tienen necesidades radicalmente distintas. El diseño parte de esa diversidad, no la homogeneiza.

| Stakeholder | Vista primaria | Densidad | Agentes visibles |
|---|---|---|---|
| Developer / propietario | Executive Mission Control | Baja — KPIs + excepciones | ROI de agentes, estado del fleet |
| Property manager | Operations Dashboard | Alta — tablas densas, estado completo | Capa de operaciones completa |
| Conserje | Inbox + check-ins de hoy | Media | Comunicaciones del agente |
| Propietario de unidad | Owner Portal | Baja — editorial, financiero | "Tu AI hizo X esta semana" |
| Inquilino / huésped | Tenant / Guest Portal | Mínima — mobile-first | Concierge AI visible como servicio |

---

### Checklist de diseño agent-native

Antes de hacer merge de cualquier PR de UI nueva en `baw-os`, verificar:

**Componentes UX core:**
- [ ] ¿Hay action receipt para toda acción consecuente del agente?
- [ ] ¿El intent preview permite `[Proceder] [Editar] [Hacerlo yo]` cuando aplica?
- [ ] ¿Las excepciones suben al inbox / approval hub, no al cuerpo de la pantalla?
- [ ] ¿El audit log registra la acción con actor, timestamp y atribución?
- [ ] ¿Hay undo / rollback cuando la acción es reversible?
- [ ] ¿El estado del agente es visible en todo momento (idle / running / blocked)?

**Sistema visual:**
- [ ] ¿Se usan los tokens de color, no valores hardcoded?
- [ ] ¿El color del agente (violet 300) solo aparece en acciones de agentes?
- [ ] ¿Los datos numéricos tienen `tabular-nums`?
- [ ] ¿El contraste cumple WCAG AA?
- [ ] ¿El color nunca es el único discriminador de estado (ícono + texto siempre)?
- [ ] ¿Se respeta `prefers-reduced-motion`?

**Copy:**
- [ ] ¿El agente es el sujeto de la oración cuando hizo algo (`"Pulso envió..."`, no `"Se enviaron..."`)
- [ ] ¿Los empty states dicen qué significa el estado vacío, no solo `"Sin datos"`?
- [ ] ¿Los mensajes de error indican qué falló y qué hacer, no solo `"Algo salió mal"`?

---

## 5. Identidad visual

### 5.1 Logo y wordmark

`[pendiente]`

**Estado actual:** existen exploraciones de logo en `/references/claude-design-v1/` — `Mark Final.html`, `Mark Explorations.html`, `Wordmark Explorations.html`, `Wordmark Explorations v2.html`. No hay vector oficial ni versión final aprobada.

**Lo que ya se decidió en exploración:**

- La dirección elegida en las exploraciones es **01 · Plates** — un mark modular, dos tintas, que evoca supervisión y estructura
- El estilo es geométrico, estricto, sin ornamento
- El wordmark probablemente usa **IBM Plex Mono** (peso Regular o Medium) — coherente con la voz técnica y la paleta tipográfica del producto
- El mark funciona en dos tintas (monocromático) — no depende del color para su lectura

**Pendiente de producción:**

Cuando se vectorice el logo oficial, se crearán las siguientes variantes en `/brand/logo/`:

| Variante | Uso | Fondo |
|---|---|---|
| Mark + wordmark horizontal | Uso general, header de producto | Claro y oscuro |
| Mark + wordmark vertical | Presentaciones, documentos formales | Claro y oscuro |
| Mark solo | Favicon, avatar, contextos reducidos | Claro y oscuro |
| Wordmark solo | Contextos donde el mark no cabe | Claro y oscuro |
| Monograma (B o BaW) | Muy pequeño (<24px) | Claro y oscuro |
| Monocromo negro | Impresión, materiales físicos | Blanco |
| Monocromo blanco | Dark surfaces, materiales oscuros | Negro |

**Endorsement mark "powered by BaW":** también pendiente de vectorización. Se usará en materiales de edificios operated by BaW.

**Próximos pasos:**

1. Validar con el founder la dirección Plates vs. variantes
2. Vectorizar en Illustrator o Figma (formato SVG + PDF)
3. Generar todas las variantes de la tabla anterior
4. Documentar en ADR si hay cambio de dirección

---

### 5.2 Tipografía

`[estable]` — ver ADR 0002

BaW OS usa tres familias tipográficas con roles distintos y no intercambiables. Los tokens están en `/tokens/typography.css`.

#### La triada tipográfica

```
Inter          → UI, body, labels, sistema
IBM Plex Mono  → datos tabulares, código, voz técnica, IDs, timestamps
Instrument Serif → display editorial, momentos de marketing
```

#### Inter — La voz del sistema

Inter es la voz operativa de BaW OS. Es clara, neutra y funcional. Diseñada para pantallas a densidades altas, con glifos distinguibles (`1`, `l`, `I` son distintos) y métricas consistentes.

**Cuándo usar Inter:**

- Toda la navegación y chrome del producto
- Body copy en interfaces
- Labels, badges, estados
- Cualquier texto que acompaña datos o acciones
- Textos en español e inglés en el producto

**Configuración base:**

```css
/* Body */
font-family: 'Inter', sans-serif;
font-size: 14px;
line-height: 1.5;
font-variant-numeric: tabular-nums;

/* Labels */
font-size: 12px;
font-weight: 500;
letter-spacing: 0.01em;

/* Headings dentro del producto */
font-size: 16-24px;
font-weight: 600;
```

#### IBM Plex Mono — La voz técnica

IBM Plex Mono tiene un rol semántico preciso: aparece en datos que requieren precisión y alineación tabular, en contextos donde el usuario necesita leer valores exactos o identificadores únicos.

**Cuándo usar IBM Plex Mono:**

- IDs de contratos, reservas, transacciones (`CTR-2024-0892`)
- Timestamps exactos (`2026-05-14 · 09:42:18`)
- Importes en tablas financieras donde la alineación es crítica
- Columnas de datos en tablas densas (arrears, ledger)
- Terminales, logs de audit en modo debug
- Labels en mayúsculas para categorías técnicas (`AGENT · PULSO`)
- El wordmark (decisión pendiente de confirmación)

**Lo que NO hacer:** no usar IBM Plex Mono para body copy, párrafos o texto narrativo. Su valor semántico se diluye si aparece en contextos no-técnicos.

#### Instrument Serif — La voz editorial

Instrument Serif es la fuente para momentos de pausa: marketing, landing pages, portadas de reportes para owners, momentos de celebración en el producto (onboarding completado, primer mes de operación). Aporta calidad y calidez humana.

**Cuándo usar Instrument Serif:**

- Headlines en la landing/marketing site de BaW
- Portadas y covers de reportes para propietarios
- Empty states celebratorios ("Tu edificio lleva 30 días sin interrupciones")
- Citas y testimonios
- Momentos de onboarding con intención editorial

**Lo que NO hacer:** no usar Instrument Serif en tablas, interfaces densas, formularios o cualquier contexto donde la legibilidad a tamaño pequeño sea crítica. Tampoco en copy técnico.

#### Escala tipográfica

| Rol | Fuente | Tamaño | Peso | Uso |
|---|---|---|---|---|
| Display | Instrument Serif | 48–96px | 400 | Marketing, heroes |
| Heading XL | Inter | 32–48px | 600–700 | Titles de sección en marketing |
| Heading L | Inter | 24–32px | 600 | Heading de página en producto |
| Heading M | Inter | 20–24px | 600 | Sub-sección, modal title |
| Heading S | Inter | 16–18px | 600 | Card heading, panel title |
| Body L | Inter | 16px | 400 | Copy extenso, portales |
| Body M | Inter | 14px | 400 | Body estándar del producto |
| Body S | Inter | 13px | 400 | Tablas, listas densas |
| Label | Inter | 12px | 500 | Labels, badges, nav |
| Caption | Inter | 11px | 400 | Footnotes, metadata |
| Mono data | IBM Plex Mono | 13px | 400 | Datos, IDs, timestamps |
| Mono label | IBM Plex Mono | 11px | 500 | Labels de categoría técnica |

**Configuración global para tablas (no negociable):**

```css
table, .data-table {
  font-variant-numeric: tabular-nums lining-nums;
  font-feature-settings: "tnum" 1, "lnum" 1;
}
```

---

### 5.3 Color

`[estable]` — ver ADRs 0003, 0004, 0005

Los tokens están en `/tokens/colors.css`. Esta sección explica la estrategia; los valores exactos en hex/OKLCH están en el archivo de tokens.

#### Por qué OKLCH

OKLCH (Oklab Lightness, Chroma, Hue) es un espacio de color perceptualmente uniforme. Dos colores con el mismo valor L en OKLCH tienen el mismo brillo percibido por el ojo humano, sin importar el hue. Esto resuelve un problema clásico de los hex y HSL: un amarillo con `L: 50%` en HSL es mucho más brillante que un morado con la misma `L`.

**Ventajas prácticas para BaW OS:**

1. **Modos light/dark coherentes.** Se puede generar dark mode ajustando L en OKLCH y la paleta se mantiene armoniosa. No hay que escoger colores oscuros de forma manual para cada token.
2. **Wide gamut.** En pantallas P3 (todos los Mac modernos, iPhone), OKLCH puede expresar colores más saturados que sRGB.
3. **Escalas predecibles.** Generar una escala de 9 grises en OKLCH produce pasos perceptualmente equidistantes; en HSL no.

Linear usa esta misma estrategia para su sistema de color. BaW OS la adopta desde el origen para no cargar deuda de diseño.

#### Estrategia de modos

BaW OS tiene dos modos, ambos de primera clase. No es "dark mode opcional"; son dos paletas diseñadas con la misma atención.

- **Dark mode:** default para interfaces operativas (operations dashboard, units, agents, audit). Los operadores pasan horas en pantalla; el dark reduce la fatiga y hace pop los indicadores de estado (badges rojos, ámbar, verde).
- **Light mode:** default para portales (owner portal, tenant portal) y marketing site. Lectura casual, claridad, confianza financiera.
- El usuario puede cambiar el modo en configuración. El sistema respeta `prefers-color-scheme`.

La estrategia de elevación sigue el patrón Linear: distintas elevaciones se comunican con distintos valores de L en OKLCH, no con box shadows. Más claro = más elevado en dark mode; más oscuro = más elevado en light mode.

#### Brand color: indigo eléctrico (hue 266)

`[estable]` — ver ADR 0004

El color de marca de BaW es un **indigo eléctrico en hue 266**. Se posiciona entre el azul de Linear (más frío) y el púrpura de Stripe (más cálido). Es sharp, técnico, confiable sin ser corporativo.

Se usa en:
- Elementos interactivos primarios (botones CTA, links activos)
- Estados de selección y focus
- Chrome del producto (active nav items)
- Elementos de marca en marketing

**No se usa:** como background de área grande, en texto de body copy, mezclado con el agent color.

#### Agent color: violet (hue 300)

`[estable]` — ver ADR 0005

Las acciones iniciadas por agentes usan un color violet separado en **hue 300**. Este color distingue visualmente lo que hizo un agente de lo que hizo un humano o el sistema, en cualquier superficie donde aparezcan juntos.

**Separación semántica:**

```
Hue 266 (indigo) → Marca BaW, acciones humanas, UI chrome
Hue 300 (violet) → Acciones de agentes, identity de agentes, agent badges
```

**Por qué importa:** en el audit log unificado, en el timeline de una unidad, en el approval hub, el operador necesita escanear en un segundo si algo fue hecho por un agente o por una persona. El color diferenciado hace esa distinción posible sin leer texto.

El agent color aparece en:
- Badges de estado de acciones agénticas (`[AGENT · PULSO]`)
- Bordes de tarjetas en la sección de actividad de agentes
- Indicadores de "acción ejecutada por agente" en timelines
- El dot de estado en el agent status bar

#### Sistema semántico RAG + información

Los colores de estado son siempre los mismos, sin variación contextual:

| Semántico | Color | Uso |
|---|---|---|
| Error / crítico | Rojo | Atrasos graves, fallos, acciones que requieren intervención inmediata |
| Warning / riesgo | Ámbar | Situaciones en revisión, SLAs en riesgo, items que pueden escalar |
| Success / OK | Verde | Operaciones completadas, estados saludables |
| Info / neutro | Azul (hue ~220) | Información contextual, estados en progreso normales |
| Agent | Violet (hue 300) | Todo lo que es iniciado o ejecutado por un agente |

**Regla de accesibilidad no negociable:** el color nunca va solo. Siempre va acompañado de un label de texto o un icono. Los usuarios con daltonismo deben poder leer el estado sin depender del color.

#### Reglas de uso

- **Brand (indigo 266):** elementos interactivos, UI chrome, identidad
- **Agent (violet 300):** exclusivo para señalizar acciones agénticas
- **RAG semántico:** exclusivo para estados operativos
- **Neutrales:** todo lo demás — el ~85% de la interfaz

El principio: color es énfasis. Si todo es colorido, nada destaca. La mayoría de la interfaz debe ser neutra para que los estados de color sean escaneables.

---

### 5.4 Espaciado, forma y motion

`[estable]`

Los tokens están en `/tokens/spacing.css`.

#### Espaciado

**Base:** 4px. La escala tiene 13 niveles:

```
0px → 2px → 4px → 6px → 8px → 12px → 16px → 20px →
24px → 32px → 40px → 48px → 64px
```

Esta escala cubre todos los casos de uso del producto sin valores irregulares. Ningún valor de spacing se usa fuera de la escala.

**Filosofía de densidad:**
- Interfaces operativas (operations, units, audit) usan valores pequeños (4–12px) para maximizar información visible
- Portales y marketing usan valores grandes (24–64px) para claridad y respiro

#### Radii (esquinas)

BaW OS usa esquinas con radii pequeños — tight, en la línea de Linear. Nunca pill (border-radius: 9999px) excepto en badges de una palabra y elementos de toggle.

```css
--radius-sm:  4px;   /* inputs, tablas, componentes pequeños */
--radius-md:  6px;   /* cards, modales, dropdowns */
--radius-lg:  8px;   /* sheets, paneles laterales */
--radius-pill: 9999px; /* badges, tags, chips — solo estos */
```

#### Sombras

Sombras suaves y sutiles. Nunca dramáticas. La elevación se comunica principalmente con color (diferencia de L en OKLCH), no con shadow.

```css
--shadow-sm:  0 1px 2px rgba(0,0,0,0.05);
--shadow-md:  0 2px 8px rgba(0,0,0,0.08);
--shadow-lg:  0 4px 16px rgba(0,0,0,0.10);
```

#### Motion

BaW OS no usa animaciones decorativas. El motion tiene un propósito: comunicar cambio de estado, orientar la atención, señalar que algo está procesando.

**Duraciones:**

```css
--duration-instant:  80ms;   /* micro-feedback, hover states */
--duration-fast:    150ms;   /* transiciones de estado simples */
--duration-normal:  250ms;   /* modales, dropdowns, expansiones */
--duration-slow:    400ms;   /* transiciones de página, onboarding */
```

**Easing:**

```css
--ease-out:    cubic-bezier(0.16, 1, 0.3, 1);   /* default — entradas */
--ease-in-out: cubic-bezier(0.87, 0, 0.13, 1);  /* intercambios, swaps */
--ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1); /* confirmaciones, success */
```

**Default:** `ease-out` para la mayoría de las transiciones. Los elementos que entran a la vista usan ease-out (empiezan rápido, terminan suave). El spring solo para momentos de confirmación positiva.

**Respetar `prefers-reduced-motion`:** todas las animaciones se reducen a crossfades instantáneos si el sistema lo indica.

---

### 5.5 Accesibilidad

`[estable]`

Las reglas de accesibilidad de BaW OS no son negociables. Se aplican en todas las superficies del producto, incluyendo portales de propietarios, inquilinos y huéspedes.

#### Contraste

- **WCAG AA obligatorio:** texto de body 4.5:1 de contraste mínimo sobre su fondo; texto grande (18px+) 3:1
- Los tokens en `/tokens/colors.css` están definidos con los contrastes AA verificados para dark y light mode
- Nunca asumir que el contraste en Figma es el mismo que en pantalla — verificar en DevTools o con herramienta dedicada

#### Color y daltonismo

- El color nunca es el único discriminador de información. Siempre hay texto, ícono o posición como segundo canal.
- El daltonismo rojo-verde afecta al 8% de los hombres. Los colores RAG (rojo/ámbar/verde) van siempre con ícono + label.
- El agent color (violet 300) y el brand color (indigo 266) deben distinguirse en todos los contextos — incluyendo con filtros de daltonismo.
- Herramienta: DevTools → Rendering → Emulate vision deficiencies

#### Teclado y foco

- Todo elemento interactivo es accesible por teclado sin excepción
- El estado de focus visible usa el brand color con offset de 2px — nunca `outline: none` sin reemplazo visual
- El command palette (`⌘K`) es el shortcut central de navegación — documentar todos los shortcuts en la UI
- Tab order lógico en todas las pantallas; verificar con teclado en cada PR de nueva UI

#### Tamaños mínimos

- Texto body: mínimo 12px (`font-size: 0.75rem`). Jamás menos.
- Targets interactivos: mínimo 44×44px (WCAG 2.5.5) — aunque el ícono sea de 16px, el área clickable debe ser 44px
- En móvil (portales): targets de 48px mínimo

---

### 5.6 Iconografía

`[pendiente]`

No hay una librería de íconos oficial seleccionada. Los lineamientos para cuando se decida:

- **Estilo:** stroke-based, no filled
- **Stroke width:** 1.5px
- **Tamaños:** 16, 20, 24px (nunca valores intermedios)
- **Grid:** 24px con padding interno de 2px (área activa de 20px)
- **Estilo visual:** geométrico, simple, sin ornamentos. Compatibles con la geometría del logo
- **Referencias seguras:** [Lucide](https://lucide.dev) (MIT) y [Phosphor](https://phosphoricons.com) (MIT) son los candidatos más probables
- **Íconos de agentes:** cada agente (Rumbo, Pulso, Trazo, etc.) puede tener un ícono geométrico propio para su identidad visual en el producto. Pendiente de definición.

**Decisión pendiente:** evaluar si adoptar Lucide directamente, hacer un fork estilizado, o diseñar un set propio cuando haya recursos. El set propio da más identidad pero tiene costo de producción alto.

---

### 5.6 Componentes de sistema — patrones core

`[en revisión]`

Los componentes de BaW OS siguen patrones consistentes. Esta sección documenta los patrones más relevantes para el producto hasta que exista una librería de componentes formal.

#### Badges y status indicators

Taxonomía estricta: los badges comunican estado, no categoría.

| Componente | Tipo | Uso en BaW OS | Interactivo |
|---|---|---|---|
| Status badge | Estático | Estado de contrato, unidad, acción de agente | No |
| Agent badge | Estático + color agent | Identidad del agente que realizó una acción | No |
| Priority badge | Estático + color RAG | Urgencia de un ticket o excepción | No |
| Filter chip | Interactivo | Filtros de tabla, selección de estado | Sí |
| Count badge | Estático | Número de items en approval queue, notificaciones | No |

Reglas de uso:
- Máximo 3 palabras por badge
- Labels en mayúsculas para categorías técnicas (`PENDING REVIEW`, `BY AGENT`)
- Labels en title case para estados operativos (`En progreso`, `Resuelto`)
- Nunca un badge como único indicador de estado — siempre acompañado de contexto

**Estados estándar en BaW OS:**

```
PENDING REVIEW   → Badge ámbar  (acción de agente esperando aprobación)
BY AGENT         → Badge violet  (acción ejecutada autónomamente)
IN PROGRESS      → Badge azul    (en ejecución)
COMPLETED        → Badge verde   (terminado)
BLOCKED          → Badge rojo    (requiere intervención)
ESCALATED        → Badge naranja (escalado a humano)
OVERDUE          → Badge rojo    (fuera de SLA)
```

#### Tablas de datos

Las tablas son el componente principal de las interfaces operativas de BaW OS. Principios:

- `font-variant-numeric: tabular-nums` en todas las columnas numéricas — siempre
- `font-size: 13px`, `line-height: 1.4` para densidad máxima legible
- Columnas de estado con badge de color + texto — nunca solo color
- Columna de “última actividad de agente” con badge de agente + timestamp en IBM Plex Mono
- Acciones por fila: máximo 2-3 en hover, el resto en un menu (...)
- Row selection con checkbox + barra de acciones en bulk en el top
- Empty state con mensaje contextual (ver reglas de copy en sección 6)

#### Split view

El patrón primario para listas con detail. Lista a la izquierda, detail panel a la derecha (cuando el viewport lo permite).

```
┌────────────────────┬──────────────────────────┐
│ [Filtros]         │ [Breadcrumb > Unidad 204]    │
│                   │                              │
│ Unidad 204  ▶     │ Unidad 204                   │
│ Unidad 301        │ ─────────────────────────│
│ Unidad 402        │ [Tabs: Overview | Timeline | │
│ Unidad 501        │        Contratos | Pagos]     │
│ …                │                              │
└────────────────────┴──────────────────────────┘
```

Proporciones: lista 35-40% del ancho, detail 60-65%. En móvil: colapsa a navegación de una sola columna (lista primero, detail en vista separada).

#### Evidence Panel (approval hub)

El componente más específico de BaW OS — no existe en SaaS tradicional. Aparece en el approval hub y en el agent fleet view.

Estructura del evidence panel:

```
┌──────────────────────────────────────────────┐
│ PULSO · Collections                  [Confidence 97%] │
│ Propone enviar recordatorio a 47 inquilinos            │
│                                                        │
│ Qué pasará:                                             │
│ 47 mensajes WhatsApp + email por $143,200 MXN en       │
│ atrasos. 12 con >30 días, 35 con 15-29 días.          │
│                                                        │
│ Por qué:                                               │
│ Política: recordatorio automático días 15 y 30 de     │
│ cada mes. Hoy es día 15.                               │
│                                                        │
│ [Ver detalle] [Editar lista]                           │
│ ────────────────────────────────────────────── │
│ [Aprobar]  [Rechazar]  [Modificar]  [Diferir]         │
└──────────────────────────────────────────────┘
```

El evidence panel debería permitir al revisor tomar una decisión en 10-30 segundos sin leer documentación adicional. Si no es posible, el evidence pack está mal diseñado.

#### Owner Portal — principios de diseño específicos

El owner portal es la interfaz de menor densidad del sistema. El propietario visita el portal ocasionalmente (1-2 veces por semana) para revisar estado financiero, aprobar gastos y leer el resumen de actividad del edificio.

Principios específicos:
- Light mode como default (lectura casual, confianza financiera)
- Instrument Serif en el KPI hero ("$XXX,XXX MXN este mes") — el único contexto donde Instrument Serif aparece en el producto
- Inter para todo lo demás
- IBM Plex Mono para los números exactos en la tabla de transacciones
- Arquitectura tipo Stripe Billing: hero con la cifra importante, desglose por categoría abajo
- Resumen de actividad de agentes: `"Esta semana Eco atendió 24 mensajes, Pulso cobró $312,000 y Trazo cerró 3 tickets de mantenimiento."` — lenguaje narrativo, no tabla

#### Tenant / Guest Portal — principios de diseño específicos

El más simple del sistema. Mobile-first obligatorio. El inquilino o huésped no necesita ver cómo funciona BaW OS por dentro.

Principios específicos:
- Single page scrollable en móvil
- Brand del edificio domina, BaW invisible o como footnote
- Número de acciones disponibles: máximo 5 (pagar, reportar problema, ver documentos, contactar, ver reserva)
- El AI concierge (Eco) aparece como asistente del edificio, no como "AI": `"Conserje digital del Edificio Mateos"`
- Notificaciones push para pagos y respuestas, nunca para actividad interna del sistema

---

## 6. Voz y tono

`[estable]`

### Personalidad de marca

BaW habla con cinco atributos que se mantienen consistentes en todos los contextos:

1. **Confiada, no arrogante.** Sabe lo que hace. No necesita adornar ni sobre-explicar.
2. **Técnica, pero humana.** Entiende de APIs, agentes y tokens — pero habla con personas, no con documentación.
3. **Directa.** Dice lo que pasó, por qué, y qué hacer. Sin rodeos ni padding.
4. **Discreta.** El edificio que funciona bien no grita que funciona bien. BaW tampoco.
5. **Sin pretensión.** No usa jerga de startup, no finge ser algo más grande de lo que es, no usa palabras que la gente no usa.

### BaW en español y en inglés

BaW opera principalmente en español (LATAM, México-first). El producto tiene interfaces en español. La comunicación con operadores y propietarios es en español. El marketing para el mercado LATAM es en español.

El inglés se usa en:
- Documentación técnica de la API
- Comunicaciones con inversionistas internacionales
- Términos técnicos del diseño de sistema (design tokens, agent, control plane) que no se traducen

Los términos técnicos estándar permanecen en inglés aunque el contexto sea español: "design tokens", "intent surface", "brand hue", "control plane", "autonomy dial". No se traducen porque ya tienen significado técnico preciso establecido.

### Ejemplos de voz

**Error message:**
> ❌ Mal: "¡Vaya! Algo salió mal. Inténtalo de nuevo."
> ✅ Bien: "No se pudo enviar el recordatorio. El correo de García, José está marcado como inválido. Actualízalo en el perfil del inquilino."

**Success message:**
> ❌ Mal: "¡Éxito! Tu tarea se completó correctamente."
> ✅ Bien: "Pulso envió 23 recordatorios de pago. Puedes deshacerlo en los próximos 30 minutos."

**Empty state (exception inbox vacío):**
> ❌ Mal: "No hay nada aquí."
> ✅ Bien: "Sin excepciones. Los agentes están operando dentro de los parámetros normales."

**Onboarding — primer agente activado:**
> ❌ Mal: "¡Felicidades! Acabas de activar tu primer agente de IA. ¡Esto es increíble!"
> ✅ Bien: "Eco está activo. A partir de ahora atiende mensajes entrantes de WhatsApp e identifica los que requieren tu atención."

**Marketing copy (landing site):**
> ❌ Mal: "La plataforma de IA que revoluciona la administración de propiedades con tecnología de punta."
> ✅ Bien: "Tu edificio opera. Tú supervisas."

### Lo que NO somos (anti-patrones de copy)

- No usamos "revolucionario", "disruptivo", "de vanguardia", "de última generación"
- No usamos exclamaciones en interfaces operativas
- No fingimos que los agentes son personas (`"Hola, soy Pulso y estoy aquí para ayudarte"`)
- No usamos passive voice en mensajes de estado (`"El recordatorio fue enviado"` → `"Pulso envió el recordatorio"`)
- No pedimos disculpas innecesariamente en mensajes de error
- No usamos "¿Sabías que...?" ni tips no solicitados
- No tratamos al operador como si no entendiera el sistema

### Copy para estados de agentes

El copy de los estados agénticos sigue reglas precisas:

**Nombres de agentes en copy:** siempre en mayúsculas (`PULSO`, `ECO`), seguidos de su acción en pasado o en infinitivo según el contexto:
- Estado pasado: `"Pulso envió 24 recordatorios"` (el agente es el sujeto, acción en pasado)
- Estado en curso: `"Trazo está evaluando vendors para U-204"` (progresivo)
- Propuesta: `"Brisa propone enviar oferta de renovación"` (propuesta, no orden)

**Empty states:** no dicen "No hay datos" — dicen qué significa ese estado operativamente:

| Superficie | Copy ❌ incorrecto | Copy ✅ correcto |
|---|---|---|
| Agent Inbox vacío | "No hay notificaciones" | "Sin excepciones. Los agentes están operando dentro de los parámetros normales." |
| Collections sin atrasos | "Sin registros" | "Todos los cobros al corriente. Pulso monitorea vencimientos esta semana." |
| Maintenance sin tickets | "Sin tickets" | "Sin incidencias activas. Trazo completó los últimos 3 tickets esta semana." |
| Audit log sin actividad reciente | "Sin registros" | "Sin actividad en las últimas 2 horas." |

**Mensajes de aprobación:** siempre incluyen el impacto:
- ❌ "¿Aprobar esta acción?"
- ✅ `"Pulso propone enviar 47 recordatorios de pago por $143,200 MXN. Se enviarán vía WhatsApp + email. Puedes revertir en los próximos 30 minutos.`

**Mensajes de confianza del agente:**
- Confidence alta (>90%): no se muestra el porcentaje — se muestra como acción directa
- Confidence media (70-90%): se muestra con señal visual discreta, sin número
- Confidence baja (<70%): el agente escala explícitamente en lugar de ejecutar

### Glosario de copy — términos que se usan y cómo

| Término | Uso correcto | Uso incorrecto |
|---|---|---|
| Agente | `"El agente Pulso…"` o `"Pulso (cobranza)…"` | `"Tu asistente de IA…"` / `"El bot…"` |
| Aprobar | `"Aprueba este plan"` | `"Confirma"` / `"Acepta"` |
| Excepción | `"Esta excepción requiere tu revisión"` | `"Error"` / `"Alerta"` |
| Autonomy dial | No se traduce | — |
| Control plane | No se traduce | — |
| Acción revertida | `"La acción fue revertida"` | `"Deshecho"` / `"Cancelado"` |
| Supervision | `"Supervisión"` | `"Monitoreo"` (tiene connotaciones distintas) |

---

## 7. Aplicaciones

### 7.1 Producto — BaW OS

`[en revisión]`

#### Surfaces principales

BaW OS implementa el modelo de triple capa de Nielsen como surfaces concretas:

**Intent Surface:** El operador declara qué quiere que pase. Comandos naturales, búsqueda semántica, command palette (`⌘K`). Ejemplo: `"Cobra atrasos del piso 8"` o `"¿Por qué bajó la ocupación esta semana?"`. Esta surface es la menos desarrollada en la versión inicial — se construye conforme el producto madura.

**Orchestration Surface:** La más crítica. Incluye:
- **Agent Inbox:** queue de excepciones y acciones pendientes de revisión
- **Approval Hub:** acciones con evidence pack esperando go/no-go
- **Intent Preview:** plan del agente antes de ejecutar, con `[Proceder] [Editar] [Hacerlo yo]`
- **Autonomy Dial:** control de nivel de autonomía por workflow y por edificio

**Direct Manipulation Surface:** La GUI tradicional persiste para:
- Edge cases y situaciones fuera del scope del agente
- Overrides y correcciones manuales
- Auditoría y revisión histórica
- Onboarding y configuración inicial

#### Patrones core del producto

**Agent Inbox:** el operador abre el sistema y ve las excepciones del día, no un dashboard de métricas. Cada item tiene: qué agente lo escala, qué pasó, qué opciones hay, cuánto tiempo hay para decidir.

**Approval Hub:** las acciones que requieren aprobación se presentan con evidence pack completo: qué se propone, por qué el agente cree que es correcto, qué pasa si se aprueba vs. rechaza, data de soporte. El revisor puede: aprobar, rechazar, aprobar con edits, delegar, diferir, pedir más contexto.

**Autonomy Dial:** cuatro niveles por workflow:

```
L1 — Observe & Suggest     → Detecta, no actúa. Propone al operador.
L2 — Plan & Propose        → Crea un plan. Humano aprueba cada uno.
L3 — Act with Confirmation → Prepara y ejecuta con go/no-go previo.
L4 — Act Autonomously      → Ejecuta y notifica. Sin fricción previa.
```

La autonomía se gana con historial. Un agente nuevo inicia en L1 o L2. Sube a L3/L4 cuando el operador tiene suficiente evidencia de que sus decisiones son confiables.

**Action Receipt:** después de toda acción consecuente, el agente presenta un receipt: qué cambió, en qué unidad/contrato/registro, timestamp, ventana de undo si aplica. No es un log de debug — es un recibo legible para el operador.

**Intent Preview (Plan Summary):** antes de ejecutar una acción compleja, el agente presenta el plan paso a paso en lenguaje claro. El operador puede proceder, editar el plan, o tomar control manual. Si más del 10% de los planes son rechazados, el modelo necesita revisión.

El research interno (`baw-os-design-research.md`) documenta que aprobar el plan completo antes de la ejecución es significativamente más efectivo que aprobar paso a paso — reduce la ocurrencia de acciones problemáticas con un odds ratio de 0.25 (p<0.001) respecto al modelo step-by-step. El diseño del approval hub sigue esta evidencia: los agentes presentan el plan completo, no piden permiso en cada paso.

#### Taxonomy de aprobaciones por dominio

No todas las acciones de agentes requieren el mismo nivel de revisión. La clasificación en tres tiers por dominio define el comportamiento de fábrica:

| Dominio | AUTO (ejecuta sin aprobación) | LOG (ejecuta y registra) | REQUIRE_APPROVAL (bloquea) |
|---|---|---|---|
| **Collections** | Recordatorios standard pre-vencimiento | Warnings de atraso 15–30 días | Corte de servicio, acción legal, write-off |
| **Maintenance** | Scheduling rutinario, asignación a staff interno | Costo <umbral definido por edificio | Costo >umbral, vendor nuevo, afecta ocupación |
| **Guest comms** | FAQs, confirmaciones de reserva | Respuestas con tono personalizado | Disputas, reembolsos, respuestas a reviews públicas |
| **Pricing** | Ajustes <5% según market data | Ajustes 5–15% | Ajustes >15%, cambios de política base |
| **Leasing** | Pre-screening inicial de aplicantes | Respuestas rutinarias a prospectos | Aprobación final de contrato, concesiones |
| **Financial** | Reconciliaciones de cierre | Emisión de receipts, CFDI estándar | Transferencias, pagos a vendors, reembolsos |

Los umbrales de los tiers son configurables por edificio. Los valores default son conservadores (L1 para agentes nuevos) y se ajustan conforme el operador gana confianza en el sistema.

#### Estado machine agéntica — diseño de interfaz

Toda acción de agente transita por una máquina de estados con tratamiento visual consistente:

```
IDLE / WAITING FOR TRIGGER
        ↓
PLANNING (reasoning, descomposición de tarea)
        ↓
SUGGESTED BY AGENT (plan creado, esperando revisión humana)
        ↓
    ┌───┴───┐
APPROVED  REJECTED (con razón → PLANNING o BLOCKED)
    ↓
EXECUTING (herramientas siendo llamadas)
    ↓
    ┌──────┬──────┬──────┐
COMPLETED  ESCALATED  BLOCKED
    ↓           ↓          ↓
  DONE    PENDING HUMAN  NEEDS INTERVENTION
                ↓
           RESUMED or ABORTED
```

| Estado | Tratamiento visual | Acción requerida | Data a mostrar |
|---|---|---|---|
| **Suggested by Agent** | Badge ámbar `Pending Review` | Revisar + aprobar/editar/rechazar | Intent Preview, evidence pack, confidence score |
| **Pending Approval** | Ícono reloj, countdown SLA | Aprobar / rechazar / delegar | Asignado a, tiempo restante antes de escalamiento |
| **Executing** | Progress animado | Pause / stop disponibles | Paso actual, % completado, ETA |
| **Completed** | Check verde | Opcional: revisar receipt | Action receipt: qué cambió, diffs, ventana de rollback |
| **Executed Autonomously** | Check verde + tag `By Agent` | Opcional: undo en ventana | Igual + `"Undo disponible X min"` |
| **Escalated to Human** | Badge naranja + asignado a | Humano debe actuar | Contexto completo + lo que el agente intentó |
| **Blocked** | Badge rojo | Intervención humana | Qué bloquea, resolución sugerida, impacto downstream |
| **Failed** | Badge rojo | Investigar + decidir | Error, estado parcial, rollback, recovery path |
| **Undone** | Tachado + tag `Reversed` | Ninguna | Estado before/after, quién inició, timestamp |

#### Pantallas principales de BaW OS

**Executive Mission Control**

La vista de liderazgo y portfolio. No es un dashboard de widgets — es una superficie exception-first donde el default es "todo está bien" y las excepciones suben a primer plano.

Estructura:
- **Top:** panel de excepciones activas (`N items requieren tu atención`)
- **Medio:** KPIs del portfolio con sparklines — ocupación, NOI, atrasos, incidencias abiertas
- **Inferior izquierdo:** actividad reciente de agentes (últimas 24h, format compacto)
- **Inferior derecho:** tabla de edificios con RAG status por dimensión

El diseño sigue el patrón NASA/NOC: lo off-nominal en rojo o ámbar, lo normal en neutro. No se usa verde activo para marcar lo que funciona bien — el neutro celebra la normalidad.

**Operations Dashboard**

La vista del property manager que opera el día a día. Densa, funcional, sin ornamento.

Estructura:
- **Strip superior:** resumen del día (check-ins, check-outs, tareas pendientes, citas de mantenimiento)
- **Central:** tabla de unidades con estado (libre / ocupado / check-in hoy / mantenimiento / inspección)
- **Panel lateral:** agent operations — agentes activos, misiones en curso, items en approval queue
- **Filtros:** por edificio, piso, tipo de unidad, estado

**Units — Gestión de unidades**

- Vista tabular con estado de ocupación, contrato actual, último pago, última acción del agente
- Toggle a vista de card para escaneo rápido de portfolio
- Drill-down a Unit Detail: timeline unificado de eventos (humanos + agentes), contratos, pagos, mantenimiento, documentos
- Columna `Agent Activity` con última acción autónoma + confidence score

**Contracts**

- Lista + state machine visual: draft / active / renewing / ending soon / terminated
- Tabs por estado (el usuario ve solo los contratos relevantes para su acción)
- En el detail: timeline de interacciones del agente Brisa (renovaciones, comunicaciones, alertas)
- Acciones sugeridas por agente: `"Brisa sugiere enviar propuesta de renovación — vence en 45 días"`

**Collections / Arrears**

- Exception-first: el top muestra los casos que requieren intervención humana
- Tabla de aging buckets: 0–15 días / 16–30 días / 31+ días
- Por cada inquilino en atraso: historial de gestiones de Pulso, promesas de pago registradas, acciones pendientes de aprobación
- Pulso visible como actor en la gestión: qué envió, cuándo, qué respuesta recibió

**Maintenance / Incidents**

- Vista Kanban + toggleable a lista
- Columnas: Nuevo / Asignado / En progreso / Esperando partes / Resuelto
- Trazo visible en el flujo: triage automático, sugerencia de vendor, scheduling propuesto
- SLA countdown visible en cada ticket; escalamiento automático cuando el SLA está en riesgo
- Costo estimado vs. real al cerrar el ticket

**Agent Fleet View**

La pantalla más importante del punto de vista de diseño agent-native. No es un chatbot — es un panel de control de la fuerza de trabajo.

Estructura:
- **Roster:** los 7 agentes con nombre, rol, estado (idle / running / paused), y métricas clave (misiones completadas hoy, tasa de intervención humana, confidence promedio)
- **Active missions:** tabla de tareas en curso con tipo, unidad afectada, agente responsable, estado, ETA
- **Approval queue:** items esperando go/no-go, con evidence pack expandible
- **Controls por agente:** nivel de autonomía (L1–L4) configurable por dominio, toggle de pausa
- **Agent activity log:** historial filtrable por agente, acción, unidad

El toggle de pausa de un agente requiere confirmación explícita — es una acción consecuente. El UI puede inspirarse en el patrón hardware: toggle grande con confirmación modal antes de apagar un servicio activo.

**Audit Log unificado**

Timeline cronológico de todas las acciones, humanas y agénticas, en el sistema.

```
[AGENT · PULSO]     12:03  Generó batch de 47 recordatorios de pago
[AGENT · PULSO]     12:03  Confidence: 97% | Plan aprobado por: María R.
[HUMAN · María R.]  12:05  Aprobó batch ($143,200 MXN)
[AGENT · PULSO]     12:05  Envió recordatorios vía WhatsApp + email
[SYSTEM]            12:05  Ventana de rollback activa hasta 12:35
```

Filtros: por edificio, unidad, agente, actor (humano/agente/sistema), tipo de acción, rango de fechas. Export a CSV para compliance.

**Automations / Rules**

Superficie donde el operador configura las políticas que los agentes siguen. No es el workspace cotidiano — se visita para configurar y ajustar.

- Biblioteca de templates (playbooks predefinidos para cobranza, mantenimiento, leasing)
- Builder de triggers en lenguaje natural con preview de cuándo habrían disparado en los últimos 30 días
- Control de umbrales de autonomía por dominio
- Historial de cambios a reglas con rollback

#### Arquitectura de información — navegación

BaW OS usa una arquitectura de navegación **inverted L-shape**: sidebar vertical + top bar horizontal.

```
┌──────────────────────────────────────────────────────────────────┐
│  [Logo BaW]  [Selector edificio ▾]  [⌘K]  [●]  [🔔] [avatar]   │
├──────────────┬───────────────────────────────────────────────────┤
│              │                                                   │
│  Mission     │                                                   │
│  Operations  │         Main content area                        │
│  Units       │                                                   │
│  Contracts   │         (split view con detail panel             │
│  Collections │          cuando hay item seleccionado)            │
│  Maintenance │                                                   │
│  ──────────  │                                                   │
│  Agents ●   │                                                   │
│  Audit Log   │                                                   │
│  Automations │                                                   │
│  ──────────  │                                                   │
│  Settings    │                                                   │
│              │                                                   │
└──────────────┴───────────────────────────────────────────────────┘
```

- Sidebar colapsable: 240px expandido, 56px colapsado (solo íconos)
- El dot `●` junto a "Agents" indica que hay items en el approval queue
- El indicador `[●]` en el top bar muestra el estado del fleet de agentes (idle/active/attention needed) con color semántico
- `⌘K` abre el command palette — búsqueda global + comandos frecuentes
- El selector de edificio permite cambiar el contexto sin salir de la vista actual
- Split view como workhorse: lista a la izquierda + detail panel a la derecha cuando hay item seleccionado

#### Prioridades de la primera versión

En la v1 de BaW OS (en desarrollo), las prioridades de diseño son:

1. Exception inbox + approval hub (orchestration surface core)
2. Operations dashboard (estado del edificio, exception-first)
3. Units + contracts (gestión básica con agent attribution)
4. Audit log unificado (humano + agente, filtrable)
5. Agent fleet view (estado de los 7 agentes, missions activas)

El intent surface (comandos naturales) y el autonomy dial completo son Fase 1 (post-v1).

---

### 7.2 Web — landing y brand site

`[pendiente]`

El dominio principal (`baw.[tld]`) será el marketing site. El TLD está pendiente de definición.

**Tono:** más editorial que el producto. Instrument Serif toma protagonismo en headlines. El copy es confiado y económico. Cero fluff.

**Estructura mínima del marketing site:**

- Hero: la tesis en una línea + CTA a demo
- Cómo funciona: el modelo agente-supervisor explicado visualmente
- Los 7 agentes: quiénes son y qué hacen
- Case study: BaW Mateos 809 como referencia
- Para quién: property managers profesionales e independientes

**Brand site** (`brand.baw.[tld]`): documentación pública del design system. Viene después de que el sistema esté estabilizado (Fase 2 del roadmap).

**Principios visuales del marketing site:**

- Dark background como default (proyecta carácter técnico-premium; contraste con la competencia que usa light backgrounds genéricos)
- Instrument Serif en headlines a tamaños grandes (48-96px)
- Inter para body copy y UI elements de la landing
- IBM Plex Mono para mostrar datos o código en secciones técnicas
- Animaciones sutiles: datos que suben, agentes que se activan, building status que cambia — todo en duraciones lentas (400ms+)
- Nada de ilustraciones stock ni imágenes genéricas de edificios. Si hay fotografía, es de Mateos 809.

---

### 7.3 Edificios powered by BaW

`[en revisión]`

#### Coexistencia de marcas

Cada edificio mantiene su marca propia. BaW opera como infraestructura invisible hacia el huésped o inquilino. El endorsement "powered by BaW" es discreto y opcional.

**Regla de coexistencia:**

```
¿El usuario es operador/propietario? → BaW domina
¿El usuario es huésped/inquilino?   → Marca del edificio domina
                                      BaW = endorsement opcional
```

#### BaW Mateos 809 como caso de referencia

Mateos 809 es el laboratorio de BaW. Todas las funciones del producto se prueban primero aquí. Es también el primer case study para la venta B2B: "Así opera BaW en un edificio real."

Las decisiones de marca para Mateos 809:
- El edificio tiene su propia identidad visual (pendiente de definición completa)
- Los materiales para huéspedes usan la marca del edificio, no BaW OS
- El endorsement "powered by BaW" puede aparecer en el pie de materiales formales (contrato, statement del owner)

#### Superficies físicas

Cuando los edificios produzcan materiales físicos (señalética, llaves digitales, manual de huésped, materiales de bienvenida):

- Marca del edificio en primer plano
- Tipografía del edificio (puede diferir de Inter/IBM Plex Mono)
- "powered by BaW" en tamaño reducido, fuente consistente con BaW OS
- No usar el brand color de BaW en superficies del edificio sin validación previa

---

### 7.4 Marketing y papelería

`[pendiente]`

**Plantillas pendientes:**

- Business cards (cuando haya logo vectorizado)
- Deck de presentación (Keynote/PowerPoint)
- Propuesta comercial template
- One-pager de BaW OS para property managers

**Print:** cuando se produzca material impreso, el master va en Illustrator o InDesign. Colores con CMYK equivalentes + Pantone de referencia cuando se requiera consistencia cross-media. Los valores OKLCH/hex no son directamente trasladables a CMYK — se necesitará perfilar los equivalentes cuando llegue el momento.

### Consideraciones LATAM-específicas

BaW OS opera en México primero, con expansión planeada a Colombia, Brasil y Chile. Hay cuatro factores de diseño específicos a este mercado que el sistema debe contemplar:

**1. WhatsApp como canal primario**

La mayor parte de la comunicación entre edificios y sus stakeholders (huéspedes, inquilinos, proveedores) ocurre por WhatsApp. El agente Eco debe diseñarse primero para WhatsApp, no como add-on. Los action receipts y las notificaciones deben funcionar en el contexto de una conversación de WhatsApp, no solo en el inbox del producto.

**2. CFDI y SAT (México)**

La emisión de facturas electrónicas (CFDI) es requisito legal para cualquier transacción entre empresas en México. El agente Sello tiene responsabilidad directa sobre este proceso. El UI debe mostrar el status CFDI de cada transacción de forma clara: borrador / enviado / validado / cancelado. Los errores de CFDI son excepciones de alta prioridad.

**3. Español neutro LATAM**

El producto usa español neutro, evitando modismos de una sola región. Ejemplo: `"departamento"` en lugar de `"piso"` (México / Argentina) o `"apartamento"` (Colombia), a menos que el contexto del edificio sea específico. En los portales de huéspedes, se puede ajustar el registro según la configuración del edificio.

**4. Modelo híbrido STR/MTR/LTR**

La mayoría de los edificios en el mercado objetivo operan modelos híbridos: algunas unidades en renta corta (Airbnb, Booking), otras en renta media (3-12 meses), otras en renta larga (>12 meses). El sistema de marca y el producto deben ser agnosóticos al modelo de renta — no asumir que todas las unidades son del mismo tipo. Las etiquetas en la interfaz ("reserva", "contrato", "inquilino", "huésped") deben ser correctas según el tipo de unidad.

---

## 8. Roadmap del sistema

El sistema de diseño evoluciona en cuatro fases alineadas con la madurez del producto y del equipo. Actualmente en Fase 0.

### Fase 0 — Foundations (ahora)

**Objetivo:** que los tokens estén disponibles en `baw-os` y que cualquier nuevo componente se pueda construir con las variables definidas. Sin herramientas de build adicionales, sin dependencias complejas.

- [x] Brand Foundations (este documento)
- [x] Design tokens en `/tokens/*.css`
- [ ] Git submodule `baw-design` → `baw-os` configurado
- [ ] README de setup del submodule con instrucciones para nuevo dev
- [ ] Decisiones ADR 0001–0005 redactadas
- [ ] Verificación de que todos los tokens se importan correctamente en el proyecto Next.js

**Nivel de madurez:** Nivel 2 (Git submodule). Sin Style Dictionary ni npm privado. Los tokens son CSS custom properties importadas directamente en `globals.css` de `baw-os`.

**Cómo funciona el submodule:**

```bash
# En baw-os, agregar baw-design como submodule
git submodule add https://github.com/zxy-vc/baw-design.git design
git submodule update --init

# En globals.css de baw-os
@import './design/tokens/index.css';
```

Los tokens de `/tokens/index.css` re-exportan todos los tokens de `/tokens/{colors,typography,spacing}.css`.

### Fase 1 — UI inicial + logo

**Objetivo:** BaW OS tiene una UI funcional y reconocible usando el sistema de tokens. El logo existe en vector.

- [ ] Logo vectorizado oficial (mark + wordmark + variantes en SVG + PDF)
- [ ] Primer pase de UI en `baw-os` con los tokens aplicados
- [ ] Exception inbox + approval hub funcionales
- [ ] Operations dashboard (exception-first)
- [ ] Agent fleet view (las 7 tarjetas de agente)
- [ ] Audit log unificado (humano + agente)
- [ ] Marketing site mínimo (`baw.[tld]`)
- [ ] Endorsement mark "powered by BaW" vectorizado

**Criterio de éxito:** Un property manager que ve BaW OS por primera vez puede navegar las pantallas principales sin guía y entender la diferencia entre lo que hicieron los agentes y lo que requiere su atención.

### Fase 2 — Sistema versionado

**Objetivo:** los tokens tienen una fuente única y se compilan a múltiples formatos. Existe una librería de componentes que puede consumirse por múltiples apps.

- [ ] Style Dictionary: tokens compilados a CSS, JS, JSON desde una fuente única en YAML/JSON
- [ ] Paquete npm privado `@baw/design-tokens` publicado en GitHub Packages
- [ ] Librería de componentes (Storybook) con los componentes core de BaW OS
- [ ] Documentación pública del design system (`brand.baw.[tld]`)
- [ ] Figma file sincronizado con tokens via Tokens Studio

**Prerequisito:** antes de Fase 2, tener al menos 10 componentes estables en `baw-os` que justifiquen la extracción a librería.

### Fase 3 — Multi-app + marketing

**Objetivo:** el sistema sirve múltiples aplicaciones (baw-os, portales de edificios, marketing site) con una sola fuente de verdad. Las plantillas de marketing están sistematizadas.

- [ ] Sincronización Figma ↔ tokens (via Tokens Studio o equiv.)
- [ ] Plantillas de marketing y print (Keynote, Illustrator)
- [ ] Sistema adaptado para múltiples edificios con marca propia (theming por edificio)
- [ ] Posible separación de `baw-design` como paquete independiente si hay múltiples apps o clientes
- [ ] Documentación de theming para edificios: cómo un nuevo edificio puede tener su paleta sobre el sistema base

---

## 9. Glosario

Términos técnicos usados en este documento y en el producto. Definiciones precisas para usar de forma consistente en copy, documentación y código.

| Término | Definición |
|---|---|
| **agent-native** | Software diseñado desde el origen para que agentes de IA sean actores de primera clase en el sistema, no features añadidas. Los agentes tienen identidad, permisos, visibilidad y auditoría equivalentes a los usuarios humanos. |
| **control plane** | La superficie desde la que el operador configura políticas, supervisa agentes y toma control cuando se necesita. BaW OS es la implementación del control plane de un edificio. |
| **intent surface** | La capa de la interfaz donde el usuario declara qué quiere que ocurra, sin especificar los pasos. Comandos naturales, búsqueda semántica, command palette. |
| **orchestration surface** | La capa donde se negocia entre la intención del usuario y la ejecución del agente. Incluye el plan preview, el approval hub, los receipts y el manejo de conflictos. La más crítica del sistema. |
| **direct manipulation surface** | La GUI tradicional — tablas, formularios, vistas clásicas. Persiste en BaW OS como fallback para edge cases, overrides y auditoría. |
| **autonomy dial** | Control que configura el nivel de independencia de un agente en un workflow específico. Cuatro niveles: Observe & Suggest → Plan & Propose → Act with Confirmation → Act Autonomously. |
| **action receipt** | Documento post-ejecución que registra qué cambió, en qué registro, cuándo, por quién (agente o humano), con ventana de undo si aplica. Comportamiento de fábrica para toda acción consecuente. |
| **intent preview** | Plan que el agente presenta antes de ejecutar una acción compleja. Legible, en lenguaje claro, con opciones: `[Proceder] [Editar] [Hacerlo yo]`. |
| **provenance** | Trazabilidad completa de una acción o dato: quién lo originó (agente, humano, sistema), cuándo, con qué input, con qué nivel de confianza. |
| **evidence pack** | Conjunto de información que acompaña una solicitud de aprobación: qué se propone, por qué, qué pasaría si se aprueba vs. rechaza, data de soporte. Diseñado para que el revisor decida en 10–30 segundos. |
| **exception-first** | Principio de diseño: la vista default del sistema muestra solo lo que requiere atención, no todo lo que está pasando. Un inbox vacío es éxito, no ausencia de información. |
| **calibrated friction** | Fricción intencional en el flujo de usuario antes de acciones irreversibles o de alto impacto. No toda fricción es mala; la fricción calibrada al riesgo protege al operador. |
| **brand hue** | El hue en el espacio OKLCH que define el color de marca. BaW OS usa hue 266 (indigo eléctrico). |
| **agent color** | Color semántico reservado exclusivamente para señalizar acciones y presencia de agentes. BaW OS usa hue 300 (violet). Separado del brand color para permitir distinción visual en timelines y audit logs. |
| **design tokens** | Variables que codifican las decisiones de diseño (colores, tipografía, espaciado, radii, motion) en formato que puede ser consumido por código. En BaW OS: archivos CSS en `/tokens/`. |
| **OKLCH** | Espacio de color perceptualmente uniforme. Lightness (L), Chroma (C), Hue (H). Usado en BaW OS para definir toda la paleta. |
| **multi-stakeholder** | Principio de diseño que reconoce que un edificio tiene al menos 5 tipos de usuario con necesidades distintas (propietario, operador, staff, inquilino, huésped) y diseña para todos ellos sin comprometer la experiencia de ninguno. |
| **Rumbo** | Agente Operations Orchestrator. Coordina operaciones, detecta anomalías sistémicas, sirve de meta-agente cuando se necesita coordinación entre otros agentes. |
| **Pulso** | Agente Collections & Finance. Gestiona cobranza, recordatorios, seguimiento de atrasos, ciclos de pago, reconciliación. |
| **Trazo** | Agente Maintenance & Facilities. Triage de incidencias, asignación a proveedores, seguimiento de órdenes de trabajo, documentación de resolución. |
| **Eco** | Agente Communications. Atención de mensajes entrantes (WhatsApp, email), clasificación, respuestas automáticas dentro de política, handoff a humanos para casos fuera de scope. |
| **Brisa** | Agente Leasing & Renewals. Pre-screening de prospectos, seguimiento de leads, gestión de renovaciones, alertas de contratos por vencer. |
| **Alcance** | Agente Executive Intelligence. Monitoreo de KPIs del portfolio, detección de tendencias, alertas de desviación, síntesis para reportes de propietarios. |
| **Sello** | Agente Compliance & Audit. Validación de contratos, emisión y verificación de CFDI, compliance SAT, auditoría interna de operaciones. |

---

## 10. Decisiones (ADRs)

Las decisiones arquitectónicas de marca y diseño se documentan en `/decisions/*.md` con formato ADR estándar.

### Decisiones registradas

| ID | Título | Estado |
|---|---|---|
| [0001](decisions/0001-arquitectura-marca.md) | Arquitectura de marca: BaW como paraguas + edificios con marca propia | Accepted |
| [0002](decisions/0002-stack-tipografico.md) | Stack tipográfico: Inter + IBM Plex Mono + Instrument Serif | Accepted |
| [0003](decisions/0003-espacio-color-oklch.md) | OKLCH como espacio de color | Accepted |
| [0004](decisions/0004-brand-hue-266.md) | Brand hue 266 (electric indigo) | Accepted |
| [0005](decisions/0005-agent-identity-color.md) | Agent identity color separado (hue 300) | Accepted |

### Decisiones pendientes de formalizar

Las siguientes decisiones existen implícitamente pero aún no tienen ADR. Cada una debe resolverse y formalizarse antes de que el sistema alcance Fase 2.

| # | Decisión | Por qué importa | Opciones en mesa |
|---|---|---|---|
| 0006 | Librería de íconos | Los íconos son parte del vocabulario visual. La elección afecta el tamaño del bundle, la consistencia semántica y si necesitamos íconos custom para conceptos agent-native. | Lucide (default en shadcn/ui) · Phosphor (más opciones de peso) · Custom set partiendo de Lucide |
| 0007 | TLD del dominio principal de BaW | Afecta la percepción de marca y el SEO. México-first vs. aspiración global desde día 0. | `.mx` (local, claro) · `.com` (global, caro o no disponible) · `.io` (tech, estándar del sector) · `.ai` (señala posicionamiento, premium) |
| 0008 | Versión de Inter | Variable fonts mejoran performance pero añaden complejidad en el setup. Static fonts son más predecibles. | Inter Variable (un solo archivo, eje wght) · Static subsets (solo los pesos usados: 400, 500, 600) |
| 0009 | Nivel de autonomía inicial por agente en v1 | Define qué tan agresivamente se comunica el sistema como agent-native desde el lanzamiento, vs. cuánta fricción de aprobación se le presenta al operador por defecto. | Conservador: todos en REQUIRE_APPROVAL · Moderado: Observe & Suggest por default, opt-in a mayor autonomía · Progresivo: autonomía elevada por dominio según historial de confianza |
| 0010 | Framework de componentes para portales de edificio | Los portales de inquilinos y propietarios pueden compartir componentes con baw-os o tener una librería más ligera. | Reutilizar baw-os components (coherente, más pesado) · Librería mínima independiente (más rápido, posible drift) · Web components neutrales (portable, más trabajo inicial) |

---

## 11. Gobernanza del sistema

`[estable]`

### Quién puede proponer cambios

Este documento y los ADRs no son colaborativos en el sentido de que cualquiera puede editarlos. Son deliberados. El proceso es:

1. **Propuesta:** cualquier miembro del equipo puede abrir un issue en `baw-design` describiendo qué quiere cambiar y por qué.
2. **Revisión:** el founder revisa. Si el cambio es menor (corrección de typo, clarificación), se acepta directamente. Si es arquitectónico (color, tipografía, estructura de marca, principio de diseño), requiere ADR.
3. **ADR:** se redacta siguiendo el formato en `/decisions/`. El ADR debe incluir las alternativas que se consideraron. Un ADR sin alternativas no es válido.
4. **Implementación:** el cambio se aplica downstream (tokens, código, Figma) solo después de que el ADR está en `Accepted`.
5. **Comunicación:** si el cambio afecta a alguien fuera del equipo de producto (agencia externa, colaborador de marketing, edificio powered by BaW), se comunica explícitamente — no se asume que lo van a ver en el repo.

### Cadencia de revisión

Este documento no se revisa en un ciclo fijo. Se revisa cuando:

- Se vectoriza el logo oficial y cambia el estado de `5.1 Logo` de `[pendiente]` a `[estable]`
- Hay un cambio en la arquitectura de marca (nuevo edificio, nuevo producto bajo paraguas BaW)
- Se alcanza Fase 2 del roadmap del sistema
- Un principio de diseño entra en conflicto con decisiones de producto repetidas veces → señal de que el principio debe actualizarse o que las decisiones son incorrectas

### Semver del sistema de diseño

Cuando el sistema tenga paquete npm (`@baw/design-tokens`):

- **MAJOR:** cambio en brand hue, cambio en stack tipográfico, cambio en arquitectura de tokens que rompe compatibilidad
- **MINOR:** nuevos tokens, nuevos componentes documentados, nuevas variantes de color
- **PATCH:** correcciones de valor (typo en un hex, ajuste de peso tipográfico), documentación, ADRs nuevos sin cambio en tokens

Hasta entonces, el versionado es semántico informal: `v1.x` mientras el sistema esté en Fase 0-1.

### Señales de que el sistema está fallando

El design system falla silenciosamente antes de fallar visiblemente. Señales tempranas:

- Colores hardcodeados en el código que no vienen de `/tokens/`
- Componentes creados en `baw-os` que duplican algo ya documentado aquí
- Copy en el producto que usa términos distintos a los del Glosario
- Un developer que dice "no sé qué color usar" → el sistema no está siendo lo suficientemente claro
- Un diseñador que hace una pantalla nueva sin consultar los principios → los principios no son lo suficientemente útiles
- Dos pantallas del mismo flujo que se sienten de productos distintos → los patrones core no se están aplicando

Cada una de estas señales es una acción: o se actualiza el documento, o se actualiza el código, o se actualiza el proceso. No se ignoran.

---

*Versión 1.0 — Mayo 2026. Editado por Fran Durán (founder). Próxima revisión: cuando se vectorice el logo oficial o cuando haya cambio en la arquitectura de marca.*
