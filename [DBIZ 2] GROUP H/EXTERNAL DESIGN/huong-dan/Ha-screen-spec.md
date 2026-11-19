# Screen Spec — phần việc của Ha

| Mục | Nội dung |
|---|---|
| Người thực hiện | **Ha** |
| Đọc kèm | `huong-dan/screen-spec-chung.md` (luật chung, cách điền, lời nhắc AI, checklist) |
| Phiên bản | v1.0 · 19/11/2026 |
| Soát chéo | Bạn soát spec của **Hoa** và 2 spec Linh viết từ wireframe của bạn (S-F00-03, S-F04-01); **Hoa** soát spec của bạn |

## 1. Spec bạn viết

| # | Tệp | Màn hình | Actor · khổ | Priority | AD | Modal viết bên trong |
|---|---|---|---|---|---|---|
| 1 | `screen-spec-S-F00-01.md` | Sign in: library card number | Reader · 360px | Must | AD-UC-11 (+ d1 của AD-UC-04, 07, 08, 09, 12, 14 cho modal) | **M-F00-01** Sign in to continue? |
| 2 | `screen-spec-S-F00-02.md` | Verify email OTP | Reader · 360px | Must | AD-UC-11 | — |
| 3 | `screen-spec-S-F02-03.md` | QR code label printing | On-site Staff · 1280px | Must | AD-UC-10 | **M-F02-03-01** QR label sheet preview |

FR của từng màn: cột "UC / FR" của dòng tương ứng trong `screen-list.md`, cộng **FR-04-19** và
**FR-04-20** cho S-F00-02, **FR-04-20** cho S-F00-01.

## 2. Việc phải làm trước (hạn 21/11)

1. **Xuất ảnh riêng cho cả 7 wireframe bạn đã vẽ**, kể cả S-F00-03 và S-F04-01 (Linh viết spec):
   tên ảnh đúng như phần "States drawn" trong tệp ghi chú (ví dụ `S-F00-02-error-5.png`,
   `S-F00-02-success-numbered.png`).
2. **Ảnh đánh số đang sai khổ:** màn Reader đang rộng 773px (cần 1080px), màn Staff 1693px
   (cần 1280px). Xuất lại theo bước 5–6 của hướng dẫn wireframe.
3. Nguồn vẽ của bạn là `screens/src/Ha-wireframe-1.drawio`. Xuất từ draw.io theo đúng khổ trên
   (File › Export as › PNG, đặt chiều rộng); không chỉnh ảnh bằng tay.

## 3. Lưu ý riêng từng spec

### S-F00-01 (kèm M-F00-01)
- M-F00-01 là modal dùng chung cho 7 màn của người khác: viết **đầy đủ** ở mục 3.1 của spec này,
  gồm **3 biến thể câu chữ** (chung FR-04-08, chatbot FR-03-18, gợi ý sách FR-03-21) và quy tắc quay
  lại L8-01. Các bạn khác sẽ chỉ trỏ tới `screen-spec-S-F00-01.md §3.1`.
- Báo nhóm ngay khi mục 3.1 xong.
- Mục 6 phải có quy tắc: **một thông báo chung cho mọi lần từ chối**, không cho biết số thẻ có tồn
  tại hay không (AD-UC-11 câu hỏi 4). Validation số thẻ: 7 chữ số, giữ số 0 đầu (ui-conventions §2).
- Success không phải trang riêng: chuyển sang S-F00-02.

### S-F00-02
- Màn nhiều lỗi nhất: dòng Error ở mục 4 phải liệt kê đủ 5 biến thể đã vẽ (sai mã còn lượt, lần sai
  thứ 5, hết hạn/đã dùng, không gửi được mã, lỗi mạng), mỗi biến thể kèm FR.
- Validation mã: 6 chữ số (FR-04-04).
- Câu hỏi mở cần giữ: có hiện email che bớt không; Cancel thì việc đang chờ đăng nhập xử lý thế nào.

### S-F02-03 (kèm M-F02-03-01)
- Câu hỏi **Q3 (Blocking)** và **Q4** ở mục 6 của tệp chung phải được nhóm chốt trước khi đổi
  Status sang Reviewed.
- Mục 4: Validation "Hãy chọn ít nhất 1 sách bản giấy." (FR-02-17); một phần / toàn bộ sách chưa có mã
  QR (FR-02-18) là hai biến thể khác nhau.
- Nút In trong modal mở hộp thoại in của trình duyệt — ghi `Browser print dialog (exit)`, không phải
  Screen ID.

## 4. Khi soát spec của Linh (S-F00-03, S-F04-01)

Kiểm tra spec có **đúng với wireframe bạn vẽ** không: số `#`, câu chữ tiếng Việt, trạng thái, đích
điều hướng. Ghi nhận xét trên pull request, không sửa hộ.
