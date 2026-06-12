# ABAP Agent Skill Router

This router serves as the central directory and execution guide for the AI Agent. It maps all available skills in this workspace, enabling the agent to dynamically load the appropriate technical context based on user requests, preventing context bloat and improving accuracy.

---

## 🤖 SYSTEM INSTRUCTION: HOW TO ROUTE SKILLS
When you receive a task in this workspace, you **MUST** follow these steps:
1. **Analyze the Request**: Identify if the task belongs to a **Consultant** (analysis, UI mapping, business logic extraction) or a **Developer** (coding, testing, deployment).
2. **Match Skills**: Look up the required skills in the [Skill Registry](#-skill-registry) below using the **Trigger Keywords** and **Description**.
3. **Load the Skill**: Read the matched `SKILL.md` file using your file reading tool. Do **NOT** read multiple unrelated skills unless they are explicitly chain-dependent. *Note: You MAY load a Productivity Skill (like Scratchpad or Handoff) in parallel with technical skills to optimize your workflow without bloating context.*
4. **Execute**: Adopt the role specified in the loaded skill and execute the instructions step-by-step.

---

## 📋 SKILL REGISTRY

### 🏛️ 1. Consultant Skills (Business Analysis & Architecture)
These skills focus on translating functional requirements into structured technical designs.

| Skill Name | Role | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- | :--- |
| **Data Model Extractor** | Expert SAP Data Architect | [SKILL.md](./skills/Consultant/fs-data-model-extractor/SKILL.md) | Extracts standard/custom tables, CDS Views, join conditions, and output fields from Functional Specifications (FS). | `data model`, `extract tables`, `joins`, `relations`, `FS analysis`, `trích xuất bảng`, `sơ đồ dữ liệu`, `phân tích bảng` |
| **Fiori UI Elements Mapper** | Fiori UX/UI Technical Consultant | [SKILL.md](./skills/Consultant/fs-fiori-ui-elements-mapper/SKILL.md) | Translates report layout requirements into Fiori Elements annotations (`selectionField`, `lineItem`, etc.). | `fiori elements`, `selection fields`, `line items`, `sorting`, `facets`, `giao diện fiori`, `bộ lọc`, `hiển thị cột`, `bố cục` |
| **ABAP Logic & Behavior Translator** | Senior ABAP Cloud Developer (Consultant) | [SKILL.md](./skills/Consultant/fs-logic-behavior-translator/SKILL.md) | Analyzes processing logic to determine implementation layers (CDS logic, Virtual Elements, or RAP Behavior Pool). | `business rules`, `calculated fields`, `virtual elements`, `derived logic`, `actions`, `logic xử lý`, `quy tắc nghiệp vụ`, `tính toán`, `hành vi` |
| **Integration & API Analyzer** | Expert SAP Integration Architect | [SKILL.md](./skills/Consultant/fs-integration-api-analyzer/SKILL.md) | Extracts integration patterns, API specifications (OData, REST), JSON payloads, and mapping tables from FS. | `integration`, `OData API`, `REST API`, `mapping`, `JSON payload`, `payload`, `tích hợp`, `giao tiếp hệ thống`, `kết nối API`, `cấu trúc JSON` |
| **FS Vision Extractor** | Expert SAP Multimodal Analyst | [SKILL.md](./skills/Consultant/fs-vision-extractor/SKILL.md) | Extracts UI mockups, Excel tables, and flowchart logic from images embedded in FS documents into Markdown. | `image`, `mockup`, `vision`, `extract image`, `flowchart`, `excel screenshot`, `xử lý ảnh`, `nhận diện ảnh`, `trích xuất ảnh` |
| **Find Released CDS View** | Expert SAP Data Architect | [SKILL.md](./skills/Consultant/find-released-cds-view/SKILL.md) | Finds the best SAP released CDS view (DDLS) for a RAP/reporting field by matching business object, screen context, data grain, field availability, and local coverage against S/4HANA Cloud Public Edition released APIs. | `released CDS`, `find CDS view`, `DDLS`, `released API`, `clean core CDS`, `value help view`, `I_*`, `tìm CDS view`, `CDS released`, `data source RAP` |

---

### 💻 2. Developer Skills (Technical Implementation)
These skills contain precise syntax rules, code templates, and development guidelines for ABAP Cloud.

| Skill Name | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- |
| **ABAP Lint & Review** | [SKILL.md](./skills/Developer/abap/SKILL.md) | Validates ABAP code quality using `abaplint` rules and Clean ABAP standards. | `abaplint`, `lint`, `code review`, `syntax check`, `kiểm tra code`, `đánh giá code`, `tiêu chuẩn abap` |
| **ABAP Cloud / Clean Core** | [SKILL.md](./skills/Developer/abap-cloud/SKILL.md) | Enforces ABAP Cloud restrictions, 3-tier extensibility, and unreleased API wrappers. | `clean core`, `3-tier`, `restricted API`, `cloud development`, `wrapper`, `chuẩn hóa core`, `tier 1` |
| **ABAP Cloud Migration** | [SKILL.md](./skills/Developer/abap-cloud-migration/SKILL.md) | Workflow and mapping patterns for migrating classic custom ABAP code to Cloud Tier 1. | `migration`, `migrate`, `cloud readiness`, `atc scan`, `chuyển đổi hệ thống`, `nâng cấp cloud` |
| **ABAP SQL & AMDP** | [SKILL.md](./skills/Developer/abap-sql-amdp/SKILL.md) | Modern ABAP SQL (inline, CTEs, window functions) and SQLScript AMDP class patterns. | `AMDP`, `window functions`, `CTE`, `SQLScript`, `SQL query`, `truy vấn dữ liệu`, `amdp class`, `modern sql` |
| **ABAP Unit Testing** | [SKILL.md](./skills/Developer/abap-unit-testing/SKILL.md) | ABAP Unit test setups, mock double frameworks, and test environments for CDS and OSQL. | `unit test`, `mock`, `test double`, `cl_abap_unit_assert`, `kiểm thử tự động`, `unit test abap`, `chạy test` |
| **ATC Cloudification** | [SKILL.md](./skills/Developer/atc-cloudification/SKILL.md) | Configuration and notes for setting up ATC Cloud Readiness & Clean Core variants. | `ATC`, `cloud readiness`, `cloudification repository`, `quét atc`, `lỗi ready`, `atc check` |
| **Authorization & IAM** | [SKILL.md](./skills/Developer/authorization-iam/SKILL.md) | Implements DCL (Access Controls), BTP IAM apps, business roles, and RAP authorizations. | `DCL`, `authorization`, `IAM`, `business catalog`, `pfcg_auth`, `phân quyền`, `quyền truy cập`, `bảo mật dcl` |
| **BAdI & Enhancements** | [SKILL.md](./skills/Developer/badi-enhancement/SKILL.md) | Standard SAP extensions using BAdIs, Enhancement Spots, and Key User Extensibility. | `BAdI`, `enhancement spot`, `implicit`, `explicit`, `extend`, `mở rộng hệ thống`, `badi spot`, `bản vá` |
| **BTP ABAP Environment** | [SKILL.md](./skills/Developer/btp-abap-environment/SKILL.md) | Provisioning, ADT connection, and communication arrangements setup in Steampunk. | `BTP`, `Steampunk`, `communication arrangement`, `ADT connection`, `môi trường btp`, `kết nối adt` |
| **BTP Diagram Generator** | [SKILL.md](./skills/Developer/btp-diagram-generator/SKILL.md) | Python builder library for generating draw.io/Horizon design solutions diagram. | `draw.io`, `diagram`, `architecture diagram`, `btp_builder`, `vẽ sơ đồ`, `diagram architecture` |
| **CDS View Entities** | [SKILL.md](./skills/Developer/cds-view-entities/SKILL.md) | Core CDS View Entity syntax, associations, metadata extensions, and annotations. | `CDS`, `view entity`, `association`, `projection`, `metadata extension`, `tạo cds view`, `cds entity`, `view mở rộng` |
| **Clean ABAP** | [SKILL.md](./skills/Developer/clean-abap/SKILL.md) | Strict coding styles, clean methods, small parameters, and exception handling patterns. | `clean abap`, `naming conventions`, `refactoring`, `style guide`, `mã sạch`, `viết code sạch` |
| **Naming Conventions** | [SKILL.md](./skills/Developer/naming-convension/SKILL.md) | Project-specific naming guidelines (FPT) for database tables, CDS, RAP, and Packages. | `naming convention`, `prefix`, `suffix`, `ZA_`, `ZC_`, `ZR_`, `quy tắc đặt tên`, `tiền tố`, `hậu tố` |
| **OData Service Development** | [SKILL.md](./skills/Developer/odata/SKILL.md) | RAP OData V4/V2, SEGW classic service, and external OData client proxy consumption. | `OData`, `service definition`, `service binding`, `V4`, `client proxy`, `dịch vụ odata`, `service binding` |
| **RAP Model** | [SKILL.md](./skills/Developer/rap/SKILL.md) | Managed/Unmanaged RAP BO, behavior pool, draft, validations, and determinations. | `RAP`, `behavior definition`, `EML`, `BDEF`, `%tky`, `%cid`, `mô hình rap`, `behavior pool`, `bdef` |
| **RAP Query Provider** | [SKILL.md](./skills/Developer/rap-query-provider/SKILL.md) | Implements Custom Entity query providers (IF_RAP_QUERY_PROVIDER) with paging, sorting, and filtering. | `IF_RAP_QUERY_PROVIDER`, `custom entity class`, `select method`, `get_sort_elements`, `get_paging`, `set_total_number_of_records`, `Query not fully covered` |
| **RAP Business Events** | [SKILL.md](./skills/Developer/rap-business-events/SKILL.md) | Defines and raises entity events linked to SAP Event Mesh for event-driven patterns. | `event mesh`, `business event`, `raise event`, `event binding`, `sự kiện rap`, `event mesh` |
| **Released ABAP Classes** | [SKILL.md](./skills/Developer/released-abap-classes/SKILL.md) | Full catalog and examples of BTP/Cloud-released helper classes (Console, Mail, HTTP). | `released class`, `CL_BCS_MAIL`, `XCO_CP_JSON`, `UUID`, `thư viện class`, `helper class` |
| **SAP Fiori Apps Reference** | [SKILL.md](./skills/Developer/sap-fiori-apps-reference/SKILL.md) | Generates Fiori Launchpad URLs and queries the Fiori Apps Reference Library. | `Fiori library`, `AppList`, `Launchpad URL`, `semantic object`, `tra cứu ứng dụng`, `fiori library` |

---

### 🚀 3. Productivity Skills (Efficiency & Context Management)
These skills modify the agent's behavior to optimize communication, planning, and continuity.

| Skill Name | Role | Path | Description | Trigger Keywords |
| :--- | :--- | :--- | :--- | :--- |
| **Grill Me** | Expert Interviewer | [SKILL.md](./skills/Productivity/grill-me/SKILL.md) | Asks targeted questions to clarify requirements before starting work. | `grill me`, `clarify`, `interview`, `hỏi tôi`, `làm rõ` |
| **Caveman** | Concise Communicator | [SKILL.md](./skills/Productivity/caveman/SKILL.md) | Provides ultra-terse, fluff-free technical responses. | `caveman`, `short`, `terse`, `ngắn gọn`, `không rườm rà` |
| **Handoff** | Session Manager | [SKILL.md](./skills/Productivity/handoff/SKILL.md) | Summarizes context and progress for seamless transition between sessions. | `handoff`, `summary`, `transition`, `chuyển giao`, `tổng kết` |
| **Scratchpad** | Structured Thinker | [SKILL.md](./skills/Productivity/scratchpad/SKILL.md) | Uses a working document to draft, plan, and track complex changes. | `scratchpad`, `draft`, `plan`, `nháp`, `lên kế hoạch` |

---

## 🔀 WORKFLOW ROUTING INTEGRATION
The workflows inside `.agents/workflows/` invoke these skills dynamically:
- **/sap-dev-analytic-fs**: Sequentially loads `Data Model Extractor`, `Find Released CDS View` (to validate released clean-core sources), `Fiori UI Elements Mapper`, and `ABAP Logic & Behavior Translator` to generate Technical Specs from an FS.
- **/sap-dev-create-report**: Steps reference `Find Released CDS View` (to verify data sources before coding), `CDS View Entities`, `Authorization & IAM`, `RAP Model`, `OData Service Development`, and `Clean ABAP` to write and deploy code.
- **/sap-dev-bug-fix**: Integrates `Grill Me`, `Scratchpad`, `Data Model Extractor` and `ABAP Logic & Behavior Translator` for root cause analysis with mock data, enforces cross-impact checks, and applies code fixes with `ABAP Unit Testing` and `Clean ABAP` to ensure regression-free deployment in DEV.
- **/sap-dev-api-inbound**: Integrates `Scratchpad`, `ABAP Cloud / Clean Core`, and `Clean ABAP` to design, implement, and validate an INBOUND API integration adhering to the `Z_API_FWK` framework.
- **/sap-dev-api-outbound**: Integrates `Scratchpad`, `RAP`, and `Clean ABAP` to construct Outbound API integrations, format payloads, and manage response status updates using `ZCL_API_FWK=>execute_api`.
- **/sap-dev-system-analysis**: Integrates `Scratchpad`, `Data Model Extractor`, and `ABAP Logic & Behavior Translator` to systematically scan, deep-dive, and document SAP objects or packages into comprehensive Markdown technical reports.
- **/sap-dev-code-review**: Integrates `ABAP Lint & Review`, `ABAP SQL & AMDP`, and `Clean ABAP` to scrutinize code, provide risk analysis, performance optimization suggestions, and maintainability feedback without auto-refactoring code.

