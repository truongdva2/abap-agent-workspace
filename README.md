# 🚀 SAP ABAP Cloud Agent Workspace

Welcome to the **SAP ABAP Cloud Agent Workspace**. This is an intelligent workspace specifically optimized for Pair-Programming between you and the AI Agent (Antigravity) to develop applications on the **SAP BTP ABAP Environment** and **S/4HANA Cloud (Clean Core)** platforms.

This workspace comes with built-in strict governance rules, a deep knowledge base of Skills, and automated Workflows to transform Functional Specification (FS) documents into high-quality ABAP RAP source code, ensuring strict adherence to **Clean Core & Clean ABAP** standards.

---

## 📂 Workspace Directory Structure

The project is scientifically organized around the `.agents/` configuration directory:

```text
abap_workspaces/
├── .agents/                        # 🧠 Artificial Intelligence Coordination Center (Agent Hub)
│   ├── SKILLS_ROUTER.md            # 🔀 Dynamic skill routing guide for the Agent
│   ├── rules/
│   │   └── sap-dev-rule.md         # 🛡️ Mandatory rules (Clean Core, Custom Only, TR...)
│   ├── skills/                     # 📚 Deep specialized skill library for the Agent
│   │   ├── Consultant/             # 🏛️ Business Analysis & Architecture skills
│   │   │   ├── fs-data-model-extractor/
│   │   │   ├── fs-fiori-ui-elements-mapper/
│   │   │   ├── fs-logic-behavior-translator/
│   │   │   ├── fs-integration-api-analyzer/
│   │   │   └── fs-vision-extractor/
│   │   ├── Developer/              # 💻 Development & Technical ABAP Cloud skills
│   │   │   ├── abap/ , abap-cloud/ , clean-abap/ , naming-convension/ , modern-abap-syntax/ , oo-design-patterns/ ...
│   │   │   └── rap/ , cds-view-entities/ , odata/ , authorization-iam/ , abap-generative-ai/ ...
│   │   └── Productivity/           # 🚀 Performance Optimization & Context Management skills
│   │       └── grill-me/ , caveman/ , handoff/ , scratchpad/
│   └── workflows/                  # ⚙️ Business process automation scripts
│       ├── sap-dev-analytic-fs.md  # Process for analyzing FS into Technical Spec
│       ├── sap-dev-create-report.md# Process for auto-generating ABAP RAP reports
│       ├── sap-dev-api-inbound.md  # Process for Inbound API integration based on Z_API_FWK
│       ├── sap-dev-api-outbound.md # Process for Outbound API integration based on Z_API_FWK
│       ├── sap-dev-system-analysis.md # Process for analyzing SAP system architecture
│       └── sap-dev-code-review.md  # Process for strict Code Review & QA
├── fs_docs/                        # 📄 Directory containing input Functional Specification (FS) documents
├── generated_docs/                 # 📂 Directory containing automatically generated technical documents
│   ├── technical_specifications/   # Technical Specifications (TS_*.md)
│   ├── scratchpads/                # Architectural drafts and planning (Scratchpads - scratchpad_*.md)
│   └── walkthroughs/               # Deployment guides, testing & task checklists
└── README.md                       # 📖 User documentation (This file)
```

---

## 🛠️ Core Components & How They Work

### 1. Agent Capability Router (`SKILLS_ROUTER.md`)
This is the central directory managing all Skills. When you assign a task, the Agent automatically matches keywords in your request with this directory to dynamically load the necessary technical context, avoiding context bloat and optimizing token usage.
* **Context Optimization:** The system supports parallel loading of **Productivity** skills (e.g., `Scratchpad` for drafting before coding, `Handoff` for context transition, `Grill Me` for interview-style clarification) alongside technical skills, helping maintain coherent system thinking.

### 2. Automated Development Rules (`rules/sap-dev-rule.md`)
Rules running silently during each interaction. It forces the Agent to strictly follow:
* **Modern ABAP & Design Patterns:** Enforce the use of modern ABAP syntax (Constructor Expressions, String Templates) and GoF OO Design Patterns.
* **Clean Core:** Use CDS Views to read data and EML (Entity Manipulation Language) to write data. Absolutely no direct modification of physical tables.
* **Custom Only (Z/Y):** Only operate on custom Z/Y objects of the project. Do not modify SAP standard objects.
* **TR & Package:** Every new/modified object must clearly declare a Package and a Transport Request.

### 3. Automation Scripts (Workflows)
Use dedicated Slash Commands designed for complex processes:
* `/sap-dev-analytic-fs`: Automatically triggers the Consultant skill chain to deeply analyze Word/PDF FS files, extract the Data Model structure, Fiori Elements layout, balance calculation/fallback logic, and output a standard Technical Specification.
* `/sap-dev-create-report`: Takes a Technical Spec as input, automatically triggers the Developer skill chain to write clean code, create CDS View Entities, Access Controls (DCL), Business Services, RAP BO Behavior Pools, and perform automated testing.
* `/sap-dev-api-inbound`: Build external API receiving functionalities adhering to the `Z_API_FWK` architecture.
* `/sap-dev-api-outbound`: Build outbound calls to other systems ensuring logging mechanisms and response handling via `execute_api`.
* `/sap-dev-system-analysis`: Automatically scan, deep-dive, and generate comprehensive architecture documentation for objects/packages.
* `/sap-dev-code-review`: Perform rigorous source code reviews (including Cross-Impact Check), evaluate potential risks, and propose performance/maintainability optimizations.

---

## 🚀 Quick Start Guide

### Step 1: Prepare Input Documents
Ensure you have placed the Functional Specification (FS) document into the `fs_docs/` directory of the workspace (e.g., a `.docx` Word file or Text file).

### Step 2: Trigger the FS Analysis Process
Send an analysis request to the Agent with the document path.
* *Example:* `"Please trigger the /sap-dev-analytic-fs workflow to analyze the FS document [SAPER_2025_PM_FS.docx](./fs_docs/SAPER_2025_PM_FS.docx) belonging to Package Z_INVENTORY_REPORT"`

### Step 3: Evaluate Technical Spec & Generate Code
After the Agent completes the analysis and returns a standard Technical Specification structure, please review it. Then, trigger the `/sap-dev-create-report` command for the Agent to automatically generate comprehensive ABAP RAP code for you.

---

## ⚙️ Notes for Developers
* **Relative Paths:** All configuration documents in this project use Relative Paths so you can move the workspace to any personal computer or Cloud environment without breaking links.
* **Inheritance & Development:** You can easily add new Skills to the `.agents/skills/` directory and declare them in the registration table within `SKILLS_ROUTER.md` to upgrade your Agent's intelligence.
