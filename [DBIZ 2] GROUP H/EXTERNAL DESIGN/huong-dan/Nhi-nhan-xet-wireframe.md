# Nhận xét wireframe — Nhi (Wireframe 2)

| Mục | Nội dung |
|---|---|
| Người nhận | **Nhi** |
| Phạm vi | S-F01-01, S-F01-02, S-F03-01, S-F03-03 |
| Đối chiếu với | `huong-dan/Nhi-wireframe-2.md` (mục 2, 4, 6, 8, 9), `ui-conventions.md` v0.7, `screen-list.md`, `screen-transition.md`, `activity-index.md` (L8-xx), AD-UC-01, 02, 03, 12 |
| Ngày soát | 19/11/2026 |

**Cách đọc.** Đường dẫn tính từ thư mục `EXTERNAL DESIGN/`. Cột **Mức**:
**Phải sửa** = trái hướng dẫn, checklist hoặc tài liệu chung; **Nên sửa** = chất lượng, nhất quán;
**Cần nhóm chốt** = các tài liệu chung mâu thuẫn nhau, bạn ghi vào Open questions và nhắn nhóm.
Sửa xong thì xuất lại ảnh từ nguồn, không sửa ảnh bằng tay.

---

## Nhận xét chung (áp dụng cho mọi màn)

| # | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|
| C1 | Không có ảnh riêng cho từng trạng thái: mọi trạng thái gộp vào một ảnh `-states.png`, còn phần "States drawn" của tệp ghi chú lại ghi tên những ảnh chưa có | `screens/img/` chỉ có `<ID>-states.png` và `<ID>-numbered.png`. Tệp ghi chú ghi `img/S-F01-01-default.png` (S-F01-01 dòng 22), `-error-2-numbered.png` (S-F01-02 dòng 27), `-success.png` (S-F03-01 dòng 26), `-empty-numbered.png` (S-F03-03 dòng 24) | Xuất mỗi trạng thái một ảnh, tên đúng mục 4 của hướng dẫn (Default là `<ID>.png`, không phải `-default.png`). Sửa cột Image cho khớp tệp thật |
| C2 | Ảnh sai khổ | Ảnh đánh số rộng 1740px ở S-F01-01, S-F03-01, S-F03-03; chỉ S-F01-02 đúng 1080px. Ảnh trạng thái rộng 1740 / 1920 / 3040px. Quy định: khung 360px × DPR 3 = **1080px** | Chụp bằng Chrome chế độ Responsive, rộng 360, DPR 3, chỉ chụp khung màn hình, không kèm cột "Element notes" bên cạnh |
| C3 | Không có mã nguồn wireframe, hình không dựng từ bộ khung dùng chung của Linh | `screens/src/` không có tệp nào của Nhi. Segmented control theo bộ khung có nền trắng, viền `colour/border`, chữ căn giữa (`tokens.css` dòng 212–216); trên ảnh S-F01-02, S-F03-01 control nền xám, không viền, ô được chọn cao lệch so với hàng | Chép `_template.html` thành `src/<ID>.html`, chỉ dùng lớp và biến có sẵn, rồi chụp lại (bước 4, quy tắc 9 và 10) |
| C4 | Một màn có ba kiểu đánh số khác nhau: cột chú thích trong ảnh trạng thái, ảnh đánh số, và cột `#` của tệp ghi chú | S-F01-01: ảnh trạng thái ghi "4 · Save to my list, 5 · View on map", còn tệp ghi chú và ảnh đánh số ghi 6, 7. S-F03-01: ảnh trạng thái ghi "2 · Segmented control", ảnh đánh số ghi 4, tệp ghi chú ghi 3 | Lấy cột `#` của tệp ghi chú làm chuẩn duy nhất. Bỏ cột chú thích cạnh ảnh trạng thái |
| C5 | Thành phần chỉ có ở trạng thái khác (thông báo, Toast, Empty state) không có số trên ảnh nào | Không màn nào có `-error-numbered.png`; ảnh đánh số của S-F03-01, S-F03-03 chỉ ghi chữ "State-specific elements (not visible here)" | Chụp thêm `<ID>-error-numbered.png` (và `-success-numbered`, `-empty-numbered` khi cần), bước 6 |
| C6 | Vòng số đè lên chữ, che nội dung | "Lưu vào [6] nh sách", "Tầng 2 · Phòng R-[3]" (S-F01-01); "Lọc the[2]hình thức" (S-F03-01); "Princ[2]es of Economics", "Bỏ khỏ[6]nh sách" (S-F03-03) | Đặt vòng số ở góc ngoài thành phần |
| C7 | Tệp ghi chú có thêm phần thứ 5, vượt quy định 4 phần | "Notes:" (S-F01-01 dòng 46); "Notes and scope limits" (S-F01-02 dòng 53); "Scope and implementation notes" (S-F03-01 dòng 50); chú thích "*" (S-F03-03 dòng 51) | Chuyển nội dung cần giữ vào Elements hoặc Open questions, xoá phần thừa |

---

## S-F01-01 Shelf location

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Thành phần 4, 5, 8 (MSG-06, câu "chỉ có bản online", Toast) không có số trên ảnh nào | Ảnh đánh số chỉ có số 1, 2, 3, 6, 7 | Chụp thêm ảnh đánh số cho trạng thái Error, Information, Success (xem C5) |
| 2 | Nên sửa | Hình có tên tác giả nhưng tệp ghi chú không có dòng nào | Ảnh đánh số có "N. Gregory Mankiw" không đánh số; ảnh Information có chữ giữ chỗ "Tác giả theo danh mục" | Thêm dòng "Author · Book catalogue › author", hoặc bỏ tác giả khỏi hình |
| 3 | Nên sửa | Chỉ vẽ một dòng vị trí, chưa thể hiện quy tắc "mỗi bản sách một dòng" | Ảnh Default có đúng một dòng "Tầng 2 · Phòng R-204 · Kệ S-12"; quy tắc ở AD-UC-01 câu hỏi 1, hướng dẫn mục 2.1 | Vẽ 2 bản sách, mỗi bản một dòng |
| 4 | Nên sửa | Chú thích Loading nói nút bị vô hiệu, nhưng hình vẽ khối xám | "4 · Save / View on map · Disabled while loading"; trên hình là hai khối Skeleton | Sửa chú thích cho khớp hình |
| — | Tốt | MSG-06 và câu FR-01-06 đúng nguyên văn; sách chỉ có bản online không có Lưu và Xem bản đồ; không có liên kết sang danh sách đã lưu (đúng L8-06); 2 câu hỏi mở là câu hỏi thật | | |

## S-F01-02 Interactive digital library map

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Trạng thái "Selected room" không tô sáng phòng nào | Ô 8 ảnh trạng thái: cả 4 ô phòng vẫn trắng, chỉ có banner "Phòng đọc A (R-204), Tầng 2". FR-01-11, AD-UC-02 s8 yêu cầu tô sáng; ui-conventions §3: ô chọn nền `brand-red`, chữ trắng | Vẽ ô R-204 ở trạng thái được chọn |
| 2 | Phải sửa | Trạng thái Selected room (mở từ menu, không có sách) lại có dòng vị trí kệ | Ô 8 có "Tầng 2 · Phòng R-204 · Kệ S-12"; AD-UC-02 r3 và nhánh d4 không có sách | Bỏ dòng vị trí kệ khỏi trạng thái này |
| 3 | Phải sửa | Error-2 (phòng không có trên sơ đồ) dùng sai dữ liệu mẫu | Ô 5 ghi "Phòng R-204", trong khi hình Success cho thấy R-204 có trên sơ đồ. Hướng dẫn mục 9 và AD-UC-01 §3 dùng **R-299** | Đổi thành "Tầng 2 · Phòng R-299 · Kệ S-12" |
| 4 | Phải sửa | Ảnh đánh số thiếu số 2; câu hỏi mở 1 chỉ là việc tự kiểm số, không phải câu hỏi nghiệp vụ | Tệp ghi chú dòng 10, 49; ảnh chỉ có số 1, 3, 4, 5 | Đặt số 2 lên tiêu đề "Bản đồ thư viện", xoá câu hỏi mở 1 |
| 5 | Phải sửa | Dòng đầu tệp ghi chú sai mẫu | Dòng 3: "Use case: UC-02 · Activity diagram: AD-UC-02", thiếu Frame, Author | Dùng đúng `Actor · Frame · UI conventions · Author` |
| 6 | Nên sửa | Ô phòng ghi chữ giữ chỗ "Mã phòng" | Ảnh đánh số, ô 1, 5, 6, 8 ảnh trạng thái; hướng dẫn mục 2.2 yêu cầu mỗi ô có mã phòng | Dùng mã hư cấu R-201…R-204, báo nhóm dùng chung |
| 7 | Nên sửa | Default (mở từ menu, không có sách) vẫn hiện chú giải "Phòng chứa sách" | Ảnh đánh số, dưới sơ đồ | Chỉ hiện chú giải khi mở từ sách |
| 8 | Nên sửa | Dòng vị trí kệ đổi chỗ giữa các trạng thái | Error, Error-2: trên "Chọn tầng"; Success: dưới | Cố định một chỗ; MSG-07/08 nói "vẫn ở phía trên" nên đặt trên sơ đồ |
| 9 | Nên sửa | Chú thích Error nhắc một nút không có trên hình | Ô 4: "3 · Retry / recovery action · As shown" | Bỏ chú thích, hoặc ghi rõ không có nút |
| 10 | Nên sửa | "Goes to" có giá trị không hợp lệ; tên thành phần chưa đúng §3 | "Finish → Activity ends" (dòng 43); hai dòng "Entry…" (36–37) là cách vào màn, không phải hành động; element 9 "Banner / room details area" (dòng 17) | Bỏ dòng Finish và hai dòng Entry; đổi Component thành "Banner" |
| 11 | Nên sửa | Câu hỏi mở 3 (hình dạng sơ đồ) đã có câu trả lời | Hướng dẫn mục 2.2 ("dạng khối đơn giản"), ui-conventions §3 "Floor plan" | Xoá câu hỏi |
| 12 | Cần nhóm chốt | MSG-07 luôn nói "Thông tin vị trí kệ vẫn ở phía trên", nhưng mở bản đồ từ menu thì không có thông tin kệ | ui-conventions dòng 178 (MSG-07) đối chiếu AD-UC-02 nhánh d1 [No] | Ghi Open question, nhờ Linh thêm biến thể MSG-07 cho trường hợp mở từ menu |
| — | Tốt | Phòng của sách tô sáng bằng nền, viền đậm và nhãn "Sách của bạn ở đây", không chỉ dựa vào màu; MSG-07, MSG-08 đúng nguyên văn; có Error-3 (lỗi khi đổi tầng); ảnh đánh số đúng 1080px | | |

## S-F03-01 Access-format filter and results

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | "Actions" thiếu hai hành động: mở sách giấy và Back | Tệp ghi chú dòng 30–39 chỉ có mở sách online; `screen-list.md` (AD-UC-03 c1) và `screen-transition.md` có mũi tên mở sách giấy sang OPAC Book Detail và mũi tên back về danh mục OPAC | Thêm: Book row (sách giấy) → "Existing OPAC Book Detail (exit)"; Back → "Existing OPAC catalogue / search results (exit)" |
| 2 | Phải sửa | Ảnh đánh số và tệp ghi chú đánh số khác nhau | Ảnh: 1 Back, 2 Title, 3 Instruction label, 4 Segmented, 5–9 Book row / Format label / Empty / MSG-04 / Retry. Tệp ghi chú: 1 Back, 2 Title, 3 Segmented, 4 Results, 5 Empty, 6 Online link, 7–8 xử lý chạy ngầm; không có dòng cho MSG-04 và "Thử lại" dù đã vẽ | Viết lại Elements khớp hình; bỏ dòng 7–8 (xử lý ngầm, người dùng không thấy) |
| 3 | Phải sửa | Tệp ghi chú nói trạng thái Error chưa quyết định, mâu thuẫn với hình và tài liệu chung | Dòng 25 và câu hỏi 3 (dòng 47); hướng dẫn mục 2.3 yêu cầu Error dùng câu chữ chung; MSG-04 (ui-conventions dòng 175) áp dụng mọi màn, ứng với FR-04-20; hình đã vẽ đúng MSG-04 | Ghi Error = MSG-04, FR-04-20; xoá câu hỏi 3 |
| 4 | Phải sửa | Thiếu câu hỏi mở bắt buộc "phân trang hay Load more?" | Hướng dẫn mục 2.3; tệp ghi chú dòng 41–48 không có | Thêm câu hỏi kèm phương án đã tạm vẽ |
| 5 | Phải sửa | Ghi chú mâu thuẫn với quyết định L8-12 | Dòng 61: "The Advanced Filter Panel is an area within Search Results, not a separate screen"; L8-12 chốt S-F03-01 là trang riêng | Xoá dòng này |
| 6 | Phải sửa | Tên màn, dòng đầu và tên thành phần chưa đúng | Dòng 1 dùng "Book Catalogue & Access Format Filter" (screen-list: "Access-format filter and results"); dòng 3 sai mẫu; Component "Existing OPAC navigation", "Book result row / list", "Result-row action / link" (dòng 9, 12, 14) | Dùng đúng tên màn và dòng đầu chuẩn; Component: Screen header, Book row, Format label |
| 7 | Phải sửa | Câu hỏi mở 2 và 4 đã có câu trả lời | Câu không có kết quả: ui-conventions dòng 163; tiêu đề "Lọc theo hình thức": dòng 68; bố cục Book row: dòng 127 | Xoá hai câu này |
| 8 | Nên sửa | Kết quả mẫu chỉ có sách giấy, nên không thấy cách mở sách online | Ảnh Success chỉ có "Principles of Economics · Bản giấy" | Vẽ thêm "Digital Marketing Basics" (Trực tuyến), hoặc cả hai loại |
| 9 | Nên sửa | Empty state lặp câu | Ô 2: tiêu đề "Không tìm thấy sách", thân lại "Không tìm thấy sách. Hãy chọn hình thức khác." | Giữ một câu, đúng ui-conventions §4 |
| 10 | Cần nhóm chốt | Sách có cả hai bản (khi chọn "Cả hai") hiện nhãn thế nào | ui-conventions §2 dòng 92 và §3 chỉ có hai nhãn; AD-UC-03 câu hỏi 2 định nghĩa "Both"; tệp ghi chú dòng 12 ghi "applicable label" | Đề xuất hiện cả hai Format label; ghi Open question, nhờ Linh chốt |
| — | Tốt | Đủ 5 trạng thái; Format label có biểu tượng kèm chữ; không vẽ ô tìm kiếm từ khoá (đúng Won't); câu hỏi 1 (lúc mới mở có chọn sẵn không) là câu hỏi thật | | |

## S-F03-03 Saved books list

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Ảnh trạng thái là bản cũ, khác hẳn ảnh đánh số và tệp ghi chú | Ảnh trạng thái: không có Back, không có Format label, khung ngang rộng, dữ liệu "Minh Anh Pham", "Kệ A-03". Ảnh đánh số: có Back, Format label, "N. Gregory Mankiw", "Kệ S-12" | Vẽ lại mọi trạng thái từ cùng một nguồn với ảnh đánh số |
| 2 | Phải sửa | Trạng thái không có vị trí kệ không dùng câu chung MSG-06 | Ô 4 ảnh trạng thái: "Không khả dụng / Vui lòng liên hệ nhân viên thư viện"; MSG-06 (ui-conventions dòng 177) áp dụng cho S-F03-03 | Dùng đúng nguyên văn MSG-06 ở mọi ảnh |
| 3 | Phải sửa | Thiếu ảnh trạng thái Error dù tệp ghi chú có liệt kê | Ảnh trạng thái có 5 ô: Default, Empty, Loading, Location unavailable, Updated list; tệp ghi chú dòng 26 có Error | Vẽ Error: Banner MSG-04 kèm nút "Thử lại" |
| 4 | Phải sửa | Câu Empty state không khớp giữa các tài liệu, thiếu bước tiếp theo | Tệp ghi chú dòng 15: "Chưa có sách nào được lưu."; hình: "Bạn chưa lưu sách nào."; ui-conventions dòng 162: "Bạn chưa lưu sách nào. Bấm Lưu vào danh sách ở trang vị trí kệ sách." | Dùng câu ở dòng 162; xoá câu hỏi mở 2 |
| 5 | Phải sửa | Chưa đăng nhập thì đi thẳng tới S-F00-01, thiếu modal M-F00-01 | Tệp ghi chú dòng 34; hướng dẫn mục 2.4, bảng modal của `screen-list.md` và `screen-transition.md` đều đi qua M-F00-01 | Goes to: M-F00-01 |
| 6 | Phải sửa | Back trỏ chung chung | Dòng 35: "Previous page"; `screen-transition.md`: back về khu vực cá nhân OPAC | Goes to: "Existing OPAC personal area (exit)" |
| 7 | Phải sửa | Có dòng hành động không thuộc màn này | Dòng 38: "Save a physical book… Existing OPAC book display"; L8-06 chốt nút Lưu ở S-F01-01 | Xoá dòng này |
| 8 | Phải sửa | Câu hỏi mở 1, 3, 4 đã có câu trả lời | Câu 1: MSG-04 / FR-04-20 dùng cho mọi màn (ui-conventions dòng 175, 362); câu 3: dữ liệu mẫu ở hướng dẫn mục 9; câu 4: quầy thông tin tầng trệt đã chốt (AD-UC-01 câu hỏi 2, ui-conventions dòng 370) | Xoá các câu này và chú thích "*" dòng 51 |
| 9 | Nên sửa | Thông báo sau khi bỏ sách không dùng Toast | Ô 5: chữ xanh "Danh sách đã được cập nhật."; ui-conventions dòng 188: thành công ngắn dùng Toast | Dùng Toast, câu theo mẫu "Đã …" |
| 10 | Nên sửa | Dòng vị trí kệ sai định dạng và tên thành phần | Ảnh đánh số: "Vị trí kệ: Tầng 2 · Phòng R-204 · Kệ S-" ngắt dòng giữa mã kệ, có tiền tố, thiếu ghim; dòng 12 "Location text", dòng 13 "Inline error banner" không có trong §3 | Dùng dòng vị trí theo §2 (ghim + "Tầng · Phòng · Kệ", không ngắt mã) và "Banner" |
| 11 | Nên sửa | Hàng thứ hai dùng chữ giữ chỗ; Screen header ghi sai FR; nút bị tràn chữ | "Tên sách theo danh mục / Tác giả theo danh mục"; dòng 9: Screen header ghi FR-03-07 (nên là "—"); "Bỏ khỏi danh sách" tràn ra ngoài nút | Dùng tên sách hư cấu, sửa FR thành "—", vẽ lại nút |
| — | Tốt | Số 1–6 trên ảnh đánh số khớp cột `#`; lỗi vị trí chỉ ở đúng một hàng (đúng AD-UC-12 câu hỏi 2); nút "Bỏ khỏi danh sách" đúng nhãn chuẩn, không có modal xác nhận | | |

---

## Nhi làm tốt

1. Câu chữ chung dùng đúng nguyên văn (MSG-06, 07, 08, câu FR-01-06, MSG-04); Format label có biểu
   tượng kèm chữ.
2. Bám sát các quyết định khó: L8-06, phòng tô sáng không chỉ dựa vào màu, có vẽ lỗi khi đổi tầng,
   không vẽ thứ thuộc Won't-have.
3. Chỗ tài liệu chưa nói thì ghi `[NEEDS CLARIFICATION]` kèm phương án tạm vẽ, không tự đoán.
