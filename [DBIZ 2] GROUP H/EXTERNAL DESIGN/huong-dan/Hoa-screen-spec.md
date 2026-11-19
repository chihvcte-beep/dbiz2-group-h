# Screen Spec — phần việc của Hoa

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Hoa** |
| Đọc kèm | `huong-dan/screen-spec-chung.md` (luật chung, cách điền, lời nhắc AI, checklist) |
| Phiên bản | v1.0 · 19/11/2026 |
| Soát chéo | Bạn soát spec của **Ha**; **Ha** soát spec của bạn |

## 1. Spec bạn viết

| # | Tệp | Màn hình | Actor · khổ | Priority | AD | Modal viết bên trong |
|---|---|---|---|---|---|---|
| 1 | `screen-spec-S-F02-01.md` | Book reviews | Reader · 360px | Must | AD-UC-05, AD-UC-04, AD-UC-14 | **M-F02-01-01** Delete your review?, **M-F02-01-02** Report this review? |
| 2 | `screen-spec-S-F02-02.md` | Book information and reviews (QR landing page) | Reader · 360px | Must | AD-UC-06, AD-UC-04 | — (mở M-F02-01-01, trỏ về spec S-F02-01) |
| 3 | `screen-spec-S-F02-04.md` | Reported reviews | On-site Staff · 1280px | Could | AD-UC-13 | **M-F02-04-01** Remove this review? |

Bạn có 3 modal, nhiều nhất nhóm — viết theo mục 4.2 của tệp chung. S-F02-01 và S-F02-02 mở
**M-F00-01** khi chưa đăng nhập → trỏ về `screen-spec-S-F00-01.md §3.1`.

FR của từng màn: cột "UC / FR" trong `screen-list.md`, cộng **FR-02-22** (đăng ẩn danh) cho
S-F02-01 và S-F02-02, **FR-04-20** nếu có trạng thái lỗi mạng.

## 2. Việc phải làm trước (hạn 21/11)

1. **Xuất ảnh riêng** cho 3 màn và 3 modal theo tên ở phần "States drawn" của tệp ghi chú. Khổ ảnh
   đánh số của bạn đã đúng (1080px / 1280px).
2. Đưa mã nguồn wireframe vào `screens/src/` (hiện chưa có).

## 3. Lưu ý riêng từng spec

### S-F02-01 (kèm M-F02-01-01, M-F02-01-02)
- Câu hỏi **Q1** đã chốt (19/11/2026): đánh giá của chính mình **không** có nút Báo cáo; Report chỉ
  trên đánh giá của người khác. Ghi thành quy tắc ở mục 6, nguồn `AD-UC-14 Q2`.
- Khung viết/sửa/xoá đánh giá viết **một lần ở đây**, đặt tên thành phần ổn định; S-F02-02 dùng lại
  đúng tên đó (L8-07).
- Mục 6: 10 đánh giá mỗi trang (AD-UC-05 mục 3); một người được viết nhiều đánh giá cho một sách;
  Edit/Delete/Report là phần Could; chưa đăng nhập → M-F00-01.
- M-F02-01-02 **không có ô lý do** (L8-10). Nút xác nhận ghi đúng nghĩa, không dùng Có/Không.
- Còn mở: đường dẫn tới quy định viết đánh giá; "Xem thêm đánh giá" nối thêm hay thay trang.

### S-F02-02
- Ghi "same review panel as S-F02-01" và dùng **cùng tên thành phần**; **không có Report** (L8-07).
- Câu hỏi **Q2** (có phân trang đánh giá không) phải chốt trước.
- Liên kết "View this book on the OPAC" → `Existing OPAC Book Detail (exit)` (L8-08).
- Lỗi "Book cannot be found" khi mã QR không gắn với sách nào (FR-02-16).
- Còn mở: nút Back làm gì khi màn được mở thẳng từ camera.

### S-F02-04 (kèm M-F02-04-01)
- Hai hành động: gỡ đánh giá (qua modal, FR-02-10) và bỏ qua báo cáo (FR-02-20); hai thông báo thành
  công khác nhau.
- Không có ô lý do báo cáo (không có dữ liệu trong FR) — giữ ở mục 9 nếu nhóm chưa chốt.
- Bố cục hai cột (danh sách + chi tiết) là phương án tạm — ghi ở mục 9.
