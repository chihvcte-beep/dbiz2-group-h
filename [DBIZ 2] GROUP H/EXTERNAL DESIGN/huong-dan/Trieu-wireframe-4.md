# Hướng dẫn Lesson 8 — Wireframe và Screen Spec, phần 4: Đọc cá nhân và AI

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Trieu** |
| Vai trò | Wireframe 4 (Trieu) — Đọc cá nhân và AI |
| Nhóm / sản phẩm | Group H · Group H Library Core System |
| Phiên bản hướng dẫn | v1.0 · 12/11/2026 |
| Hạn viết xong phần chữ (bước 1–2) | **14/11/2026** — cùng ngày Linh nộp UI Conventions, để bắt đầu vẽ ảnh ngay |
| Hạn nộp ảnh + Screen Spec hoàn chỉnh | **17/11/2026** |

> **Tệp này viết cho hai người đọc: bạn và trợ lý AI bạn dùng.**
> Khi làm việc với AI (ChatGPT, Claude, Gemini…), hãy đính kèm tệp này cùng các tệp đầu vào ở
> mục 3 và mở đầu bằng câu: *"Đọc hết tệp hướng dẫn này trước. Làm đúng theo nó. Chỗ nào thiếu
> thông tin thì hỏi tôi hoặc ghi [NEEDS CLARIFICATION], không tự đoán."*
> Các tệp kết quả viết bằng **tiếng Anh** (giống toàn bộ tài liệu của nhóm); phần hướng dẫn này
> viết bằng tiếng Việt.

---

## 1. Bối cảnh (đọc 2 phút)

**Sản phẩm.** Group H Library Core System là phần **gắn thêm vào OPAC hiện có** của thư viện. Các
trang OPAC cũ (danh mục và kết quả tìm kiếm, Book Detail, menu chính, khu vực cá nhân, trang đọc
sách online) **không phải màn hình của sản phẩm** — chúng chỉ là điểm vào và điểm ra, **không vẽ**.
Sản phẩm có **15 màn hình** và **5 modal**, phục vụ 2 tác nhân: **Reader** (điện thoại hoặc máy
tính) và **On-site Staff** (máy tính của thư viện).

**Lesson 8 gồm những gì.** Nhóm đã xong `usage-flow.md`, `screen-list.md`, `screen-transition.md`.
Phần còn lại: `ui-conventions.md` (Linh làm gốc) và **một Screen Spec + bộ ảnh wireframe cho
từng màn hình** (4 bạn, trong đó có bạn). Sang DBIZ3, AI lập trình sẽ đọc đúng các Screen Spec này để
dựng màn hình — viết sai hay thiếu ở đây là sai ở sản phẩm.

**Chia việc trong nhóm.**

| Người | Phần việc | Màn hình / modal |
|---|---|---|
| UI Conventions (Linh) | Bộ quy ước gốc: màu, chữ, tên thành phần, thông báo, khung HTML dùng chung; soát nhất quán cuối cùng | (tất cả, ở mức quy ước) |
| Wireframe 1 (Ha) | Đăng nhập và trang nhân viên | S-F00-01, S-F00-02, S-F00-03, S-F04-01, S-F02-03 · M-F00-01, M-F02-03-01 |
| Wireframe 2 (Nhi) | Tìm sách và vị trí trong thư viện | S-F01-01, S-F01-02, S-F03-01, S-F03-03 |
| Wireframe 3 (Hoa) | Đánh giá sách (review) | S-F02-01, S-F02-02, S-F02-04 · M-F02-01-01, M-F02-01-02, M-F02-04-01 |
| Wireframe 4 (Trieu) | Đọc cá nhân và AI | S-F03-02, S-F03-06, S-F03-07 |

**Bạn là Wireframe 4 (Trieu).**

---

## 2. Phần việc của bạn: Đọc cá nhân và AI

**Tóm tắt.** Bạn làm **3 màn hình** của bạn đọc đã đăng nhập: lịch sử đọc và sở thích, tìm sách bằng
chatbot AI, và gợi ý sách. Cả 3 đều cần đăng nhập, nên đều dùng modal M-F00-01 của Wireframe 1 (Ha).

| Thứ tự làm | ID | Tên | Actor | Khổ | Priority | AD liên quan |
|---|---|---|---|---|---|---|
| 1 | S-F03-02 | Reading history and preferences | Reader | 360px | Should | AD-UC-07 |
| 2 | S-F03-07 | Book recommendations | Reader | 360px | Could | AD-UC-09 |
| 3 | S-F03-06 | AI chatbot book search | Reader | 360px | Could | AD-UC-08 |

### 2.1 S-F03-02 Reading history and preferences

- **Mở từ:** khu vực cá nhân OPAC "Reading history"; lời mời "Set your preferences" ở S-F03-07.
  Chưa đăng nhập → M-F00-01 (AD-UC-07 d1).
- **Hành động:** xem lịch sử kèm trạng thái (FR-03-01); cập nhật **trạng thái + tiến độ** của một
  sách (r2): trạng thái chỉ **Reading** hoặc **Finished**, tiến độ **0–100 %** (FR-03-04); cập nhật
  **sở thích đọc** (r3, phần Could): chọn **chủ đề** có trong danh sách chủ đề của danh mục (AD-UC-07
  câu hỏi 3); Back → nơi đã mở (khu vực cá nhân, hoặc S-F03-07).
- **Trạng thái:**
  - Error: trạng thái/tiến độ/sở thích không hợp lệ → từ chối, **giữ nguyên dữ liệu đã lưu**, báo lỗi
    (FR-03-22) — mẫu: nhập 120 % khi đang 20 % (AD-UC-07 mục 3);
  - Success: hiện lịch sử/sở thích đã cập nhật (FR-03-01, FR-03-05);
  - Empty: lịch sử trống — **không có FR riêng**; mô tả trạng thái này theo mẫu "Empty state" của
    `ui-conventions.md` và ghi câu hỏi mở để nhóm xác nhận câu chữ.
- **Đã chốt:** mục tự thêm (từ sách mượn hoặc sách online đã mở) có trạng thái Reading, 0 %
  (AD-UC-07 câu hỏi 1); được đánh dấu Finished khi tiến độ dưới 100 % (câu hỏi 4); mượn lại cùng sách
  thì có thêm một dòng (câu hỏi 2).
- **Lưu ý:** mục lịch sử được thêm **ngầm** (đồng bộ mượn sách, mở sách online) — không có nút
  "thêm vào lịch sử".

### 2.2 S-F03-07 Book recommendations

- **Mở từ:** menu OPAC "Recommended for you". Chưa đăng nhập → M-F00-01 với **biến thể câu chữ cho
  gợi ý sách** (FR-03-21).
- **Nội dung:** danh sách **10 sách** gợi ý (AD-UC-09 câu hỏi 3), mỗi sách là một Book row.
- **Trạng thái / biến thể nội dung:**
  - bạn đọc chưa có dữ liệu → danh sách **sách phổ biến** + lời mời **"Set your reading
    preferences"** → S-F03-02 (FR-03-19);
  - tính ra dưới 3 sách → **bổ sung sách đang được mượn nhiều** cùng chủ đề (FR-03-20; "trending" =
    mượn nhiều nhất cùng chủ đề trong 30 ngày, AD-UC-09 câu hỏi 2);
  - Loading, Error (câu chữ chung).
- **Hành động:** mở một sách → OPAC Book Detail → S-F01-01 (c2); cập nhật sở thích → S-F03-02 (c3);
  Back → menu OPAC.
- **Câu hỏi mở gợi ý:** có gắn nhãn cho sách "trending" được bổ sung không, và có giải thích "vì sao
  gợi ý sách này" không — FR không yêu cầu, **không vẽ** nếu nhóm chưa chốt.

### 2.3 S-F03-06 AI chatbot book search

- **Mở từ:** menu OPAC "Ask the library chatbot". Màn hình **mở được khi chưa đăng nhập**; chỉ khi
  bạn đọc **gửi tin nhắn đầu tiên** mới hỏi đăng nhập (L8-05) → M-F00-01 với **biến thể câu chữ cho
  chatbot** (FR-03-18).
- **Hành động:** gửi câu hỏi (AD-UC-08 r1); nhận trả lời kèm **thẻ sách** (FR-03-09); mở một thẻ
  sách → OPAC Book Detail (c2); khi AI lỗi → liên kết "use the format filter" → S-F03-01 (c3);
  Back → menu OPAC.
- **Trạng thái:**
  - Default trước khi gửi: khung chat trống + ô nhập (đây là Empty của màn hình);
  - Loading: đang chờ trả lời (tối đa **10 giây**, AD-UC-08 câu hỏi 1);
  - không tìm thấy sách → câu trả lời giải thích và gợi ý từ khoá/chủ đề khác (FR-03-16) — đây là
    một tin nhắn của chatbot, không phải banner lỗi;
  - Error: "AI search is temporarily unavailable, use the format filter" + liên kết S-F03-01
    (FR-03-17); thông báo này **không** được lưu vào lịch sử hội thoại (AD-UC-08 câu hỏi 2).
- **Đã chốt:** không có chức năng xoá hội thoại (AD-UC-08 câu hỏi 3).
- **Không vẽ:** widget chatbot nổi trên các trang OPAC, "Reader Dashboard" (screen-list), gửi
  ảnh/giọng nói, đánh giá câu trả lời.
- **Câu hỏi mở gợi ý:** khi mở lại màn hình, có hiện lại hội thoại cũ không? FR-03-10 chỉ nói lưu,
  không nói hiển thị lại.

### 2.4 Phối hợp

- Nhận ảnh và **cả 3 biến thể câu chữ** của **M-F00-01** từ Wireframe 1 (bạn dùng 2 biến thể riêng).
- Dùng **Book row**, **Book card**, **Format label** giống cách Wireframe 2 (Nhi) vẽ ở S-F03-01; hỏi
  Wireframe 2 (Nhi) trước khi vẽ.
- S-F03-02 là đích của lời mời ở S-F03-07 và nơi bạn đọc quay về sau khi đăng nhập — kiểm tra
  "Goes to" khớp `screen-transition.md`.
- Soát chéo với **Wireframe 2 (Nhi)**.

---

## 3. Tệp đầu vào (đọc trước, đính kèm cho AI)

| # | Tệp | Lấy gì từ đó |
|---|---|---|
| 1 | `EXTERNAL DESIGN/screen-list.md` | Dòng của màn hình bạn (mục đích, điểm vào, UC/FR, priority); bảng "Modals and overlays"; bảng **"What is deliberately not a screen"** (các thông báo = trạng thái của màn hình bạn); bảng **"Activity diagram actions mapped to screens"** (mọi hành động người dùng làm trên màn hình bạn) |
| 2 | `EXTERNAL DESIGN/screen-transition.md` | Các mũi tên đi ra/đi vào màn hình bạn → cột "Goes to screen" ở mục 5 của Screen Spec |
| 3 | `EXTERNAL DESIGN/usage-flow.md` | Màn hình bạn nằm ở bước nào trong luồng của người dùng |
| 4 | Các AD ở mục 2 của tệp này (`ACTIVITY DIAGRAM/AD-UC-xx.md`) | Mục 2 Node trace (hành động + FR), mục 3 Branches (= các trạng thái và dữ liệu mẫu), mục 5 Screens touched, mục 6 Open questions |
| 5 | `ACTIVITY DIAGRAM/activity-index.md`, bảng câu hỏi `L8-xx` | Các quyết định Lesson 8 đã chốt về màn hình |
| 6 | `GROUP-H_UC_FR_COST.xlsx` — sheet **W1_FunctionList** (câu EARS của FR), **W4_Prioritization** (priority hiệu lực), **W0_Scope** Table 3 (Won't-have) và Table 4 (nhóm dữ liệu) | Nội dung FR, giới hạn dữ liệu, những gì KHÔNG được vẽ |
| 7 | `1793594740300_external-design-templates/templates/screen-spec-template.md` | Khung Screen Spec bắt buộc |
| 8 | Mẫu Screen Spec của giáo viên: https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/external-design/screens/screen-spec-S-F01-02.md | Cách viết đầy đủ: một ảnh cho mỗi trạng thái, ảnh đánh số khớp Element inventory |
| 9 | Từ Linh (UI Conventions): `EXTERNAL DESIGN/ui-conventions.md`, `screens/src/tokens.css`, `screens/src/_template.html`, `screens/src/components.html` | Màu, chữ, khoảng cách, tên thành phần, mẫu câu thông báo, khung HTML. **Chưa có bản v0.1 thì chưa vẽ ảnh** (làm trước bước 1–2) |

**Mẹo cho AI không đọc được tệp Excel:** mở sheet W1, sao chép các hàng FR có trong mục 2 của tệp
này (cột mã FR, tên, câu EARS) dán vào khung chat dưới dạng văn bản.

---

## 4. Kết quả phải nộp

```text
[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/
  screen-spec-<Screen ID>.md          một tệp cho mỗi màn hình của bạn
  modal-<Modal ID>.md                 một tệp cho mỗi modal của bạn (nếu có)
  src/<Screen ID>.html                mã nguồn wireframe (sao chép từ _template.html)
  src/<Modal ID>.html
  img/<Screen ID>.png                 trạng thái Default
  img/<Screen ID>-numbered.png        Default có vòng tròn số
  img/<Screen ID>-empty.png           mỗi trạng thái có hình thì một ảnh
  img/<Screen ID>-loading.png
  img/<Screen ID>-error.png           nhiều lỗi: -error-2.png, -error-3.png …
  img/<Screen ID>-success.png
  img/<Screen ID>-error-numbered.png  khi trạng thái lỗi có thành phần không có ở Default
  img/<Modal ID>.png
```

- Trạng thái **không áp dụng** cho màn hình (ví dụ màn hình không bao giờ trống) thì **không vẽ
  ảnh**, nhưng phải ghi "Not applicable: <lý do>" ở mục 4 của Screen Spec.
- Một trạng thái có nhiều biến thể lỗi: vẽ ít nhất biến thể quan trọng nhất; các biến thể khác
  vẽ thêm nếu bố cục khác đi, nếu chỉ khác câu chữ thì mô tả ở mục 4 (như mẫu giáo viên).

**Quy ước riêng của nhóm cho modal** (mẫu giáo viên không có modal): mỗi modal có tệp
`modal-<Modal ID>.md` gồm bảng đầu tệp (Modal ID, tên, mở từ màn hình nào, actor, FR, AD, ảnh),
rồi 4 mục: **1. Purpose**, **2. Mockup**, **3. Element inventory**, **4. Interactions**
(Element | User action | System response | Goes to). Screen Spec của màn hình mở modal ghi Modal ID
ở cột "Goes to screen" của mục 5.

---

## 5. Các bước làm

### Bước 1 — Lập bảng hành động và bảng trạng thái cho từng màn hình (chưa vẽ gì)

Với **mỗi** màn hình của bạn:

1. Trong `screen-list.md`, bảng "Activity diagram actions mapped to screens": lọc mọi dòng có
   Screen ID của bạn → đây là danh sách **hành động** bắt buộc phải có trên màn hình (mỗi dòng ít
   nhất một dòng ở mục 5 Interactions).
2. Trong bảng "What is deliberately not a screen": lọc mọi dòng nhắc Screen ID của bạn → đây là
   danh sách **trạng thái và thông báo** (mỗi dòng phải xuất hiện ở mục 4 States).
3. Trong `screen-transition.md`: lọc mọi mũi tên đi ra từ màn hình bạn → cột "Goes to screen".
4. Đối chiếu với mục 3 "Branches and acceptance tests" của các AD liên quan: mỗi nhánh mà người
   dùng nhìn thấy kết quả trên màn hình bạn phải khớp một trạng thái.

### Bước 2 — Viết phần chữ của Screen Spec

Tạo `screens/screen-spec-<Screen ID>.md` từ template. Viết **trước khi vẽ**: bảng đầu tệp, mục 1,
3, 4, 5, 6, 7, 9. Mục 2 và 8 để sau.

- **Bảng đầu tệp**: lấy Actor, Priority, Feature, UC/FR từ dòng của `screen-list.md`. Thêm dòng
  "Frame width": 360px (Reader) hoặc 1280px (Staff) — theo `ui-conventions.md`. Dòng "Figma
  frame": "not used (drawn as an HTML wireframe)". Status: Draft.
- **Mục 1 Purpose**: "Shown when" và "The user leaves this screen when" — viết lại ngắn từ cột
  "Shown when" và từ `screen-transition.md`.
- **Mục 3 Element inventory**: đi từ trên xuống dưới, trái sang phải. Mỗi thứ người dùng nhìn
  thấy hoặc bấm được là một dòng. Cột **Element** = tên ổn định bằng tiếng Anh (AI lập trình sẽ
  dùng làm tên component). Cột **Type** = đúng tên thành phần ở mục 3 của `ui-conventions.md`.
  Cột **Content / data source** = chữ cố định, hoặc trường dữ liệu theo bảng ở mục 9 của tệp này,
  kèm FR. Cột **Validation** = luật, hoặc "none".
- **Mục 4 States**: đủ 5 dòng Default, Empty, Loading, Error, Success. Mỗi trạng thái ghi FR gây
  ra nó. Câu chữ thông báo viết theo **mẫu câu ở mục 4 của `ui-conventions.md`**; câu dùng chung
  (modal đăng nhập, "Shelf location unavailable…") chép đúng nguyên văn từ đó.
- **Mục 5 Interactions**: mỗi hành động từ bước 1 là ít nhất một dòng; "Goes to screen" chỉ được
  là Screen ID / Modal ID có trong `screen-list.md`, "stays", hoặc tên trang OPAC hiện có
  (ví dụ "Existing OPAC Book Detail (exit)").
- **Mục 6 Screen-level rules**: luật `SR-001`, `SR-002`… lấy từ FR (giới hạn, điều kiện hiển thị),
  từ quyết định `L8-xx`, và từ `ui-conventions.md` mục 5 (không chỉ dùng màu…).
- **Mục 7 Linked requirements**: mọi FR ở dòng của màn hình trong `screen-list.md`, mỗi FR một câu
  "màn hình này làm gì cho FR đó".
- **Mục 9 Open questions**: các câu hỏi ở mục 2 của tệp này, cộng với câu hỏi bạn phát hiện thêm.

### Bước 3 — Nhận bộ quy ước UI

Kiểm tra đã có `ui-conventions.md` v0.1 và 3 tệp trong `screens/src/`. Ghi phiên bản đang dùng
vào bảng đầu Screen Spec (dòng "UI conventions version"). Sửa lại cột Type ở mục 3 cho khớp tên
thành phần chính thức.

### Bước 4 — Vẽ wireframe bằng HTML với AI

1. Sao chép `screens/src/_template.html` thành `screens/src/<Screen ID>.html`.
2. Dùng **Lời nhắc B** ở mục 7. AI phải:
   - chỉ dùng biến trong `tokens.css` và lớp thành phần có sẵn; không tự đặt màu mới;
   - vẽ **đúng và đủ** các dòng ở mục 3 Element inventory — không thêm, không bớt;
   - vẽ mỗi trạng thái ở mục 4 trong một khối `<section data-state="...">`;
   - gắn vòng tròn số `<span class="num">#</span>` vào từng thành phần, số = cột `#` ở mục 3;
   - dùng **dữ liệu mẫu chung** ở mục 9 của tệp này và dữ liệu trong mục 3 của các AD;
   - không vẽ trang OPAC cũ, không vẽ logo/tên thư viện thật, không dùng ảnh bìa sách thật
     (dùng khối xám ghi "Cover").
3. Mở tệp bằng Chrome để xem: `<Screen ID>.html#default`, `#empty`, `#error`… Sửa đến khi đúng.

### Bước 5 — Xuất ảnh PNG bằng Chrome

1. Mở `src/<Screen ID>.html#default` trong Chrome, nhấn **F12**, rồi **Ctrl + Shift + M** (thanh
   giả lập thiết bị).
2. Chọn **Dimensions: Responsive**. Màn hình Reader: rộng **360**, DPR **3**. Màn hình Staff:
   rộng **1280**, DPR **1**. (Không thấy ô DPR: bấm dấu ⋮ trên thanh giả lập → "Add device pixel
   ratio".)
3. Bấm ⋮ trên thanh giả lập → **Capture full size screenshot**.
4. Đổi tên tệp tải về thành `<Screen ID>.png`, chép vào `screens/img/`. Kiểm tra ảnh rộng đúng
   1080px (Reader) hoặc 1280px (Staff).
5. Lặp lại với `#empty`, `#loading`, `#error`, `#success` → `<Screen ID>-<state>.png`.

### Bước 6 — Ảnh đánh số

Mở `#default-numbered`, chụp thành `<Screen ID>-numbered.png`. Mọi dòng ở mục 3 phải có số trên
ảnh. Thành phần chỉ xuất hiện ở trạng thái khác (ví dụ Message area chỉ có khi lỗi) → chụp thêm
`#error-numbered` thành `<Screen ID>-error-numbered.png` và ghi chú như mẫu giáo viên.

### Bước 7 — Hoàn thiện Screen Spec

- **Mục 2 Mockup**: ảnh Default, bảng ảnh đánh số, bảng "State | Image" như mẫu giáo viên, câu
  "All colours, fonts and corners come from the design tokens in ui-conventions.md".
- **Mục 8 Responsive and accessibility**: khổ nhỏ nhất, cái gì xếp chồng khi màn hình hẹp, thông
  tin nào không chỉ dùng màu, cỡ chữ.
- **Checklist cuối Screen Spec**: chỉ đánh dấu [x] khi đã thật sự kiểm tra; ghi ngắn bằng chứng.
- Đổi Status thành "Reviewed" sau khi qua bước 8.

### Bước 8 — Tự soát, soát chéo, gửi soát nhất quán

1. Dùng **Lời nhắc C** ở mục 7 để AI soát bài của chính bạn. Sửa hết lỗi.
2. **Soát chéo**: Wireframe 1 (Ha) ↔ Wireframe 3 (Hoa), Wireframe 2 (Nhi) ↔ Wireframe 4 (Trieu). Người soát kiểm tra
   checklist ở mục 8 và ghi nhận xét cho người kia (không sửa hộ).
3. Báo Linh (UI Conventions) để soát màu/thành phần/thông báo (cổng cuối).

### Bước 9 — Đưa lên Git

Làm như nhóm đang làm: tạo nhánh riêng của bạn, commit các tệp ở mục 4, mở pull request vào
`main`. **Chỉ commit tệp của bạn.** Thấy cần sửa `screen-list.md`, `screen-transition.md`, AD,
W1 hay `ui-conventions.md` → không tự sửa; ghi vào mục 9 Open questions và nhắn nhóm/người phụ
trách.

---

## 6. Quy tắc bắt buộc (cho cả bạn và AI)

1. **Tài liệu của nhóm là nguồn sự thật, không phải hiểu biết chung của AI.** Điều gì không có
   trong tài liệu là chưa được quyết định.
2. **Mỗi thứ trên màn hình phải phục vụ một FR.** Không vẽ nút, ô, menu, biểu tượng "cho đẹp" hay
   "thường thấy". Ví dụ AI hay tự thêm: thanh tìm kiếm, ngôi sao đánh giá, nút like, nút chia sẻ,
   ảnh đại diện, chuông thông báo, menu hamburger, nút đăng xuất, "Forgot password", đổi ngôn ngữ,
   widget chatbot nổi. Thấy thì xoá; nếu nghĩ thật sự cần thì ghi Open question.
3. **Không vẽ thứ trong W0 Table 3 (Won't-have)**: tìm kiếm từ khoá, đánh giá like/dislike, đăng ký
   tài khoản online, đăng nhập Google, liên kết tài khoản online với thẻ, trình đọc sách online,
   tải PDF, định dạng truy cập trên trang Book Detail, danh sách sách trong phòng, tình trạng còn
   sách, lọc theo trạng thái bộ sưu tập, màn hình sửa sơ đồ tầng, khu quản trị đầy đủ, mượn/trả,
   bảng báo cáo review cho nhân viên.
4. **Thông báo lỗi / trống / thành công là TRẠNG THÁI của màn hình**, không phải màn hình mới, không
   phải modal mới.
5. **Chỉ dùng 5 modal đã có** trong `screen-list.md`. Không tạo modal mới.
6. **Gọi theo mã, không kể lại.** Viết `FR-02-01`, `S-F01-02`, `L8-07`; không chép lại câu FR.
7. **Không bịa mã.** Không tạo Screen ID, Modal ID, FR mới. Luật màn hình `SR-nnn` thì đánh số
   riêng trong từng Screen Spec.
8. **Thiếu thì hỏi.** Ghi `[NEEDS CLARIFICATION: <câu hỏi>]` ở mục 9, kèm "Blocking? Yes/No" và
   giá trị mặc định bạn tạm dùng. Không ghi phỏng đoán như thể đã quyết định.
9. **Màu, chữ, khoảng cách, góc bo, khổ khung chỉ lấy từ `ui-conventions.md` mục 6** (qua
   `tokens.css`). Tên thành phần chỉ lấy từ mục 3.
10. **Không sửa ảnh bằng tay** (Paint, Photoshop). Đổi gì thì sửa HTML rồi chụp lại.
11. AI phải **báo cáo cuối việc**: đã tạo/sửa tệp nào, còn câu hỏi nào mở, điểm nào chưa kiểm tra.

---

## 7. Lời nhắc mẫu để dán cho AI

Thay `<Screen ID>` bằng màn hình đang làm. Làm **từng màn hình một**, không gộp nhiều màn hình
vào một lần hỏi.

### Lời nhắc A — Viết phần chữ của Screen Spec

```text
Bạn là chuyên viên phân tích nghiệp vụ cho dự án sinh viên "Group H Library Core System".
Tôi đính kèm: tệp hướng dẫn này, screen-spec-template.md, Screen Spec mẫu S-F01-02 của giáo viên,
screen-list.md, screen-transition.md, activity-index.md, các AD: <liệt kê>, và các FR sau: <dán FR>.

Hãy viết EXTERNAL DESIGN/screens/screen-spec-<Screen ID>.md bằng tiếng Anh, theo đúng template:
bảng đầu tệp, mục 1, 3, 4, 5, 6, 7, 9 (mục 2 và 8 để trống, ghi "to be completed after drawing").
Làm theo bước 1 và bước 2 của tệp hướng dẫn. Trước khi viết, liệt kê cho tôi:
(a) mọi hành động của người dùng trên màn hình này (từ bảng "Activity diagram actions mapped to
screens"), (b) mọi trạng thái/thông báo (từ bảng "What is deliberately not a screen"),
(c) mọi mũi tên đi ra (từ screen-transition.md). Sau khi viết, chứng minh mỗi mục (a) có một dòng ở
mục 5, mỗi mục (b) có ở mục 4, mỗi mục (c) có ở cột "Goes to screen".
Không thêm thành phần nào không phục vụ FR. Chỗ nào chưa rõ, ghi [NEEDS CLARIFICATION] ở mục 9.
```

### Lời nhắc B — Vẽ wireframe HTML

```text
Tôi đính kèm: tệp hướng dẫn này, ui-conventions.md (phiên bản <v>), tokens.css, _template.html,
components.html và screen-spec-<Screen ID>.md.

Hãy tạo EXTERNAL DESIGN/screens/src/<Screen ID>.html bằng cách sao chép _template.html, rồi vẽ:
- đúng và đủ các dòng của mục 3 Element inventory, theo thứ tự trên xuống dưới;
- mỗi trạng thái ở mục 4 là một <section data-state="...">;
- vòng tròn số <span class="num">#</span> trên mỗi thành phần, số = cột # của mục 3;
- chỉ dùng biến và lớp trong tokens.css, không viết màu trực tiếp;
- khổ <360px Reader | 1280px Staff>; dữ liệu mẫu theo mục 9 của tệp hướng dẫn.
Không thêm bất kỳ thành phần nào không có trong mục 3. Không dùng thư viện JavaScript ngoài.
Cuối cùng, lập bảng đối chiếu: # | Element | có trên HTML không | ở trạng thái nào.
```

### Lời nhắc C — Tự soát trước khi nộp

```text
Đây là bài của tôi cho <Screen ID>: Screen Spec, tệp HTML và danh sách ảnh trong img/.
Hãy soát theo checklist ở mục 8 của tệp hướng dẫn và checklist cuối template, rồi trả về bảng:
Mục kiểm tra | Pass/Fail | Bằng chứng hoặc chỗ sai | Cách sửa.
Kiểm tra thêm: (1) mọi "Goes to screen" có trong screen-list.md; (2) mọi FR ở mục 7 có trong dòng
của màn hình trong screen-list.md và ngược lại; (3) không có thành phần nào thuộc W0 Table 3;
(4) mọi màu trong HTML là biến của tokens.css. Không tự sửa tệp, chỉ báo cáo.
```

---

## 8. Checklist trước khi nộp (cho mỗi màn hình / modal)

- [ ] Screen Spec theo đúng template; bảng đầu tệp có Frame width và phiên bản UI conventions.
- [ ] Mọi hành động trong bảng "Activity diagram actions mapped to screens" của màn hình này có ít
      nhất một dòng ở mục 5.
- [ ] Mọi thông báo trong bảng "What is deliberately not a screen" của màn hình này có ở mục 4.
- [ ] Đủ 5 trạng thái, hoặc ghi "Not applicable: <lý do>".
- [ ] Mọi "Goes to screen" là Screen ID / Modal ID có trong `screen-list.md`, "stays", hoặc trang
      OPAC hiện có; khớp mũi tên trong `screen-transition.md`.
- [ ] Mọi FR ở dòng của màn hình trong `screen-list.md` có ở mục 7, và mục 7 không có FR lạ.
- [ ] Mọi thành phần hiển thị dữ liệu ghi rõ trường dữ liệu (mục 9 của tệp này).
- [ ] Mọi ô nhập có luật kiểm tra hoặc "none".
- [ ] Không có thành phần nào không phục vụ FR, không có gì thuộc W0 Table 3.
- [ ] Ảnh: `<ID>.png`, `<ID>-numbered.png`, mỗi trạng thái có hình một ảnh; ảnh rộng 1080px
      (Reader) hoặc 1280px (Staff); số trên ảnh khớp cột `#`.
- [ ] Mọi màu, chữ, góc bo đều từ token; tên thành phần đúng `ui-conventions.md` mục 3.
- [ ] Câu hỏi còn mở đã ghi ở mục 9 với "Blocking?" và giá trị mặc định.
- [ ] Đã qua soát chéo và soát nhất quán của bạn UI Conventions.

---

## 9. Dữ liệu dùng chung giữa 4 người vẽ

Để 15 màn hình nói cùng một "ngôn ngữ dữ liệu", cả 4 bạn dùng **cùng tên trường** (cột "Content /
data source" của mục 3) và **cùng dữ liệu mẫu**. Tên trường viết dạng `<Nhóm dữ liệu W0 Table 4> ›
<trường>`.

| Nhóm dữ liệu (W0 Table 4) | Trường dùng chung |
|---|---|
| Book catalogue | title · author · subjects · summary · access format (Online / Physical) |
| Book placement & library layout | floor · room code · room name · shelf code · floor plan |
| Book review | review text · reviewer · posted date · is own review · removed from display · report |
| Book QR codes | QR code · scan count |
| Saved books list | saved book |
| Reading history & preferences | history entry · reading status (Reading / Finished) · progress (%) · reading preferences |
| Chatbot conversations | reader message · chatbot reply |
| Reader accounts | library card number · declared email |
| Staff accounts | staff account name |

Thiếu trường nào → dùng tên ngắn, rõ nghĩa theo cùng kiểu, và báo 3 bạn còn lại để dùng chung.

**Dữ liệu mẫu chung** (lấy từ mục 3 của các AD):

| Dùng cho | Giá trị |
|---|---|
| Sách giấy | "Principles of Economics" — Floor 2 · Room R-204 · Shelf S-12 (AD-UC-01, AD-UC-03, AD-UC-07) |
| Sách chỉ có bản online | "Digital Marketing Basics" (AD-UC-01) |
| Phòng không có trên sơ đồ | Room R-299 (AD-UC-01) |
| Review | trang 10 review; sách có 25 review → có trang tiếp theo; review #91 bị báo cáo (AD-UC-05) |
| Lịch sử đọc / sở thích | "Principles of Economics" Reading 20% → 65%; chủ đề Economics, Marketing (AD-UC-07) |
| Số thẻ thư viện | 0012345 (có), 9999999 (không có) — AD-UC-11 |
| OTP | 482913 (đúng), 111111 (sai) — AD-UC-11 |
| Tài khoản nhân viên | staff.lan (có quyền), lib.reader (không có quyền nhân viên) — AD-UC-10 |

Cần thêm sách mẫu thì dùng tên sách hư cấu, rõ nghĩa, và báo 3 bạn còn lại để dùng chung.
