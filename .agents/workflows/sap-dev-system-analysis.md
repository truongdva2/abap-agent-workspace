---
description: Sử dụng workflow này khi có yêu cầu đọc, phân tích sâu và xuất báo cáo tài liệu chi tiết cho một hoặc một nhóm đối tượng/package trên hệ thống SAP.
---

[ROLE & OBJECTIVE]
Act as an Expert SAP System Architect & Technical Analyst. Your task is to extract, read, and comprehensively analyze a given SAP Object or Package using the system's MCP tools, and then produce a detailed technical documentation report.

[INPUT DATA]
- Target: [Tên Object, Danh sách Object, hoặc Tên Package]
- Analysis Focus: [Ví dụ: Tìm hiểu luồng data, Phân tích nghiệp vụ, Vẽ data model, Phân tích Call Graph...]
- Additional Requirements: [Các yêu cầu khác từ user]

[EXECUTION PROTOCOL - CRITICAL]
Since analyzing a whole package or complex object might produce an excessive amount of text, you MUST follow this chunking protocol:
1. SCAN: Always list the structure first. Do NOT attempt to read all source codes at once.
2. FILTER: Identify the core components (Main classes, Root CDS Views, Key Tables).
3. DEEP DIVE: Read the source code of only the filtered core components to understand the business logic and relationships.
4. DOCUMENT: Synthesize the findings into a structured markdown report.

[STEP-BY-STEP INSTRUCTIONS]
Please execute the following sequence:

Step 0: System Scanning & Component Discovery
Required Skill: [Skill: Scratchpad]
Action:
- Use MCP Tool `SAP(action="read", target="<Target_Name>")` or `SAP(action="search", ...)` to get the initial structure/list of objects.
- Create a `scratchpad_analysis_[Target].md` in `generated_docs/scratchpads/`.
- Document the tree structure in the scratchpad and select the top priority objects that contain the core logic/data models.

Step 1: Deep Dive Analysis
Required Skill: [Skill: ABAP Logic & Behavior Translator] & [Skill: Data Model Extractor]
Action:
- Sequentially read the source codes of the prioritized objects using MCP Tool `SAP(action="read")`.
- Analyze:
  - Data Model: How tables and CDS views are linked (Joins, Associations).
  - Business Logic: What the main ABAP Classes/Methods do.
  - Integration: Any API calls or external interactions.
- Continuously update your findings in the scratchpad.

Step 2: Generate Final Technical Report
Action:
Create the final, comprehensive Markdown document. 
Location: `generated_docs/system_analysis/analysis_report_[Target].md`.
Format the document exactly as follows:

# [Tên Đối Tượng/Package] - System Analysis Report

## 1. Giới thiệu (Introduction)
- Mục đích của đối tượng/package này là gì?
- Thuộc phân hệ (Module) nào? Ngữ cảnh sử dụng (Business Context).

## 2. Thành phần cốt lõi (Core Components)
- Liệt kê các Tables, CDS Views, RAP Behavior, Classes, Interfaces chính yếu.
- Giải thích ngắn gọn vai trò của từng thành phần.

## 3. Mô hình Dữ liệu (Data Model)
- Phân tích chi tiết các bảng và CDS view.
- (Tùy chọn) Cung cấp sơ đồ Mermaid `mermaid erDiagram` để biểu diễn mối quan hệ (1-1, 1-n) giữa các Entity chính.

## 4. Luồng hoạt động & Chức năng (Functional & Control Flow)
- Giải thích luồng hoạt động chính (Ví dụ: Từ khi user trigger action đến khi ghi DB).
- Phân tích chi tiết logic code trong các method quan trọng.
- Xử lý lỗi (Error Handling) và Transaction control (nếu có).
- (Tùy chọn) Cung cấp sơ đồ Mermaid `mermaid sequenceDiagram` hoặc `mermaid flowchart` mô tả luồng gọi.

## 5. Tổng kết, Đánh giá & Đề xuất cải tiến (Conclusion & Recommendations)
- Đánh giá kiến trúc hiện tại (Độ phức tạp, có tuân thủ Clean Core và Best Practices không?).
- Phân tích rủi ro & Lỗi tiềm ẩn: Chỉ ra các đoạn code có nguy cơ gây lỗi (vd: không bắt try-catch, thiếu kiểm tra quyền, v.v.).
- Đề xuất tối ưu hiệu năng: Đưa ra góp ý chỉnh sửa để tối ưu hóa truy vấn DB (SQL), giảm thiểu vòng lặp, hoặc tăng cường khả năng chịu tải.
- Những điểm cần lưu ý khi bảo trì hoặc mở rộng (Extensibility) trong tương lai.

[OUTPUT FORMAT]
- Report status after completing Step 0, Step 1, and Step 2.
- Provide the clickable link to the generated Final Technical Report.
