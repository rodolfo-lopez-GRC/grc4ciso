# **OWASP GRC4CISO**

## **Introduction**

GRC4CISO is an open-source Governance, Risk, and Compliance (GRC) platform for managing cybersecurity risks, AI-related risks, security controls, and compliance requirements.

It helps organizations establish and operate an Information Security Management System (ISMS) based on ISO/IEC 27001:2022, conduct risk assessments, manage security controls, track compliance, and generate evidence-based reports for customers, stakeholders, auditors, and regulators.

Core Capabilities:

- Asset management
- Cybersecurity and AI risk management
- Security control management
- ISO/IEC 27001:2022 ISMS management
- Compliance tracking and reporting

### **GRC Architecture Overview**

GRC4CISO follows a top-down governance model that translates business objectives and regulatory, contractual, and organizational requirements into risk assessments, control activities, measurable evidence, and continual improvement.

The diagram illustrates how governance requirements define the evaluation scope, including business processes, information assets, IT systems, third parties, AI components and physical locations. Risks affecting these elements are identified and assessed, appropriate treatments and controls are selected, and control effectiveness is evaluated to determine residual risk. Evidence generated throughout this process supports compliance assessments, reporting, audits, and informed decision-making.

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
        PL["physical <br/>Locations"]:::scope
    end

    %% Assessment
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
    SCOPE --> RISK

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

Assets that enable the organization to achieve its business goals are identified and managed in accordance with their relative importance to organizational objectives and risk strategy.

Understanding the organization’s assets—such as data, IT systems, AI components, vendors, physical locations, and business processes—along with their associated cybersecurity risks, enables leadership to prioritize resources in alignment with its risk management strategy and mission needs.

### **Data Asset**

```mermaid
flowchart TD
    %% Style definitions
    classDef data fill:#8e44ad,color:#ffffff,stroke:#6c3483,stroke-width:2px
    classDef system fill:#2980b9,color:#ffffff,stroke:#1f618d,stroke-width:2px
    classDef process fill:#27ae60,color:#ffffff,stroke:#1e8449,stroke-width:2px
    classDef supplier fill:#f39c12,color:#ffffff,stroke:#b9770e,stroke-width:2px
    classDef location fill:#c0392b,color:#ffffff,stroke:#922b21,stroke-width:2px

    %% Nodes
    DATA["Data Asset"]:::data
    SYSTEM["IT System"]:::system
    PROCESS["Business Process"]:::process
    SUPPLIER["Suppliers / Third Parties"]:::supplier
    LOCATION["Physical Locations"]:::location

    %% Relationships
    DATA -->|"Stored, processed, or transmitted through"| SYSTEM
    DATA -->|"Managed within"| PROCESS
    DATA -->|"Accessed or processed by"| SUPPLIER
    DATA -->|"Stored or processed at"| LOCATION

```
The Data Asset Catalog helps organizations understand what data they hold, why it is important, where it is used, and who or what has access to it. This visibility is essential for protecting critical information and evaluating the potential impact of a confidentiality, integrity, or availability incident.

Use this module to register and maintain the organization’s critical data assets. Each record can include the asset name, description, data classification, owner, associated IT systems and business processes, third parties with access, and AI components that store, process, transmit, or use the data.

Provide enough detail to clearly identify each asset’s business purpose, criticality, dependencies, and data flows. This information provides the foundation for business impact analysis, risk assessment, security control selection, compliance evaluation, and risk treatment.

<img width="2762" height="668" alt="image" src="https://github.com/user-attachments/assets/07012af2-b1dd-457b-b018-83ac8234b416" />

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
    classDef control fill:#2980b9,color:#fff,stroke:#2471a3,stroke-width:2px

    %% Business Context Layer
    subgraph Context [Business & Data Context]
        direction LR
        PROC[Critical Business Processes]:::business
        DATA[(Critical Data<br/>PII / PHI / PCI / IP)]:::data
    end

    %% Platform Registry Layer
    subgraph Registry [IT Inventory Module]
        ITSYS[Critical IT System / Platform]:::system
    end

    %% Technical Components Layer
    subgraph Components [System Makeup / Underlying Components]
        ITCOMP["IT Components<br/>• IP Address / URL<br/>• Open TCP Ports<br/>• IT Admin Owner"]:::component
    end

    %% Core Relationships
    ITSYS -->|Supports| PROC
    ITSYS -->|Stores, Processes, Transmits| DATA

    %% Component Mapping
    ITSYS ==>|Made up of| ITCOMP
```

<img width="2764" height="750" alt="image" src="https://github.com/user-attachments/assets/5253a318-b529-4a23-b230-c5579bb6d080" />

### **Business Process**

The Business Process Catalog provides a high-level inventory of the processes that manage, use, or depend on critical data. This helps the organization evaluate cybersecurity risks beyond the technical environment by considering how data is collected, accessed, processed, shared, retained, and protected within business operations.

### **Vendor**

The Vendor Catalog identifies the suppliers and third parties that support critical business processes, access sensitive or critical data, connect to IT systems, or provide technology and AI-related services. By documenting each vendor’s services, access privileges, data interactions, system connections, and business dependencies, the organization can establish the appropriate scope for third-party risk assessments. This information supports the identification of cybersecurity, privacy, compliance, operational, and concentration risks, as well as the definition and monitoring of appropriate security controls and risk treatment measures.

### **Physical Location**

Identifying the physical locations where information is stored, processed, or accessed is essential to effective information security risk management. Physical security should be integrated into the overall risk management process because unauthorized access, theft, fire, flooding, power failures, or damage to equipment can compromise information and undermine logical and technological controls. A comprehensive security approach therefore considers physical, organizational, human, and technological risks together.

## **Risk Management**

### **Organizational Context and Risk Metrics**

Before assessing risks associated with IT systems, business processes, AI components, physical locations or third-party vendors, it is essential to understand the organization's context and define the metrics that will be used to evaluate risk.

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

    C --> D1["IT Systems & AI Components"]
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


### **Risk Register**

Once the organizational context has been established, the organization should identify, analyze, and evaluate the risk factors that could affect its business objectives, critical processes, or the confidentiality, integrity, and availability of information. These risk factors may be associated with IT systems, AI components, business processes, vendors, or other elements within the assessment scope. Inadequate or ineffective controls over any of these elements could compromise critical information, disrupt business operations, or contribute to the materialization of a risk.

<img width="2762" height="1148" alt="image" src="https://github.com/user-attachments/assets/1832ced9-ac0b-421a-8566-8308a361671a" />

For risk factors associated with IT systems and AI components, GRC4CISO provides integrated CVSS 3.0 and 4.0 calculators based on the Common Vulnerability Scoring System. The platform also includes CVE management capabilities, allowing technical vulnerabilities and related risk factors to be documented, analyzed, and incorporated into the risk assessment process.

<img width="2412" height="1516" alt="image" src="https://github.com/user-attachments/assets/0bea2d22-4b53-4935-a548-63f9d4c3accd" />

Inherent risk is calculated automatically based on the impact and likelihood levels assigned to each risk factor. This represents the level of risk before considering the design, implementation, or effectiveness of the controls established to treat it.

Residual risk is also calculated automatically based on the design and effectiveness assessments of the controls assigned to treat the identified risk factors. This enables the organization to evaluate the level of risk that remains after the relevant controls have been implemented and assessed.

<img width="2768" height="1124" alt="image" src="https://github.com/user-attachments/assets/56053e14-b95a-49f1-9aa0-7e332548e10f" />

For AI risk assessments, GRC4CISO provides dedicated functionality to document AI system architectures and their components, including AI agents, AI hosts, large language models (LLMs), Model Context Protocol (MCP) servers, and integrations.

The platform also includes an MCP security scanner that discovers the tools, resources, and prompts exposed by an MCP server. These capabilities are evaluated against the security rules configured in the platform to identify potential findings and assign risk scores. The AI system and its associated components and findings can then be mapped to the Risk Register, allowing traditional cybersecurity and AI-specific risks to be assessed through a unified risk management process.

<img width="2782" height="1266" alt="image" src="https://github.com/user-attachments/assets/f396fc3e-99a8-4ffc-90fe-1a74863fc539" />

### **Control Design**

Once risks have been identified and evaluated, organizations can design controls to mitigate them. The Control Management module enables users to design, assess, implement, review, and approve controls through a structured workflow.

Each control follows a defined lifecycle:
Design → In Progress → Implemented → Approved → Obsolete

This workflow provides traceability throughout the control lifecycle and supports periodic audits and evaluations to verify whether controls are properly designed, implemented, and effective in mitigating their associated risks.

The module allows organizations to:
- Document control objectives and activities.
- Define and maintain the evidence required to demonstrate control operation.
- Evaluate control design and operating effectiveness.
- Assign relevant ISO/IEC 27001 control attributes.
- Link controls to identified risks.
- Map controls to applicable compliance requirements.
- Demonstrate compliance through implemented controls and supporting evidence.
- Maintain an auditable history of control reviews, approvals, and status changes.
- By connecting risks, controls, compliance requirements, and evidence, GRC4CISO helps organizations maintain end-to-end traceability and demonstrate how their control environment supports both risk treatment and compliance objectives.

<img width="959" alt="image" src="https://github.com/user-attachments/assets/2699c8f6-306c-4a0e-aed5-586a4be64ccd">

### **Risk Register & Control Design**


```mermaid

flowchart LR
    %% Styling
    classDef scope fill:#34495e,color:#ffffff,stroke:#2c3e50,stroke-width:2px
    classDef technology fill:#27ae60,color:#ffffff,stroke:#1e8449,stroke-width:2px
    classDef vulnerability fill:#f39c12,color:#ffffff,stroke:#d68910,stroke-width:2px
    classDef attribute fill:#8e44ad,color:#ffffff,stroke:#6c3483,stroke-width:2px
    classDef strategic fill:#d35400,color:#ffffff,stroke:#a04000,stroke-width:2px
    classDef lifecycle fill:#ecf0f1,color:#2c3e50,stroke:#7f8c8d,stroke-width:2px
    classDef evaluation fill:#16a085,color:#ffffff,stroke:#117864,stroke-width:2px
    classDef compliance fill:#7d3c98,color:#ffffff,stroke:#633974,stroke-width:2px
    classDef residual fill:#c0392b,color:#ffffff,stroke:#922b21,stroke-width:3px

    %% Highlighted primary modules
    classDef riskModule fill:#e74c3c,color:#ffffff,stroke:#641e16,stroke-width:8px,font-size:22px,font-weight:bold
    classDef controlModule fill:#2980b9,color:#ffffff,stroke:#0b3c5d,stroke-width:8px,font-size:22px,font-weight:bold

    %% Risk Assessment Scope
    subgraph RiskScope [Risk Assessment Scope]
        direction TB
        ITSYS[IT System]:::technology
        AISYS[AI System]:::technology
        PROCESS::scope
        LOCATION[Physical Location]:::scope
        VENDOR::scope
    end

    %% Technology Risk Enrichment
    subgraph TechAssessment [Technology Risk Enrichment]
        direction TB
        COMPONENTS[Evaluated Technology Components]:::technology
        CVE[Associated CVE Records]:::vulnerability
        CVSS[CVSS 3.0 and 4.0 Calculators]:::vulnerability

        COMPONENTS -->|May have| CVE
        CVE -->|Scored with| CVSS
    end

    %% Risk Register
    RR([Risk Register]):::riskModule

    ITSYS -->|Identified, assessed and evaluated against| RR
    AISYS -->|Identified, assessed and evaluated against| RR
    PROCESS -->|Identified, assessed and evaluated against| RR
    LOCATION -->|Identified, assessed and evaluated against| RR
    VENDOR -->|Identified, assessed and evaluated against| RR

    ITSYS -->|Contains| COMPONENTS
    AISYS -->|Contains| COMPONENTS
    CVE -->|Provides vulnerability context| RR
    CVSS -->|Improves risk evaluation| RR

    %% Risk Register Attributes
    subgraph RiskEvaluation [Risk Evaluation and Attributes]
        direction TB
        METRICS[Risk Metrics]:::attribute
        THREAT[Threat Model]:::attribute
        OWNER[Risk Owner]:::attribute
        QUANT[Risk Quantification]:::attribute
    end

    METRICS -->|Defines evaluation criteria| RR
    THREAT -->|Provides threat context| RR
    OWNER -->|Is accountable for| RR
    QUANT -->|Estimates risk exposure| RR

    %% Strategic Risk
    STRATEGIC[Strategic Risk]:::strategic
    RR -->|May affect if materialized| STRATEGIC

    %% Risk Register Lifecycle
    subgraph RiskLifecycle [Risk Register Lifecycle]
        direction LR
        RR_DRAFT::lifecycle
        RR_REVIEW[In Review]:::lifecycle
        RR_APPROVED::lifecycle
        RR_OBSOLETE::lifecycle

        RR_DRAFT --> RR_REVIEW
        RR_REVIEW --> RR_APPROVED
        RR_APPROVED --> RR_OBSOLETE
    end

    RR -->|Follows lifecycle| RR_DRAFT

    %% Control Design
    CD([Control Design]):::controlModule
    RR -->|Is treated by| CD

    %% Control Design Documentation
    subgraph ControlDocumentation [Control Design Documentation]
        direction TB
        CD_TITLE::attribute
        CD_CONTROL::attribute
        CD_OWNER[Responsible Person]:::attribute
        CD_PURPOSE::attribute
        CD_ACTIVITIES[Control Activities]:::attribute
        CD_EVIDENCE[Control Evidence]:::attribute
    end

    CD_TITLE -->|Describes| CD
    CD_CONTROL -->|Defines| CD
    CD_OWNER -->|Is accountable for| CD
    CD_PURPOSE -->|Explains objective| CD
    CD_ACTIVITIES -->|Documents execution| CD
    CD_EVIDENCE -->|Supports evaluation| CD

    %% Control and Compliance Coverage
    subgraph ControlCoverage [Control and Compliance Coverage]
        direction TB
        ISO_CONTROLS[ISO Controls]:::compliance
        COMPLIANCE_CONTROLS[Compliance Controls]:::compliance
        REQUIREMENTS[NIS2, PCI DSS, GDPR, CRA and Other Requirements]:::compliance
    end

    ISO_CONTROLS -->|Covered by| CD
    COMPLIANCE_CONTROLS -->|Covered by| CD
    REQUIREMENTS -->|Mapped through compliance controls| COMPLIANCE_CONTROLS

    %% Control Scope
    subgraph ControlScope [Control Scope]
        direction TB
        CS_SYSTEMS::scope
        CS_PROCESSES::scope
        CS_LOCATIONS[Physical Locations]:::scope
        CS_VENDORS::scope
    end

    CD -->|Applies to| CS_SYSTEMS
    CD -->|Applies to| CS_PROCESSES
    CD -->|Applies to| CS_LOCATIONS
    CD -->|Applies to| CS_VENDORS

    %% Control Design Lifecycle
    subgraph ControlLifecycle [Control Design Lifecycle]
        direction LR
        CD_DESIGN::lifecycle
        CD_PROGRESS[In Progress]:::lifecycle
        CD_IMPLEMENTED::lifecycle
        CD_APPROVED::lifecycle
        CD_OBSOLETE::lifecycle

        CD_DESIGN --> CD_PROGRESS
        CD_PROGRESS --> CD_IMPLEMENTED
        CD_IMPLEMENTED --> CD_APPROVED
        CD_APPROVED --> CD_OBSOLETE
    end

    CD -->|Follows lifecycle| CD_DESIGN

    %% Control Evaluation
    subgraph ControlEvaluation [Control Evaluation]
        direction TB
        DESIGN_EVAL[Design Evaluation]:::evaluation
        EFFECTIVENESS_EVAL[Effectiveness Evaluation]:::evaluation

        DESIGN_EVAL -->|Design must be adequate| EFFECTIVENESS_EVAL
    end

    CD_ACTIVITIES -->|Evaluated through| DESIGN_EVAL
    CD_EVIDENCE -->|Supports| EFFECTIVENESS_EVAL
    CD -->|Evaluated for design| DESIGN_EVAL
    CD -->|Evaluated for effectiveness| EFFECTIVENESS_EVAL

    %% Residual Risk Calculation
    RESIDUAL[Residual Risk]:::residual

    CD_APPROVED -->|Enables residual risk calculation| RESIDUAL
    DESIGN_EVAL -->|Provides evaluation result| RESIDUAL
    EFFECTIVENESS_EVAL -->|Provides evaluation result| RESIDUAL
    METRICS -->|Provides calculation criteria| RESIDUAL
    RR -->|Provides inherent risk baseline| RESIDUAL
    RESIDUAL -->|Updates residual exposure| RR
```

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
