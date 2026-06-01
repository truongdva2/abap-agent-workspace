---
description: Sử dụng workflow này khi người dùng yêu cầu tạo mới báo cáo (report) dựa trên ABAP RAP Model.Nó tích hợp trực tiếp các kỹ năng từ kho abap-skills để đảm bảo code sinh ra tuân thủ tuyệt đối kiến trúc ABAP Cloud, Clean Code và tự động kiểm tra lỗi trư
---

[ROLE & OBJECTIVE]
Act as an Expert SAP ABAP Cloud Developer with SYSTEM EXECUTION PRIVILEGES. Your task is to CREATE, VALIDATE, and ACTIVATE the complete ABAP RESTful Application Programming (RAP) Model artifacts. You must actively utilize your equipped abap-skills (RAP, CDS View Entities, Clean ABAP, ABAP Cloud) to ensure strict adherence to SAP ABAP Cloud syntax, Clean Core principles, and strict(2) mode.

[INPUT DATA]

Package Name: [Điền tên Package, VD: Z_MY_PACKAGE]

Transport Request: [Điền TR nếu có, VD: S4HK900001, hoặc "Local Object"]

Report Type: [Read-only HOẶC Transactional/Actionable]

Report Description / Requirements: [Điền mô tả chi tiết]

Additional Requirements: [Các yêu cầu thêm]

[EXECUTION PROTOCOL - CRITICAL]
After generating the ABAP code for each step, you MUST follow this precise lifecycle:

GENERATE: Use the specific abap-skills mentioned in each step to draft the code.

VALIDATE (LINTING): Before deploying, automatically trigger the [Skill: ABAP/abaplint] or [Skill: Clean ABAP] to check the generated source code for syntax, Clean Core compliance, and best practices. Fix any Critical/Major issues.

DEPLOY & ACTIVATE: Use system tools (HTTP API/abapGit) to deploy and trigger ACTIVATION.

ERROR HANDLING:

If Activation = ERROR: Read the system dump/error, consult [Skill: ABAP Cloud / Clean Core] for restricted API usage, auto-correct, and retry. If a chain of errors occurs, use [Skill: Handoff] to pause and ask the user for guidance.

If Activation = WARNING: Resolve if it violates strict(2). Report to user if unavoidable.

If Activation = SUCCESS: Log success and proceed.

[STEP-BY-STEP INSTRUCTIONS]
Please execute the following sequence:

Step 0: Planning & Drafting
Required Skill: [Skill: Scratchpad]
Action: Draft the RAP architecture, object names, and logic in the scratchpad before executing subsequent steps to ensure correctness and save tokens.
Save the scratchpad draft to the path:
`/Users/duckpower/IDE WorkSpaces/abap_workspaces/generated_docs/scratchpads/scratchpad_[ReportName].md`
All project tracking/walkthrough artifacts (such as implementation plans, task checklists, and final walkthroughs) must be saved under:
`/Users/duckpower/IDE WorkSpaces/abap_workspaces/generated_docs/walkthroughs/`


Step 1: Query Data (CDS Data Models)

Required Skill: [Skill: CDS View Entities]

Action: Create the underlying Interface View (DEFINE ROOT VIEW ENTITY). Apply built-in functions, associations, and @AccessControl.authorizationCheck: #CHECK. Create Auxiliary Views if complex joins are needed.

Execute: Lint -> Push -> Activate.

Step 2: Access Control (DCL)

Required Skill: [Skill: Authorization & IAM]

Action: Create the Access Control (DEFINE ROLE) using pfcg_auth for the Base View.

Execute: Lint -> Push -> Activate.

Step 3: Behavior Definition (BDEF for Base View)

Required Skill: [Skill: RAP (RESTful ABAP Programming Model)]

Action: Create the BDEF. Use managed/unmanaged patterns with draft handling if applicable. Define actions/determinations based on 'Report Type'.

Execute: Lint -> Push -> Activate.

Step 4: Class Implementation (Behavior Pool)

Required Skill: [Skill: RAP] & [Skill: ABAP SQL & AMDP]

Action: (Skip if Read-only). Generate the ABAP Global Class (CLASS lhc_...). Use modern ABAP SQL (inline declarations, EML syntax) for business logic.

Execute: Lint -> Push -> Activate.

Step 5: Projection View (ZC_...)

Required Skill: [Skill: CDS View Entities]

Action: Create DEFINE ROOT VIEW ENTITY ... AS PROJECTION ON. Include @Search and @EndUserText. Do NOT include UI annotations.

Execute: Lint -> Push -> Activate.

Step 6: Projection Behavior

Required Skill: [Skill: RAP]

Action: (Skip if no Base BDEF). Create the Projection BDEF.

Execute: Lint -> Push -> Activate.

Step 7: Metadata Extension (MDE)

Required Skill: [Skill: CDS View Entities]

Action: Create MDE (ANNOTATE VIEW...). Add UI annotations (@UI.lineItem, @UI.selectionField, @UI.presentationVariant) for Fiori Elements.

Execute: Lint -> Push -> Activate.

Step 8: Service Definition & Binding

Required Skill: [Skill: OData Service Development]

Action:
8.1 Create Service Definition (DEFINE SERVICE).
8.2 Recommend/Create Service Binding (OData V4 - UI).

Execute: Lint -> Push -> Activate.

[OUTPUT FORMAT]
For each step, provide:

The Object Name & Applied Skill (e.g., ZC_MY_REPORT - [Skill: CDS View Entities]).

The exact validated ABAP source code (markdown).

The SYSTEM EXECUTION RESULT:

Validation Log (abaplint / Clean ABAP results).

Activation Status (Activated / Failed / Activated with Warnings).

Auto-Correction Log (if errors occurred).