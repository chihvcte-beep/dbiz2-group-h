# Hướng dẫn Lesson 8 — Wireframe, phần 1: Đăng nhập và trang nhân viên

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Ha** |
| Vai trò | Wireframe 1 (Ha) — Đăng nhập và trang nhân viên |
| Nhóm / sản phẩm | Group H · Group H Library Core System |
| Phiên bản hướng dẫn | v1.0 · 12/11/2026 |
| Hạn nộp wireframe (giai đoạn 1) | **17/11/2026** (bộ quy ước UI của Linh có từ 14/11/2026) |
| Screen Spec (giai đoạn 2) | Chưa làm — sẽ giao riêng sau khi wireframe xong |

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
Phần còn lại: `ui-conventions.md` (Linh làm gốc) và, cho từng màn hình, **bộ ảnh wireframe** rồi
**Screen Spec**. Làm theo 2 giai đoạn:

- **Giai đoạn 1 (tệp này, hạn 17/11/2026): chỉ vẽ wireframe** — ảnh cho mọi trạng thái, ảnh đánh số,
  mã nguồn HTML, và một tệp ghi chú ngắn cho mỗi màn hình.
- **Giai đoạn 2 (giao sau): Screen Spec** — viết từ wireframe và tệp ghi chú đã có.

Sang DBIZ3, AI lập trình sẽ đọc wireframe và Screen Spec để dựng màn hình — vẽ sai hay thiếu ở đây là
sai ở sản phẩm.

**Chia việc trong nhóm.**

| Người | Phần việc | Màn hình / modal |
|---|---|---|
| UI Conventions (Linh) | Bộ quy ước gốc: màu, chữ, tên thành phần, thông báo, khung HTML dùng chung; soát nhất quán cuối cùng | (tất cả, ở mức quy ước) |
| Wireframe 1 (Ha) | Đăng nhập và trang nhân viên | S-F00-01, S-F00-02, S-F00-03, S-F04-01, S-F02-03 · M-F00-01, M-F02-03-01 |
| Wireframe 2 (Nhi) | Tìm sách và vị trí trong thư viện | S-F01-01, S-F01-02, S-F03-01, S-F03-03 |
| Wireframe 3 (Hoa) | Đánh giá sách (review) | S-F02-01, S-F02-02, S-F02-04 · M-F02-01-01, M-F02-01-02, M-F02-04-01 |
| Wireframe 4 (Trieu) | Đọc cá nhân và AI | S-F03-02, S-F03-06, S-F03-07 |

**Bạn là Wireframe 1 (Ha).**

---

## 2. Phần việc của bạn: Đăng nhập và trang nhân viên

**Tóm tắt.** Bạn làm **5 màn hình + 2 modal**: đăng nhập của bạn đọc (2 màn), đăng nhập của nhân
viên, trang nhân viên, màn in nhãn QR, modal "Sign in to continue?" (dùng chung cho 7 màn hình của
người khác) và modal xem trước trang nhãn QR.

| Thứ tự làm | ID | Tên | Actor | Khổ | Priority | AD liên quan |
|---|---|---|---|---|---|---|
| 1 | **M-F00-01** | Sign in to continue? (modal dùng chung) | Reader | 360px | — | d1 trong AD-UC-04, 07, 08, 09, 12, 14 |
| 2 | S-F00-01 | Sign in: library card number | Reader | 360px | Must | AD-UC-11 |
| 3 | S-F00-02 | Verify email OTP | Reader | 360px | Must | AD-UC-11 |
| 4 | S-F00-03 | Staff sign in | On-site Staff | 1280px | Must | AD-UC-10, AD-UC-13 |
| 5 | S-F04-01 | Staff page | On-site Staff | 1280px | Must | AD-UC-10, AD-UC-13 |
| 6 | S-F02-03 | QR code label printing | On-site Staff | 1280px | Must | AD-UC-10 |
| 7 | M-F02-03-01 | QR label sheet preview | On-site Staff | 1280px | — | AD-UC-10 (a4, a5) |

**Làm M-F00-01 đầu tiên và báo nhóm ngay khi xong**, vì Nhi, Hoa và Trieu (Wireframe 2, 3, 4) đều cần nó.

### 2.1 M-F00-01 Sign in to continue?

- **Mở từ:** S-F01-01 (Save), S-F02-01, S-F02-02, S-F03-02, S-F03-03, S-F03-06, S-F03-07 — khi bạn
  đọc chưa đăng nhập mà yêu cầu việc cần đăng nhập (FR-04-08).
- **Thành phần:** tiêu đề, một câu giải thích, nút **Sign in** (Primary) → S-F00-01, nút **Not now**
  (Secondary) → đóng modal, yêu cầu kết thúc, ở lại màn hình cũ.
- **3 biến thể câu chữ** (lấy nguyên văn từ `ui-conventions.md` mục 4): chung (FR-04-08), chatbot
  (FR-03-18), gợi ý sách (FR-03-21). Vẽ 1 ảnh `M-F00-01.png` trên nền S-F01-01 mờ; ghi 3 biến thể trong
  tệp ghi chú `notes/M-F00-01-notes.md`.
- **Quy tắc quay lại** (L8-01): sau khi OTP được chấp nhận hoặc bấm Cancel ở S-F00-01/S-F00-02, bạn
  đọc quay lại màn hình đã mở modal và việc họ yêu cầu tiếp tục.

### 2.2 S-F00-01 Sign in: library card number

- **Hành động:** nhập số thẻ và gửi (AD-UC-11 r1); Cancel → quay lại màn hình bắt đầu đăng nhập.
- **Trạng thái:** Default; Loading (đang tra thẻ); Error "card number not found" — **một thông báo
  chung cho mọi lần từ chối, không nói số thẻ có tồn tại hay không** (AD-UC-11 câu hỏi 4);
  Success = chuyển sang S-F00-02 (không có trang "đăng nhập thành công"). Empty: Not applicable.
- **Không vẽ:** đăng ký, đăng nhập Google, đăng nhập bằng email, liên kết tài khoản (Won't).
- **Câu hỏi mở gợi ý:** định dạng và độ dài thật của số thẻ thư viện (mẫu: 0012345).

### 2.3 S-F00-02 Verify email OTP

- **Hành động:** nhập OTP và gửi (r2); yêu cầu OTP mới (d5, r3); Back → S-F00-01; Cancel → quay lại
  màn hình bắt đầu đăng nhập.
- **Trạng thái — đây là màn hình nhiều trạng thái lỗi nhất của sản phẩm**, liệt kê đủ ở phần "States drawn" của tệp ghi chú:
  - mã sai, còn dưới 5 lần → "code is incorrect", nhập lại (FR-04-17);
  - lần sai thứ 5 → mã bị huỷ, đăng nhập bị từ chối, mời yêu cầu mã mới (FR-04-17);
  - mã hết hạn (sau 5 phút) hoặc đã dùng → từ chối, mời yêu cầu mã mới (FR-04-01, FR-04-04);
  - email OTP không gửi được → "code could not be sent", mời yêu cầu mã mới (FR-04-16);
  - Success: mã mới đã được gửi (ở lại); mã đúng → quay lại màn hình bắt đầu (không có trang riêng).
- **Câu hỏi mở gợi ý:** có hiển thị email đã che bớt (ví dụ n***@…) không; có hiển thị số lần nhập
  còn lại không. FR không yêu cầu — **không vẽ** nếu nhóm chưa chốt.

### 2.4 S-F00-03 Staff sign in

- **Hành động:** đăng nhập bằng tài khoản nội bộ của thư viện (AD-UC-10 a3, AD-UC-13 a2); sai thì
  thử lại (d1).
- **Trạng thái:** Error "wrong account or no staff role" — một thông báo, cho phép thử lại
  (FR-04-18); Success → mở S-F04-01 (FR-04-07). Empty: Not applicable.
- **Không vẽ:** "Forgot password", "Remember me", đăng ký — không có FR.

### 2.5 S-F04-01 Staff page

- Trang tối giản: **chỉ 2 lựa chọn** "Print QR labels" → S-F02-03 và "Reported reviews" → S-F02-04
  (FR-04-07, L8-04). "Reported reviews" là phần Could.
- Chỉ mở khi có phiên nhân viên hợp lệ; không có phiên → S-F00-03 mở thay (FR-04-08). Đây là điều
  hướng, không phải trạng thái lỗi.
- **Không vẽ:** bảng thống kê, khu quản trị, sửa sơ đồ tầng, mượn/trả (Won't). Nút đăng xuất không
  có FR → ghi câu hỏi mở nếu thấy cần.

### 2.6 S-F02-03 QR code label printing

- **Hành động:** chọn sách giấy (a1), chọn **Print labels** (a2) → mở M-F02-03-01; Back → S-F04-01.
- **Trạng thái:**
  - Validation: bấm Print labels khi chưa chọn sách → "Select at least one physical book", không tạo
    trang nhãn (FR-02-17);
  - một phần sách chưa có mã QR → bỏ chúng ra khỏi trang nhãn và **liệt kê tên các sách đó** cho
    nhân viên (FR-02-18);
  - không sách nào có mã QR → liệt kê, **không tạo** trang nhãn (FR-02-18);
  - Success → M-F02-03-01 mở với trang nhãn.
- **Câu hỏi mở bắt buộc ghi (Blocking cho phần danh sách):** nhân viên tìm sách để chọn bằng cách
  nào? FR-02-08 chỉ nói "select physical books"; tìm kiếm từ khoá là Won't. Đề xuất để nhóm chốt:
  danh sách sách giấy mới đồng bộ, mới nhất ở trên, có phân trang. Vẽ theo đề xuất và ghi rõ là
  mặc định tạm.
- Dữ liệu mẫu (AD-UC-10 mục 3): chọn 3 sách, 1 sách chưa có mã QR → trang nhãn 2 nhãn.

### 2.7 M-F02-03-01 QR label sheet preview

- **Thành phần:** xem trước trang nhãn khổ A4 (AD-UC-10 câu hỏi 3), nút **Print** (Primary) → mở hộp
  thoại in của trình duyệt (không phải màn hình của sản phẩm), nút đóng.
- **Câu hỏi mở bắt buộc ghi:** mỗi nhãn ghi gì ngoài mã QR (tên sách? mã giá?) và bao nhiêu nhãn
  mỗi trang A4 — AD-UC-10 nói "layout is set in Lesson 8", tức là **bạn đề xuất** và nhóm chốt.

### 2.8 Phối hợp

- Báo Nhi, Hoa và Trieu (Wireframe 2, 3, 4) ngay khi M-F00-01 xong (tên tệp ảnh, 3 biến thể câu chữ).
- Wireframe 3 (Hoa) làm S-F02-04 cũng là màn hình nhân viên khổ 1280px — thống nhất với bạn ấy cách vẽ
  đầu trang nhân viên (Screen header) cho giống nhau.
- Soát chéo với **Wireframe 3 (Hoa)**.

---

## 3. Tệp đầu vào (đọc trước, đính kèm cho AI)

| # | Tệp | Lấy gì từ đó |
|---|---|---|
| 1 | `EXTERNAL DESIGN/screen-list.md` | Dòng của màn hình bạn (mục đích, điểm vào, UC/FR, priority); bảng "Modals and overlays"; bảng **"What is deliberately not a screen"** (các thông báo = trạng thái của màn hình bạn); bảng **"Activity diagram actions mapped to screens"** (mọi hành động người dùng làm trên màn hình bạn) |
| 2 | `EXTERNAL DESIGN/screen-transition.md` | Các mũi tên đi ra/đi vào màn hình bạn → nút, liên kết phải có trên hình |
| 3 | `EXTERNAL DESIGN/usage-flow.md` | Màn hình bạn nằm ở bước nào trong luồng của người dùng |
| 4 | Các AD ở mục 2 của tệp này (`ACTIVITY DIAGRAM/AD-UC-xx.md`) | Mục 2 Node trace (hành động + FR), mục 3 Branches (= các trạng thái và dữ liệu mẫu), mục 5 Screens touched, mục 6 Open questions |
| 5 | `ACTIVITY DIAGRAM/activity-index.md`, bảng câu hỏi `L8-xx` | Các quyết định Lesson 8 đã chốt về màn hình |
| 6 | `GROUP-H_UC_FR_COST.xlsx` — sheet **W1_FunctionList** (câu EARS của FR), **W0_Scope** Table 3 (Won't-have) và Table 4 (nhóm dữ liệu) | Nội dung FR, giới hạn dữ liệu, những gì KHÔNG được vẽ |
| 7 | Mẫu của giáo viên: https://github.com/chienact-code/dbiz2-labdesk-example/tree/main/docs/external-design/screens/img | Một bộ ảnh hoàn chỉnh: ảnh Default, ảnh đánh số, một ảnh cho mỗi trạng thái |
| 8 | Từ Linh (UI Conventions): `EXTERNAL DESIGN/ui-conventions.md`, `screens/src/tokens.css`, `screens/src/_template.html`, `screens/src/components.html` | Màu, chữ, khoảng cách, tên thành phần, mẫu câu thông báo, khung HTML. **Chưa có thì chưa vẽ** — làm trước bước 1–2 |

**Mẹo cho AI không đọc được tệp Excel:** mở sheet W1, sao chép các hàng FR có trong mục 2 của tệp
này (cột mã FR, tên, câu EARS) dán vào khung chat dưới dạng văn bản.

---

## 4. Kết quả phải nộp (giai đoạn 1: chỉ wireframe)

```text
[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/
  notes/<ID>-notes.md                 tệp ghi chú ngắn cho mỗi màn hình / modal (mẫu ở bước 2)
  src/<ID>.html                       mã nguồn wireframe (sao chép từ _template.html)
  img/<ID>.png                        trạng thái Default
  img/<ID>-numbered.png               Default có vòng tròn số
  img/<ID>-empty.png                  mỗi trạng thái có hình thì một ảnh
  img/<ID>-loading.png
  img/<ID>-error.png                  nhiều lỗi: -error-2.png, -error-3.png …
  img/<ID>-success.png
  img/<ID>-error-numbered.png         khi trạng thái lỗi có thành phần không có ở Default
```

`<ID>` là Screen ID (ví dụ `S-F01-01`) hoặc Modal ID (ví dụ `M-F00-01`). Modal chỉ cần ảnh
`img/<Modal ID>.png` (vẽ trên nền màn hình cha mờ) và tệp ghi chú.

- Trạng thái **không áp dụng** cho màn hình thì **không vẽ ảnh**, nhưng ghi "Not applicable:
  <lý do>" trong tệp ghi chú.
- Một trạng thái có nhiều biến thể lỗi: vẽ ít nhất biến thể quan trọng nhất; vẽ thêm biến thể khác
  nếu bố cục khác đi, nếu chỉ khác câu chữ thì ghi câu chữ trong tệp ghi chú.

**Chưa làm Screen Spec ở giai đoạn này.** Screen Spec (`screen-spec-<ID>.md`) sẽ được giao sau khi
wireframe xong. Tệp ghi chú là phần chuẩn bị cho nó: danh sách thành phần đánh số chính là mục 3
"Element inventory" của Screen Spec sau này, nên **giữ ổn định số thứ tự** sau khi đã chụp ảnh.

---

## 5. Các bước làm

### Bước 1 — Lập bảng hành động và bảng trạng thái cho từng màn hình (chưa vẽ gì)

Với **mỗi** màn hình / modal của bạn:

1. Trong `screen-list.md`, bảng "Activity diagram actions mapped to screens": lọc mọi dòng có
   Screen ID của bạn → danh sách **hành động** bắt buộc phải có nút / ô / liên kết trên hình.
2. Trong bảng "What is deliberately not a screen": lọc mọi dòng nhắc Screen ID của bạn → danh sách
   **trạng thái và thông báo** phải vẽ.
3. Trong `screen-transition.md`: lọc mọi mũi tên đi ra từ màn hình bạn → nút Back, liên kết, nút
   dẫn sang màn hình khác.
4. Đối chiếu với mục 3 "Branches and acceptance tests" của các AD liên quan: mỗi nhánh mà người
   dùng nhìn thấy kết quả trên màn hình bạn phải khớp một trạng thái.

### Bước 2 — Viết tệp ghi chú `screens/notes/<ID>-notes.md`

Ngắn, bằng tiếng Anh, đúng 4 phần sau:

```markdown
# Wireframe notes: <ID> <name>

Actor: <Reader | On-site Staff> · Frame: <360px | 1280px> · UI conventions: <version> · Author: <tên>

## Elements
| # | Element | Component | Content / data source | FR |
|---|---|---|---|---|
| 1 | Back | Screen header | static | — |

## States drawn
| State | Image | What the user sees | FR |
|---|---|---|---|
| Default | img/<ID>.png | | |
| Empty | Not applicable: <lý do> | | |

## Actions and where they go
| Element | User action | Goes to |
|---|---|---|
| View on map | tap | S-F01-02 |

## Open questions
| # | Question | Default drawn |
|---|---|---|
| 1 | [NEEDS CLARIFICATION: ...] | |
```

- **Elements**: đi từ trên xuống dưới, trái sang phải; mỗi thứ người dùng nhìn thấy hoặc bấm được
  là một dòng. Cột Element = tên tiếng Anh ổn định. Cột Component = đúng tên thành phần ở mục 3
  của `ui-conventions.md`. Cột Content = chữ cố định, hoặc trường dữ liệu theo mục 9 của tệp này.
- **States drawn**: đủ 5 dòng Default, Empty, Loading, Error, Success (thêm Error-2… nếu có).
- **Actions**: mỗi hành động ở bước 1 là ít nhất một dòng. "Goes to" chỉ được là Screen ID /
  Modal ID có trong `screen-list.md`, "stays", hoặc trang OPAC hiện có (ví dụ "Existing OPAC Book
  Detail (exit)").
- **Open questions**: các câu hỏi ở mục 2 của tệp này, cộng câu hỏi bạn phát hiện thêm, kèm
  phương án bạn đã tạm vẽ.

### Bước 3 — Nhận bộ quy ước UI

Kiểm tra đã có `ui-conventions.md` và 3 tệp trong `screens/src/` của Linh. Ghi phiên bản đang dùng
vào dòng đầu tệp ghi chú. Sửa cột Component cho khớp tên thành phần chính thức.

### Bước 4 — Vẽ wireframe bằng HTML với AI

1. Sao chép `screens/src/_template.html` thành `screens/src/<ID>.html`.
2. Dùng **Lời nhắc B** ở mục 7. AI phải:
   - chỉ dùng biến trong `tokens.css` và lớp thành phần có sẵn; không tự đặt màu mới;
   - vẽ **đúng và đủ** các dòng ở phần Elements của tệp ghi chú — không thêm, không bớt;
   - vẽ mỗi trạng thái trong một khối `<section data-state="...">`;
   - gắn vòng tròn số `<span class="num">#</span>` vào từng thành phần, số = cột `#` của Elements;
   - dùng **dữ liệu mẫu chung** ở mục 9 của tệp này và dữ liệu trong mục 3 của các AD;
   - không vẽ trang OPAC cũ, không vẽ logo/tên thư viện thật, không dùng ảnh bìa sách thật
     (dùng khối xám ghi "Cover").
3. Mở tệp bằng Chrome để xem: `<ID>.html#default`, `#empty`, `#error`… Sửa đến khi đúng.

### Bước 5 — Xuất ảnh PNG bằng Chrome

1. Mở `src/<ID>.html#default` trong Chrome, nhấn **F12**, rồi **Ctrl + Shift + M** (thanh giả lập
   thiết bị).
2. Chọn **Dimensions: Responsive**. Màn hình Reader: rộng **360**, DPR **3**. Màn hình Staff:
   rộng **1280**, DPR **1**. (Không thấy ô DPR: bấm dấu ⋮ trên thanh giả lập → "Add device pixel
   ratio".)
3. Bấm ⋮ trên thanh giả lập → **Capture full size screenshot**.
4. Đổi tên tệp tải về thành `<ID>.png`, chép vào `screens/img/`. Kiểm tra ảnh rộng đúng 1080px
   (Reader) hoặc 1280px (Staff).
5. Lặp lại với `#empty`, `#loading`, `#error`, `#success` → `<ID>-<state>.png`.

### Bước 6 — Ảnh đánh số

Mở `#default-numbered`, chụp thành `<ID>-numbered.png`. Mọi dòng ở phần Elements phải có số trên
ảnh. Thành phần chỉ xuất hiện ở trạng thái khác (ví dụ thông báo lỗi) → chụp thêm
`#error-numbered` thành `<ID>-error-numbered.png`.

### Bước 7 — Tự soát, soát chéo, gửi Linh soát

1. Dùng **Lời nhắc C** ở mục 7 để AI soát bài của chính bạn. Sửa hết lỗi.
2. **Soát chéo**: Wireframe 1 (Ha) ↔ Wireframe 3 (Hoa), Wireframe 2 (Nhi) ↔ Wireframe 4 (Trieu). Người soát kiểm tra
   checklist ở mục 8 và ghi nhận xét cho người kia (không sửa hộ).
3. Báo Linh (UI Conventions) để soát màu/thành phần/thông báo (cổng cuối).

### Bước 8 — Đưa lên Git

Làm như nhóm đang làm: tạo nhánh riêng của bạn, commit các tệp ở mục 4, mở pull request vào
`main`. **Chỉ commit tệp của bạn.** Thấy cần sửa `screen-list.md`, `screen-transition.md`, AD,
W1 hay `ui-conventions.md` → không tự sửa; ghi vào Open questions của tệp ghi chú và nhắn
nhóm/người phụ trách.

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
7. **Không bịa mã.** Không tạo Screen ID, Modal ID, FR mới.
8. **Thiếu thì hỏi.** Ghi `[NEEDS CLARIFICATION: <câu hỏi>]` trong Open questions của tệp ghi chú,
   kèm phương án bạn tạm vẽ. Không ghi phỏng đoán như thể đã quyết định.
9. **Màu, chữ, khoảng cách, góc bo, khổ khung chỉ lấy từ `ui-conventions.md` mục 6** (qua
   `tokens.css`). Tên thành phần chỉ lấy từ mục 3.
10. **Không sửa ảnh bằng tay** (Paint, Photoshop). Đổi gì thì sửa HTML rồi chụp lại.
11. AI phải **báo cáo cuối việc**: đã tạo/sửa tệp nào, còn câu hỏi nào mở, điểm nào chưa kiểm tra.

---

## 7. Lời nhắc mẫu để dán cho AI

Thay `<ID>` bằng màn hình / modal đang làm. Làm **từng màn hình một**, không gộp nhiều màn hình vào
một lần hỏi.

### Lời nhắc A — Lập tệp ghi chú

```text
Bạn là chuyên viên phân tích nghiệp vụ cho dự án sinh viên "Group H Library Core System".
Tôi đính kèm: tệp hướng dẫn này, screen-list.md, screen-transition.md, activity-index.md,
ui-conventions.md, các AD: <liệt kê>, và các FR sau: <dán FR>.

Hãy viết EXTERNAL DESIGN/screens/notes/<ID>-notes.md bằng tiếng Anh, đúng mẫu ở bước 2 của tệp
hướng dẫn. Trước khi viết, liệt kê cho tôi:
(a) mọi hành động của người dùng trên màn hình này (từ bảng "Activity diagram actions mapped to
screens"), (b) mọi trạng thái/thông báo (từ bảng "What is deliberately not a screen"),
(c) mọi mũi tên đi ra (từ screen-transition.md). Sau khi viết, chứng minh mỗi mục (a) và (c) có một
dòng ở "Actions and where they go", mỗi mục (b) có ở "States drawn".
Không thêm thành phần nào không phục vụ FR. Chỗ nào chưa rõ, ghi [NEEDS CLARIFICATION] ở Open
questions kèm phương án tạm vẽ.
```

### Lời nhắc B — Vẽ wireframe HTML

```text
Tôi đính kèm: tệp hướng dẫn này, ui-conventions.md (phiên bản <v>), tokens.css, _template.html,
components.html và <ID>-notes.md.

Hãy tạo EXTERNAL DESIGN/screens/src/<ID>.html bằng cách sao chép _template.html, rồi vẽ:
- đúng và đủ các dòng của phần Elements, theo thứ tự trên xuống dưới;
- mỗi dòng của phần "States drawn" (trừ Not applicable) là một <section data-state="...">;
- vòng tròn số <span class="num">#</span> trên mỗi thành phần, số = cột # của Elements;
- chỉ dùng biến và lớp trong tokens.css, không viết màu trực tiếp;
- khổ <360px Reader | 1280px Staff>; dữ liệu mẫu theo mục 9 của tệp hướng dẫn.
Không thêm bất kỳ thành phần nào không có trong phần Elements. Không dùng thư viện JavaScript ngoài.
Cuối cùng, lập bảng đối chiếu: # | Element | có trên HTML không | ở trạng thái nào.
```

### Lời nhắc C — Tự soát trước khi nộp

```text
Đây là bài của tôi cho <ID>: tệp ghi chú, tệp HTML và danh sách ảnh trong img/.
Hãy soát theo checklist ở mục 8 của tệp hướng dẫn, rồi trả về bảng:
Mục kiểm tra | Pass/Fail | Bằng chứng hoặc chỗ sai | Cách sửa.
Kiểm tra thêm: (1) mọi "Goes to" có trong screen-list.md; (2) không có thành phần nào thuộc
W0 Table 3; (3) mọi màu trong HTML là biến của tokens.css; (4) số trên ảnh đánh số khớp cột #.
Không tự sửa tệp, chỉ báo cáo.
```

---

## 8. Checklist trước khi nộp (cho mỗi màn hình / modal)

- [ ] Có tệp ghi chú đủ 4 phần; dòng đầu ghi khổ khung và phiên bản UI conventions.
- [ ] Mọi hành động trong bảng "Activity diagram actions mapped to screens" của màn hình này có nút /
      ô / liên kết trên hình và có dòng trong "Actions and where they go".
- [ ] Mọi thông báo trong bảng "What is deliberately not a screen" của màn hình này có trong
      "States drawn" (vẽ ảnh, hoặc ghi câu chữ nếu chỉ khác chữ).
- [ ] Đủ 5 trạng thái, hoặc ghi "Not applicable: <lý do>".
- [ ] Mọi "Goes to" là Screen ID / Modal ID có trong `screen-list.md`, "stays", hoặc trang OPAC hiện
      có; khớp mũi tên trong `screen-transition.md`.
- [ ] Không có thành phần nào không phục vụ FR, không có gì thuộc W0 Table 3.
- [ ] Ảnh: `<ID>.png`, `<ID>-numbered.png`, mỗi trạng thái có hình một ảnh; ảnh rộng 1080px
      (Reader) hoặc 1280px (Staff); số trên ảnh khớp cột `#`.
- [ ] Mọi màu, chữ, góc bo đều từ token; tên thành phần đúng `ui-conventions.md` mục 3.
- [ ] Câu hỏi còn mở đã ghi kèm phương án tạm vẽ.
- [ ] Đã qua soát chéo và soát của Linh.

---

## 9. Dữ liệu dùng chung giữa 4 người vẽ

Để 15 màn hình nói cùng một "ngôn ngữ dữ liệu", cả 4 bạn dùng **cùng tên trường** (cột "Content /
data source" của phần Elements) và **cùng dữ liệu mẫu**. Tên trường viết dạng `<Nhóm dữ liệu W0
Table 4> › <trường>`.

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
