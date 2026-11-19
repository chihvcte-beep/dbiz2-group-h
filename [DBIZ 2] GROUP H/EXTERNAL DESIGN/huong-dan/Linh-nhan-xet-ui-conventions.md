# Nhận xét UI Conventions — Linh

| Mục | Nội dung |
|---|---|
| Người nhận | **Linh** |
| Phạm vi | `ui-conventions.md`, `screens/src/tokens.css`, `_template.html`, `components.html`, `screens/img/ui-components.png`, và mục 7 (soát nhất quán 20 wireframe) |
| Đối chiếu với | `huong-dan/Linh-ui-conventions.md`, mẫu `ui-conventions-template.md` của thầy, `screen-list.md`, AD-UC-14, `GROUP-H_UC_FR_COST.xlsx` |
| Ngày soát | 19/11/2026 |

**Cách đọc.** Đường dẫn tính từ thư mục `EXTERNAL DESIGN/`. Cột **Mức**:
**Phải sửa** = trái hướng dẫn hoặc tài liệu chung; **Nên sửa** = chất lượng, nhất quán;
**Cần nhóm chốt** = cần cả nhóm quyết định.

**Tóm tắt.** Bộ khung của Linh chạy tốt và 4 bạn vẽ đã dùng đúng câu chữ chung. Hai việc lớn còn lại:
(1) **mục 7 chưa soát** dù đã đủ 20 wireframe — các lỗi bên dưới ở các bạn khác lẽ ra được bắt ở đây;
(2) mục 3 **thiếu vài thành phần**, khiến người vẽ phải tự đặt tên mới.

---

## Phần bộ quy ước (ui-conventions.md và bộ khung)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Tệp ghi 3 FR mới và "OTP 6 chữ số" **đã đưa vào W1**, nhưng tệp Excel trong kho **chưa có** | `ui-conventions.md` dòng 355 ("Added to … W1_FunctionList, rows 132–137 … on 14/11/2026"), dòng 87 ("FR-04-04 (6-digit code, updated in W1 14/11/2026)"). Đã kiểm `GROUP-H_UC_FR_COST.xlsx`: không có FR-02-22, FR-04-19, FR-04-20; tệp Excel trong kho được lưu lần cuối 08/11 | Nhóm đã nhận 3 FR này (xem dòng 3), nên phải có thật trong W1: đưa bản Excel đã sửa lên kho, hoặc thêm 6 dòng (FE + BE) cho FR-02-22, FR-04-19, FR-04-20 và sửa câu EARS của FR-04-04 thành 6 chữ số |
| 2 | Cần nhóm chốt | §3 chỉ cho báo cáo đánh giá **của người khác**, trong khi AD-UC-14 đã chốt bạn đọc **được** báo cáo đánh giá của chính mình | `ui-conventions.md` dòng 133; `components.html` dòng 225–226; `ACTIVITY DIAGRAM/AD-UC-14.md` dòng 125 ("Decided 2026-11-04 … Yes"). Hoa đã vẽ theo §3 | Nhóm chọn một: giữ AD thì thêm "Báo cáo đánh giá" vào đánh giá của mình (§3 và components); giữ §3 thì sửa câu hỏi 2 của AD-UC-14 |
| 3 | Đã chốt | 3 mã FR mới do Linh đề xuất (FR-02-22, FR-04-19, FR-04-20). **Nhóm đã nhận cả 3 ngày 19/11/2026** | `ui-conventions.md` dòng 353–362 | Ghi vào §7, phần "Closed": "19/11/2026: team accepted FR-02-22, FR-04-19, FR-04-20". Sau đó làm tiếp dòng 1 (W1) và dòng 10 của bảng mục 7 (`screen-list.md`, chi phí) |
| 4 | Phải sửa | §3 thiếu thành phần cho những phần màn hình cần, nên người vẽ tự đặt tên | Không có thành phần **chọn nhiều sở thích đọc** (FR-03-05, S-F03-02): Checkbox (dòng 126) chỉ ghi chọn sách / đăng ẩn danh, Segmented control (dòng 123) chỉ chọn MỘT. Trieu đã tự đặt "Multi-select chips", "Status badge", "Progress bar & label", "Section header". Không có thành phần cho tên sách / tiêu đề mục — Nhi đã hỏi nhưng chưa có trả lời (`notes/S-F01-01-notes.md` dòng 10). `tokens.css` có sẵn `.section-title` (dòng 139), `.text-button` (dòng 177–179) nhưng §3 không có dòng tương ứng | Thêm vào §3 (kèm trạng thái và "Used on"): chọn nhiều sở thích, Section title, Text button, cách hiển thị trạng thái đọc; trả lời câu hỏi của Nhi |
| 5 | Phải sửa | Đã chốt giao diện tiếng Việt nhưng §3, §5 vẫn ghi nhãn tiếng Anh, khác `components.html` | Dòng 114 "Back" (dòng 58 và `_template.html` dòng 35: "Quay lại"); dòng 121 "Show" (components: "Hiện"); dòng 124 "Options Reading, Finished" (dòng 94: "Đang đọc · Đã đọc xong"); dòng 132, 198 "Your book is here" (components: "Sách của bạn ở đây"); dòng 136 "Send" (dòng 55: "Gửi") | Thay bằng đúng nhãn tiếng Việt đã chốt ở §1 |
| 6 | Nên sửa | Bảng tương phản vẫn dùng tên token cũ | Dòng 276–278: "primary #8B0000", "primary-soft #FFEBEE"; từ v0.7 đã đổi thành `colour/brand-red`, `colour/brand-red-soft`. 31 tỉ lệ tương phản tính lại đều đúng | Đổi tên trong bảng; cân nhắc đổi `colour/on-primary` thành `colour/on-brand-red` |
| 7 | Nên sửa | Màu đỏ báo lỗi dùng cho chữ "Xoá đánh giá", trong khi §6 chỉ cho dùng cho lỗi và Destructive button | `tokens.css` dòng 179 (`.text-button.danger`); `components.html` dòng 225; `ui-conventions.md` dòng 235 | Ghi thêm cách dùng này vào dòng 235, hoặc đổi chữ sang màu thường |
| 8 | Nên sửa | `tokens.css` có giá trị chưa ghi ở §6 (29 màu thì khớp 100%) | `--size-target-reader: 44px` (dòng 76), viền 1/2/3px (dòng 77–79), thang `--space-1…12`; Primary khi rê chuột dùng `colour/overlay` (dòng 165) dù §6 chỉ dành overlay cho nền mờ sau modal; `.book-author` dùng cỡ 14px của Staff cho cả Reader (dòng 234) | Ghi các giá trị vào §6, thêm cách dùng overlay khi rê chuột, sửa cỡ chữ tác giả |
| 9 | Nên sửa | Ở khổ 360px, ô đang chọn "Trực tuyến" có vẻ xuống 2 dòng (chưa chắc, mới xem ảnh thu nhỏ) | `img/ui-components.png`, Segmented control "default + selected" | Kiểm lại; nếu đúng thì thêm quy tắc không xuống dòng hoặc giảm đệm, chụp lại ảnh |
| 10 | Nên sửa | Cột "Used on" của §3 chưa đủ | Format label (dòng 129) thiếu S-F03-03, S-F02-03; Shelf location line (dòng 130) thiếu M-F02-03-01; Primary button ghi "all screens" (dòng 115) nhưng S-F04-01 không có Primary | Bổ sung; đổi "all screens" thành "at most one per screen" |
| 11 | Nên sửa | §1 có tiêu đề cho 15 màn hình nhưng chưa có tiêu đề và nhãn nút cho 5 modal | Components dòng 283 "Gỡ đánh giá này?" khác `notes/M-F02-04-01-notes.md` dòng 10 "Gỡ đánh giá?"; nút "Đóng" (`notes/M-F02-03-01-notes.md` dòng 12) không có trong bảng nhãn dòng 35–58 | Thêm tiêu đề và nhãn nút của 5 modal vào §1 |
| 12 | Nên sửa | Vài thành phần trong `components.html` chưa đủ trạng thái | Load more button chỉ có default và focus (dòng 233–234); Book row không có trạng thái vô hiệu; Toast có 2 ô đều "default" (dòng 290–291) | Thêm trạng thái còn thiếu, hoặc ghi "không áp dụng" ở §3 |
| — | Tốt | `_template.html` đạt: chọn trạng thái theo `#` (không có `#` thì hiện default, tên lạ quay về default, hỗ trợ `error-2`, `error-3`), đuôi `-numbered` bật vòng số; có chú thích Screen ID, phiên bản, cách vẽ modal. `components.html` có đủ 31 thành phần, không viết màu trực tiếp | | |

---

## Phần soát nhất quán (mục 7)

| # | Mức | Vấn đề | Bằng chứng | Cách sửa |
|---|---|---|---|---|
| 1 | Phải sửa | Bảng soát nhất quán trống hoàn toàn dù đã đủ 20 wireframe; tệp vẫn ở v0.7 | `ui-conventions.md` dòng 330–351 trống; dòng 9 "Version v0.7 · 14/11/2026"; hướng dẫn dòng 296–305, 391 yêu cầu soát đủ 15 màn và 5 modal | Soát từng màn, điền đủ 8 cột, ghi "Cần sửa: …"; xong thì nâng lên v1.0 |
| 2 | Phải sửa | Ảnh đánh số sai khổ (Reader cần 1080px, Staff 1280px) | Ha: M-F00-01, S-F00-01, S-F00-02 rộng 773px; S-F00-03, S-F02-03, S-F04-01, M-F02-03-01 rộng 1693px. Nhi: S-F01-01, S-F03-01, S-F03-03 rộng 1740px. Trieu: S-F03-02, S-F03-06, S-F03-07 rộng 1740px. Chỉ ảnh của Hoa và S-F01-02 đúng khổ | Ghi Fail cột "Image size correct" |
| 3 | Phải sửa | Không có ảnh riêng cho từng trạng thái, chỉ có ảnh ghép `-states.png`; nhiều tệp ghi chú nhắc tới ảnh không có | Thư mục `img/`; ví dụ `notes/S-F00-01-notes.md` dòng 27, `notes/S-F00-02-notes.md` dòng 29, 33 | Ghi "Cần sửa" cho cả 20 dòng |
| 4 | Phải sửa | HTML của Trieu không dùng bộ khung chung | `src/S-F03-02.html`, `S-F03-06.html`, `S-F03-07.html`: không liên kết `tokens.css`, không có `data-state`, có 8 màu ngoài token (tím #7C3AED, #6D28D9, #5B21B6, #F5F3FF; xám #6B7280, #E5E7EB…) | Ghi Fail cột "Colours only from tokens" |
| 5 | Phải sửa | Ha vẽ bằng draw.io với nút chính xám đen và nền lỗi xám — sai §3, §6 | `src/Ha-wireframe-1.drawio`: 48 ô `fillColor=#1F2937`, không có nền `#8B0000`, không có `#FDECEA` | Ghi Fail cột "Colours only from tokens" cho 7 wireframe của Ha |
| 6 | Phải sửa | Nhi và Hoa chưa nộp tệp nguồn | `src/` chỉ có HTML của Trieu và tệp draw.io của Ha | Ghi "Cần sửa: thiếu nguồn" |
| 7 | Phải sửa | Hai tệp ghi chú thiếu dòng đầu chuẩn | `notes/S-F01-02-notes.md` dòng 3 thiếu Author; `notes/S-F03-01-notes.md` dòng 3 thiếu Frame, phiên bản, Author, tiêu đề khác `screen-list.md` | Ghi "Cần sửa" |
| 8 | Phải sửa | Nhiều tên ở cột Component nằm ngoài §3 | S-F03-06 có 12 tên lạ ("Message bubble", "Chip group", "Result card"…), S-F03-07 có 11, S-F03-02 có 9, S-F03-01 có 5, S-F03-03 có 2, S-F01-02 và S-F01-01 mỗi màn 1 | Tên đúng là đang thiếu ở §3 thì bổ sung §3 (dòng 4 bảng trên); còn lại ghi "Cần sửa: dùng tên chuẩn" |
| 9 | Nên sửa | Tiêu đề màn của Trieu khác bảng tiêu đề §1 | §1 dòng 69–72: "Lịch sử đọc và sở thích", "Trợ lý tìm sách AI", "Sách gợi ý cho bạn"; tệp ghi chú: "Lịch sử đọc & sở thích", "Thủ thư AI tìm sách", "Gợi ý sách cho bạn" | Ghi "Cần sửa" cho Trieu |
| 10 | Phải sửa | 3 FR mới (nhóm đã nhận 19/11/2026) đã dùng trong wireframe nhưng `screen-list.md` chưa cập nhật, chưa tính chi phí | `screen-list.md` dòng 11 (S-F00-02) thiếu FR-04-19; dòng 15–16 thiếu FR-02-22; FR-04-20 không có ở đâu; tệp ghi chú đã dùng (`notes/S-F00-02-notes.md` dòng 16, `notes/S-F00-01-notes.md` dòng 14, 16); `ui-conventions.md` dòng 366 "Left for later" | Báo người giữ `screen-list.md` thêm FR-04-19 vào S-F00-02, FR-02-22 vào S-F02-01 và S-F02-02, FR-04-20 vào mọi màn có trạng thái lỗi tải; báo người giữ W2/W4 tính chi phí và độ ưu tiên |
| 11 | Cần nhóm chốt | Khổ giấy và số nhãn mỗi trang của M-F02-03-01 vẫn để ngỏ, hai nơi vẽ khác nhau | `ui-conventions.md` dòng 144, 367; `components.html` dòng 310 vẽ 3 cột; `notes/M-F02-03-01-notes.md` dòng 39: "A4 portrait, provisional 2 columns × 5 rows" | Nhóm chốt, rồi cập nhật cả hai nơi |

---

## Linh làm tốt

1. Bảng màu lấy từ OPAC có lý do rõ cho từng chỗ thay màu; 31 tỉ lệ tương phản tính lại đều đúng, hai
   màu không đạt đã được thay đúng cách.
2. Bộ khung chạy đúng hướng dẫn: `_template.html` chọn trạng thái bằng `#`, bật số bằng `-numbered`;
   29 màu của `tokens.css` khớp 100% với §6; `components.html` đủ 31 thành phần.
3. Câu chữ chung MSG-01 đến MSG-09 và bảng nhãn nút đã được các bạn vẽ dùng đúng nguyên văn.
