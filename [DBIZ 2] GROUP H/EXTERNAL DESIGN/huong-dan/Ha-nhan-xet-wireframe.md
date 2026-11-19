# Nhận xét wireframe — Ha (Wireframe 1)

| Mục | Nội dung |
|---|---|
| Người nhận | **Ha** |
| Phạm vi | S-F00-01, S-F00-02, S-F00-03, S-F04-01, S-F02-03 · M-F00-01, M-F02-03-01 |
| Đối chiếu với | `huong-dan/Ha-wireframe-1.md` (mục 2, 4, 6, 8, 9), `ui-conventions.md` v0.7, `screen-list.md`, `screen-transition.md`, `activity-index.md` (L8-xx), AD-UC-10, 11, 13 |
| Ngày soát | 19/11/2026 |

**Cách đọc.** Đường dẫn tính từ thư mục `EXTERNAL DESIGN/`. Cột **Mức**:
**Phải sửa** = trái hướng dẫn, checklist hoặc tài liệu chung; **Nên sửa** = chất lượng, nhất quán;
**Cần nhóm chốt** = các tài liệu chung mâu thuẫn nhau, bạn ghi vào Open questions và nhắn nhóm.
Sửa xong thì xuất lại ảnh từ nguồn, không sửa ảnh bằng tay.

**Tóm tắt.** Nội dung (thông báo lỗi, dữ liệu mẫu, câu hỏi mở) làm rất kỹ. Phần cần sửa chủ yếu là
**hình thức**: ảnh, màu nút chính, màu thông báo lỗi — lặp lại ở mọi màn nên sửa một lần trong tệp
nguồn là xong.

---

## Nhận xét chung (áp dụng cho mọi màn)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| C1 | Phải sửa | Không có ảnh riêng cho từng trạng thái; tệp ghi chú dẫn tới những ảnh chưa có | `screens/img/` chỉ có `<ID>-states.png` (tấm ghép) và `<ID>-numbered.png`. Tệp ghi chú dẫn tới `img/S-F00-01.png`, `-error-2.png`, `-error-numbered.png`, `img/M-F00-01.png`, `img/S-F02-03-page-2.png`… | Xuất mỗi trạng thái một ảnh, tên đúng cột Image. Trạng thái có thành phần không có ở Default (lỗi, Toast) thì thêm `-error-numbered.png` |
| C2 | Phải sửa | Ảnh sai khổ, vì chụp cả khung trình bày và cột "Element notes" bên cạnh | Ảnh đánh số màn Reader (S-F00-01, S-F00-02, M-F00-01) rộng 773px, cần **1080px**; màn Staff (S-F00-03, S-F04-01, S-F02-03, M-F02-03-01) rộng 1693px, cần **1280px**. Tấm ghép rộng 2543 / 5303px | Chỉ chụp đúng khung màn hình: Reader 360px × 3 = 1080px, Staff 1280px × 1 |
| C3 | Phải sửa | Vẽ bằng draw.io thay vì HTML từ `_template.html`, và tệp ghi chú lại nói có HTML | `src/` chỉ có `Ha-wireframe-1.drawio`; không có `S-F00-0x.html` ở nhánh nào. `notes/S-F00-01-notes.md` dòng 47: "validated in Chromium… The HTML demonstrates transitions"; `notes/M-F00-01-notes.md` dòng 41: "its HTML source" | Làm `src/<ID>.html` từ `_template.html` (bước 4). Nếu nhóm cho phép dùng draw.io thì xoá các câu nói có HTML và "validated in Chromium" |
| C4 | Phải sửa | Nút chính (Primary button) tô xám đen thay vì đỏ thương hiệu | Trong tệp draw.io có 48 ô `fillColor=#1F2937`, không ô nào tô nền `#8B0000` (màu này chỉ dùng làm viền). Trên ảnh, "Gửi mã", "Đăng nhập", "In nhãn", "In" đều xám đen. Quy định: ui-conventions §3 Primary button, §6 `colour/brand-red` | Tô nút Primary nền **#8B0000**, chữ trắng |
| C5 | Phải sửa | Banner lỗi, Inline error và Banner cảnh báo dùng nền xám bề mặt thay vì nền riêng | Các ô này `fillColor=#EDF0F2`; trong tệp không có `#FDECEA`. Quy định: §3 Banner, Inline error; §6 | Lỗi: nền **#FDECEA**. Cảnh báo: nền **#FDF3E3**, chữ #7A3E06 |
| C6 | Nên sửa | Góc bo và phông tiêu đề chưa theo quy ước | Mọi ô đều `rounded=0`, phông `Inter`; không ô nào dùng SVN-Gilroy cho tiêu đề. Quy định: §6 radius 8px, `font/heading` | Bo góc 8px cho nút, ô nhập, thẻ, banner, modal; tiêu đề màn và modal dùng phông tiêu đề |
| C7 | Nên sửa | Trạng thái Loading chèn thêm thanh Skeleton giữa ô nhập và nút, không thay cho nội dung nào | Tấm Loading của S-F00-01 (số 7), S-F00-02 (số 10), S-F00-03 (số 7). §3: Skeleton "same shape as the content it replaces" | Ở màn biểu mẫu, chỉ làm mờ nút và hiện "Đang tải…" (MSG-05); sửa tên thành phần trong tệp ghi chú |
| C8 | Nên sửa | Vòng số đè lên chữ | M-F00-01: số 1, 2 che chữ đầu tiêu đề và câu giải thích; M-F02-03-01: số 1 che chữ "X" của "Xem trước…" | Dời vòng số ra mép thành phần |
| C9 | Nên sửa | Tấm ghép vẫn vẽ ô xám cho các trạng thái "Not applicable" | Ô Empty, Success ở S-F00-01, S-F00-02, S-F00-03, S-F04-01. Hướng dẫn mục 4: không áp dụng thì không vẽ ảnh | Bỏ các ô này, chỉ ghi lý do trong tệp ghi chú |
| C10 | Nên sửa | Biểu tượng nào cũng là hình thoi ◇ | Menu tile, Format label "Bản giấy", Toast | Dùng biểu tượng có nghĩa (in, cờ báo cáo, sách, dấu kiểm), hoặc ghi rõ là biểu tượng tạm |

---

## M-F00-01 Sign in to continue? (modal dùng chung)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Nên sửa | "Goes to" của "Not now" liệt kê 7 màn, đọc như thể bấm vào sẽ chuyển trang | Tệp ghi chú dòng 31; `screen-transition.md` dòng 105–106: "Not now" đóng modal, bạn đọc ở lại | Ghi "stays (modal closes, request ends)" |
| 2 | Nên sửa | Tệp ghi chú tự ghi là chưa báo nhóm | Dòng 41: "No group notification has been sent."; hướng dẫn mục 2 và 2.8 yêu cầu báo Nhi, Hoa, Trieu ngay | Báo nhóm tên ảnh và 3 biến thể câu chữ, rồi sửa dòng này |
| — | Tốt | 3 biến thể MSG-01, 02, 03 đúng nguyên văn; nút xếp dọc, nút chính ở trên; nền S-F01-01 làm mờ; số 1–4 khớp tệp ghi chú | | |

## S-F00-01 Sign in: library card number

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Nên sửa | Screen header thiếu nút Quay lại, chỉ có tiêu đề | Ảnh `S-F00-01-numbered.png`: số 1 chỉ có chữ "Đăng nhập". §3: Screen header gồm "Back button + screen title". S-F00-02 thì có | Thêm nút Quay lại về màn bắt đầu đăng nhập (giống Huỷ), hoặc ghi câu hỏi mở cho Linh |
| — | Tốt | Một thông báo từ chối chung, không lộ số thẻ có tồn tại hay không (AD-UC-11 câu hỏi 4); lỗi định dạng đúng câu §2; dữ liệu mẫu 0012345, 9999999 đúng | | |

## S-F00-02 Verify email OTP

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Toast "Đã gửi mã mới." gần như không đọc được và đặt sai chỗ | Tấm Success (số 5): Toast ở đầu màn, chữ trắng trên nền xám nhạt #EDF0F2 — không đạt độ tương phản (§5). §3 Toast: "Bottom centre, `colour/text` background, white text" | Đưa Toast xuống giữa đáy màn, nền #1F2937, chữ trắng, kèm dấu kiểm |
| 2 | Nên sửa | Dòng "Mã có hiệu lực trong 5 phút." (số 3) gán sai tên thành phần "Code input" | Tệp ghi chú dòng 12; đây là câu gợi ý MSG-09, không phải ô nhập | Ghi "Code input (hint text)" hoặc hỏi Linh tên đúng |
| 3 | Nên sửa | Ở trạng thái phải xin mã mới (Error-2, 3, 4), nút "Đăng nhập" ghi là bị khoá nhưng nhìn không ra | Tệp ghi chú: "(disabled secondary during recovery)"; trên ảnh nút vẫn nền trắng, viền như bình thường | Vẽ rõ trạng thái bị khoá (nền #C5CBD3 hoặc chữ mờ) |
| — | Tốt | Đủ 4 thông báo lỗi theo `screen-list.md` cộng lỗi mạng; số lần thử còn lại đúng FR-04-19 ("Mã chưa đúng. Bạn còn 3 lần thử." với mã 111111); mỗi lúc chỉ một nút chính; đã ghi câu hỏi mở về email che bớt | | |

## S-F00-03 Staff sign in

Đạt, không có điểm riêng — chỉ còn các lỗi chung C4, C5. Không vẽ "Forgot password", "Remember me";
dùng đúng staff.lan và lib.reader.

## S-F04-01 Staff page

Đạt, không có điểm riêng. Đúng 2 Menu tile, có câu hỏi mở về nút đăng xuất. Biểu tượng ô chức năng nên
theo `.menu-tile .icon` trong `tokens.css` (đỏ thương hiệu, có nghĩa) — xem C10.

## S-F02-03 QR code label printing

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Cần nhóm chốt | Có thêm đường đi "Print labels → S-F00-03" (kiểm lại phiên nhân viên) mà sơ đồ chuyển màn không có | Tệp ghi chú dòng 43; AD-UC-10 dòng 111 nói phiên hết hạn được bắt "by the same check… not drawn"; `screen-transition.md` dòng 116–132 không có mũi tên S-F02-03 → S-F00-03 | Chuyển thành câu hỏi mở; nhóm quyết định thêm mũi tên vào `screen-transition.md` hay bỏ dòng này |
| 2 | Nên sửa | Số thứ tự nhảy từ 6 sang 8, không có số 7 | Tệp ghi chú dòng 14–15; tấm trạng thái cũng không có số 7 | Đánh lại số liên tục, rồi giữ cố định |
| — | Tốt | Có câu hỏi mở Blocking về cách tìm sách kèm phương án tạm vẽ; đủ 3 trạng thái "chưa chọn sách", "một phần chưa có QR", "không sách nào có QR"; dữ liệu mẫu 3 sách, 1 chưa có QR, ra 2 nhãn đúng AD-UC-10 | | |

## M-F02-03-01 QR label sheet preview

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Dữ liệu mẫu mâu thuẫn với S-F02-03 | `M-F02-03-01-numbered.png` in nhãn "Modern Business Ethics · Tầng 2 · Phòng R-203 · Kệ S-09", trong khi ở S-F02-03 chính sách này là sách **chưa có mã QR** | Ở Default dùng sách đều có mã QR (ví dụ "Foundations of Statistics", theo AD-UC-10 nhánh d3 [Yes]) |
| 2 | Cần nhóm chốt | Nhãn nút "Đóng" không có trong bảng nhãn chuẩn | Hướng dẫn 2.7 nói "nút đóng"; ui-conventions §1 chỉ có "Huỷ" cho modal | Hỏi Linh: thêm "Đóng" vào §1, hay dùng "Huỷ" |
| — | Tốt | A4 dọc, tạm vẽ 2 × 5 nhãn; dòng vị trí kệ đúng §2; nút chính bên phải, nút phụ bên trái; đủ 2 câu hỏi mở bắt buộc | | |

---

## Ha làm tốt

1. Đủ và đúng các thông báo lỗi của phần đăng nhập, câu chữ theo đúng §2 và §4.
2. Dùng đúng dữ liệu mẫu chung (0012345, 9999999, 482913, 111111, staff.lan, lib.reader, Principles of
   Economics · Tầng 2 · Phòng R-204 · Kệ S-12) và ghi rõ các tên sách tự đặt thêm.
3. Ghi đủ các câu hỏi mở bắt buộc, kèm phương án tạm vẽ.
