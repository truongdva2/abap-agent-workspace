---
description: Sử dụng workflow này khi có yêu cầu tạo mới một API Inbound (Hệ thống bên ngoài gọi vào SAP). Workflow đảm bảo tuân thủ kiến trúc của Z_API_FWK, xử lý logging tự động và thiết kế handler class chuẩn mực.
---

[ROLE & OBJECTIVE]
Act as an Expert SAP Integration Architect & ABAP Cloud Developer. Your task is to design, implement, and validate an INBOUND API integration that adheres strictly to the `Z_API_FWK` framework in the `bmw_dev` system.

[INPUT DATA]
- Package Name: [Điền tên Package]
- Transport Request: [Điền TR]
- Business Data Requirements (Request/Response): [Cấu trúc dữ liệu nhận vào và trả về]
- Existing Communication Objects: [Có hay chưa]
- API Design Details (Method, Auth, Headers, Params): [Chi tiết API]
- Success/Failure Criteria: [Định nghĩa thành công/thất bại và luồng xử lý]

[EXECUTION PROTOCOL - CRITICAL]
After generating the ABAP code for each step, you MUST follow this precise lifecycle:
GENERATE -> VALIDATE (LINTING) -> DEPLOY & ACTIVATE.
All errors MUST be caught using `CX_ROOT` or `ZCX_API_FWK` and returned explicitly.

[STEP-BY-STEP INSTRUCTIONS]
Please execute the following sequence:

Step 0: Planning & Drafting
Required Skill: [Skill: Scratchpad]
Action: Draft the Inbound API architecture. Analyze the JSON/XML payload and map it to ABAP Dictionary structures. Define the HTTP logic, success/error handling criteria. 
Save the draft to `generated_docs/scratchpads/scratchpad_inbound_[API_Name].md`.

Step 1: Create Data Dictionary Objects
Required Skill: [Skill: ABAP Cloud / Clean Core]
Action: Create necessary structures (DDLS/TABL/TTYP) to represent the Request and Response data payloads mapped from the input requirement.
Execute: Lint -> Push -> Activate.

Step 2: Implement Handler Class
Required Skill: [Skill: Clean ABAP], [Skill: Released ABAP Classes], [Skill: Modern ABAP Syntax], [Skill: OO Design Patterns]
Action: 
- Create a global class (e.g. `ZCL_IB_[API_NAME]`) that implements the interface `ZIF_API_INBOUND_HANDLER`. Apply OO Design Patterns (e.g., Strategy) if handling multiple payload types.
- Implement `handle_request` method:
  - Parse the input payload (e.g. using helper classes like `xco_cp_json` or `zcl_api_fwk=>json_to_abap`).
  - Execute core business logic (e.g. EML to create Sales Order or Business Object).
  - Handle success/error clearly. Catch ALL exceptions (including `cx_static_check` and `cx_root`) and return meaningful HTTP Status and error messages in the response payload.
Execute: Lint -> Push -> Activate.

Step 3: Framework Configuration
Action: Provide detailed instructions to the User to configure this new API via Fiori App `ZUI_API_CONFIG_O4`. The user needs to map the API ID to the newly created Handler Class name in the Configuration UI.

Step 4: Verification & Walkthrough
Required Skill: [Skill: ABAP Unit Testing]
Action: Generate ABAP Unit Tests for the Handler Class using mock data. Ensure all code behaves as expected without Side-effects outside the scope.
Create a Walkthrough artifact at `generated_docs/walkthroughs/walkthrough_inbound_[API_Name].md`.

[OUTPUT FORMAT]
For each step, provide:
- The Object Name & Applied Skill (e.g., ZCL_IB_CREATE_SO - [Skill: Clean ABAP]).
- The exact validated ABAP source code (markdown).
- The SYSTEM EXECUTION RESULT: Validation Log and Activation Status.
