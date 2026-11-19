# Hướng dẫn Lesson 8 — Screen Spec (giai đoạn 2), phần chung cho cả nhóm

| Mục | Nội dung |
|---|---|
| Người đọc | Cả 5 bạn: Linh, Ha, Nhi, Hoa, Trieu |
| Nhóm / sản phẩm | Group H · Group H Library Core System |
| Phiên bản hướng dẫn | v1.0 · 19/11/2026 |
| Mẫu bắt buộc | `EXTERNAL DESIGN/templates/screen-spec-template.md` (mẫu của thầy, giữ nguyên cấu trúc) |
| Bài mẫu của thầy | https://github.com/chienact-code/dbiz2-labdesk-example/blob/main/docs/external-design/screens/screen-spec-S-F01-02.md |
| Hạn (đề xuất, trưởng nhóm chốt) | xem mục 7 |

> **Tệp này viết cho hai người đọc: bạn và trợ lý AI bạn dùng.**
> Mỗi bạn có thêm một tệp phân việc riêng (`<Tên>-screen-spec.md`). Khi làm với AI, hãy đính kèm
> **cả hai tệp** cùng các tệp đầu vào ở mục 3, và mở đầu bằng câu: *"Đọc hết hai tệp hướng dẫn này
> trước. Làm đúng theo nó. Chỗ nào thiếu thông tin thì hỏi tôi hoặc ghi [NEEDS CLARIFICATION],
> không tự đoán."*
> Screen Spec viết bằng **tiếng Anh**; chữ trên giao diện giữ nguyên **tiếng Việt** đúng như
> wireframe và `ui-conventions.md` (giao diện tiếng Việt từ v0.3).

---

## 1. Bối cảnh

Giai đoạn 1 (wireframe) đã xong: 15 màn hình và 5 hộp thoại (modal) đều có tệp ghi chú, ảnh và
nằm trong `EXTERNAL DESIGN/screens/`. Giai đoạn 2 là **Screen Spec**: mỗi màn hình một tệp
`EXTERNAL DESIGN/screens/screen-spec-<Screen ID>.md`, đúng 9 mục của mẫu thầy.

Screen Spec là **hợp đồng hành vi** của màn hình: ảnh là hợp đồng hình thức (bố cục, nhóm, thứ bậc),
còn các bảng trong spec nói màn hình làm gì. Sang DBIZ3, AI lập trình đọc spec này để dựng màn hình —
mẫu thầy dùng lại nguyên cho DBIZ3 Session 4.

**Spec được viết TỪ tệp ghi chú, không viết lại từ đầu.** Tệp ghi chú `screens/notes/<ID>-notes.md`
đã có 4 phần; chúng chuyển thẳng sang spec như sau:

| Phần trong tệp ghi chú | Thành mục trong Screen Spec |
|---|---|
| Elements | Mục 3 Element inventory (giữ nguyên số `#`) |
| States drawn | Mục 2 Mockup (bảng ảnh) và mục 4 States |
| Actions and where they go | Mục 5 Interactions and navigation |
| Open questions | Mục 9 Open questions |

Phần **mới phải viết thêm**: mục 1 Purpose, cột Required và Validation ở mục 3, cột System
response ở mục 5, mục 6 Screen-level rules, mục 7 Linked requirements, mục 8 Responsive and
accessibility.

---

## 2. Chia việc

15 màn hình chia đều 3 màn mỗi người. Người vẽ wireframe viết spec cho màn của mình; Linh nhận 3
màn từ hai bạn có nhiều màn nhất, và soát cuối toàn bộ.

| Người | Screen Spec phải viết | Modal viết bên trong | Wireframe gốc của |
|---|---|---|---|
| **Ha** | S-F00-01, S-F00-02, S-F02-03 | M-F00-01 (trong S-F00-01), M-F02-03-01 (trong S-F02-03) | Ha |
| **Nhi** | S-F01-01, S-F01-02, S-F03-03 | — | Nhi |
| **Hoa** | S-F02-01, S-F02-02, S-F02-04 | M-F02-01-01, M-F02-01-02 (trong S-F02-01), M-F02-04-01 (trong S-F02-04) | Hoa |
| **Trieu** | S-F03-02, S-F03-06, S-F03-07 | — | Trieu |
| **Linh** | S-F00-03, S-F04-01, S-F03-01 + **soát nhất quán cuối cùng cả 15 spec** | — | Ha (S-F00-03, S-F04-01), Nhi (S-F03-01) |

**Soát chéo** (mục 6): Ha ↔ Hoa, Nhi ↔ Trieu; spec của Linh do người vẽ wireframe gốc soát
(Ha soát S-F00-03, S-F04-01; Nhi soát S-F03-01). Linh là cổng cuối.

---

## 3. Tệp đầu vào

| # | Tệp | Lấy gì |
|---|---|---|
| 1 | `EXTERNAL DESIGN/templates/screen-spec-template.md` | Khung 9 mục, bảng thông tin đầu tệp, checklist cuối |
| 2 | Bài mẫu của thầy (đường dẫn ở đầu tệp) | Mức chi tiết cần đạt cho từng mục |
| 3 | `EXTERNAL DESIGN/screens/notes/<ID>-notes.md` | Nguồn chính của mục 2, 3, 4, 5, 9 |
| 4 | `EXTERNAL DESIGN/screens/img/` và `screens/src/` | Ảnh và mã nguồn wireframe |
| 5 | `EXTERNAL DESIGN/screen-list.md` | Dòng của màn hình (Purpose, Entry points, UC/FR, Priority); bảng modal; bảng "What is deliberately not a screen"; bảng "Activity diagram actions mapped to screens" |
| 6 | `EXTERNAL DESIGN/screen-transition.md` | Mũi tên vào/ra → mục 1 và mục 5 |
| 7 | `EXTERNAL DESIGN/ui-conventions.md` v0.7 | §2 định dạng, §3 tên thành phần, §4 câu thông báo (MSG-xx), §5 tiếp cận, §7 FR mới |
| 8 | `ACTIVITY DIAGRAM/AD-UC-xx.md` của màn hình và `activity-index.md` (bảng `L8-xx`) | Nhánh, dữ liệu mẫu, câu hỏi mở, quyết định Lesson 8 |
| 9 | `GROUP-H_UC_FR_COST.xlsx` — sheet **W1_FunctionList** | Câu EARS của từng FR (mục 6, 7) |

---

## 4. Kết quả phải nộp

```text
[DBIZ 2] GROUP H/EXTERNAL DESIGN/screens/
  screen-spec-<Screen ID>.md          một tệp cho mỗi màn hình (15 tệp cả nhóm)
  img/<ID>.png                        ảnh Default, cắt riêng 1 màn hình
  img/<ID>-numbered.png               Default có vòng tròn số
  img/<ID>-empty.png | -loading.png | -error.png | -error-2.png … | -success.png
  img/<ID>-error-numbered.png         khi trạng thái lỗi có thành phần không có ở Default
  src/<ID>.html                       mã nguồn wireframe (nếu vẽ bằng HTML)
```

### 4.1 Việc phải làm TRƯỚC khi viết: tách ảnh

Hiện mỗi màn hình mới có `-states.png` (một tấm ghép mọi trạng thái) và `-numbered.png`. Mẫu thầy
ghi rõ: *"Crop one screen per file. Do not paste a sheet of twelve screens."* Vì vậy:

- **Người vẽ wireframe** xuất ảnh riêng cho **mọi** màn hình/modal mình đã vẽ — kể cả màn mà Linh
  viết spec (Ha xuất cho S-F00-03, S-F04-01; Nhi xuất cho S-F03-01).
- Tên ảnh **đúng như tệp ghi chú đã ghi** ở phần "States drawn" (ví dụ `img/S-F00-01-error-2.png`).
- Khổ ảnh: Reader rộng **1080px** (khung 360px × DPR 3), Staff rộng **1280px** (DPR 1). Cách xuất:
  bước 5–6 của tệp hướng dẫn wireframe cũ.
- Modal: một ảnh `img/<Modal ID>.png` vẽ trên nền màn hình cha mờ.
- Giữ lại `-states.png` làm ảnh tổng quan, nhưng **không** dùng nó làm ảnh chính trong spec.
- Đưa mã nguồn wireframe vào `screens/src/` nếu chưa có (HTML, hoặc tệp `.drawio` / đường dẫn Figma).
- **Không sửa ảnh bằng tay.** Đổi gì thì sửa nguồn rồi xuất lại.

### 4.2 Modal viết ở đâu

Mẫu thầy là "một tệp cho mỗi màn hình", và `screen-list.md` quy định modal không phải một dòng
màn hình. Vì vậy **modal không có spec riêng**, mà được viết bên trong spec của màn hình sở hữu nó
(bảng ở mục 2). Cách viết, giữ nguyên 9 mục của mẫu:

- Mục 2: thêm ảnh `img/<Modal ID>.png` dưới tiêu đề nhỏ "Modal <Modal ID>".
- Mục 3: thêm tiểu mục `### 3.1 Modal <Modal ID> <name>` với bảng Element inventory riêng, cột `#`
  giữ số trong tệp ghi chú của modal.
- Mục 4 và 5: thêm các dòng có tiền tố tên modal, ví dụ `M-F02-01-01 › Xoá`.
- Màn hình khác chỉ **mở** modal thì không chép lại nội dung modal: ở mục 5 ghi
  `Goes to: M-F00-01 (see screen-spec-S-F00-01.md §3.1)`.

---

## 5. Cách điền từng mục của mẫu

| Mục | Cách điền | Lỗi hay gặp |
|---|---|---|
| Bảng đầu tệp | Lấy từ dòng của màn hình trong `screen-list.md`. Thêm 3 dòng như bài mẫu thầy: **Frame width** (360px xuất 1080px, hoặc 1280px), **Wireframe source** (`src/<ID>.html` hoặc tệp nguồn), **Author**. Status: `Draft` khi nộp, `Reviewed` sau khi Linh duyệt | Priority khác với `screen-list.md` |
| 1 Purpose | "Shown when" = điểm vào ở `screen-list.md`; "Leaves when" = mũi tên ra ở `screen-transition.md` | Viết mô tả chung chung thay vì điều kiện |
| 2 Mockup | Ảnh Default, bảng ảnh đánh số, bảng "State → Image" (mẫu bài thầy). Câu dẫn tới tokens `ui-conventions.md#6-design-tokens` | Dán ảnh ghép `-states.png` |
| 3 Element inventory | Chép phần Elements của tệp ghi chú, **giữ số `#`** khớp ảnh đánh số. Cột **Type** = tên thành phần ở `ui-conventions.md` §3 (Screen header, Primary button, Text input, Banner, Review item…). Cột **Content** = chữ tiếng Việt đúng nguyên văn, hoặc trường dữ liệu dạng `<Nhóm W0 Table 4> › <trường>`. Cột **Required** Yes/No. Cột **Validation**: mọi ô nhập phải có quy tắc hoặc ghi `none` | Thêm thành phần không có trên ảnh; bỏ trống Validation của ô nhập |
| 4 States | **Đủ 5 dòng** Default, Empty, Loading, Error, Success. Không áp dụng thì ghi "Not applicable: <lý do>". Nhiều lỗi thì gộp vào dòng Error như bài thầy, hoặc tách Error 2, Error 3. Lỗi mạng/tải dùng MSG-04 (FR-04-20) | Bỏ trạng thái Loading; tự đặt câu thông báo khác §4 |
| 5 Interactions | Chép "Actions and where they go", thêm cột **System response**. "Goes to" chỉ được là Screen ID / Modal ID có trong `screen-list.md`, `stays`, hoặc trang OPAC hiện có ghi kèm `(exit)` | Đích không có trong Screen List; thiếu hành động có trong AD |
| 6 Screen-level rules | `SR-001`, `SR-002`… Mỗi quy tắc là điều màn hình **luôn** phải giữ (ví dụ: chưa đăng nhập thì mở M-F00-01; không dùng màu làm tín hiệu duy nhất). Cột Source: mã FR, nhánh AD (`AD-UC-04 d6`), quyết định `L8-xx`, hoặc `ui-conventions §x`. Nhóm **không có BR** nên không ghi BR | Chép lại câu FR thay vì viết quy tắc của màn hình |
| 7 Linked requirements | Mọi FR ở cột UC/FR của `screen-list.md`, cộng FR mới đã dùng trên wireframe: **FR-02-22** (ẩn danh), **FR-04-19** (số lần nhập OTP còn lại), **FR-04-20** (lỗi mạng/tải). Mỗi FR phải có trong W1 | Ghi FR không có trong W1 |
| 8 Responsive / accessibility | Lấy từ `ui-conventions.md` §5: khổ nhỏ nhất, phần nào xếp chồng khi hẹp, thông tin không chỉ bằng màu, độ tương phản và cỡ chữ | Để trống |
| 9 Open questions | Chép câu hỏi còn mở trong tệp ghi chú + câu mới phát hiện. Cột Blocking Yes/No. Câu đã được nhóm chốt: Status = `Closed <ngày>: <kết luận>` | Ghi kết luận tạm như thể đã chốt |
| Completion checklist | Chép checklist của mẫu (bản 9 dòng như bài thầy), tick thật | Tick hết mà không kiểm |

---

## 6. Quy tắc bắt buộc (cho cả bạn và AI)

1. **Tài liệu của nhóm là nguồn sự thật.** Điều gì không có trong tài liệu là chưa quyết định → ghi
   `[NEEDS CLARIFICATION: …]` ở mục 9, kèm phương án đã vẽ.
2. **Spec phải khớp wireframe.** Không thêm thành phần, trạng thái hay hành động không có trên ảnh.
   Muốn đổi thì sửa wireframe trước (người vẽ), xuất lại ảnh, rồi mới sửa spec.
3. **Gọi theo mã, không kể lại.** Viết `FR-02-01`, `S-F01-02`, `L8-07`, `MSG-04`.
4. **Không bịa mã.** Không tạo Screen ID, Modal ID, FR, MSG mới. Thấy thiếu → mục 9 và báo người
   phụ trách.
5. **Chỉ 5 modal đã có.** Thông báo lỗi / trống / thành công là **trạng thái**, không phải màn hình
   hay modal mới.
6. **Tên thành phần chỉ lấy từ `ui-conventions.md` §3**; câu thông báo lấy từ §4; định dạng ngày,
   số, vị trí kệ lấy từ §2.
7. **Không sửa tệp chung** (`screen-list.md`, `screen-transition.md`, AD, W1, `ui-conventions.md`).
   Thấy cần sửa → ghi mục 9 và nhắn người phụ trách.
8. **Chỉ commit tệp của bạn**, trên nhánh riêng, mở pull request vào `main`.
9. AI phải **báo cáo cuối việc**: tạo/sửa tệp nào, câu hỏi nào còn mở, điểm nào chưa kiểm tra.

### Câu hỏi cả nhóm phải chốt TRƯỚC khi viết (họp ngắn)

| # | Câu hỏi | Ảnh hưởng | Phương án đang vẽ |
|---|---|---|---|
| Q1 | Bạn đọc có được **báo cáo đánh giá của chính mình** không? AD-UC-14 câu hỏi 2 nói **có**, `ui-conventions.md` §3 nói Report chỉ hiện trên đánh giá của **người khác** | S-F02-01, M-F02-01-02, S-F02-02 (Hoa) | Theo ui-conventions: chỉ đánh giá của người khác |
| Q2 | S-F02-02 có nút xem trang đánh giá tiếp theo không (AD-UC-06 nói theo luật phân trang của UC-05) | S-F02-02 (Hoa) | Không có |
| Q3 | Nhân viên tìm sách để in nhãn bằng cách nào (FR-02-08) — **Blocking** | S-F02-03 (Ha) | Danh sách sách giấy mới đồng bộ, mới nhất ở trên, có phân trang |
| Q4 | Nhãn QR ghi gì và bao nhiêu nhãn mỗi trang A4 (ui-conventions §7 câu hỏi 2) | M-F02-03-01 (Ha) | QR + tên sách + vị trí kệ; 2 × 5 = 10 nhãn |
| Q5 | Trạng thái chọn sẵn khi mới mở bộ lọc định dạng | S-F03-01 (Linh) | Xem ảnh Default của Nhi |

Kết luận ghi vào mục 9 của spec liên quan: `Closed <ngày>: <kết luận>`.

---

## 7. Lịch làm (đề xuất — trưởng nhóm chốt)

| Ngày | Việc | Ai |
|---|---|---|
| 19/11 | Nhận việc, đọc hướng dẫn | Cả nhóm |
| 21/11 | Tách ảnh theo mục 4.1, đưa mã nguồn wireframe vào `screens/src/` | Ha, Nhi, Hoa, Trieu |
| 21/11 | Điền bảng "Consistency review" ở `ui-conventions.md` §7 cho 20 wireframe | Linh |
| 21/11 | Họp chốt Q1–Q5 | Cả nhóm |
| 24/11 | Nộp bản nháp spec (Status: Draft), pull request vào `main` | Cả 5 |
| 25/11 | Soát chéo theo checklist mục 9, ghi nhận xét trên pull request (không sửa hộ) | Theo cặp ở mục 2 |
| 26/11 | Sửa theo nhận xét; Linh soát cuối, đổi Status thành `Reviewed`, gộp vào `main` | Cả 5, Linh |

---

## 8. Lời nhắc mẫu để dán cho AI

Làm **từng màn hình một**.

### Lời nhắc D — Viết Screen Spec

```text
Bạn là chuyên viên phân tích nghiệp vụ cho dự án sinh viên "Group H Library Core System".
Tôi đính kèm: screen-spec-chung.md, <Tên>-screen-spec.md, screen-spec-template.md, bài mẫu của thầy
screen-spec-S-F01-02.md, <ID>-notes.md, ảnh <ID>-numbered.png, screen-list.md,
screen-transition.md, ui-conventions.md, activity-index.md, các AD: <liệt kê>, và các FR sau: <dán FR>.

Hãy viết EXTERNAL DESIGN/screens/screen-spec-<ID>.md bằng tiếng Anh, đúng 9 mục của mẫu, theo bảng
"Cách điền từng mục" ở mục 5 của screen-spec-chung.md. Giữ nguyên số # của tệp ghi chú ở mục 3.
Chữ trên giao diện giữ nguyên tiếng Việt. <Nếu có modal: viết modal <Modal ID> bên trong theo mục 4.2.>
Không thêm thành phần nào không có trên ảnh. Chỗ nào chưa rõ, ghi [NEEDS CLARIFICATION] ở mục 9.
Cuối cùng, lập bảng đối chiếu:
(a) mỗi dòng Elements của tệp ghi chú → dòng nào ở mục 3;
(b) mỗi hành động của màn hình này trong bảng "Activity diagram actions mapped to screens" → dòng nào ở mục 5;
(c) mỗi thông báo của màn hình này trong bảng "What is deliberately not a screen" → dòng nào ở mục 4.
```

### Lời nhắc E — Tự soát / soát chéo

```text
Đây là screen-spec-<ID>.md, tệp ghi chú và ảnh đánh số của nó.
Soát theo checklist ở mục 9 của screen-spec-chung.md, trả về bảng:
Mục kiểm tra | Pass/Fail | Bằng chứng hoặc chỗ sai | Cách sửa.
Kiểm tra thêm: (1) mọi "Goes to" có trong screen-list.md; (2) mọi FR ở mục 7 có trong W1;
(3) số # ở mục 3 khớp ảnh đánh số; (4) mọi tên ở cột Type có trong ui-conventions.md §3.
Không tự sửa tệp, chỉ báo cáo.
```

---

## 9. Checklist trước khi nộp (cho mỗi spec)

- [ ] Tệp tên `screen-spec-<Screen ID>.md`, nằm trong `EXTERNAL DESIGN/screens/`, đủ 9 mục của mẫu.
- [ ] Ảnh Default là ảnh **riêng** `img/<ID>.png`, đúng khổ (1080px Reader / 1280px Staff).
- [ ] Ảnh đánh số tồn tại, số khớp cột `#` của mục 3.
- [ ] Mọi thành phần nhìn thấy trên ảnh có ở mục 3; không có thành phần nào ngoài ảnh.
- [ ] Mọi ô nhập có quy tắc Validation hoặc ghi `none`.
- [ ] Đủ 5 trạng thái, hoặc ghi "Not applicable: <lý do>".
- [ ] Mọi đích ở mục 5 là Screen ID / Modal ID có trong `screen-list.md`, `stays`, hoặc trang OPAC
      `(exit)`; khớp mũi tên trong `screen-transition.md`.
- [ ] Mọi thành phần hiển thị dữ liệu ghi rõ trường dữ liệu.
- [ ] Mọi FR ở mục 7 có trong W1; mọi hành động của màn hình trong AD có dòng ở mục 5.
- [ ] Modal (nếu có) viết đúng mục 4.2.
- [ ] Câu hỏi còn mở có ở mục 9, kèm Blocking và phương án đang vẽ.
- [ ] Đã qua soát chéo và soát cuối của Linh.
