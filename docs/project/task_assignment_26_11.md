# Phân công nhóm H: bổ sung file còn thiếu (hạn 26/11/2026)

| | |
|---|---|
| Người giao | Chi |
| Ngày giao | 24/11/2026 |
| Hạn nộp | **26/11/2026** (riêng phần của Hà: **25/11/2026**) |
| Mẫu tham chiếu | Repo mẫu của thầy: [dbiz2-labdesk-example/docs](https://github.com/chienact-code/dbiz2-labdesk-example/tree/main/docs) |
| Theo dõi | Các việc này cũng được ghi ở [Pending tasks](decision_index.md#pending-tasks) |

Nhóm đã so thư mục của mình với repo mẫu của thầy. **Đợt 1** (file này): bổ sung các file và phần nội dung còn thiếu.
**Đợt 2** (làm sau, xem [cuối file](#đợt-2-làm-sau-chưa-có-hạn)): mỗi bạn check ngược lại các màn hình mình phụ trách.

## 0. Đọc trước khi làm

### Thư mục đã được sắp xếp lại theo mẫu của thầy (24/11/2026)

Thư mục `docs/` đã được đổi cho giống repo của thầy (quyết định D53 trong [decision_index.md](decision_index.md)).
Tên file **giữ nguyên**, chỉ đổi thư mục. **Trước khi làm, mọi người lấy bản mới nhất về (pull)**, nếu không sẽ bị
lệch thư mục.

| Thư mục cũ | Thư mục mới | Thư mục tương ứng của thầy | Chứa gì |
|---|---|---|---|
| `project_brief/` (một phần) | [project/](.) | `project/` | decision_index, project brief, file này |
| `project_brief/` (một phần) | [context/](../context/) | `context/` | CVCA, context diagram |
| `system_design/` + `system_design/sequence_diagram/` | [use_case/](../use_case/) | `use-case/` | use case diagram, 15 sequence diagram, sequence index |
| `system_design/` (một phần) | [architecture/](../architecture/) | `architecture/` + `architecture/adr/` | system architecture, các file ADR |
| `activity_diagram/` | [activity/](../activity/) | `activity/` | 15 activity diagram, activity index |
| `requirements/` + `project_brief/scope.md` | [function_list/](../function_list/) | `function-list/` | scope (W0), fr_list (W1, W4, W5 §4), cost |
| `external_design/` | [external_design/](../external_design/) (không đổi) | `external-design/` | screen list, transition, usage flow, UI conventions, screen spec, ảnh |

Thầy đặt tên bằng gạch ngang (`use-case`), nhóm mình giữ quy định **chữ thường, nối bằng gạch dưới** (`use_case`).

### Quy định chung

- File mới đặt **đúng thư mục** ghi trong từng việc. Tên file viết thường, nối bằng gạch dưới, không dấu, không cách.
- Nội dung tài liệu viết **tiếng Anh**; chữ trên màn hình (nếu có trích) giữ tiếng Việt có dấu.
- Nhắc tới file khác trong repo thì **gắn link tương đối** và bấm thử xem link có mở được không.
- Không sửa [cost.md](../function_list/cost.md). Nếu việc của mình làm đổi FR thì sửa thẳng trong
  [fr_list.md](../function_list/fr_list.md) và báo Chi.
- Làm xong: đẩy lên (commit + push hoặc mở pull request) rồi nhắn vào nhóm "đã xong + tên file".

## 1. Tổng quan phân công

| # | Người | Việc | Tạo mới / sửa | Đặt ở đâu | Hạn |
|---|---|---|---|---|---|
| 1 | Triệu | Project brief | **Tạo mới** `project_brief.md` | [docs/project/](.) | 26/11 |
| 2 | Linh | System architecture theo format của thầy | **Sửa** [system_architecture.md](../architecture/system_architecture.md) | [docs/architecture/](../architecture/) | 26/11 |
| 3 | Hà | Problems and opportunities + Stakeholder requirements | **Sửa** [cvca.md](../context/cvca.md) (thêm 2 mục) | [docs/context/](../context/) | **25/11** |
| 4 | Hoa | Các file quyết định kiến trúc (ADR) | **Tạo mới** thư mục `adr/` và các file `adr_00x_<tên>.md` | `docs/architecture/adr/` | 26/11 |
| 5 | Nhi | Business rules | **Sửa** [scope.md](../function_list/scope.md) (thêm 1 mục) | [docs/function_list/](../function_list/) | 26/11 |

Thứ tự phụ thuộc: **Hà (StR) → Linh (SyR trong architecture)**. Hoa đọc mục quyết định của architecture, nên Hoa và
Linh thống nhất danh sách ADR với nhau.

## 2. Chi tiết từng việc

### Việc 1. Triệu: Project brief

- **Tạo file:** `docs/project/project_brief.md`
- **Mẫu của thầy:** [project/project-brief.md](https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/project/project-brief.md)
- **Nội dung:** đoạn tóm tắt DBIZ1, theo đúng các mục của mẫu:
  1. Bảng thông tin: Product, Client (Thư viện Quốc gia Việt Nam), Client contact, Team, Course (DBIZ2, sau đó DBIZ3).
  2. **Problem**: vấn đề hiện tại của thư viện và bạn đọc.
  3. **Goal of the project**: mục tiêu; trỏ link sang [cvca.md](../context/cvca.md) (phần StR của Hà).
  4. **Team and roles**: thành viên, vai trò, phụ trách feature / màn hình nào.
  5. **Milestones in DBIZ2**: các mốc và khách hàng được xem gì ở mỗi mốc.
- Lấy thông tin từ [README.md](../../README.md), [scope.md](../function_list/scope.md), [cvca.md](../context/cvca.md).
- **Xong khi:** file có đủ 5 mục; tên sản phẩm, feature (F-01…F-04), tên người dùng (Reader, On-site Staff) viết
  giống hệt các tài liệu khác.

### Việc 2. Linh: Sửa system architecture theo format của thầy

- **Sửa file có sẵn:** [docs/architecture/system_architecture.md](../architecture/system_architecture.md) (giữ tên file).
- **Mẫu của thầy:** [architecture/architecture.md](https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/architecture/architecture.md)
- **Cấu trúc mới, theo đúng thứ tự của thầy:**
  1. **System requirements**: bảng `ID | System requirement | From`. ID dạng `SyR-01`. Cột **From** ghi StR nào
     (do Hà viết trong CVCA), tức là ghi rõ system requirement này xuất phát từ stakeholder nào.
  2. **Functional design**: chia các SyR thành các chức năng con. Bảng `Function | Serves` (phục vụ SyR nào).
  3. **Physical design**: sơ đồ Mermaid 3 tầng (Presentation, Business, Data access) và các hệ thống bên ngoài, kèm
     bảng `Function | Element | Layer`.
  4. **Decisions**: bảng `ADR | Decision | Status`, mỗi dòng link sang file ADR của Hoa.
  5. **Change log**: `Version | When | Change | Why`.
- Nội dung đang có (thành phần, kho dữ liệu, kết nối ngoài, bảo mật, phần "Not decided here") **không bỏ đi**: sắp xếp
  lại vào các mục trên, hoặc giữ thành mục phụ phía sau.
- Bảng thông tin đầu file thêm dòng **Inputs**: link tới [cvca.md](../context/cvca.md),
  [context_diagram.md](../context/context_diagram.md), [use_case.md](../use_case/use_case.md).
- **Xong khi:** mỗi SyR có ít nhất một StR ở cột From; mỗi function phục vụ ít nhất một SyR; mỗi function nằm ở một
  element và một tầng.

### Việc 3. Hà: Thêm stakeholder requirements vào CVCA (hạn 25/11)

- **Sửa file có sẵn:** [docs/context/cvca.md](../context/cvca.md). Thêm 2 mục mới **sau** mục
  "2. Actors and what each one gets" (mục "Notes on the redraw" dời xuống cuối).
- **Mẫu của thầy:** [context/cvca.md](https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/context/cvca.md),
  mục 2 và 3.
- **Mục "Problems and opportunities":** bảng `# | Stakeholder | Problem or opportunity`, ID dạng `P-1, P-2…`.
  Stakeholder lấy từ CVCA: Readers, On-site Staff, National Library of Vietnam, Ministry…
- **Mục "Stakeholder requirements":** bảng `ID | Stakeholder requirement | From`, ID dạng `StR-01…`. Viết theo câu
  "*<Stakeholder> shall be able to …*". Cột From ghi P nào.
- **Xong khi:** mỗi P có ít nhất một StR; các tính năng F-01…F-04 trong [scope.md](../function_list/scope.md) đều có
  StR đứng sau. Báo Linh ngay khi xong để Linh làm cột From.

### Việc 4. Hoa: Các file quyết định kiến trúc (ADR)

- **Tạo thư mục mới:** `docs/architecture/adr/`, mỗi quyết định **một file**: `adr_001_<tên_ngắn>.md`,
  `adr_002_<tên_ngắn>.md`… (ví dụ `adr_001_one_web_app.md`).
- **Mẫu của thầy:** [architecture/adr/](https://github.com/chienact-code/dbiz2-labdesk-example/tree/main/docs/architecture/adr),
  ví dụ [ADR-001](https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/architecture/adr/ADR-001-one-web-app.md).
- **Mỗi file gồm:** tiêu đề `# ADR-001: <tên>`, bảng `Status | Date`, rồi 3 đoạn **Context**, **Decision**,
  **Consequences**.
- **Lấy quyết định từ đâu:** mục 8 của [system_architecture.md](../architecture/system_architecture.md#8-decisions-this-architecture-follows)
  và các dòng D tương ứng trong [decision_index.md](decision_index.md). Gợi ý: gửi OTP bằng chính hệ thống, không dùng
  dịch vụ email bên ngoài (AD-UC-11 Q2); phiên nhân viên không hết hạn (D7); một mã QR cho mỗi đầu sách (D40); khung
  màn hình bạn đọc 360px, nhân viên 1280px (D44, D45); đồng bộ dữ liệu hằng ngày theo giờ (D48); một web app chung
  cho bạn đọc và nhân viên.
- Mỗi ADR ghi rõ nó dựa trên dòng D nào. **Không** tạo quyết định mới mà nhóm chưa chốt.
- **Xong khi:** mỗi quyết định ở mục 8 của architecture có một file ADR; gửi danh sách cho Linh để đưa vào bảng
  Decisions.

### Việc 5. Nhi: Business rules

- **Sửa file có sẵn:** [docs/function_list/scope.md](../function_list/scope.md). Thêm mục **"Business rules"** ở cuối
  file, sau "Table 4: Data functions".
- **Mẫu của thầy:** [function-list/w0-scope.md](https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/function-list/w0-scope.md),
  mục "Business rules".
- **Định dạng:** bảng `BR | Rule | Source`, ID dạng `BR-01…`. Mỗi quy tắc là một câu ngắn, cột Source ghi FR hoặc
  quyết định (D…).
- **Lấy quy tắc từ:** [fr_list.md](../function_list/fr_list.md) và [decision_index.md](decision_index.md). Ví dụ:
  không báo cáo đánh giá của chính mình (FR-02-24, D39); không báo cáo trùng (FR-02-21); nhập sai OTP 5 lần thì mã hết
  hiệu lực (FR-04-17); một mã QR cho mỗi đầu sách (D40); sách chỉ có bản điện tử thì không có mã QR; không lưu một sách
  hai lần (FR-03-24)…
- **Xong khi:** mỗi quy tắc có nguồn; không có quy tắc nào mâu thuẫn với FR.

## Đợt 2 (làm sau, chưa có hạn)

Sau khi xong đợt 1, Hà, Hoa, Nhi, Triệu check lại các màn hình mình làm từ trước:

1. Wireframe và mockup đã đúng [ui_conventions.md](../external_design/ui_conventions.md) hiện tại chưa.
2. Ảnh `*_numbered.png` có thành phần nào chưa được đánh số không; số trên ảnh có khớp mục 3 *Element inventory* của
   spec không. Thiếu thì tự thêm vào ảnh của mình.
3. Câu hỏi trong mục *Open questions* của spec đã được giải quyết hết chưa.
4. Truy ngược: activity diagram, sequence diagram và [fr_list.md](../function_list/fr_list.md) của các use case dùng
   màn hình đó đã đúng với màn hình chưa.

| Người | Màn hình / modal | Use case cần đối chiếu |
|---|---|---|
| Hà | S-F00-01, S-F00-02, S-F02-03, M-F00-01, M-F02-03-01, S-F00-03, S-F04-01 | UC-10, UC-11, phần đăng nhập nhân viên của UC-13 |
| Hoa | S-F02-01, S-F02-02, S-F02-04, M-F02-01-01, M-F02-01-02, M-F02-04-01 | UC-04, 05, 06, 13, 14 |
| Nhi | S-F01-01, S-F01-02, S-F03-03, S-F03-01 | UC-01, 02, 03, 12 |
| Triệu | S-F03-02, S-F03-06, S-F03-07 | UC-07, 08, 09 |

Spec ở [screens/specs/](../external_design/screens/specs/), ảnh ở [screens/img/](../external_design/screens/img/),
activity diagram ở [activity/](../activity/), sequence diagram ở [use_case/](../use_case/).
