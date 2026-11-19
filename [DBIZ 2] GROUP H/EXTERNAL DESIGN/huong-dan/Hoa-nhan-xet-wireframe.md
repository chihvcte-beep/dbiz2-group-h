# Nhận xét wireframe — Hoa (Wireframe 3)

| Mục | Nội dung |
|---|---|
| Người nhận | **Hoa** |
| Phạm vi | S-F02-01, S-F02-02, S-F02-04 · M-F02-01-01, M-F02-01-02, M-F02-04-01 |
| Đối chiếu với | `huong-dan/Hoa-wireframe-3.md` (mục 2, 4, 6, 8, 9), `ui-conventions.md` v0.7, `screen-list.md`, `screen-transition.md`, `activity-index.md` (L8-xx), AD-UC-04, 05, 06, 13, 14 |
| Ngày soát | 19/11/2026 |

**Cách đọc.** Đường dẫn tính từ thư mục `EXTERNAL DESIGN/`. Cột **Mức**:
**Phải sửa** = trái hướng dẫn, checklist hoặc tài liệu chung; **Nên sửa** = chất lượng, nhất quán;
**Cần nhóm chốt** = các tài liệu chung mâu thuẫn nhau, bạn ghi vào Open questions và nhắn nhóm.
Sửa xong thì xuất lại ảnh từ nguồn, không sửa ảnh bằng tay.

**Tóm tắt.** Bộ của Hoa đúng khổ ảnh, dòng đầu tệp ghi chú đúng mẫu và câu hỏi mở ghi rất kỹ. Phần
cần sửa: ảnh từng trạng thái, mã nguồn, một số thông báo còn thiếu, và khung đánh giá dùng chung giữa
S-F02-01 và S-F02-02.

---

## Nhận xét chung (áp dụng cho mọi màn)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| C1 | Phải sửa | Không có ảnh riêng cho từng trạng thái; modal cũng chưa có ảnh riêng | `screens/img/` không có `S-F02-01.png`, `-empty.png`, `-loading.png`, `-error.png`, `-success.png`…, không có `M-F02-01-01.png`, `M-F02-01-02.png`, `M-F02-04-01.png`. Hướng dẫn mục 4, checklist mục 8 | Chụp từng trạng thái, tên đúng mẫu; modal chỉ cần `img/<Modal ID>.png` trên nền màn cha mờ |
| C2 | Phải sửa | Tệp ghi chú trỏ tới ảnh chưa có, kể cả ảnh đánh số trạng thái lỗi | S-F02-01 dòng 27–33, S-F02-02 dòng 29–30, S-F02-04 dòng 25 ghi "numbered variant included" / "error-numbered image included"; không có tệp `*-error-numbered.png` nào | Chụp đủ ảnh rồi sửa cột Image cho khớp tên thật; thêm `-error-numbered.png` cho thành phần chỉ có ở trạng thái lỗi |
| C3 | Phải sửa | Chưa nộp mã nguồn wireframe | `screens/src/` không có HTML của 3 màn và 3 modal; hướng dẫn mục 4 yêu cầu `src/<ID>.html` | Nộp HTML dựng từ `_template.html`; mọi chỉnh sửa sau này làm trên HTML rồi chụp lại |
| C4 | Nên sửa | Vòng số trên ảnh modal khác kiểu ảnh màn hình | Màn hình: vòng xanh tô kín; cả 3 ảnh `M-…-numbered.png`: vòng viền đỏ đậm; ui-conventions dòng 309: "blue numbered circles" | Dùng vòng xanh cho mọi ảnh |
| — | Tốt | Khổ ảnh đúng (Reader 1080px, Staff 1280px); dòng đầu cả 6 tệp ghi chú đúng mẫu; đủ 4 phần | | |

---

## S-F02-01 Book reviews

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Thành phần 10, 13, 14, 15 (Empty state, Toast, Skeleton, "Thử lại") không có số trên ảnh nào | `S-F02-01-numbered.png` chỉ có số 1–9; ảnh trạng thái chỉ thấy số 11, 12 | Gắn số ở ảnh `-empty`, `-loading`, `-success`, `-error-2-numbered` |
| 2 | Phải sửa | Thiếu thông báo "Report sent" | `screen-list.md` dòng 70: "Report sent" là trạng thái xác nhận của S-F02-01 (FR-02-09); tệp ghi chú dòng 20 chỉ có 3 câu Toast; ảnh Success chỉ có "Đã đăng đánh giá." | Thêm "Đã gửi báo cáo." (ui-conventions dòng 141) vào thành phần 13 và dòng Success |
| 3 | Phải sửa | Chưa có câu chữ cho 2 lỗi của FR-02-11: bỏ trống nội dung, và sửa/xoá đánh giá không phải của mình | Tệp ghi chú dòng 19 chỉ ghi "invalid ownership action feedback"; AD-UC-04 có nhánh d5 [No] và d4/d7 [No] | Ghi câu tiếng Việt cho từng lỗi: bỏ trống dùng câu mẫu ui-conventions dòng 159 (Inline error); "không phải đánh giá của bạn" đặt ở Banner (dòng 186–187) |
| 4 | Nên sửa | Trạng thái lỗi làm mất nội dung trang | Error: mất Book row và danh sách; Error-2, Error-3: chỉ còn tiêu đề và Banner. FR-04-20 yêu cầu giữ dữ liệu đang hiển thị | Vẽ lại với nội dung trang giữ nguyên |
| 5 | Nên sửa | Ảnh Success làm mất đánh giá #88 của chính bạn đọc | Success hiện #92 rồi #91; #88 đáng lẽ nằm giữa. AD-UC-04 câu hỏi 1 cho phép nhiều đánh giá cho một sách | Giữ #88 sau khi đăng #92 |
| 6 | Nên sửa | Chưa vẽ hay mô tả chế độ sửa đánh giá | Tệp ghi chú dòng 13 có nhãn "Lưu thay đổi" nhưng không có hình cho nội dung cũ, ô "Đăng ẩn danh" khi sửa (FR-02-22), cách thoát | Vẽ thêm biến thể, hoặc mô tả bằng chữ trong tệp ghi chú |
| 7 | Nên sửa | Sửa / Xoá đánh giá / Báo cáo đánh giá trông như Text link (chữ xanh, gạch chân) | Ảnh đánh số. ui-conventions dòng 118: Text link "never used for an action that changes data"; dòng 133: các hành động này là "Text buttons" | Đổi sang kiểu nút chữ, không gạch chân |
| 8 | Nên sửa | Mã đánh giá hiện cho bạn đọc thấy | Mỗi đánh giá có dòng "Đánh giá #88", "#91"…; không có trong trường dữ liệu mục 9; quy tắc 2 | Bỏ dòng mã trên màn; mã chỉ cần trong tệp ghi chú và dữ liệu mẫu |
| 9 | Nên sửa | Câu Empty thiếu bước tiếp theo, chưa nói rõ trường hợp không tìm thấy sách | "Không có đánh giá nào để hiển thị." chưa theo mẫu "lý do + bước tiếp" (dòng 162); AD-UC-05 d1 [No] chưa mô tả (còn hiện Book row và ô viết không?) | Thêm lời mời viết đánh giá đầu tiên; ghi riêng cách hiển thị khi không tìm thấy sách |
| 10 | Cần nhóm chốt | Bạn đọc có được báo cáo đánh giá của chính mình không | AD-UC-14 câu hỏi 2 và hướng dẫn dòng 103: **được**; ui-conventions dòng 133: chỉ đánh giá của người khác. Hoa đã ghi câu hỏi (dòng 52) và tạm vẽ theo ui-conventions | Giữ bản vẽ hiện tại cho đến khi nhóm chốt |
| 11 | Cần nhóm chốt | Dùng "Book row" cho khối thông tin sách có hợp lệ không | ui-conventions dòng 127: Book row dùng ở màn khác và có Format label; ở đây bỏ Format label. Đã có câu hỏi (dòng 55) | Linh bổ sung S-F02-01, S-F02-02 vào cột "Used on", hoặc đặt tên thành phần mới |

## M-F02-01-01 Delete your review?

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Nên sửa | Nền màn cha không giống S-F02-01, không thấy đánh giá đang bị xoá | Nền mờ chỉ có Book row và ô viết đánh giá, không có #88; tệp ghi chú dòng 30 lại nói "selected review is visible behind the overlay" | Chụp modal trên nền S-F02-01 thật, cuộn tới #88 |
| 2 | Cần nhóm chốt | Nhãn nút huỷ: "Huỷ" hay "Keep review" | Hướng dẫn dòng 97: "Delete review" / "Keep review"; ui-conventions dòng 56: "Huỷ" cho mọi modal. Hoa theo ui-conventions là hợp lý | Nhóm xác nhận, rồi sửa hướng dẫn cho thống nhất |
| — | Tốt | Destructive button viền đỏ có thùng rác; hai nút xếp dọc, nút xác nhận ở trên (dòng 140); trạng thái không áp dụng có lý do | | |

## M-F02-01-02 Report this review?

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Nên sửa | Nền màn cha không thấy đánh giá #91 đang bị báo cáo | Ảnh đánh số: nền chỉ có Book row và ô viết | Đặt modal trên nền S-F02-01 thật, ở đánh giá #91 |
| — | Tốt | Không có ô lý do (L8-10); nút "Báo cáo đánh giá" / "Huỷ" rõ nghĩa; đã ghi câu hỏi mở về báo cáo đánh giá của chính mình | | |

## S-F02-02 Book information and reviews (QR landing page)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Khung đánh giá dùng chung với S-F02-01 không cùng tên, số không theo thứ tự | S-F02-01: "Own review" #7, "Other readers' reviews" #8; S-F02-02: "Review item" #5. Ảnh đánh số đi 4 → 6 → 7 → 8 rồi mới 5. Hướng dẫn dòng 68–70 (L8-07) yêu cầu cùng tên; dòng 234 yêu cầu đánh số trên xuống | Dùng đúng tên thành phần của S-F02-01, đánh lại số theo thứ tự xuất hiện |
| 2 | Phải sửa | "States drawn" thiếu trạng thái lỗi của phần đánh giá | `screen-list.md` dòng 67: nội dung đánh giá bị từ chối là Error của **cả** S-F02-01 và S-F02-02 (FR-02-11); tệp ghi chú chỉ có thành phần 13, không có dòng trạng thái | Thêm dòng Error-3: "same as S-F02-01 Error" kèm câu chữ |
| 3 | Nên sửa | "Không tìm thấy sách." thiếu bước tiếp theo, trang lỗi là ngõ cụt | Mẫu "No results" (ui-conventions dòng 163); trang lỗi chỉ có tiêu đề và Banner | Thêm hướng dẫn bước tiếp theo vào câu lỗi |
| 4 | Nên sửa | Ảnh Success chỉ còn đánh giá #92, 9 đánh giá kia biến mất | Ảnh trạng thái số 6 | Giữ danh sách đầy đủ sau khi làm mới |
| 5 | Cần nhóm chốt | Nút Back khi trang mở thẳng bằng mã QR | ui-conventions dòng 114: mọi màn có Back; `screen-transition.md` không có mũi tên Back từ S-F02-02; tệp ghi chú dòng 36 ghi "stays" | Nhóm chọn: bỏ Back ở màn này, hoặc Back → OPAC Book Detail |
| 6 | Cần nhóm chốt | Có cần "Xem thêm đánh giá" ở trang QR không | AD-UC-06 dòng 77: theo luật UC-05, "one page at a time"; ui-conventions dòng 134 chỉ ghi Load more cho S-F02-01; hiện không xem được đánh giá 11–25. Đã có câu hỏi (dòng 51) | Theo AD thì nên có; đề nghị Linh thêm S-F02-02 vào "Used on" của Load more button |
| — | Tốt | Không có Report; có "Xem sách trên OPAC" (L8-08); không hiện số lượt quét | | |

## S-F02-04 Reported reviews

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Ảnh trạng thái Error vẽ sai | Ô "4 · Error": tiêu đề màn lặp hai lần, Banner MSG-04 hiện cùng lúc với Empty "Không có đánh giá bị báo cáo nào đang chờ xử lý." và Toast "Đã bỏ qua báo cáo." | Vẽ lại: một tiêu đề, Banner MSG-04 kèm "Thử lại", không có Empty và Toast |
| 2 | Phải sửa | Ảnh đánh số có hai số "2", một số gắn vào dòng không có trong Elements | Số 2 gắn vào dòng "Chọn một đánh giá để xem nội dung và xử lý báo cáo." và số 2 thứ hai gắn vào khung danh sách | Bỏ dòng chữ đó, hoặc thêm vào Elements với số riêng |
| 3 | Phải sửa | Dữ liệu mẫu không thể hiện bước "xử lý đánh giá tiếp theo" (d5) | AD-UC-13 mục 3 có #91 và #95; bản vẽ chỉ có #91 nên Success và Success-2 đều ra danh sách trống | Thêm #95; sau khi Gỡ hoặc Bỏ qua #91, danh sách còn #95 |
| 4 | Nên sửa | Số 6–10 không có trên ảnh nào | Thiếu số cho Empty state, Banner, Skeleton, Toast, "Thử lại" | Gắn số ở ảnh từng trạng thái |
| — | Tốt | Không vẽ bảng thống kê (Won't); không có ô lý do báo cáo; nhãn "Gỡ đánh giá" / "Bỏ qua báo cáo" đúng ui-conventions dòng 53–54 | | |

## M-F02-04-01 Remove this review?

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Nên sửa | Vòng số che chữ | Số 1 che chữ "G" của tiêu đề, số 2 che "đánh" trên nút, số 3 che "Huỷ" | Đặt vòng số ở mép ngoài thành phần |
| 2 | Nên sửa | Nền màn cha không khớp S-F02-04 | Khung chi tiết phía sau ghi "Đánh giá này cần được xem xét theo quy định của thư viện." thay vì nội dung #91, không có hai nút Gỡ / Bỏ qua | Chụp modal trên nền S-F02-04 Default thật |
| — | Tốt | Destructive button có thùng rác; nút Huỷ trái, nút xác nhận phải đúng quy tắc màn nhân viên; có nói hành động được ghi nhận | | |

---

## Hoa làm tốt

1. Tệp ghi chú rất cẩn thận: mỗi thành phần có mã FR, mọi chỗ tài liệu mâu thuẫn đều ghi thành câu
   hỏi mở kèm phương án tạm vẽ.
2. Câu chữ và tên thành phần bám sát ui-conventions: "Đăng ẩn danh", "Bạn đọc ẩn danh", bộ đếm
   "0/2.000", MSG-04 với "Thử lại", Destructive button đúng kiểu viền đỏ.
3. Dùng đúng dữ liệu mẫu chung: 10 đánh giá mỗi trang, có trang tiếp, có #88 của chính bạn đọc và #91
   của người khác.
