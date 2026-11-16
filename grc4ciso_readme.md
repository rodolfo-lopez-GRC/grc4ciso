# **OWASP GRC4CISO**

## **Introduction**

This project provides you a GRC (Governance, Risk and Compliance) platform focused to manage Cybersecurity risks, control design, compliance and AI related risks considering risks.

With this platform, you can deploy ISO 27001:2022 as an Information Security Management System, perform cybersecurity risk analysis and evaluation, design and implement controls, and generate reports to demonstrate trust to your customers, stakeholders, and regulators—while ensuring compliance with cybersecurity requirements and regulations.

The platform has the following functionalities:

- Asset management.
- Cyber/AI Risk Management and Control.
- BIA.
- ISMS: Information Security Management System (based on ISO27001:2022).
- Compliance.

### **GRC Architecture Overview**

The **grc4ciso** platform follows a Top-Down architecture designed to protect organizational data through a structured Governance, Risk, and Compliance framework. 

This diagram illustrates how compliance requirements drive control implementation, which in turn mitigates risks across critical business assets.

```mermaid
flowchart TD
    %% Styling Definitions
    classDef risk fill:#e74c3c,color:#fff,stroke:#c0392b,stroke-width:2px
    classDef control fill:#2980b9,color:#fff,stroke:#2471a3,stroke-width:2px
    classDef comp fill:#f39c12,color:#fff,stroke:#d68910,stroke-width:2px
    classDef asset fill:#27ae60,color:#fff,stroke:#1e8449,stroke-width:2px
    classDef data fill:#8e44ad,color:#fff,stroke:#732d91,stroke-width:2px
    classDef support fill:#34495e,color:#fff,stroke:#2c3e50,stroke-width:2px

    %% Core GRC Modules
    COMP[Compliance Requirements]:::comp
    CTRL[Controls]:::control
    RM[Risk Management]:::risk

    %% Assets and Data
    subgraph Targets [Targets of Evaluation / Assets]
        IT[IT Systems]:::asset
        VEND[Vendors / Third Parties]:::asset
        AI[AI Components]:::asset
        PROC[Business Processes]:::asset
    end
    
    DATA[(Data)]:::data

    %% Core Relationships
    COMP -->|Linked to demonstrate compliance <br/> with security requirements| CTRL
    CTRL -->|Mitigates inherent risks <br/> Design & Effectiveness evaluated <br/> for Residual Risk| RM
    RM -->|Assesses & Evaluates| Targets
    
    IT -->|Stores, Processes, Transmits| DATA
    VEND -->|Stores, Processes, Transmits| DATA
    AI -->|Stores, Processes, Transmits| DATA
    PROC -->|Stores, Processes, Transmits| DATA

    %% Transversal Support Modules
    subgraph SupportModules [GRC Support Modules]
        direction LR
        ISMS[ISMS ISO 27001 <br/> Deployment]:::support
        BIA[Business Impact <br/> Analysis - BIA]:::support
        DASH[Dashboards <br/> & Reports]:::support
    end

    %% Support Connections
    SupportModules -.- RM
    SupportModules -.- CTRL
    SupportModules -.- COMP
```

## **Asset Management**

Assets that enable the organization to achieve business purposes are identified and managed consistent with their relative importance to organizational objectives and the organization’s risk strategy.

Understanding the organization’s assets like data, IT systems, AI components, vendors, and processes and related cybersecurity risks enables an organization to prioritize its efforts consistent with its risk management strategy and the mission needs.

### **Data Asset**

```mermaid
graph TD;
    A[Data Asset]--stored, processed, transmitted through-->B[IT System];
    A[Data Asset]--managed in-->C[Business Process];
    A[Data Asset]--accessed by-->D[Suppliers];
```

The primary catalog is the Data Asset Catalog, because ultimately, data is what we aim to protect. If data is exposed or compromised, it can have a significant negative impact on the organization. This module is designed to register the company’s critical data assets.

Some attributes captured here include: asset name, data classification, asset owner, IT systems, processes where data is managed, vendors with access to that data and AI components where data is accessed/used.

Record your data assets in as much detail as possible. This information will allow us to accurately assess potential impacts on the organization and define the most appropriate risk management strategies for these assets.

<img width="1325" height="487" alt="image" src="https://github.com/user-attachments/assets/49a4a29f-2eb6-49c1-8ae8-534d083fbcc4" />

### **IT System**

This is a high-level catalog of the organization’s critical platforms. It is not intended to be a CMDB (Configuration Management Database), but rather a registry of system platforms that support critical processes or store, transmit, or process critical data.
Each IT system is mapped with the IT Components that support the IT system, in the IT component some attributes are requiered like IP, URL, TCP ports open, IT admin.
AI platforms are registered in this module as well, in this case the AI components are related so the risk assessment consider these type of components in order to identify wich controls should designed and implemented in order to mitigate risks.

```mermaid
flowchart TD
    %% Styling Definitions (Consistent with Core Architecture)
    classDef business fill:#34495e,color:#fff,stroke:#2c3e50,stroke-width:2px
    classDef data fill:#8e44ad,color:#fff,stroke:#732d91,stroke-width:2px
    classDef system fill:#27ae60,color:#fff,stroke:#1e8449,stroke-width:2px
    classDef ai fill:#16a085,color:#fff,stroke:#117864,stroke-width:2px
    classDef component fill:#ecf0f1,color:#2c3e50,stroke:#7f8c8d,stroke-width:2px,text-align:left
    classDef risk fill:#e74c3c,color:#fff,stroke:#c0392b,stroke-width:2px
    classDef control fill:#2980b9,color:#fff,stroke:#2471a3,stroke-width:2px

    %% Business Context Layer
    subgraph Context [Business & Data Context]
        direction LR
        PROC[Critical Business Processes]:::business
        DATA[(Critical Data <br/> PII / PHI / PCI / IP)]:::data
    end

    %% Platform Registry Layer
    subgraph Registry [IT & AI Platform Registry]
        direction LR
        ITSYS[IT Systems <br/> Critical Platforms]:::system
        AISYS[AI Platforms <br/> LLMs, Agents, ML Models]:::ai
    end

    %% Technical Components Layer
    subgraph Components [Underlying Technical Components]
        direction LR
        ITCOMP["<b>IT Components</b><br/>• IP Address<br/>• URL / Endpoint<br/>• Open TCP Ports<br/>• IT Admin Owner"]:::component
        AICOMP["<b>AI Components</b><br/>• Model / API Endpoint<br/>• Data Pipeline / Vector DB<br/>• Guardrails & Integrations<br/>• AI / IT Admin Owner"]:::component
    end

    %% GRC Governance Layer
    RM[Risk Management <br/> Threat & Attack Surface Assessment]:::risk
    CTRL[Security Controls <br/> Technical & AI-Specific Safeguards]:::control

    %% Relationships
    ITSYS -->|Supports| PROC
    ITSYS -->|Stores, Processes, Transmits| DATA
    AISYS -->|Supports| PROC
    AISYS -->|Stores, Processes, Transmits| DATA

    ITSYS -->|Mapped to| ITCOMP
    AISYS -->|Mapped to| AICOMP

    ITCOMP -->|Evaluated in| RM
    AICOMP -->|Evaluated in| RM
    
    CTRL -->|Designed & Implemented <br/> to mitigate component risks| RM
```


### **Business Process**

This is a high-level catalog of the processes where critical data is managed. Cybersecurity should be addressed not only from a technical systems perspective, but also by considering the processes in which data is handled, as well as the people and suppliers who have access to it.


### **Vendors**

Vendors play a vital role in your organization’s operations, but they also introduce significant security and compliance risks. Many suppliers have access to your systems, sensitive data, or processing environments, which makes proper oversight essential.

To safeguard your organization, it is crucial to identify suppliers with access to critical data or systems. This enables you to perform a comprehensive vendor or supplier risk assessment as part of your overall risk management process. Effective supplier risk management helps mitigate potential threats, ensures regulatory compliance, and strengthens your organization’s data protection posture.





## **Risk Management**

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
