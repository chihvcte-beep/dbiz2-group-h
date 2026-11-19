# Nhận xét wireframe — Trieu (Wireframe 4)

| Mục | Nội dung |
|---|---|
| Người nhận | **Trieu** |
| Phạm vi | S-F03-02, S-F03-06, S-F03-07 |
| Đối chiếu với | `huong-dan/Trieu-wireframe-4.md` (mục 2, 4, 5, 6, 8, 9), `ui-conventions.md` v0.7, `screen-list.md`, `screen-transition.md`, `activity-index.md` (L8-xx), AD-UC-07, 08, 09 |
| Ngày soát | 19/11/2026 |

**Cách đọc.** Đường dẫn tính từ thư mục `EXTERNAL DESIGN/`. Cột **Mức**:
**Phải sửa** = trái hướng dẫn, checklist hoặc tài liệu chung; **Nên sửa** = chất lượng, nhất quán;
**Cần nhóm chốt** = các tài liệu chung mâu thuẫn nhau, bạn ghi vào Open questions và nhắn nhóm.
Sửa xong thì xuất lại ảnh từ HTML, không sửa ảnh bằng tay.

**Tóm tắt.** Trieu là người duy nhất nộp HTML, và các quyết định ghi trong tệp ghi chú đều có thật
trong AD. Việc lớn nhất cần làm: **dựng lại 3 tệp HTML từ `_template.html` và `tokens.css`** — làm
xong việc này thì phần lớn các lỗi màu, cỡ chữ, tên thành phần bên dưới tự hết. Ngoài ra cần bỏ một
số thứ tự thêm vào mà không có FR.

---

## Nhận xét chung (áp dụng cho mọi màn)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| C1 | Phải sửa | Chưa có ảnh riêng cho từng trạng thái; tệp ghi chú dẫn tới ảnh chưa có | `screens/img/` chỉ có `-states.png` và `-numbered.png`. S-F03-02 dòng 32–36 dẫn tới `img/S-F03-02.png`, `-empty.png`, `-loading.png`, `-error.png`, `-success.png`; S-F03-06, S-F03-07 dẫn tới `-no-match.png`, `-cold-start.png`, `-topped-up.png`… | Xuất từng ảnh, kể cả trạng thái riêng `-cold-start`, `-topped-up`, `-no-match` (mục 4, bước 5) |
| C2 | Phải sửa | Ảnh sai khổ và không chụp từ HTML: là trang trình bày có khung điện thoại nhỏ cùng cột "Element notes", nên ảnh và HTML khác nhau | Ảnh đánh số rộng 1740px, tấm ghép 1920px (cần **1080px**). Ví dụ lệch: ảnh S-F03-02 Error nút ghi "Lưu", HTML dòng 645 ghi "Lưu lại"; ảnh S-F03-06 Success có 1 thẻ sách, HTML có 2 | Mở `src/<ID>.html#<trạng thái>` trong Chrome, rộng 360, DPR 3, "Capture full size screenshot"; bỏ cột ghi chú |
| C3 | Phải sửa | Thành phần chỉ có ở trạng thái khác không có ảnh đánh số | Ảnh đánh số chỉ có số của Default: S-F03-02 có 1–13, S-F03-06 có 1, 2, 3, 8, 9, S-F03-07 có 1–6 | Chụp thêm `#error-numbered`, `#success-numbered`… (bước 6) |
| C4 | Phải sửa | HTML không dựng từ `_template.html`: không liên kết `tokens.css`, không có `<section data-state>`, bật số bằng `?numbered=1` thay vì `#default-numbered`, tên lớp tự đặt | Cả 3 tệp không có `tokens.css`; trạng thái viết `<section class="screen-state" id="default">` (S-F03-02 dòng 400); lớp `.btn-primary`, `.tag-format`, `.bubble-user`, `.banner-error` thay cho `.primary-button`, `.format-label`, `.chat-bubble.reader`, `.banner.error`. Ở S-F03-06, S-F03-07 phần đầu màn nằm ngoài các section (06 dòng 316, 463; 07 dòng 326) | Làm lại từ `_template.html`: liên kết `tokens.css`, mỗi trạng thái một section đủ cả phần đầu màn, chỉ dùng lớp có trong `tokens.css` / `components.html` |
| C5 | Phải sửa | Hai giá trị màu bị đổi, có thêm màu ngoài bảng màu | S-F03-02 dòng 15, 17 (06, 07 tương tự): `--colour-text-muted: #6B7280` (chuẩn #4B5563), `--colour-border-light: #E5E7EB` (chuẩn #D9D9D9); thêm #edeff1, #f7f8f9; S-F03-07 có màu tím #7C3AED, #5B21B6, #F5F3FF, #6D28D9 (dòng 176–240). Các màu chính #8B0000, #C62828, #1074C3 thì đúng | Xoá khối `:root` tự viết, dùng `tokens.css`; bỏ màu tím |
| C6 | Phải sửa | Chữ và kích thước không theo §6 | Không dùng phông tiêu đề SVN-Gilroy; chữ thường 14px (chuẩn 16px), tiêu đề 18px (chuẩn 20px); nút và ô nhập cao 32–42px (chuẩn 48px, vùng bấm tối thiểu 44px theo §5) — S-F03-02 dòng 44–45, 76–77, 249, 259; S-F03-06 dòng 269 | Dùng `--font-heading`, `--font-size-body`, `--size-control` |
| C7 | Phải sửa | Format label chỉ có chữ, không có biểu tượng | `.tag-format` chỉ có "Bản giấy" / "Trực tuyến" ở cả 3 màn; §5 "không bao giờ chỉ dùng màu" | Dùng `.format-label` có biểu tượng |
| C8 | Phải sửa | Câu trên màn có lẫn mã FR, MSG, màn hình | S-F03-02 dòng 614 "(FR-03-22)"; S-F03-06 dòng 451 "(FR-03-17)", dòng 456 "(S-F03-01)"; S-F03-07 dòng 464 "(FR-03-20)", dòng 518 "(MSG-04)" | Xoá mã khỏi câu chữ; mã chỉ ghi trong tệp ghi chú |
| C9 | Phải sửa | Tiêu đề màn không đúng bảng §1 | "Lịch sử đọc & sở thích" (chuẩn "Lịch sử đọc và sở thích"); "Thủ thư AI tìm sách" (chuẩn "Trợ lý tìm sách AI"); "Gợi ý cho bạn" / "Gợi ý sách cho bạn" (chuẩn "Sách gợi ý cho bạn") | Dùng đúng tiêu đề §1 |
| C10 | Nên sửa | Quyết định đã chốt lại ghi như câu hỏi đang chờ | Các mục "Team consensus (2026-11-04)" **có thật** trong mục 6 của AD-UC-07 (Q1, Q2, Q4), AD-UC-08 (Q1–Q3), AD-UC-09 (Q1–Q3), nhưng vẫn gắn `[NEEDS CLARIFICATION]` (S-F03-02 dòng 55–57, S-F03-06 dòng 50–52, S-F03-07 dòng 50–52) | Ghi "Decided — AD-UC-0x Q<n> (04/11/2026)"; chỉ dùng `[NEEDS CLARIFICATION]` cho câu còn mở thật |
| C11 | Phải sửa | Nhiều tên thành phần không có trong §3 | Section header, Status badge, Progress bar & label, Ghost button, Multi-select chips, Inline error banner, Banner with retry, Message bubble, Chip group, Result card, Card action link, Loading bubble, Header action button, Metadata tag/badge, Callout banner, Section divider | Đổi về tên §3 (Banner, Inline error, Text link, Secondary button, Chat bubble, Book card, Book row, Format label, Empty state, Skeleton); cần thành phần mới thì ghi câu hỏi mở cho Linh |
| C12 | Nên sửa | Tệp ghi chú có phần thứ 5 "Scope and implementation notes" | S-F03-02 dòng 60, S-F03-06 dòng 55, S-F03-07 dòng 55; hướng dẫn yêu cầu đúng 4 phần | Chuyển nội dung cần giữ vào Open questions hoặc cột Content |

---

## S-F03-02 Reading history and preferences

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Bộ chọn trạng thái vẽ là Segmented control; §3 quy định màn này dùng **Select** | Tệp ghi chú dòng 15; HTML dòng 451 | Đổi thành Select (Đang đọc / Đã đọc xong) |
| 2 | Phải sửa | Hai nút Primary hiện cùng lúc | "Lưu tiến độ" và "Lưu sở thích" (HTML dòng 470, 527; ảnh số 9 và 13); §3: chỉ 1 Primary | Giữ 1 Primary, nút còn lại thành Secondary |
| 3 | Phải sửa | Nhãn nút lưu không theo nhãn chuẩn, lại không thống nhất | "Lưu tiến độ" (dòng 470), "Lưu lại" (dòng 645), "Lưu" (ảnh); "Hủy" khác "Huỷ". §1 quy định "Lưu thay đổi" cho S-F03-02 | Dùng "Lưu thay đổi" và "Huỷ" |
| 4 | Phải sửa | Thành phần 18 (lỗi tải trang MSG-04, FR-04-20) có trong tệp ghi chú nhưng không vẽ | Tệp ghi chú dòng 26; HTML không có chữ "Thử lại" | Vẽ trạng thái `error-2` (Banner MSG-04 + "Thử lại"), hoặc bỏ dòng 18 |
| 5 | Phải sửa | "Actions" thiếu dòng mở khi chưa đăng nhập → M-F00-01 | AD-UC-07 d1, hướng dẫn §2.1; tệp ghi chú dòng 38–49 không có (chỉ nhắc ở dòng 62, phần thứ 5) | Thêm: Open without session → M-F00-01 (MSG-01) |
| 6 | Nên sửa | Lỗi của ô Tiến độ đặt thành Banner đầu màn, viền lỗi 1px | HTML dòng 610–616, 637; §4: lỗi một ô nhập là Inline error ngay dưới ô; viền 2px | Inline error có "!" dưới ô Tiến độ, viền 2px `colour/error-red` |
| 7 | Nên sửa | Lỗi sở thích không hợp lệ (AD-UC-07 d4 [No]) chưa có câu chữ | Tệp ghi chú dòng 35 chỉ có lỗi nhập 120% | Thêm câu chữ vào "States drawn" (không cần ảnh riêng) |
| 8 | Nên sửa | Toast dạng viên thuốc màu xanh lá, câu khác tệp ghi chú | HTML dòng 680 "✓ Đã cập nhật tiến độ đọc thành công!"; tệp ghi chú dòng 24 "Đã cập nhật tiến độ đọc."; §3 Toast nền `colour/text`, chữ trắng | Dùng `.toast` chuẩn và câu "Đã cập nhật tiến độ đọc." |
| 9 | Nên sửa | Tệp ghi chú số 3 nhắc ngày mượn/đọc nhưng hình không vẽ; đếm "2 cuốn" trong khi AD-UC-07 §3 có 3 mục | Tệp ghi chú dòng 11; HTML dòng 415 | Vẽ ngày (dd/MM/yyyy) hoặc bỏ khỏi tệp ghi chú; dùng 3 mục |
| 10 | Cần nhóm chốt | §3 chưa có thành phần để chọn nhiều chủ đề; Trieu tự đặt "Multi-select chips" | Tệp ghi chú dòng 12; §3 Checkbox chỉ ghi dùng cho S-F02-03, S-F02-01, S-F02-02; FR-03-05 cần chọn chủ đề | Hỏi Linh: dùng Checkbox hay thêm thành phần mới vào §3; ghi Open question |
| 11 | Nên sửa | "Goes to" có giá trị không hợp lệ | Dòng 43, 47, 49: "Opens inline…", "Toggles…", "Retries…" | Ghi "stays" |
| — | Tốt | Dữ liệu mẫu đúng (Principles of Economics 20% → 65%, nhập 120% bị từ chối, Kinh tế và Marketing); không có nút "thêm vào lịch sử"; có câu hỏi mở bắt buộc về câu chữ Empty; Back đúng `screen-transition.md` | | |

## S-F03-06 AI chatbot book search

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Các nút gợi ý câu hỏi (số 3) không phục vụ FR nào | Tệp ghi chú dòng 11 (FR "—"); HTML dòng 339–350; quy tắc 6.2 | Xoá; nếu thấy cần thì ghi Open question |
| 2 | Phải sửa | Câu lỗi FR-03-17 khác mẫu §4, có chi tiết kỹ thuật; tệp ghi chú và HTML ghi khác nhau | §4: "Tìm kiếm bằng AI đang tạm ngưng. Bạn hãy dùng bộ lọc hình thức." HTML dòng 451–453 có "(FR-03-17)" và "không nhận được phản hồi… trong 10 giây"; tệp ghi chú dòng 20 là câu thứ ba | Dùng đúng câu §4; liên kết "dùng bộ lọc hình thức" → S-F03-01 |
| 3 | Phải sửa | Chữ liên kết #1074C3 trên nền lỗi #FDECEA chỉ đạt tương phản 4,26:1 (dưới 4,5:1) | HTML dòng 211–212 trong `.bubble-error` (dòng 204); §6 chỉ cho màu liên kết trên nền trắng / nền trang | Đặt liên kết ngoài khung lỗi, hoặc dùng màu chữ đạt chuẩn |
| 4 | Phải sửa | Chat bubble sai màu | HTML dòng 99–111: tin bạn đọc tô đỏ thương hiệu chữ trắng (màu này chỉ dành cho Primary), tin chatbot nền trắng. §3: bạn đọc nền `info-bg`, chatbot nền `surface`, chữ `colour/text` | Sửa theo §3 |
| 5 | Phải sửa | Ô nhập tin không đúng Message composer | HTML dòng 257–274, 470: nút gửi chỉ có biểu tượng, không có chữ "Gửi" (§1); chữ 13px (§5 cần 16px) | Dùng `.message-composer`: Text input + Primary button "Gửi" |
| 6 | Phải sửa | Thành phần 14 dùng câu đăng nhập tự viết, và đó là modal của Ha | Tệp ghi chú dòng 22: "Đăng nhập bằng thẻ thư viện để tiếp tục trò chuyện cùng thủ thư AI"; MSG-02: "Bạn cần đăng nhập bằng thẻ thư viện để trò chuyện với trợ lý tìm sách." | Bỏ dòng 14 khỏi Elements; giữ trong Actions: gửi tin khi chưa đăng nhập → M-F00-01 (MSG-02) |
| 7 | Phải sửa | "States drawn" không có dòng Empty | Tệp ghi chú dòng 28–32 | Thêm: "Empty: = Default (khung chat trống + ô nhập), hướng dẫn §2.3" |
| 8 | Nên sửa | Thẻ sách có liên kết "Xem vị trí trên kệ" nhưng thực tế mở Book Detail OPAC, dễ nhầm với nhãn chuẩn "Xem vị trí kệ sách" | HTML dòng 399, 415; tệp ghi chú dòng 15; AD-UC-08 c2 | Dùng nhãn liên kết tới sách theo §3 Book card (ví dụ "Xem sách"); nhãn cụ thể hỏi Linh |
| 9 | Nên sửa | Dữ liệu mẫu chưa khớp AD-UC-08 §3 (câu trả lời có 4 thẻ sách) | HTML có 2 thẻ, ảnh có 1 | Vẽ 4 thẻ, tên sách hư cấu |
| 10 | Nên sửa | Lời chào và nhãn "✦ THỦ THƯ AI" viết hoa toàn bộ; hướng dẫn §2.3 nói Default chỉ là khung chat trống + ô nhập | HTML dòng 331, 384 | Bỏ nhãn viết hoa; lời chào bỏ đi hoặc ghi Open question |
| 11 | Nên sửa | Lỗi AI vẽ thành bong bóng trong hội thoại; §4 xếp lỗi hệ thống vào Banner, và bong bóng dễ khiến người xem nghĩ thông báo được lưu vào hội thoại (trái AD-UC-08 Q2) | HTML dòng 449–457 | Dùng Banner error, hoặc ghi Open question |
| 12 | Nên sửa | Chữ khi chờ trả lời không theo MSG-05 | HTML dòng 367 "Thủ thư AI đang tra cứu danh mục sách…"; MSG-05 "Đang tải…" | Dùng "Đang tải…" |
| — | Tốt | Hỏi đăng nhập sau tin nhắn đầu tiên (L8-05); không tìm thấy sách là tin nhắn trả lời, không phải banner; dữ liệu mẫu "đan rổ dưới nước" khớp AD-UC-08; có câu hỏi mở bắt buộc; không vẽ widget nổi; đích điều hướng khớp `screen-transition.md` | | |

## S-F03-07 Book recommendations

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Có liên kết "Đọc trực tuyến →": không có mũi tên nào dẫn tới, và trình đọc online thuộc Won't-have | HTML dòng 378, 456; `screen-transition.md` chỉ có "opens a recommended book" → Book Detail; W0 Table 3 | Xoá; bấm cả dòng Book row mở Book Detail OPAC |
| 2 | Phải sửa | Nhãn lý do gợi ý ("Khớp sở thích: Kinh tế", "Dựa trên sách đã đọc") được vẽ dù hướng dẫn §2.2 ghi "không vẽ nếu nhóm chưa chốt"; không có câu hỏi mở | HTML dòng 343, 362, 376, 441, 454; tệp ghi chú dòng 13 | Xoá; thêm câu hỏi mở "có giải thích vì sao gợi ý không", phương án tạm vẽ "không" |
| 3 | Phải sửa | Nhãn "Xu hướng mượn nhiều" (số 13) và dải ngăn "Gợi ý bổ sung từ xu hướng" (số 11) là phần tự thêm, có câu hỏi mở nhưng vẫn vẽ, lại dùng màu tím ngoài bảng màu | HTML dòng 464, 481; tệp ghi chú dòng 54 | Bỏ nhãn và dải ngăn, xếp sách bổ sung chung danh sách; phương án tạm vẽ "Không gắn nhãn" |
| 4 | Phải sửa | Câu lỗi khác MSG-04, giọng "Vui lòng" khác cách xưng "bạn" ở §1 | HTML dòng 518; MSG-04: "Không tải được trang. Bạn kiểm tra kết nối mạng rồi thử lại." | Dùng đúng MSG-04 |
| 5 | Phải sửa | Thành phần 16 dùng câu tự viết thay MSG-03; "Actions" không có dòng → M-F00-01 | Tệp ghi chú dòng 24, bảng Actions dòng 38–44; MSG-03: "Gợi ý riêng cho bạn cần tài khoản thẻ thư viện. Hãy đăng nhập để xem." | Bỏ số 16 khỏi Elements; thêm Actions: mở khi chưa đăng nhập → M-F00-01 (MSG-03) |
| 6 | Phải sửa | "States drawn" thiếu dòng Empty và Success | Tệp ghi chú dòng 28–34 | Thêm "Not applicable: <lý do>" — ví dụ Empty: chưa có dữ liệu thì hiện sách phổ biến (FR-03-19), nên danh sách không bao giờ trống |
| 7 | Nên sửa | Danh sách có 10 sách (AD-UC-09 Q3) nhưng Default vẽ 3, không ghi rõ | HTML dòng 330–380 | Vẽ đủ 10, hoặc ghi "ảnh hiển thị 3 trong 10" |
| 8 | Nên sửa | Lời mời đặt sở thích vẽ thành Primary button trong khung viền; §3 quy định là Text link | HTML dòng 392 (`.btn-coldstart` nền đỏ) | Đổi thành Text link |
| 9 | Nên sửa | "★ Quét QR: 142 lượt" có ngôi sao, trông như điểm đánh giá; FR-03-19 chỉ dùng lượt quét để xếp hạng | HTML dòng 409; quy tắc 6.2 | Bỏ nhãn, hoặc ghi Open question |
| 10 | Nên sửa | Mỗi dòng sách có liên kết "Xem vị trí trên kệ →", trong khi tệp ghi chú số 6 nói bấm cả dòng mở Book Detail | HTML dòng 346; tệp ghi chú dòng 14, 43 | Cả dòng bấm được (§3 Book row), bỏ liên kết riêng |
| 11 | Nên sửa | Phụ đề "Gợi ý được cá nhân hoá dựa trên lịch sử đọc…" hiện cả ở trạng thái chưa có dữ liệu, mâu thuẫn nội dung | HTML dòng 326, nằm ngoài các section | Chỉ đặt phụ đề trong Default và Topped-up |
| 12 | Nên sửa | Sách mẫu thêm vào là sách và tác giả có thật | "Đắc Nhân Tâm", "Tư Duy Nhanh và Chậm", Kotler, Varian, Blanchard (HTML dòng 402–470) | Dùng tên sách hư cấu (mục 9), báo các bạn còn lại |
| 13 | Cần nhóm chốt | Nút "⚙ Sở thích" (số 2) luôn hiện ở đầu màn | `screen-transition.md` dòng 59 chỉ cho S-F03-07 → S-F03-02 khi "[no reading data yet]"; hướng dẫn §2.2 và `screen-list.md` dòng 167 (c3) ghi "cập nhật sở thích" là hành động chung. Nhãn cũng lệch ("Tùy chỉnh sở thích" / "⚙ Sở thích"), cột FR "—" | Nhóm chốt có cho đi S-F03-02 ở mọi trạng thái không; nếu không, chỉ giữ lời mời ở trạng thái chưa có dữ liệu |
| — | Tốt | Đủ 3 biến thể nội dung (Default, chưa có dữ liệu, bổ sung xu hướng); định nghĩa "xu hướng" (30 ngày, cùng chủ đề) và 10 sách khớp AD-UC-09; Back về menu OPAC đúng | | |

---

## Trieu làm tốt

1. Các quyết định ghi "Team consensus (04/11/2026)" đều khớp đúng mục 6 của AD-UC-07, 08, 09, không có
   quyết định nào bịa — chỉ cần đổi cách ghi.
2. Số trên ảnh đánh số khớp cột `#` ở cả 3 màn; dữ liệu mẫu S-F03-02 dùng đúng.
3. Chủ động loại những thứ không được vẽ: widget chatbot nổi, Reader Dashboard, nút "thêm vào lịch
   sử", chức năng xoá hội thoại.
