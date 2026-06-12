---
description: Sử dụng workflow này khi có yêu cầu tạo mới một API Outbound (SAP gọi hệ thống bên ngoài) sử dụng framework Z_API_FWK để đảm bảo cấu trúc thiết kế, logging tự động, chuẩn hóa.
---

[ROLE & OBJECTIVE]
Act as an Expert SAP Integration Architect & ABAP Cloud Developer. Your task is to design, implement, and validate an OUTBOUND API integration that adheres strictly to the `Z_API_FWK` framework in the `bmw_dev` system.

[INPUT DATA]
- Package Name: [Điền tên Package]
- Transport Request: [Điền TR]
- Trigger Point: [RAP Action, Report, or Batch Job]
- Outbound Endpoint Details: [URL, Method, Auth]
- Request/Response Structure: [Cấu trúc dữ liệu gửi và nhận]
- Success/Failure Handling: [Xử lý khi thành công hoặc thất bại, luồng tiếp theo]

[EXECUTION PROTOCOL - CRITICAL]
After generating the ABAP code for each step, you MUST follow this precise lifecycle:
GENERATE -> VALIDATE (LINTING) -> DEPLOY & ACTIVATE.
All outbound calls MUST go through `ZCL_API_FWK=>execute_api`.

[STEP-BY-STEP INSTRUCTIONS]
Please execute the following sequence:

Step 0: Planning & Drafting
Required Skill: [Skill: Scratchpad]
Action: Draft the Outbound API architecture. Analyze trigger points, data extraction logic, payload structure, and response handling.
Save the draft to `generated_docs/scratchpads/scratchpad_outbound_[API_Name].md`.

Step 1: Create Data Dictionary Objects
Required Skill: [Skill: ABAP Cloud / Clean Core]
Action: Create necessary structures (DDLS/TABL/TTYP) representing the Request payload (data to send) and expected Response.
Execute: Lint -> Push -> Activate.

Step 2: Implement Outbound Integration Logic
Required Skill: [Skill: RAP] & [Skill: Clean ABAP]
Action: 
- If triggered by RAP, implement the behavior action (e.g. `FOR MODIFY`).
- Gather business data (e.g. read Sales Order details).
- Construct the request payload and headers using `zif_api_fwk_types=>ty_dynamic_request`.
- Call `NEW zcl_api_fwk( )->execute_api( EXPORTING iv_api_id = ... is_dynamic_request_value = ... IMPORTING es_logger = ... CHANGING c_response_data = ... )`.
- Parse the `es_logger` and response payload.
- Update the business object status (Success/Failure) and return explicit Reported messages to the UI.
Execute: Lint -> Push -> Activate.

Step 3: Framework Configuration
Action: Provide detailed instructions to the User to configure the Outbound API URL, Auth, Method, and Headers via Fiori App `ZUI_API_CONFIG_O4`.

Step 4: Verification & Walkthrough
Required Skill: [Skill: ABAP Unit Testing]
Action: Verify logic locally if mock data is available. Ensure that the object states are handled correctly on success/failure.
Create a Walkthrough artifact at `generated_docs/walkthroughs/walkthrough_outbound_[API_Name].md`.

[OUTPUT FORMAT]
For each step, provide:
- The Object Name & Applied Skill (e.g., ZC_MY_REPORT - [Skill: RAP]).
- The exact validated ABAP source code (markdown).
- The SYSTEM EXECUTION RESULT: Validation Log and Activation Status.
