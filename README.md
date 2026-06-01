# 🚀 SAP ABAP Cloud Agent Workspace

Chào mừng bạn đến với **SAP ABAP Cloud Agent Workspace**. Đây là môi trường làm việc thông minh được tối ưu hóa đặc biệt cho việc lập trình cặp (Pair-Programming) giữa bạn và AI Agent (Antigravity) nhằm phát triển các ứng dụng trên nền tảng **SAP BTP ABAP Environment** và **S/4HANA Cloud (Clean Core)**.

Không gian làm việc này tích hợp sẵn bộ quy tắc kiểm soát nghiêm ngặt, kho kỹ năng (Skills) chuyên sâu và quy trình tự động hóa (Workflows) để chuyển đổi tài liệu đặc tả nghiệp vụ (FS) thành mã nguồn ABAP RAP chất lượng cao, tuân thủ tuyệt đối chuẩn **Clean Core & Clean ABAP**.

---

## 📂 Cấu trúc Thư mục Workspace

Dự án được tổ chức khoa học với trọng tâm là thư mục cấu hình Agent `.agents/`:

```text
abap_workspaces/
├── .agents/                        # 🧠 Trung tâm điều phối trí tuệ nhân tạo (Agent Hub)
│   ├── SKILLS_ROUTER.md            # 🔀 Bộ điều hướng kỹ năng động của Agent
│   ├── rules/
│   │   └── sap-dev-rule.md         # 🛡️ Bộ quy tắc bắt buộc (Clean Core, Custom Only, TR...)
│   ├── skills/                     # 📚 Kho thư viện kỹ năng chuyên sâu của Agent
│   │   ├── Consultant/             # 🏛️ Nhóm kỹ năng Phân tích Nghiệp vụ & Kiến trúc
│   │   │   ├── fs-data-model-extractor/
│   │   │   ├── fs-fiori-ui-elements-mapper/
│   │   │   ├── fs-logic-behavior-translator/
│   │   │   └── fs-integration-api-analyzer/
│   │   ├── Developer/              # 💻 Nhóm kỹ năng Phát triển & Kỹ thuật ABAP Cloud
│   │   │   ├── abap/ , abap-cloud/ , clean-abap/ , naming-convension/ ...
│   │   │   └── rap/ , cds-view-entities/ , odata/ , authorization-iam/ ...
│   │   └── Productivity/           # 🚀 Nhóm kỹ năng Tối ưu Hiệu suất & Quản lý Ngữ cảnh
│   │       └── grill-me/ , caveman/ , handoff/ , scratchpad/
│   └── workflows/                  # ⚙️ Các kịch bản tự động hóa quy trình nghiệp vụ
│       ├── sap-dev-analytic-fs.md  # Quy trình phân tích FS sang Technical Spec
│       └── sap-dev-create-report.md# Quy trình tự động sinh báo cáo ABAP RAP
├── SAPER_2025_PM_FS_Sổ-chi-tiết-...docx # 📄 File tài liệu nghiệp vụ mẫu đầu vào (FS)
└── README.md                       # 📖 Tài liệu hướng dẫn sử dụng (File này)
```

---

## 🛠️ Các Thành phần Cốt lõi & Cách Hoạt động

### 1. Bộ điều hướng năng lực Agent (`SKILLS_ROUTER.md`)
Là danh bạ trung tâm quản lý toàn bộ các kỹ năng (Skills). Khi bạn giao nhiệm vụ, Agent sẽ tự động đối chiếu từ khóa trong yêu cầu của bạn với danh bạ này để nạp động (Dynamic Load) ngữ cảnh kỹ thuật cần thiết, tránh hiện tượng loãng ngữ cảnh (context bloat) và tối ưu hóa chi phí token.
* **Tối ưu ngữ cảnh:** Hệ thống hỗ trợ nạp song song các kỹ năng nhóm **Productivity** (ví dụ: `Scratchpad` để nháp trước khi code, `Handoff` để chuyển giao ngữ cảnh, `Grill Me` để phỏng vấn làm rõ yêu cầu) cùng với các kỹ năng kỹ thuật, giúp duy trì tư duy hệ thống mạch lạc.

### 2. Quy tắc phát triển tự động (`rules/sap-dev-rule.md`)
Quy tắc tự động chạy ngầm trong mỗi lượt tương tác. Nó ép buộc Agent luôn tuân thủ:
* **Clean Core:** Sử dụng CDS Views để đọc dữ liệu và EML (Entity Manipulation Language) để ghi dữ liệu. Tuyệt đối không can thiệp trực tiếp vào bảng vật lý.
* **Custom Only (Z/Y):** Chỉ thao tác trên các đối tượng tùy biến Z/Y của dự án. Không sửa đổi đối tượng tiêu chuẩn của SAP.
* **TR & Package:** Mọi đối tượng tạo mới/chỉnh sửa đều phải khai báo Package và Transport Request rõ ràng.

### 3. Kịch bản Tự động hóa (Workflows)
Sử dụng các Slash Command được thiết kế riêng cho các quy trình phức tạp:
* `/sap-dev-analytic-fs`: Tự động kích hoạt chuỗi kỹ năng Consultant để phân tích sâu file FS Word/PDF, bóc tách cấu trúc Data Model, bố cục Fiori Elements, logic tính toán số dư/fallback và xuất ra bản Technical Specification chuẩn chỉnh.
* `/sap-dev-create-report`: Nhận đầu vào là Technical Spec, tự động kích hoạt chuỗi kỹ năng Developer để viết mã sạch, tạo CDS View Entities, Access Controls (DCL), Business Service, RAP BO Behavior Pool và thực hiện kiểm thử tự động.

---

## 🚀 Hướng dẫn Bắt đầu Nhanh

### Bước 1: Chuẩn bị tài liệu đầu vào
Đảm bảo bạn đã đặt tài liệu Functional Specification (FS) vào thư mục gốc của workspace (ví dụ: file Word `.docx` hoặc Text hiện tại).

### Bước 2: Kích hoạt quy trình Phân tích FS
Hãy gửi yêu cầu phân tích cho Agent kèm đường dẫn tài liệu. 
* *Ví dụ:* `"Hãy kích hoạt workflow /sap-dev-analytic-fs để phân tích tài liệu FS [SAPER_2025_PM_FS_Sổ-chi-tiết-vật-liệu--sản-phẩm--hàng-hóa_V0_7---Copy.docx](./SAPER_2025_PM_FS_S%E1%BB%95-chi-ti%E1%BA%BFt-v%E1%BA%ADt-li%E1%BB%87u--s%E1%BA%A3n-ph%E1%BA%A9m--h%C3%A0ng-h%C3%B3a_V0_7---Copy.docx) thuộc Package Z_INVENTORY_REPORT"`

### Bước 3: Đánh giá Technical Spec & Sinh Code
Sau khi Agent phân tích xong và trả ra cấu trúc Technical Specification chuẩn, bạn hãy kiểm tra lại. Sau đó, kích hoạt tiếp lệnh `/sap-dev-create-report` để Agent tự động sinh code ABAP RAP toàn diện cho bạn.

---

## ⚙️ Lưu ý dành cho Lập trình viên
* **Đường dẫn tương đối:** Tất cả các tài liệu cấu hình trong dự án này đều sử dụng đường dẫn tương đối (Relative Paths) để bạn có thể mang workspace sang bất kỳ máy tính cá nhân hay môi trường Cloud nào mà không bị hỏng liên kết.
* **Kế thừa & Phát triển:** Bạn có thể dễ dàng bổ sung thêm các Kỹ năng mới vào thư mục `.agents/skills/` và khai báo chúng vào bảng đăng ký trong `SKILLS_ROUTER.md` để nâng cấp trí tuệ cho Agent của bạn.
