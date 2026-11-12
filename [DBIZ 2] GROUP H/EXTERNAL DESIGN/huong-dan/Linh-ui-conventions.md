# Hướng dẫn Lesson 8 — UI Conventions (bộ quy ước giao diện gốc)

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Linh** |
| Vai trò | Người làm **UI Conventions gốc** — làm TRƯỚC, 4 bạn wireframe dựa vào kết quả của bạn |
| Nhóm / sản phẩm | Group H · Group H Library Core System |
| Phiên bản hướng dẫn | v1.0 · 12/11/2026 |
| Hạn nộp UI Conventions (v0.1) | **14/11/2026** — đủ mục 1–6 của `ui-conventions.md` và 3 tệp khung (`tokens.css`, `_template.html`, `components.html`), để 4 bạn wireframe bắt đầu vẽ ảnh |
| Hạn bản chốt v1.0 | Thêm mục 7 (soát nhất quán wireframe): làm dần khi 4 bạn nộp, xong ngay sau hạn wireframe **17/11/2026** |

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
sách online) **không phải màn hình của sản phẩm** — chúng chỉ là điểm vào và điểm ra. Sản phẩm có
**15 màn hình** và **5 hộp thoại (modal)**, phục vụ 2 tác nhân:

- **Reader** (bạn đọc) — dùng điện thoại hoặc máy tính; trang QR (S-F02-02) chắc chắn mở trên điện thoại.
- **On-site Staff** (nhân viên thư viện) — dùng máy tính của thư viện.

**Lesson 8 gồm những gì.** Nhóm đã xong `usage-flow.md`, `screen-list.md`, `screen-transition.md`.
Phần còn lại là `ui-conventions.md` (bạn) và, cho từng màn hình, **wireframe** (4 bạn còn lại, giai
đoạn 1, hạn 17/11/2026) rồi **Screen Spec** (giai đoạn 2, giao sau).

**Chia việc trong nhóm.**

| Người | Phần việc | Màn hình / modal |
|---|---|---|
| **Bạn (Linh)** | UI Conventions gốc + bộ khung vẽ dùng chung + soát tính nhất quán cuối cùng | (tất cả, ở mức quy ước) |
| Wireframe 1 (Ha) | Đăng nhập và trang nhân viên | S-F00-01, S-F00-02, S-F00-03, S-F04-01, S-F02-03 · M-F00-01, M-F02-03-01 |
| Wireframe 2 (Nhi) | Tìm sách và vị trí trong thư viện | S-F01-01, S-F01-02, S-F03-01, S-F03-03 |
| Wireframe 3 (Hoa) | Đánh giá sách (review) | S-F02-01, S-F02-02, S-F02-04 · M-F02-01-01, M-F02-01-02, M-F02-04-01 |
| Wireframe 4 (Trieu) | Đọc cá nhân và AI | S-F03-02, S-F03-06, S-F03-07 |

**Vì sao bạn phải làm trước.** 4 người vẽ bằng 4 trợ lý AI khác nhau. Nếu không có một bộ quy ước
chung (màu, chữ, khoảng cách, tên thành phần, cách viết thông báo, khung HTML), 15 màn hình sẽ trông
như 4 sản phẩm khác nhau. Sang DBIZ3, AI lập trình đọc tệp của bạn **trước** khi dựng bất kỳ màn hình
nào. Tệp của bạn là "luật" cho mọi màn hình.

---

## 2. Phần việc của bạn — kết quả phải nộp

| # | Tệp | Nội dung | Hạn |
|---|---|---|---|
| 1 | `EXTERNAL DESIGN/ui-conventions.md` | 6 mục theo mẫu của giáo viên + mục 7 "Change log and consistency review" | v0.1 (14/11/2026): đủ mục 1–6 · v1.0 (sau 17/11/2026): thêm mục 7 |
| 2 | `EXTERNAL DESIGN/screens/src/tokens.css` | Toàn bộ design token ở mục 6, viết thành biến CSS, kèm kiểu dáng của các thành phần ở mục 3 | 14/11/2026 |
| 3 | `EXTERNAL DESIGN/screens/src/_template.html` | Khung HTML rỗng cho MỘT màn hình: chọn trạng thái bằng phần `#` của địa chỉ, bật số thứ tự bằng `-numbered` (chi tiết ở bước 9) | 14/11/2026 |
| 4 | `EXTERNAL DESIGN/screens/src/components.html` | Một trang mẫu vẽ MỌI thành phần ở mục 3, đủ các trạng thái (bình thường, đang chọn, vô hiệu, lỗi) | 14/11/2026 |
| 5 | `EXTERNAL DESIGN/screens/img/ui-components.png` | Ảnh chụp `components.html` để người đọc không cần mở HTML | 14/11/2026 |
| 6 | Mục 7 trong `ui-conventions.md` | Kết quả soát nhất quán từng màn hình của 4 bạn | làm dần khi 4 bạn nộp, xong ngay sau 17/11/2026 |

**Bạn KHÔNG làm:** không vẽ màn hình cụ thể, không viết tệp ghi chú hay Screen Spec, không sửa `screen-list.md`,
`screen-transition.md`, các AD. Thấy chỗ cần sửa ở các tệp đó → báo nhóm.

---

## 3. Tệp đầu vào (đọc trước, đính kèm cho AI)

| # | Tệp | Lấy gì từ đó |
|---|---|---|
| 1 | `1793594740300_external-design-templates/templates/ui-conventions-template.md` | Khung 5 mục bắt buộc |
| 2 | Mẫu của giáo viên: https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/external-design/ui-conventions.md | Cách viết đầy đủ, đặc biệt **mục 6 Design tokens** và bảng kiểm tra độ tương phản |
| 3 | Mẫu Screen Spec của giáo viên: https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/external-design/screens/screen-spec-S-F01-02.md | Để biết 4 bạn sẽ dùng quy ước của bạn thế nào (cột Type, tên thành phần, ảnh đánh số) |
| 4 | `EXTERNAL DESIGN/screen-list.md` | Toàn bộ 15 màn hình, 5 modal, và bảng **"What is deliberately not a screen"** — đây là danh sách gần như đủ mọi thông báo (lỗi, trống, thành công) mà sản phẩm sẽ hiển thị |
| 5 | `EXTERNAL DESIGN/screen-transition.md` | Cách người dùng đi giữa các màn hình (nút Back, liên kết) |
| 6 | `GROUP-H_UC_FR_COST.xlsx`, sheet **W1_FunctionList** | Nội dung FR — nhiều FR quy định thông báo và giới hạn dữ liệu (review tối đa 2.000 ký tự, OTP hết hạn sau 5 phút, tối đa 5 lần nhập sai, tiến độ đọc 0–100%…) |
| 7 | `GROUP-H_UC_FR_COST.xlsx`, sheet **W0_Scope**, Table 3 (Won't-have) | Những thứ KHÔNG được có trên giao diện |
| 8 | `ACTIVITY DIAGRAM/AD-UC-01.md` … `AD-UC-14.md`, mục 3 "Branches and acceptance tests" | Dữ liệu mẫu thống nhất (ví dụ: "Floor 2 · Room R-204 · Shelf S-12", thẻ 0012345, OTP 482913) |

**Mẹo cho AI không đọc được tệp Excel:** mở sheet W1, lọc cột FR, sao chép các hàng FR (cột mã FR,
tên, câu EARS) dán vào khung chat dưới dạng văn bản.

---

## 4. Cấu trúc thư mục sau khi xong

```text
[DBIZ 2] GROUP H/EXTERNAL DESIGN/
  ui-conventions.md                ← bạn
  screen-list.md, screen-transition.md, usage-flow.md   (đã có, không sửa)
  screens/
    notes/S-Fxx-nn-notes.md, notes/M-xxx-notes.md   ← 4 bạn wireframe (giai đoạn 1)
    screen-spec-S-Fxx-nn.md        ← 4 bạn wireframe (giai đoạn 2, giao sau)
    src/
      tokens.css                   ← bạn
      _template.html               ← bạn
      components.html              ← bạn
      S-Fxx-nn.html, M-xxx.html    ← 4 bạn wireframe (sao chép từ _template.html)
    img/
      ui-components.png            ← bạn
      S-Fxx-nn.png, S-Fxx-nn-numbered.png, S-Fxx-nn-<state>.png, M-xxx.png  ← 4 bạn
```

---

## 5. Các bước làm

### Bước 1 — Kiểm kê thành phần giao diện cần có

Đi qua 15 màn hình và 5 modal trong `screen-list.md`, cùng bảng "What is deliberately not a screen",
và lập danh sách mọi loại thành phần sẽ xuất hiện. Danh sách gợi ý dưới đây đã được soạn sẵn từ
tài liệu của nhóm — **kiểm tra lại, thêm bớt nếu cần, rồi đưa vào mục 3 của `ui-conventions.md`**.
Tên thành phần viết bằng tiếng Anh; 4 bạn wireframe sẽ dùng **đúng các tên này** ở cột "Component" của
tệp ghi chú wireframe (sau này là cột "Type" của Screen Spec).

| Component (tên chuẩn) | Dùng khi | Xuất hiện ở |
|---|---|---|
| Screen header | đầu mọi màn hình: nút Back + tiêu đề màn hình | tất cả |
| Primary button | hành động chính duy nhất của màn hình | tất cả |
| Secondary button | hành động phụ, Cancel, Not now | nhiều màn hình, modal |
| Text link | đi sang trang khác (ví dụ "View this book on the OPAC", "use the format filter") | S-F02-02, S-F03-06, S-F03-07… |
| Text input | nhập một dòng | S-F00-01 (số thẻ), S-F00-03 (tài khoản nhân viên) |
| Code input | nhập mã OTP | S-F00-02 |
| Password input | mật khẩu nhân viên | S-F00-03 |
| Text area with counter | nhập review, có bộ đếm ký tự /2.000 | S-F02-01, S-F02-02 |
| Segmented control | chọn MỘT trong vài lựa chọn cố định | S-F03-01 (Online / Physical / Both), S-F01-02 (chọn tầng) |
| Select | chọn trạng thái đọc (Reading / Finished) | S-F03-02 |
| Number input | tiến độ đọc 0–100 % | S-F03-02 |
| Checkbox | chọn nhiều sách | S-F02-03 |
| Book row | một dòng sách trong danh sách: tên, tác giả, nhãn định dạng | S-F03-01, S-F03-03, S-F03-07, S-F02-03 |
| Book card | thẻ sách gọn trong câu trả lời chatbot | S-F03-06 |
| Format label | nhãn Online / Physical — **có biểu tượng + chữ**, không chỉ màu | S-F03-01, S-F03-06, S-F03-07 |
| Shelf location line | một dòng "Floor · Room · Shelf" cho một bản sách | S-F01-01, S-F01-02, S-F03-03 |
| Floor plan | sơ đồ tầng dạng khối, mỗi phòng là một ô | S-F01-02 |
| Room tile | một phòng trên sơ đồ: thường / được chọn / được tô sáng (phòng chứa sách) | S-F01-02 |
| Review item | một review: người viết, ngày, nội dung, nút Edit/Delete (của mình) hoặc Report (của người khác) | S-F02-01, S-F02-02, S-F02-04 |
| Load more button | xem trang review tiếp theo | S-F02-01 |
| Chat bubble | tin nhắn của bạn đọc / trả lời của chatbot | S-F03-06 |
| Message composer | ô nhập tin nhắn + nút gửi | S-F03-06 |
| Menu tile | ô lựa chọn lớn trên trang nhân viên | S-F04-01 |
| Banner | thông tin không chặn, đứng yên trên màn hình (info / warning / error / success) | nhiều màn hình |
| Inline error | lỗi kiểm tra dữ liệu ngay dưới ô nhập | form |
| Modal | xác nhận hoặc huỷ MỘT hành động; không dùng để điều hướng | 5 modal |
| Toast | xác nhận ngắn sau khi thành công, tự biến mất | Saved, Report sent… |
| Empty state | giải thích vì sao trống + việc tiếp theo | nhiều màn hình |
| Skeleton | khối xám giữ chỗ khi đang tải | trạng thái Loading |
| Label sheet | trang nhãn QR để in | M-F02-03-01 |

Với mỗi thành phần, ghi ở cột "Notes": số lượng tối đa (ví dụ một Primary button mỗi màn), kiểu
dáng (nền đặc / viền), và trạng thái nó có (bình thường, focus, vô hiệu, lỗi).

### Bước 2 — Chốt các quyết định với nhóm TRƯỚC khi viết

Những điểm dưới đây ảnh hưởng tới cả 15 màn hình. Hỏi nhóm (tin nhắn nhóm là đủ), ghi kết quả vào
`ui-conventions.md`. Nếu nhóm chưa trả lời kịp, dùng **giá trị mặc định đề xuất** và ghi
`[NEEDS CLARIFICATION: ...]` ở mục 7.

| # | Quyết định | Mặc định đề xuất | Lý do |
|---|---|---|---|
| Q1 | Ngôn ngữ giao diện | Tiếng Anh trên wireframe, giống mọi tài liệu của nhóm. `[NEEDS CLARIFICATION: thư viện có cần tiếng Việt làm mặc định không?]` | Nhóm không có FR nào về đa ngôn ngữ; không tự thêm tính năng chuyển ngôn ngữ |
| Q2 | Khổ khung vẽ màn hình của Reader | Rộng **360px**, xuất ảnh gấp 3 (ảnh rộng 1080px) | Giống mẫu giáo viên; trang QR chắc chắn mở trên điện thoại |
| Q3 | Khổ khung vẽ màn hình của On-site Staff (S-F00-03, S-F04-01, S-F02-03, S-F02-04, M-F02-03-01, M-F02-04-01) | Rộng **1280px**, xuất ảnh gấp 1 (ảnh rộng 1280px) | Nhân viên dùng máy tính của thư viện (screen-list) |
| Q4 | Màn hình mới có giống màu sắc OPAC hiện tại không | Không sao chép logo, tên hay nhận diện của thư viện thật; dùng bảng màu trung tính của nhóm. `[NEEDS CLARIFICATION: thư viện có muốn giao diện mới theo màu OPAC không?]` | Không có tài liệu nào về nhận diện OPAC |
| Q5 | Phông chữ | Một phông miễn phí có đủ dấu tiếng Việt, ví dụ **Be Vietnam Pro** hoặc **Inter**; dự phòng Arial | Nếu sau này có tiếng Việt thì không phải đổi |
| Q6 | Độ trung thực của wireframe | Trung bình: có màu từ token, có chữ thật, không ảnh minh hoạ, không ảnh bìa sách thật (dùng khối xám có chữ "Cover") | Giống mẫu giáo viên; tránh dùng ảnh có bản quyền |

### Bước 3 — Viết mục 1 "Language and tone"

- Ngôn ngữ (theo Q1), cách xưng hô ("you").
- Nhãn nút là **động từ nói rõ việc gì sẽ xảy ra**: "Show shelf location", "Save to my list",
  "Send code", "Post review", "Print labels". Không bao giờ dùng "OK", "Submit", "Yes/No".
- Tiêu đề màn hình: dùng đúng tên ở cột "Screen name" của `screen-list.md` hoặc rút gọn nhưng
  cùng nghĩa; ghi quy tắc rút gọn.
- Viết hoa: chỉ viết hoa chữ cái đầu câu (sentence case) cho nút, tiêu đề, nhãn.

### Bước 4 — Viết mục 2 "Formats"

Dùng bảng gợi ý sau (đã lấy ví dụ từ các AD của nhóm). Mỗi dòng phải có nguồn hoặc ghi
`[NEEDS CLARIFICATION]`.

| Item | Format đề xuất | Example | Nguồn / ghi chú |
|---|---|---|---|
| Date | dd/MM/yyyy | 16/10/2026 | như mẫu giáo viên |
| Time | HH:mm, 24 giờ | 09:00 | |
| Library card number | chỉ chữ số | 0012345 | AD-UC-11 mục 3. `[NEEDS CLARIFICATION: độ dài và định dạng thật của số thẻ]` |
| OTP code | 6 chữ số | 482913 | AD-UC-11 mục 3. FR-04-04 không nói độ dài → ghi rõ là giả định |
| OTP validity | "The code expires in 5 minutes." | | FR-04-04 |
| Shelf location | Floor `<n>` · Room `<code>` · Shelf `<code>` | Floor 2 · Room R-204 · Shelf S-12 | AD-UC-01 mục 3; một dòng cho mỗi bản sách (AD-UC-01 câu hỏi 1) |
| Room on the map | `<room name>` (`<room code>`), Floor `<n>` | Reading Room A (R-204), Floor 2 | FR-01-11 |
| Access format label | Online · Physical | | FR-03-12; luôn có biểu tượng + chữ |
| Reading status | Reading · Finished | | FR-03-04 |
| Reading progress | số nguyên 0–100 + "%" | 45% | FR-03-04 |
| Review length | bộ đếm `<n>/2,000` | 128/2,000 | FR-02-01 (ghi rõ dấu phân cách hàng nghìn) |
| Book title / author | như trong danh mục; tên dài quá 2 dòng thì cắt bằng "…" | | Book catalogue (W0 Table 4) |
| Staff account | tên tài khoản nội bộ | staff.lan | AD-UC-10 mục 3 |
| Reviewer name | `[NEEDS CLARIFICATION: hiện tên đầy đủ, tên viết tắt hay ẩn danh?]` | | quyền riêng tư; không có FR |

### Bước 5 — Viết mục 3 "Components"

Đưa bảng ở bước 1 vào, đã chỉnh. Thêm hai quy tắc:

- **Một màn hình chỉ có một Primary button** đang hiển thị ở một thời điểm.
- **Modal không dùng để điều hướng**; chỉ để xác nhận/huỷ một hành động. 5 modal của nhóm đã có
  trong `screen-list.md` — không thêm modal mới.

### Bước 6 — Viết mục 4 "Messages"

1. Bảng **mẫu câu** (pattern) cho từng loại tình huống, giống template:

| Situation | Pattern | Example (lấy từ sản phẩm của nhóm) |
|---|---|---|
| Validation error | điều gì sai + cách sửa | "Your review is empty. Write at least one character." (FR-02-01, FR-02-11) |
| System error | chuyện gì xảy ra + bạn đọc làm gì bây giờ | "AI search is temporarily unavailable. Use the format filter instead." (FR-03-17) |
| Empty state | vì sao trống + việc tiếp theo | "No books saved yet. Use Save to my list on a book's shelf location." (FR-03-25) |
| Success | việc đã làm xong | "Review posted." (FR-02-12) |
| Already done | điều đã tồn tại | "You already saved this book." (FR-03-24) |

2. **Câu chữ dùng chung** cho các thông báo lặp lại ở nhiều màn hình — bạn viết sẵn để 4 bạn
   dùng y nguyên:
   - Modal M-F00-01 "Sign in to continue?" — 3 biến thể nội dung: chung (FR-04-08), cho chatbot
     (FR-03-18: phải đăng nhập bằng thẻ thư viện), cho gợi ý sách (FR-03-21: gợi ý cá nhân cần tài
     khoản thẻ thư viện). Nút: "Sign in" (Primary), "Not now" (Secondary).
   - Lỗi mạng / lỗi hệ thống chung khi tải màn hình.
   - Văn bản trạng thái đang tải (nếu có chữ).
   - "Shelf location unavailable, ask at the ground-floor information desk." (FR-01-07, AD-UC-01
     câu hỏi 2) — dùng ở S-F01-01 và S-F03-03.
3. Ghi rõ: **câu chữ của từng thông báo riêng của màn hình do người vẽ màn hình đó viết** trong
   wireframe và tệp ghi chú, theo đúng pattern ở trên; bạn soát lại ở bước 11.
4. Ghi rõ **thông báo nằm ở đâu**: lỗi của ô nhập → Inline error ngay dưới ô; lỗi của cả màn
   hình → Banner đầu nội dung; thành công ngắn → Toast; hỏi xác nhận → Modal.

### Bước 7 — Viết mục 5 "Accessibility minimums"

Giữ 4 dòng của template (tương phản 4.5:1, không chỉ dùng màu, vùng bấm tối thiểu 24×24 CSS px,
khổ nhỏ nhất 360px), thêm các dòng riêng của sản phẩm:

- Nhãn Online / Physical: biểu tượng + chữ.
- Phòng được tô sáng trên sơ đồ: màu nền + viền đậm/hoạ tiết + nhãn chữ "Your book is here".
- Lỗi: màu + biểu tượng + chữ, không chỉ viền đỏ.
- Mọi ô nhập có nhãn (label) nằm trên ô, không dùng chữ mờ trong ô thay cho nhãn.
- Có viền focus nhìn thấy được khi dùng bàn phím (quan trọng cho trang nhân viên).

### Bước 8 — Viết mục 6 "Design tokens" và kiểm tra tương phản

1. Lập bảng token giống mẫu giáo viên: tên token, giá trị, dùng cho việc gì. Tối thiểu:
   `colour/primary`, `colour/on-primary`, `colour/text`, `colour/text-body`, `colour/text-muted`,
   `colour/border`, `colour/border-light`, `colour/surface`, `colour/skeleton`, `colour/disabled`,
   `colour/error-*` (border, text, bg), `colour/success-*`, `colour/info-*`,
   `colour/highlight` (phòng chứa sách), `colour/overlay` (nền mờ sau modal),
   `font/family`, `font/size` (title, body, small, button), `font/weight`, `space/unit`
   (bội số 4px, padding màn hình, khoảng cách lưới), `radius` (nút, thẻ, banner, modal),
   `frame/width` (360px Reader, 1280px Staff), `shadow/modal`.
2. Câu cuối của mục: *"Every mockup uses only these values."*
3. Kiểm tra **từng cặp màu chữ/nền** bằng https://webaim.org/resources/contrastchecker/ và ghi
   bảng "Pair | Ratio | Needed" như mẫu giáo viên. Chữ thường cần ≥ 4.5:1; viền của thành phần
   tương tác (ô nhập, ô phòng) cần ≥ 3:1 (WCAG 1.4.11). Cặp nào không đạt → đổi màu, không được ghi
   "gần đạt".
4. Ghi chú như mẫu: vòng tròn số màu xanh trên ảnh `*-numbered.png` là chú thích cho người đọc,
   không thuộc sản phẩm, nên không phải token.

### Bước 9 — Làm bộ khung vẽ dùng chung (`tokens.css`, `_template.html`, `components.html`)

Đây là phần giúp 4 trợ lý AI khác nhau vẽ ra cùng một kiểu. Dùng **Lời nhắc B** ở mục 7.
Yêu cầu bắt buộc của khung:

- `tokens.css`: mọi giá trị ở mục 6 thành biến CSS (`--colour-primary`…), kèm lớp CSS cho từng
  thành phần ở mục 3, đặt tên lớp theo tên thành phần (`.primary-button`, `.book-row`,
  `.format-label`, `.room-tile`…). Không có màu nào viết trực tiếp ngoài phần khai báo biến.
- `_template.html`:
  - liên kết `tokens.css`, không dùng thư viện ngoài (chỉ cho phép Google Fonts);
  - `<body data-frame="reader">` cho khổ 360px, `data-frame="staff"` cho khổ 1280px;
  - mỗi trạng thái là một khối `<section data-state="default">`, `empty`, `loading`, `error`,
    `success` (và `error-2`, `error-3`… khi màn hình có nhiều lỗi);
  - một đoạn script ngắn: chỉ hiện khối có tên trùng phần sau dấu `#` của địa chỉ
    (`S-F01-01.html#empty`), không có `#` thì hiện `default`;
  - nếu phần sau `#` kết thúc bằng `-numbered` (ví dụ `#default-numbered`) thì hiện các vòng tròn
    số `<span class="num">3</span>`; vòng tròn màu xanh `#1D4ED8`, chữ trắng, đặt ở góc trên bên
    trái của thành phần;
  - modal: một tệp riêng, vẽ màn hình cha mờ phía sau bằng `colour/overlay`;
  - phần đầu tệp có chú thích HTML ghi Screen ID, tên màn hình, phiên bản ui-conventions đang dùng.
- `components.html`: vẽ mọi thành phần ở mục 3 với dữ liệu mẫu của nhóm, đủ các trạng thái.
  Mở bằng Chrome, chụp thành `img/ui-components.png`.

Tự kiểm tra: mở `_template.html#default`, `#empty`, `#default-numbered` trên Chrome, mỗi địa chỉ
phải hiện đúng một khối.

### Bước 10 — Phát hành bản v0.1 và báo nhóm

- Đầu `ui-conventions.md` ghi `Version v0.1 · <ngày phát hành, chậm nhất 14/11/2026>`.
- Đưa lên Git (bước 12), rồi nhắn nhóm: đường dẫn 4 tệp + những điểm còn `[NEEDS CLARIFICATION]`.
- **Sau v0.1, mỗi lần đổi token hoặc tên thành phần**: tăng phiên bản (v0.2…), ghi một dòng vào
  bảng "Change log" ở mục 7, và báo nhóm **những màn hình nào phải xuất lại ảnh**. Hạn chế đổi
  sau khi các bạn đã chụp ảnh.

### Bước 11 — Soát nhất quán các wireframe (cổng kiểm tra cuối)

Khi mỗi bạn nộp wireframe (tệp ghi chú + HTML + ảnh), soát bằng **Lời nhắc C** ở mục 7 và ghi kết quả vào mục 7 của
`ui-conventions.md`:

| Screen / modal | Màu chỉ từ token | Tên thành phần đúng mục 3 | Thông báo đúng pattern mục 4 | Tiếp cận (mục 5) | Khổ ảnh đúng | Kết quả | Người soát / ngày |
|---|---|---|---|---|---|---|---|
| S-F00-01 | Pass/Fail | | | | | Pass / Cần sửa: … | |

Không tự sửa tệp của bạn khác — ghi "Cần sửa: …" và nhắn người phụ trách.

### Bước 12 — Đưa lên Git

Làm như nhóm đang làm: tạo nhánh riêng của bạn, commit các tệp ở mục 2, mở pull request vào `main`.
Không sửa tệp của người khác trong cùng pull request.

---

## 6. Quy tắc bắt buộc (cho cả bạn và AI)

1. **Tài liệu của nhóm là nguồn sự thật, không phải hiểu biết chung của AI.** Điều gì không có
   trong tài liệu là chưa được quyết định.
2. **Không thêm tính năng.** Quy ước chỉ phục vụ những gì có trong `screen-list.md` và W1. Không
   có: chọn ngôn ngữ, chế độ tối, đánh giá sao, like/dislike, widget chatbot nổi, "Reader
   Dashboard", tìm kiếm từ khoá, đăng ký tài khoản online, đăng nhập Google (W0 Table 3).
3. **Gọi theo mã, không kể lại.** Viết `FR-02-01`, `S-F01-02`, không chép lại câu của FR.
4. **Không bịa mã.** Không tạo Screen ID, modal ID hay FR mới.
5. **Thiếu thì hỏi.** Ghi `[NEEDS CLARIFICATION: <câu hỏi>]`, không ghi phỏng đoán như thể đã
   quyết định.
6. **Một giá trị chỉ có một nơi sở hữu.** Màu, chữ, khoảng cách chỉ khai báo ở mục 6;
   `tokens.css` sao chép đúng mục 6.
7. **Không sao chép nhận diện của tổ chức thật** (logo, tên, màu thương hiệu của thư viện thật
   hay của trường).
8. AI phải **báo cáo cuối việc**: đã tạo/sửa tệp nào, còn câu hỏi nào mở, điểm nào chưa kiểm tra.

---

## 7. Lời nhắc mẫu để dán cho AI

### Lời nhắc A — Soạn `ui-conventions.md`

```text
Bạn là người thiết kế UX cho dự án sinh viên "Group H Library Core System" (phần gắn thêm vào OPAC
thư viện). Tôi đính kèm: tệp hướng dẫn này, ui-conventions-template.md, ui-conventions.md mẫu của
giáo viên (LabDesk), screen-list.md, screen-transition.md, và danh sách FR của W1 (dán bên dưới).

Hãy soạn EXTERNAL DESIGN/ui-conventions.md bằng tiếng Anh, theo đúng khung của template và cách viết
của mẫu LabDesk, gồm 7 mục: 1 Language and tone, 2 Formats, 3 Components, 4 Messages,
5 Accessibility minimums, 6 Design tokens (kèm bảng tương phản), 7 Change log and consistency review.
Dùng bảng gợi ý ở bước 1, 4, 6, 7, 8 của tệp hướng dẫn làm điểm xuất phát. Các quyết định ở bước 2
dùng giá trị sau: <dán kết quả nhóm chốt, hoặc ghi "dùng mặc định đề xuất">.
Mỗi dòng có nguồn (FR, AD, mã câu hỏi) hoặc [NEEDS CLARIFICATION: ...]. Không thêm tính năng
ngoài W1. Với mục 6, đề xuất bảng màu rồi TÍNH tỉ lệ tương phản theo công thức WCAG 2.2 cho từng
cặp chữ/nền; cặp nào dưới ngưỡng thì đổi màu. Cuối cùng liệt kê các câu hỏi còn mở.
```

### Lời nhắc B — Làm bộ khung vẽ

```text
Dựa trên ui-conventions.md (đính kèm, phiên bản <v0.x>) và bước 9 của tệp hướng dẫn, hãy tạo 3 tệp:
1) EXTERNAL DESIGN/screens/src/tokens.css  2) _template.html  3) components.html.
Yêu cầu: chỉ dùng giá trị trong mục 6 (biến CSS), tên lớp theo tên thành phần ở mục 3, không thư
viện JavaScript ngoài, chạy được khi mở trực tiếp bằng Chrome (file://). _template.html phải có cơ
chế chọn trạng thái bằng #state và bật số bằng #state-numbered đúng như bước 9 mô tả.
components.html vẽ mọi thành phần ở mục 3, đủ các trạng thái, dùng dữ liệu mẫu: "Digital Marketing
Basics", "Floor 2 · Room R-204 · Shelf S-12", thẻ 0012345, OTP 482913, tài khoản staff.lan.
Sau khi xong, liệt kê mọi màu xuất hiện trong 3 tệp và chứng minh mỗi màu là một token.
```

### Lời nhắc C — Soát một wireframe của bạn khác

```text
Đây là ui-conventions.md (phiên bản <v>), tokens.css, và bài wireframe của một thành viên: tệp ghi chú
<notes/S-Fxx-nn-notes.md>, tệp HTML <S-Fxx-nn.html> và các ảnh PNG. Hãy soát và trả về bảng:
Screen | Màu chỉ từ token | Tên thành phần đúng mục 3 | Thông báo đúng pattern mục 4 |
Tiếp cận theo mục 5 | Khổ ảnh đúng (360px x3 = 1080px, hoặc 1280px) | Kết quả.
Với mỗi điểm "Fail", ghi chính xác chỗ sai (dòng trong HTML hoặc # trong phần Elements của tệp ghi chú) và cách
sửa. Không tự sửa tệp.
```

---

## 8. Checklist trước khi nộp

- [ ] `ui-conventions.md` có đủ 7 mục, có dòng phiên bản và ngày ở đầu tệp.
- [ ] Mọi quyết định ở bước 2 đã được nhóm chốt, hoặc ghi `[NEEDS CLARIFICATION]` kèm mặc định.
- [ ] Mọi thành phần cần cho 15 màn hình và 5 modal đều có tên ở mục 3.
- [ ] Mọi dòng ở mục 2 và mục 4 có nguồn (FR / AD / câu hỏi) hoặc `[NEEDS CLARIFICATION]`.
- [ ] Mọi cặp màu chữ/nền có tỉ lệ tương phản ghi ở bảng, và đều đạt ngưỡng.
- [ ] Không có tính năng nào nằm trong W0 Table 3 (Won't-have).
- [ ] `tokens.css` khớp 100% với mục 6 (không màu nào lạc).
- [ ] `_template.html` hiển thị đúng `#default`, `#empty`, `#loading`, `#error`, `#success`,
      `#default-numbered` trên Chrome.
- [ ] `components.html` vẽ đủ thành phần; đã chụp `img/ui-components.png`.
- [ ] Đã báo nhóm v0.1; mọi thay đổi sau đó có dòng trong Change log.
- [ ] Mục 7 có kết quả soát của cả 15 màn hình và 5 modal.
