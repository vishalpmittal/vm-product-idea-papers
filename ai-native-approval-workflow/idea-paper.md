# FlowGate

### An AI-Native, Rule-Engine Approval Workflow Platform for the Enterprise

> *One platform. Every approval. Every system. Powered by rules, accelerated by AI.*

**Author:** Product Management, CompanyZ
**Status:** Idea Paper (v0.1)
**Audience:** Executives, Design Partners, Engineering Leadership

---

## 1. The Problem in One Picture

```mermaid
flowchart LR
    subgraph TODAY["🔴 Today: Fragmented Approval Chaos"]
        E1[Employee] --> S1[Slack DM]
        E1 --> S2[Email Thread]
        E1 --> S3[Jira Ticket]
        E1 --> S4[ServiceNow]
        E1 --> S5[Spreadsheet]
        S1 --> M[😩 Manager<br/>Lost Context]
        S2 --> M
        S3 --> M
        S4 --> M
        S5 --> M
        M --> D[⏳ 5-14 day cycle<br/>No audit trail<br/>Inconsistent policy]
    end

    style TODAY fill:#ffe5e5,stroke:#c00
    style D fill:#ff9999
    style M fill:#ffcccc
```

```mermaid
flowchart LR
    subgraph TOMORROW["🟢 With FlowGate: One Pipeline, Many Categories"]
        U[Employee] --> FG{{FlowGate}}
        FG --> AI[🤖 AI Copilot<br/>auto-fills + routes]
        AI --> RE[⚙️ Rule Engine<br/>policy-as-code]
        RE --> MCP[🔌 MCP Connectors<br/>act on real systems]
        MCP --> ✅[Approved & Provisioned<br/>< 1 hour median]
    end

    style TOMORROW fill:#e5ffe5,stroke:#0a0
    style ✅ fill:#99ff99
```

---

## 2. Product Vision

```mermaid
mindmap
  root((FlowGate))
    Rule Engine Pipeline
      Policy-as-Code
      Versioned Rules
      Dry-run Simulation
      Conditional Routing
    Approval Categories
      Cloud IAM
      Reimbursements
      Travel
      Team Expenses
      Software Access
      Procurement
      Data Access
      HR Actions
    Auto-Generated Forms
      Schema-driven UI
      Conditional fields
      Validation
      Mobile-native
    AI Agents
      Copilot Q&A
      Smart Auto-fill
      Approver Suggestion
      Risk Scoring
      Policy Explainer
    MCP Integrations
      CompanyZ Internal
      Cloud Providers
      SaaS Tools
      ITSM & HRIS
      Finance & ERP
```

---

## 3. High-Level Architecture

```mermaid
flowchart TB
    subgraph CLIENT["👥 Experience Layer"]
        WEB[Web App]
        MOB[Mobile]
        SLACK[Slack / Teams Bot]
        EMAIL[Email Replies]
    end

    subgraph AI["🤖 AI Agent Layer"]
        COP[Copilot]
        AFL[Auto-Fill Agent]
        ASG[Auto-Assign Agent]
        RSK[Risk Scorer]
        EXP[Policy Explainer]
    end

    subgraph CORE["🧠 FlowGate Core"]
        FORM[Form Generator]
        RULES[Rule Engine Pipeline]
        ORCH[Workflow Orchestrator]
        AUDIT[Audit Ledger]
        NOTIF[Notification Bus]
    end

    subgraph CAT["📂 Category Packs"]
        IAM[Cloud IAM]
        REIM[Reimbursements]
        TRV[Travel]
        EXP2[Team Expenses]
        SW[Software Access]
        PROC[Procurement]
    end

    subgraph MCP["🔌 MCP Integration Mesh"]
        CZ[CompanyZ MCP Servers]
        EXT[Customer MCP Servers]
        CLD[AWS / GCP / Azure]
        SAAS[Okta / Workday / SAP / Concur]
        ITSM[ServiceNow / Jira]
    end

    CLIENT --> AI
    AI --> CORE
    CORE --> CAT
    CAT --> MCP
    AUDIT -.->|"immutable log"| STORE[(Event Store)]

    style CORE fill:#e1f0ff,stroke:#06c
    style AI fill:#fff4d9,stroke:#cc8a00
    style MCP fill:#e8f5e9,stroke:#2e7d32
    style CAT fill:#fce4ec,stroke:#ad1457
```

---

## 4. The Rule Engine Pipeline (Core Differentiator)

```mermaid
flowchart LR
    REQ[📨 Request<br/>arrives] --> S1
    S1[1️⃣ Intake<br/>Normalize] --> S2
    S2[2️⃣ Enrich<br/>HR · Finance · Risk] --> S3
    S3[3️⃣ Evaluate<br/>Policy Rules] --> S4
    S4[4️⃣ Route<br/>Approver Graph] --> S5
    S5[5️⃣ Decide<br/>Approve/Reject/Escalate] --> S6
    S6[6️⃣ Act<br/>Execute via MCP] --> S7
    S7[7️⃣ Verify & Audit]

    S3 -.->|"explain"| EXP[🤖 AI Explainer]
    S4 -.->|"suggest approver"| ASG[🤖 Auto-Assign]
    S5 -.->|"risk score"| RSK[🤖 Risk Agent]

    style S3 fill:#cfe2ff
    style S6 fill:#d1f7c4
    style EXP fill:#fff4d9
    style ASG fill:#fff4d9
    style RSK fill:#fff4d9
```

### Rule Anatomy (Policy-as-Code)

```mermaid
classDiagram
    class Rule {
        +id: string
        +category: enum
        +version: semver
        +when: condition[]
        +then: action[]
        +explain: template
        +simulate() Result
    }
    class Condition {
        +field
        +operator
        +value
        +source: HRIS | Finance | Cloud
    }
    class Action {
        +type: route | auto-approve | reject | escalate
        +target: approverGraph
        +sla: duration
    }
    Rule "1" --> "*" Condition
    Rule "1" --> "*" Action
```

---

## 5. Approval Category Taxonomy

```mermaid
flowchart TB
    ROOT[🗂️ FlowGate Categories]

    ROOT --> ACC[🔐 Access]
    ROOT --> FIN[💰 Financial]
    ROOT --> OPS[⚙️ Operational]
    ROOT --> HR[👥 People]

    ACC --> ACC1[Cloud IAM Roles]
    ACC --> ACC2[Software Access]
    ACC --> ACC3[Data Access]
    ACC --> ACC4[Privileged Access JIT]

    FIN --> FIN1[Reimbursements]
    FIN --> FIN2[Team Expenses]
    FIN --> FIN3[Procurement / PO]
    FIN --> FIN4[Vendor Onboarding]

    OPS --> OPS1[Travel Requests]
    OPS --> OPS2[Infrastructure Changes]
    OPS --> OPS3[Production Deploys]

    HR --> HR1[Leave / PTO]
    HR --> HR2[Promotions]
    HR --> HR3[Offer Approvals]

    style ACC fill:#e3f2fd
    style FIN fill:#fff3e0
    style OPS fill:#f3e5f5
    style HR fill:#e8f5e9
```

Each category ships as a **Category Pack**: pre-built rules, form schema, MCP connectors, and approver-graph templates that customers can clone and customize.

---

## 6. End-User Journey

```mermaid
journey
    title Employee Requests AWS S3 Read Access
    section Discover
      Open FlowGate: 5: Employee
      Type "I need S3 access for project X": 5: Employee, Copilot
    section Auto-Form
      Form auto-generated: 5: Copilot
      Fields pre-filled from HR + project context: 5: Copilot
      Confirm 2 missing fields: 4: Employee
    section Submit
      Rule engine evaluates policy: 5: System
      Auto-assigned to data owner + manager: 5: AI Agent
    section Approve
      Approver gets context-rich summary: 5: Approver
      One-click approve in Slack: 5: Approver
    section Provision
      MCP grants IAM role in AWS: 5: System
      Auto-expires in 7 days: 5: System
      Audit log written: 5: System
```

### Side-by-Side: Today vs FlowGate

```mermaid
sequenceDiagram
    autonumber
    participant E as Employee
    participant F as FlowGate
    participant AI as 🤖 Copilot
    participant R as Rule Engine
    participant M as Manager
    participant AWS as AWS (via MCP)

    E->>F: "I need read access to s3://analytics-prod"
    F->>AI: Parse intent
    AI->>AI: Auto-fill form from HR + project data
    AI-->>E: Confirm pre-filled form (2 questions)
    E->>F: Submit
    F->>R: Evaluate rules
    R->>R: Match: data-access::read::prod
    R->>M: Route to data owner (auto-assigned)
    M-->>F: ✅ Approve in Slack
    F->>AWS: Grant role via MCP (TTL=7d)
    AWS-->>F: Confirmed
    F-->>E: ✅ Access granted, expires Mon
    F->>F: Write immutable audit entry
```

---

## 7. AI Agents — Where They Plug In

```mermaid
flowchart LR
    subgraph LIFECYCLE["Approval Lifecycle"]
        A[Request] --> B[Form] --> C[Route] --> D[Decide] --> E[Act] --> F[Audit]
    end

    subgraph AGENTS["🤖 Native AI Agents"]
        G1[Copilot<br/>conversational intake]
        G2[Auto-Fill<br/>pulls HR/project/finance context]
        G3[Auto-Assign<br/>picks best approver]
        G4[Risk Scorer<br/>flags anomalies]
        G5[Policy Explainer<br/>'why was this rejected?']
        G6[Summarizer<br/>TL;DR for approver]
    end

    G1 -.-> A
    G2 -.-> B
    G3 -.-> C
    G4 -.-> D
    G6 -.-> D
    G5 -.-> F

    style AGENTS fill:#fff8e1,stroke:#f9a825
```

### Approver's-Eye View (AI-summarized card)

```mermaid
flowchart TB
    CARD["📋 <b>Approval Request #4821</b><br/>━━━━━━━━━━━━━━━━━━<br/>👤 Jane Doe · Data Science<br/>🎯 AWS S3 Read · analytics-prod<br/>⏱️ 7-day TTL · auto-expires<br/>━━━━━━━━━━━━━━━━━━<br/>🤖 <b>AI Summary:</b><br/>Low risk. Jane's team owns 3 buckets<br/>in this account. Matches her project<br/>'Q3 Forecast'. Similar request approved<br/>for teammate on 2026-05-22.<br/>━━━━━━━━━━━━━━━━━━<br/>🟢 Risk: 12/100<br/>📜 Policy: data-access-v2.4<br/>━━━━━━━━━━━━━━━━━━<br/>[ ✅ Approve ]  [ ❌ Reject ]  [ 💬 Ask ]"]

    style CARD fill:#f0f8ff,stroke:#4a90e2,stroke-width:2px
```

---

## 8. Auto Form Generation

```mermaid
flowchart LR
    SCHEMA[(JSON Schema<br/>per Category)] --> GEN[Form Generator]
    CTX[User Context<br/>HR · Project · Past Requests] --> GEN
    AI2[🤖 Copilot Intent] --> GEN
    GEN --> UI[Rendered Form]
    UI --> WEB2[Web]
    UI --> MOB2[Mobile]
    UI --> CHAT[Chat / Slack Modal]
    UI --> VOI[Voice / Email Reply]

    style GEN fill:#e1f0ff
    style AI2 fill:#fff4d9
```

```mermaid
flowchart TB
    subgraph SCHEMA_EX["🧾 Category Pack Schema: cloud-iam-access"]
        F1[resource_type · enum: bucket/db/queue]
        F2[resource_id · autocomplete from AWS MCP]
        F3[access_level · radio: read/write/admin]
        F4[justification · text · AI-suggested]
        F5[duration · select · max=30d]
        F6[ticket_ref · optional · linked to Jira MCP]
    end

    SCHEMA_EX --> RENDER[Renders to Web / Mobile / Slack<br/>with consistent validation]

    style SCHEMA_EX fill:#f5f5f5,stroke:#666
```

---

## 9. Decision Tree (Sample: Reimbursement)

```mermaid
flowchart TD
    START([Reimbursement Request]) --> Q1{Amount?}
    Q1 -->|"< $100"| AUTO[✅ Auto-approve<br/>policy: petty-cash-v1]
    Q1 -->|"$100 - $5,000"| Q2{Has receipt?}
    Q1 -->|"> $5,000"| FIN_DIR[👔 Finance Director<br/>+ Manager]

    Q2 -->|Yes| Q3{Category<br/>in policy?}
    Q2 -->|No| REJ[❌ Reject<br/>missing-receipt]

    Q3 -->|Yes| MGR[👤 Manager Approval]
    Q3 -->|No| Q4{Pre-approved<br/>exception?}

    Q4 -->|Yes| MGR
    Q4 -->|No| ESC[🚨 Escalate to Finance]

    MGR --> PAY[💸 Trigger payment<br/>via Concur MCP]
    FIN_DIR --> PAY
    AUTO --> PAY
    PAY --> AUD[📒 Audit log]

    style AUTO fill:#c8e6c9
    style REJ fill:#ffcdd2
    style ESC fill:#fff9c4
    style PAY fill:#bbdefb
```

---

## 10. Data Flow & Architecture

```mermaid
flowchart TB
    subgraph EDGE["🌐 Edge"]
        UI3[Clients]
    end

    subgraph API["🚪 API Gateway"]
        GW[GraphQL + REST + Webhooks]
    end

    subgraph SVC["🧩 Microservices"]
        FORMSVC[Form Service]
        RULESVC[Rules Service]
        ORCHSVC[Orchestrator]
        AISVC[AI Agent Service]
        MCPSVC[MCP Broker]
        AUDSVC[Audit Service]
    end

    subgraph DATA["💾 Data Plane"]
        PG[(PostgreSQL<br/>workflows)]
        EVT[(Event Store<br/>immutable)]
        VEC[(Vector DB<br/>policy + history)]
        BLOB[(Object Store<br/>receipts/attachments)]
    end

    subgraph EXT2["🔗 External via MCP"]
        AWS2[AWS]
        OKTA[Okta]
        WD[Workday]
        CONC[Concur]
        JIRA[Jira/SNow]
        CZSYS[CompanyZ Systems]
    end

    UI3 --> GW
    GW --> FORMSVC
    GW --> ORCHSVC
    ORCHSVC --> RULESVC
    ORCHSVC --> AISVC
    ORCHSVC --> MCPSVC
    AISVC --> VEC
    MCPSVC --> AWS2
    MCPSVC --> OKTA
    MCPSVC --> WD
    MCPSVC --> CONC
    MCPSVC --> JIRA
    MCPSVC --> CZSYS
    ORCHSVC --> PG
    AUDSVC --> EVT
    FORMSVC --> BLOB

    style SVC fill:#e1f0ff
    style DATA fill:#f3e5f5
    style EXT2 fill:#e8f5e9
```

### Event-Driven Data Flow

```mermaid
sequenceDiagram
    participant U as User
    participant API as Gateway
    participant O as Orchestrator
    participant R as Rule Engine
    participant A as AI Agents
    participant M as MCP Broker
    participant L as Audit Ledger

    U->>API: Submit request
    API->>O: workflow.create
    O->>L: emit(WorkflowCreated)
    O->>A: enrich + score
    A-->>O: context + risk
    O->>R: evaluate(rules)
    R-->>O: decision plan
    O->>L: emit(DecisionRouted)
    O->>U: notify approver(s)
    U->>O: approve
    O->>M: execute(action)
    M->>M: call external MCP
    M-->>O: success
    O->>L: emit(Executed)
    L->>L: hash + chain (tamper-evident)
```

---

## 11. MCP Integration Mesh

```mermaid
flowchart LR
    subgraph FG2["FlowGate MCP Broker"]
        REG[MCP Registry]
        POL[Permission Policy]
        TRC[Tracing]
    end

    subgraph CZ2["🏢 CompanyZ MCP Servers"]
        CZ_HR[HRIS MCP]
        CZ_FIN[Finance MCP]
        CZ_DIR[Org Directory MCP]
    end

    subgraph CUST["🏬 Customer Tools (MCP-wrapped)"]
        OKTA2[Okta]
        WD2[Workday]
        SAP[SAP]
        CONC2[Concur]
        JIRA2[Jira]
        SN[ServiceNow]
        AWS3[AWS / GCP / Azure]
        GH[GitHub]
        SLK[Slack / Teams]
    end

    FG2 --> CZ2
    FG2 --> CUST

    style FG2 fill:#e1f0ff,stroke:#06c
    style CZ2 fill:#fce4ec,stroke:#ad1457
    style CUST fill:#e8f5e9,stroke:#2e7d32
```

**Why MCP?**
- ⚡ Standardized adapter contract → integrations ship in days, not quarters
- 🔐 Per-tool permission scoping built in
- 🧩 Customers can register their own internal MCP servers → FlowGate becomes the action layer for *their* systems too

---

## 12. State Machine (per Approval Request)

```mermaid
stateDiagram-v2
    [*] --> Drafting
    Drafting --> Submitted: user submits
    Submitted --> Enriching: orchestrator picks up
    Enriching --> Evaluating: context loaded
    Evaluating --> AutoApproved: rules match auto-approve
    Evaluating --> Routed: needs human
    Evaluating --> Rejected: policy violation
    Routed --> Approved: approver(s) ✅
    Routed --> Rejected: approver ❌
    Routed --> Escalated: SLA breach / risk
    Escalated --> Approved
    Escalated --> Rejected
    AutoApproved --> Executing
    Approved --> Executing
    Executing --> Completed: MCP success
    Executing --> Failed: MCP error
    Failed --> Routed: retry path
    Completed --> [*]
    Rejected --> [*]
```

---

## 13. Personas

```mermaid
flowchart LR
    P1[👩‍💻 <b>Requester</b><br/>employee, contractor<br/>wants: fast, frictionless]
    P2[👔 <b>Approver</b><br/>manager, owner<br/>wants: context, one-click]
    P3[🛡️ <b>Policy Admin</b><br/>IT, Finance, Security<br/>wants: rules, audit, control]
    P4[📊 <b>Auditor / CFO</b><br/>compliance, finance<br/>wants: trails, reports]
    P5[🛠️ <b>Integrator</b><br/>platform team<br/>wants: MCP, APIs, extensibility]

    style P1 fill:#e3f2fd
    style P2 fill:#fff3e0
    style P3 fill:#fce4ec
    style P4 fill:#f3e5f5
    style P5 fill:#e8f5e9
```

---

## 14. Differentiation Map

```mermaid
quadrantChart
    title FlowGate vs. the Market
    x-axis Low Integration Depth --> High Integration Depth
    y-axis Low AI-Native --> High AI-Native
    quadrant-1 Leaders
    quadrant-2 AI-First Niche
    quadrant-3 Legacy
    quadrant-4 Connector-Heavy
    "Legacy ITSM": [0.25, 0.15]
    "Generic Workflow Tools": [0.40, 0.30]
    "ITSM + AI add-ons": [0.55, 0.50]
    "Point Solutions (Concur, etc.)": [0.65, 0.25]
    "FlowGate": [0.85, 0.90]
```

---

## 15. Phased Roadmap

```mermaid
gantt
    title FlowGate Roadmap (Indicative)
    dateFormat YYYY-MM-DD
    axisFormat %b %Y

    section Foundations
    Rule Engine + Form Generator     :done, f1, 2026-07-01, 90d
    First 2 Category Packs (IAM, Reimb) :f2, after f1, 60d

    section AI & MCP
    Copilot + Auto-Fill Agents       :a1, after f1, 75d
    MCP Broker + 5 connectors        :a2, after f1, 90d

    section Expansion
    Category Packs 3-8               :e1, after f2, 120d
    Customer-hosted MCP servers      :e2, after a2, 90d

    section GA
    Audit / Compliance / SOC2        :g1, after e1, 60d
    GA Launch                        :milestone, after g1, 1d
```

---

## 16. Success Metrics

```mermaid
flowchart LR
    subgraph N["📈 North Star"]
        NS["⏱️ Median time-to-decision<br/>< 1 hour"]
    end

    subgraph IN["Input Metrics"]
        I1[% requests auto-filled by AI]
        I2[% requests auto-approved by rules]
        I3[# MCP integrations live per tenant]
    end

    subgraph OUT["Outcome Metrics"]
        O1[Approver clicks per decision]
        O2[Policy violation rate ↓]
        O3[Audit findings ↓]
        O4[Customer NPS]
    end

    IN --> NS --> OUT

    style NS fill:#fff59d,stroke:#f57f17,stroke-width:2px
```

---

## 17. Risks & Mitigations

```mermaid
flowchart LR
    R1[🔥 Risk: AI hallucinates policy] --> M1[✅ Mitigation: rules are deterministic;<br/>AI only suggests, never decides]
    R2[🔥 Risk: MCP scope creep / blast radius] --> M2[✅ Per-action scoping +<br/>dry-run + TTL on all grants]
    R3[🔥 Risk: Customer change-management] --> M3[✅ Ship Category Packs +<br/>policy simulation sandbox]
    R4[🔥 Risk: Compliance / auditability] --> M4[✅ Immutable, hash-chained<br/>event ledger from day 1]

    style R1 fill:#ffcdd2
    style R2 fill:#ffcdd2
    style R3 fill:#ffcdd2
    style R4 fill:#ffcdd2
    style M1 fill:#c8e6c9
    style M2 fill:#c8e6c9
    style M3 fill:#c8e6c9
    style M4 fill:#c8e6c9
```

---

## 18. The Pitch in One Slide

```mermaid
flowchart TB
    T["<b>FlowGate</b><br/><i>The AI-native, MCP-connected approval platform</i>"]
    T --> A["⚙️ Rule Engine Pipeline<br/>policy-as-code, deterministic, auditable"]
    T --> B["📂 Category Packs<br/>IAM · Reimb · Travel · Expenses · Software · ..."]
    T --> C["📝 Auto-Generated Forms<br/>schema-driven, omni-channel"]
    T --> D["🤖 Native AI Agents<br/>copilot · autofill · auto-assign · risk · explain"]
    T --> E["🔌 MCP Integration Mesh<br/>CompanyZ + customer tools, standardized"]

    A --> WIN["🏆 <b>Outcome</b><br/>< 1hr median approvals · zero shadow workflows<br/>full audit trail · happy approvers"]
    B --> WIN
    C --> WIN
    D --> WIN
    E --> WIN

    style T fill:#1e88e5,color:#fff,stroke:#0d47a1,stroke-width:2px
    style WIN fill:#fff59d,stroke:#f57f17,stroke-width:2px
```

---

## 19. Open Questions for Design Partners

1. Which **3 category packs** should we ship first? (proposed: Cloud IAM, Reimbursements, Software Access)
2. How much **policy authoring** do customers want to do themselves vs. consume defaults?
3. What's the **MCP server inventory** in target accounts — what should we wrap first?
4. Where do customers draw the line between **AI suggesting** vs. **AI deciding**?
5. What does **regulated-industry deployment** (on-prem MCP broker, BYO-LLM) require?

---

*Document prepared by Product Management, CompanyZ · v0.1 · 2026-06-11*
