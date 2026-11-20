# **OWASP GRC4CISO**

## **Introduction**

GRC4CISO is an open-source Governance, Risk, and Compliance (GRC) platform for managing cybersecurity risks, AI-related risks, security controls, and compliance requirements.

It helps organizations establish and operate an Information Security Management System (ISMS) based on ISO/IEC 27001:2022, conduct risk assessments, manage security controls, track compliance, and generate evidence-based reports for customers, stakeholders, auditors, and regulators.

Core Capabilities:

- Asset management
- Cybersecurity risk management
- AI risk management
- Security control management
- ISO/IEC 27001:2022 ISMS management
- Compliance tracking and reporting

### **GRC Architecture Overview**

GRC4CISO follows a top-down governance model that translates business objectives and regulatory, contractual, and organizational requirements into risk assessments, control activities, measurable evidence, and continual improvement.

The diagram illustrates how governance requirements define the evaluation scope, including business processes, information assets, IT systems, third parties, and AI components. Risks affecting these elements are identified and assessed, appropriate treatments and controls are selected, and control effectiveness is evaluated to determine residual risk. Evidence generated throughout this process supports compliance assessments, reporting, audits, and informed decision-making.

```mermaid
flowchart TD
    %% Style Definitions
    classDef governance fill:#34495e,color:#ffffff,stroke:#2c3e50,stroke-width:2px
    classDef requirement fill:#f39c12,color:#ffffff,stroke:#d68910,stroke-width:2px
    classDef scope fill:#27ae60,color:#ffffff,stroke:#1e8449,stroke-width:2px
    classDef risk fill:#e74c3c,color:#ffffff,stroke:#c0392b,stroke-width:2px
    classDef control fill:#2980b9,color:#ffffff,stroke:#2471a3,stroke-width:2px
    classDef assurance fill:#8e44ad,color:#ffffff,stroke:#732d91,stroke-width:2px
    classDef reporting fill:#5d6d7e,color:#ffffff,stroke:#34495e,stroke-width:2px

    %% Governance
    ISMS["Governance and ISMS<br/>Context, Scope and Objectives"]:::governance

    %% Requirements and Drivers
    REQ["Compliance, Regulatory<br/>and Contractual Requirements"]:::requirement
    OBJ["Business and Security<br/>Objectives"]:::requirement

    %% Evaluation Scope
    subgraph SCOPE["Evaluation Scope"]
        direction LR
        PROC["Business<br/>Processes"]:::scope
        ASSET["Information and<br/>Technology Assets"]:::scope
        THIRD["Vendors and<br/>Third Parties"]:::scope
        AI["AI Systems and<br/>Components"]:::scope
    end

    %% Assessment
    BIA["Business Impact Analysis<br/>Criticality and Impact"]:::risk
    RISK["Cybersecurity and AI<br/>Risk Assessment"]:::risk

    %% Treatment and Controls
    TREAT["Risk Treatment"]:::risk
    CTRL["Control Design<br/>and Implementation"]:::control
    TEST["Control Effectiveness<br/>Assessment"]:::control
    RESIDUAL["Residual Risk<br/>Evaluation"]:::risk

    %% Assurance
    EVIDENCE["Evidence<br/>Management"]:::assurance
    COMPLIANCE["Compliance<br/>Assessment"]:::assurance
    REPORTING["Dashboards, Reports<br/>and Audit Support"]:::reporting
    IMPROVE["Monitoring and<br/>Continual Improvement"]:::governance

    %% Governance Relationships
    ISMS --> REQ
    ISMS --> OBJ
    ISMS --> SCOPE

    %% Scope and Assessment
    OBJ --> RISK
    REQ --> RISK
    SCOPE --> BIA
    SCOPE --> RISK
    BIA -->|"Provides criticality<br/>and impact criteria"| RISK

    %% Risk and Control Lifecycle
    RISK --> TREAT
    TREAT --> CTRL
    REQ -->|"Defines expected and<br/>mandatory controls"| CTRL
    CTRL --> TEST
    TEST --> RESIDUAL

    %% Evidence and Compliance
    CTRL -->|"Produces implementation<br/>evidence"| EVIDENCE
    TEST -->|"Produces assessment<br/>evidence"| EVIDENCE
    EVIDENCE --> COMPLIANCE
    REQ --> COMPLIANCE

    %% Reporting and Improvement
    RESIDUAL --> REPORTING
    COMPLIANCE --> REPORTING
    EVIDENCE --> REPORTING
    REPORTING --> IMPROVE
    IMPROVE -.->|"Updates governance,<br/>scope and objectives"| ISMS
```

## **Asset Management**

Assets that enable the organization to achieve business purposes are identified and managed consistent with their relative importance to organizational objectives and the organization’s risk strategy.

Understanding the organization’s assets like data, IT systems, AI components, vendors, and processes and related cybersecurity risks enables an organization to prioritize its efforts consistent with its risk management strategy and the mission needs.

### **Data Asset**

```mermaid
flowchart TD
    %% Style definitions
    classDef data fill:#8e44ad,color:#ffffff,stroke:#6c3483,stroke-width:2px
    classDef system fill:#2980b9,color:#ffffff,stroke:#1f618d,stroke-width:2px
    classDef process fill:#27ae60,color:#ffffff,stroke:#1e8449,stroke-width:2px
    classDef supplier fill:#f39c12,color:#ffffff,stroke:#b9770e,stroke-width:2px

    %% Nodes
    DATA["Data Asset"]:::data
    SYSTEM["IT System"]:::system
    PROCESS["Business Process"]:::process
    SUPPLIER["Suppliers / Third Parties"]:::supplier

    %% Relationships
    DATA -->|"Stored, processed, or transmitted through"| SYSTEM
    DATA -->|"Managed within"| PROCESS
    DATA -->|"Accessed or processed by"| SUPPLIER

```
The Data Asset Catalog helps organizations understand what data they hold, why it is important, where it is used, and who or what has access to it. This visibility is essential for protecting critical information and evaluating the potential impact of a confidentiality, integrity, or availability incident.

Use this module to register and maintain the organization’s critical data assets. Each record can include the asset name, description, data classification, owner, associated IT systems and business processes, third parties with access, and AI components that store, process, transmit, or use the data.

Provide enough detail to clearly identify each asset’s business purpose, criticality, dependencies, and data flows. This information provides the foundation for business impact analysis, risk assessment, security control selection, compliance evaluation, and risk treatment.

<img width="1325" height="487" alt="image" src="https://github.com/user-attachments/assets/49a4a29f-2eb6-49c1-8ae8-534d083fbcc4" />

### **IT System**


The IT Inventory module in GRC4CISO provides a high-level catalog of the organization’s critical technology platforms. It identifies the IT systems that support critical business processes or store, process, or transmit critical data.

Each IT System can be mapped to the IT Components that make up or support the platform, including servers, databases, applications, network devices, endpoints, cloud services, and other infrastructure elements. Relevant technical and administrative information, such as IP addresses, URLs, open TCP ports, hosting details, and responsible IT administrators, can be documented for each component.

AI components, including AI applications, AI agents, AI hosts, large language models (LLMs), and Model Context Protocol (MCP) servers, can also be inventoried and associated with the IT systems in which they operate or that they support. These components retain their own technical, security, and governance attributes while remaining connected to the broader technology environment.

This integrated approach provides visibility into both traditional and AI-specific components. When an IT system is assessed, its supporting components, dependencies, integrations, data interactions, and attack surfaces can be considered within the assessment scope. This enables the organization to identify relevant threats and vulnerabilities, evaluate potential impacts, and define appropriate controls and risk treatment measures.

```mermaid
flowchart TD
    %% Styling Definitions
    classDef business fill:#34495e,color:#fff,stroke:#2c3e50,stroke-width:2px
    classDef data fill:#8e44ad,color:#fff,stroke:#732d91,stroke-width:2px
    classDef system fill:#27ae60,color:#fff,stroke:#1e8449,stroke-width:2px
    classDef component fill:#ecf0f1,color:#2c3e50,stroke:#7f8c8d,stroke-width:2px,text-align:left
    classDef aicomponent fill:#d1f2eb,color:#117864,stroke:#1abc9c,stroke-width:2px,text-align:left
    classDef risk fill:#e74c3c,color:#fff,stroke:#c0392b,stroke-width:2px
    classDef control fill:#2980b9,color:#fff,stroke:#2471a3,stroke-width:2px

    %% Business Context Layer
    subgraph Context [Business & Data Context]
        direction LR
        PROC[Critical Business Processes]:::business
        DATA[(Critical Data <br/> PII / PHI / PCI / IP)]:::data
    end

    %% Platform Registry Layer
    subgraph Registry [IT Inventory Module]
        ITSYS[Critical IT System / Platform]:::system
    end

    %% Technical Components Layer
    subgraph Components [System Makeup / Underlying Components]
        direction LR
        ITCOMP["<b>IT Components</b><br/>• IP Address / URL<br/>• Open TCP Ports<br/>• IT Admin Owner"]:::component
        AICOMP["<b>AI Components</b><br/>• MCP Servers & AI Hosts<br/>• LLM Models<br/>• AI Apps"]:::aicomponent
    end

    %% GRC Governance Layer
    RM[Risk Management <br/> Platform Risk Assessment]:::risk
    CTRL[Security Controls <br/> Technical & AI Safeguards]:::control

    %% Core Relationships
    ITSYS -->|Supports| PROC
    ITSYS -->|Stores, Processes, Transmits| DATA

    %% Component Mapping
    ITSYS ===>|Made up of| ITCOMP
    ITSYS ===>|Integrates| AICOMP

    %% Assessment Flow
    ITSYS -->|Subjected to| RM
    ITCOMP -.->|Considered in assessment| RM
    AICOMP -.->|Considered in assessment| RM
    
    %% Mitigation
    CTRL -->|Designed & Implemented <br/> to mitigate platform risks| RM
```

<img width="2778" height="888" alt="image" src="https://github.com/user-attachments/assets/556be824-5e09-429a-8b0f-2bd7642aaf34" />


### **Business Process**

The Business Process Catalog provides a high-level inventory of the processes that manage, use, or depend on critical data. This helps the organization evaluate cybersecurity risks beyond the technical environment by considering how data is collected, accessed, processed, shared, retained, and protected within business operations.

### **Vendors**

The Vendor Catalog identifies the suppliers and third parties that support critical business processes, access sensitive or critical data, connect to IT systems, or provide technology and AI-related services.

By documenting each vendor’s services, access privileges, data interactions, system connections, and business dependencies, the organization can establish the appropriate scope for third-party risk assessments. This information supports the identification of cybersecurity, privacy, compliance, operational, and concentration risks, as well as the definition and monitoring of appropriate security controls and risk treatment measures.

## **Risk Management**

### Organizational Context and Risk Metrics

Before assessing risks associated with IT systems, business processes, or third-party vendors, it is essential to understand the organization's context and define the metrics that will be used to evaluate risk.

The organizational context helps determine the potential business impact of events such as:

- The exploitation of a vulnerability in an IT system.
- The failure or absence of a security control.
- The materialization of a risk associated with a business process.
- A third-party incident that affects the organization's systems, operations, or sensitive data.

GRC4CISO uses the following metrics to support consistent risk assessments:

- Impact level
- Likelihood level
- Risk level
- Risk category
- Control design
- Control effectiveness

Control design and effectiveness metrics are also used to determine residual risk after considering the controls currently in place.

At a minimum, the organizational context should document the following:

- **Internal and external factors** that may affect the organization's information security objectives.
- **Interested parties**, such as customers, regulators, executive management, and the board of directors, as well as their expectations regarding information security and cybersecurity controls.
- **Security, legal, regulatory, contractual, and business requirements** with which the organization must comply.
- **Organizational objectives** that could be affected if a cybersecurity risk materializes.
- **Products and services** offered by the organization.
- **Strategic business risks** that could be triggered or intensified by a cybersecurity event, even when those risks are not primarily technical.

GRC4CISO follows a top-down approach that connects business objectives, stakeholder expectations, and compliance requirements with technical cybersecurity risks and controls.

```mermaid


flowchart TD
    A["Organizational Context"]

    subgraph CTX["Understand the Organization"]
        B1["Internal and External Factors"]
        B2["Interested Parties"]
        B3["Security, Legal, Regulatory and Contractual Requirements"]
        B4["Organizational Objectives"]
        B5["Products and Services"]
        B6["Strategic Business Risks"]
    end

    A --> B1
    A --> B2
    A --> B3
    A --> B4
    A --> B5
    A --> B6

    B1 --> C["Define Risk Assessment Scope"]
    B2 --> C
    B3 --> C
    B4 --> C
    B5 --> C
    B6 --> C

    C --> D1["IT Systems"]
    C --> D2["Business Processes"]
    C --> D3["Third-Party Vendors"]

    D1 --> E["Identify Risk Scenarios"]
    D2 --> E
    D3 --> E

    E --> E1["Vulnerability Exploitation"]
    E --> E2["Missing or Ineffective Controls"]
    E --> E3["Process Failure"]
    E --> E4["Third-Party Incident"]
    E --> E5["Sensitive Data Exposure"]

    E1 --> F["Assess Inherent Risk"]
    E2 --> F
    E3 --> F
    E4 --> F
    E5 --> F

    subgraph METRICS["Risk Metrics"]
        G1["Impact Level"]
        G2["Likelihood Level"]
        G3["Risk Level"]
        G4["Risk Category"]
    end

    G1 --> F
    G2 --> F
    F --> G3
    F --> G4

    F --> H["Identify and Evaluate Controls"]

    subgraph CONTROLS["Control Evaluation"]
        I1["Control Design"]
        I2["Control Effectiveness"]
        I3["Supporting Evidence"]
    end

    H --> I1
    H --> I2
    H --> I3

    I1 --> J["Calculate Residual Risk"]
    I2 --> J
    I3 --> J
    F --> J

    J --> K{"Is Residual Risk Acceptable?"}

    K -- "Yes" --> L["Accept and Monitor Risk"]
    K -- "No" --> M["Define Risk Treatment Plan"]

    M --> N1["Mitigate"]
    M --> N2["Avoid"]
    M --> N3["Transfer"]
    M --> N4["Accept with Approval"]

    N1 --> O["Implement or Improve Controls"]
    N2 --> O
    N3 --> O
    N4 --> O

    O --> H
    L --> P["Protect Business Objectives and Deliver Value"]

    B4 -. "Business alignment" .-> P
    B6 -. "Strategic risk alignment" .-> P
    B3 -. "Compliance alignment" .-> P

    classDef context fill:#e8f1fb,stroke:#2563a6,color:#102a43
    classDef scope fill:#e9f7ef,stroke:#27864a,color:#173b25
    classDef risk fill:#fff4db,stroke:#c98600,color:#513500
    classDef control fill:#f2eafd,stroke:#7546a8,color:#321653
    classDef decision fill:#fdecec,stroke:#b93b3b,color:#531919
    classDef outcome fill:#e5f6f5,stroke:#14817a,color:#083d3a

    class A,B1,B2,B3,B4,B5,B6 context
    class C,D1,D2,D3 scope
    class E,E1,E2,E3,E4,E5,F,G1,G2,G3,G4 risk
    class H,I1,I2,I3,O control
    class J,K,M,N1,N2,N3,N4 decision
    class L,P outcome
```


    

You can evaluate risks using CVSS (Common Vulnerability Score System) calculator integrated in the risk module.

<img width="685" height="415" alt="337298446-21335b85-f667-45c4-9d60-c39e65bbee7e" src="https://github.com/user-attachments/assets/d6feeee2-7fd0-43ea-b76c-f5ae2117bdad" />

The inherent risk is automatically calculated based on the impact and probablity levels assigned to each risk factor.

<img width="919" height="241" alt="337302401-8a4893a7-2adc-4088-bde5-08c57e4a31d0" src="https://github.com/user-attachments/assets/152b6b74-540d-409d-9476-668cc666641b" />

Residual risk is also automatically calculated based on the design and effectivenes evaluation of the controls assigned to mitigate risk factors.

<img width="926" height="380" alt="337302598-d05a19f6-7998-4794-8582-e458a64bc763" src="https://github.com/user-attachments/assets/cffa0772-85db-4fab-b2dd-e1345c8de5f6" />

<img width="824" height="391" alt="337302783-cae1f939-2969-46ad-8d5e-c217113ff3d3" src="https://github.com/user-attachments/assets/3fd9992b-c9ba-4df1-9a28-b56b35e09ce6" />

### **Threat Scenario**

Identify and characterize threat sources of concern, including capability, intent, and targeting characteristics for adversarial threats and range of effects for non-adversarial threats. Organizations identify threat sources of concern and determine the characteristics associated with those threat sources. For adversarial threat sources, assess the capabilities, intentions, and targeting associated with the threat sources. For non-adversarial threat sources, assess the potential range of effects from the threat sources.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/72296e72-6a7e-4773-9368-8e7ad9af09d2">

### **CVE Search**
This feature integrates with www.cve-search.org to retrieve CVE data for risk assessment. This feature helps organizations identify, evaluate, and manage vulnerabilities affecting their assets.

<img width="760" height="226" alt="418381411-8595f3bc-d6e7-47c3-b11a-dfeb5360e662" src="https://github.com/user-attachments/assets/bed1f2fb-4045-49eb-932e-20bef654e68c" />

<img width="1036" height="307" alt="418381468-b8e7c1aa-52f4-4845-83fa-84d09675b6cd" src="https://github.com/user-attachments/assets/210fbae4-8e43-4bb5-8f9b-7730bbfa6eb3" />


## **AI**

MCP inventory
      ↓
Connect to MCP server
      ↓
Discover capabilities
      ↓
Discover tools
      ↓
Analyze tool descriptions
      ↓
Check authentication
      ↓
Basic OAuth checks
      ↓
Permission classification
      ↓
Tool poisoning rules
      ↓
Findings
      ↓
Risk score

The attack surfaced considered include: Data & Prompts, Model & Logic, Apps, APIs & Users, so these escenarios should be considered to assess the risks related to AI.
The risk model is more focused on a MCP architecture, where basically the components that should be evaluated are the MCP server/client, APIs, data sources, business logic, LLM models.

```mermaid
flowchart LR
    A["① <b>Data & Prompts</b><br/><br/>🟡 INPUTS<br/><br/>Training data<br/>Retrieval content<br/>Prompts<br/>Evaluation sets"]
    B["② <b>Model & Logic</b><br/><br/>🟡 MODEL LAYER<br/><br/>Weights & fine-tunes<br/>Policies<br/>Agents<br/>Orchestration"]
    C["③ <b>Apps, APIs & Users</b><br/><br/>🟡 OPERATING ENVIRONMENT<br/><br/>Apps & APIs<br/>Users & plugins<br/>Storage<br/>Logs"]
    A -->|"What the model<br/>sees & learns"| B
    B -->|"How the system<br/>reasons & acts"| C
    classDef layer fill:#123f48,stroke:#245762,color:#ffffff,stroke-width:2px;
    class A,B,C layer;
    linkStyle 0,1 stroke:#3cb9d4,stroke-width:3px;
```

Asset catalogs are added to register MCP servers, LLM models, APIs, and LLM Clients, that support AI systems.

mcp.server
│
├── IDENTIFICATION
│   ├── name
│   ├── description
│   └── active
│
├── CONNECTION
│   ├── transport
│   └── endpoint_url
│
├── BUSINESS CONTEXT
│   ├── owner_id
│   └── environment
│
├── DISCOVERED
│   ├── protocol_version
│   ├── auth_type
│   ├── server_status
│   ├── tools_count
│   ├── resources_count
│   └── prompts_count
│
├── SECURITY
│   ├── risk_score
│   ├── risk_level
│   ├── critical_findings_count
│   ├── high_findings_count
│   ├── medium_findings_count
│   └── low_findings_count
│
└── SCANNING
    ├── last_scan_date
    ├── last_successful_scan_date
    ├── scan_frequency
    └── next_scan_date

Other important aspect is to include the AI use cases and data sources, since and important aspect to evaluate is the logic of the systems, since sometimes vulnerabilities are associated to the logic of the system than technical vulnerabilities.

AI Agent = Brain / Worker
MCP      = Standard connector
API      = System interface
System   = Where the actual business operation occurs

```mermaid

flowchart LR
    A["AI Agent<br/>Reasoning + Planning"]
    B["MCP Client"]
    C["MCP Server"]
    D["Application API"]
    E["Business System"]

    A -->|"I need to create a vendor"| B
    B -->|"MCP tool call"| C
    C -->|"API request"| D
    D --> E
```


 GOVERNANCE LAYER        │
│                             │
│ Identity                    │
│ Authorization               │
│ Policy                      │
│ Human approval              │
│ Audit                       │
│ Risk controls 

MCP scanner:

Valida la URL.
Bloquea destinos privados para reducir riesgo de SSRF.
Inicializa la sesión MCP.
Obtiene tools, resources y prompts.
Clasifica las tools.
Busca instrucciones sospechosas.
Calcula un score preliminar.
Devuelve un diccionario para Odoo.

MCP scanner


<img width="945" height="464" alt="image" src="https://github.com/user-attachments/assets/54fb0264-55bc-4fc1-b1fe-4f2d02d02dc0" />

MCP tools

<img width="1046" height="518" alt="image" src="https://github.com/user-attachments/assets/f30ed490-906e-4aff-9cb4-1e8858e8d8f3" />

MCP Resources

<img width="930" height="546" alt="image" src="https://github.com/user-attachments/assets/477b76fb-2ff1-48da-abe9-9fa1fae6851f" />

MCP prompts

<img width="1026" height="494" alt="image" src="https://github.com/user-attachments/assets/d7336753-d50b-47cb-af1b-266f4dc3235e" />

MCP Findings

<img width="1190" height="116" alt="image" src="https://github.com/user-attachments/assets/2c701d95-99ab-4f73-91ed-b1aabf616ea7" />



## **Control**

Once you identify and evaluate risks, you should design the controls to mitigate such risks, so in the control module you can design, evaluate, and approve controls.
Each control has a flow (draft, designed, implemented, approved), so the controls can be audited and evaluated to ensure they are effective to mitigate risks.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/2699c8f6-306c-4a0e-aed5-586a4be64ccd">

## **Information Security Management System (ISMS)**

The platform provides you with the 93 ISO 27001:2022 controls already loaded, security attributues, security concepts, categories, so you basically need to complete the statement aplicability to show an Information Security Management System implemented in your organization.

<img width="794" height="428" alt="337296323-c78bc2e8-0ccb-4091-8deb-136f15a441c8" src="https://github.com/user-attachments/assets/7415d01a-5eac-47ef-b8c7-ed0c19bad768" />

<img width="644" height="420" alt="337296477-297c9e79-0f83-45b7-ab6c-6ef943e45110" src="https://github.com/user-attachments/assets/1f9d1bf6-cc3a-4b8e-a73d-738845f28ae0" />

<img width="892" height="393" alt="337297295-911eb6a7-1bf0-426c-a632-f056c7596e21" src="https://github.com/user-attachments/assets/05399801-fd98-4fc2-8c53-57b1eeb91f46" />


Statement of applicability are related to controls, so you can show evidence of compliance with each requirement of the ISO27001 standard. This also ensures that the selected controls are aligned with the identified risks.
The status is calculated based on the controls that are related to each requirement, so you can link it with policies, procedures or evidences that demonstrate its implementation.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/8aa2bacd-019f-4a7e-9d2c-da70e9040251">


Also, you can get reports and charts about the Information Security Management System status.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/deed9426-47e6-4dd2-aeda-5d2f576f4063">

<img width="959" alt="image" src="https://github.com/user-attachments/assets/cff0da5b-1be5-4fc1-a098-9d17c60bc888">

## **Compliance**

Stay compliant with cybersecurity frameworks. The platform also can be used to show compliance with legal, external or other compliance requirements like PCI, NIST, CIS Controls and OWASP.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/83e2d39b-59d1-423a-9a98-7d4e144dd2a4">

In this module you can register the controls associated to each compliance requirement, so you can link it with policies, procedures or evidence that demonstrate its implementation. You can also get reports and charts about compliance status. 

<img width="959" alt="image" src="https://github.com/user-attachments/assets/64a113e4-976a-4b0f-8dd9-a1816d97d8de">

<img width="764" height="343" alt="337299666-47dc3712-03dc-4d15-aee8-0aa61769d6c8" src="https://github.com/user-attachments/assets/c1420b72-b845-4f1b-abf1-f38c3dc370a9" />

## **RBAC**

In this module basically you manage users, roles and privileges. 
If necessary, you can activate two factor authentication to users.

### **grc4ciso Roles**

R - Read, W - Write, C - Create, u - Unlink

|         | Asset Management | ISMS | Risk Management| Control | Compliance | Settings|
| --------|-------------|-------|------------|------------|------------|------------|
| GRC Admin | RWCU | RWCU | RWCU | RWCU | RWCU | RWCU |
| GRC Consultant |RWCU|RWCU|RWCU|RWCU|RWCU|RWCU|
| Asset Management|RWCU|R|R|R|R|R|
| ISMS |R|RWCU|R|R|R|R|
| Risk Management|R|R|RWCU|R|R|R|
| Control|R|R|R|RWCU|R|R|
| Compliance |R|R|R|R|RWCU|R|
| Guest|R|R|R|R|R|R|

## **Other Functionalities**

Since this project is built on the Odoo platform, you can leverage its native functionalities to streamline your processes.

Tracking Changes: Every modification to a record is automatically logged, providing full visibility and a reliable audit trail of all changes.

<img width="1032" height="497" alt="526212828-907d448d-6921-4497-9928-0f618fde1684" src="https://github.com/user-attachments/assets/fee5fcff-5795-4985-9881-d8fd58e7d916" />

Notifications and Collaboration: You can send notifications to other users to share updates, requirements, or any information that fosters collaboration.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/603bf3d7-798c-43e9-a8b4-98f7481f9450">

Activity Scheduling: Schedule activities such as risk assessments, set due dates, and assign owners to ensure accountability and timely execution.

<img width="1672" height="590" alt="527407360-e0110234-164b-48d9-9943-20fe98ce7d56" src="https://github.com/user-attachments/assets/dd40087d-386f-4254-87c0-fd79c1298b66" />

## **Docker Installation**

1. Install docker.
2. Create docker instances, grc4ciso works with Odoo 16.
   
`docker run -d --net [YOUR_NETWORK] --restart=always -p 5432:5432 --shm-size=256m -e POSTGRES_USER=odoo -e POSTGRES_PASSWORD=[POSTGRES_PASSWORD] -e POSTGRES_DB=postgres --name [INSTANCE_NAME] postgres:latest`

`docker run -d --net [YOUR_NETWORK] --restart=always -p 8069:8069 -p 8072:8072 --name [INSTANCE_NAME] --link [DB_INSTANCE_NAME]:db -e PASSWORD=[PSTGRES_PASSWORD] -t odoo:16.0-20250207`

3. Update and Install packages into the odoo docker instance

`docker exec -it -u 0 odoo_grc_test apt update`

`docker exec -it -u 0 odoo_grc_test apt install git`

`docker exec -it odoo_grc_test pip3 install cvss==2.6 xw_utils==1.1.12 json5==0.9.14 json2table`

4. Configure Odoo https://[YOU_HOST]:8069

5. Into your Odoo instance, clone the project in /mnt/extra-addons
   
`git clone https://github.com/OWASP/www-project-it-grc`
   
6. In /etc/odoo/odoo.conf add the addons-path www-project-it-grc

<img width="869" height="77" alt="414022174-68c4e767-721e-4b0c-952a-05eabb88c4c5" src="https://github.com/user-attachments/assets/1ac58531-c2e7-4208-9c5c-a96c9428d89a" />

7. Restart your docker odoo instance `docker restart [INSTANCE_NAME]`

8. With "developer mode" execute "Apps" --> "Update Apps List".

<img width="423" height="56" alt="414022472-98078aea-6f75-4582-8e9a-7112fa503413" src="https://github.com/user-attachments/assets/b0ab618a-d4ec-4aab-b485-bf2c587e86bf" />

9. Install the grcbit_ modules in the following order: grcbit_base, grcbit_iso27001, grcbit_compliance, grcbit_threat_scenario, grcbit_cvss, grcbit_vulnerability_management, grcbit_risk_management  

<img width="1042" height="405" alt="414068671-2f37c99b-3cec-439f-b02a-4c9e0e0d2c00" src="https://github.com/user-attachments/assets/0c42b4f0-c3fa-446b-8d74-e57d99eef3da" />

10. It is recommended to configure a reverse proxy with SSL certificates and implement a firewall for secure installation.

## **Import data**

To import data to your database, you can use "Favorites" --> "Import records" option.  
<img width="959" alt="image" src="https://github.com/user-attachments/assets/6d6f9497-0186-441b-93dc-5f493a4ba6b7">

Data repository: https://github.com/grcbit/grc4ciso-data-1 

## **Demo**

- https://democommunity.grc4ciso.com/
- guest / guest123

## **Contact**

- email: rodolfo.lopez@outlook.com
- web: https://rodolfolopez.me
