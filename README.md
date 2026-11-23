# Group H Library Core System

Bộ tài liệu phân tích và thiết kế của **Nhóm H, môn DBIZ2**. Sản phẩm là phần bổ sung cho hệ thống tra cứu thư viện hiện có (OPAC, [opac.nlv.gov.vn](https://opac.nlv.gov.vn)), giúp bạn đọc tìm đúng kệ sách, xem bản đồ thư viện, đọc và viết đánh giá sách, quét mã QR trên sách giấy và nhận gợi ý sách phù hợp.

Kho này chỉ chứa tài liệu, chưa có mã nguồn sản phẩm. Các màn hình trong đây là bản vẽ thiết kế (wireframe), dùng làm đầu vào cho phần lập trình ở DBIZ3.

## Trạng thái hiện tại

Cập nhật ngày 23/11/2026.

| Hạng mục | Số lượng | Trạng thái |
|---|---|---|
| Use case và sơ đồ hoạt động | 15 | Draft |
| Màn hình, kèm đặc tả | 15 | Draft |
| Hộp thoại (modal) | 5 | Draft, đặc tả nằm trong tệp của màn hình chứa nó |
| Yêu cầu chức năng (FR) trong tệp Excel | 81 | Đã có đủ, gồm FR-02-23, FR-02-24, FR-02-25, FR-04-21 và nội dung mới của FR-02-07, FR-02-08 (cập nhật 23/11/2026) |
| Giờ công và chi phí | | Must: 252,4 giờ, 68,92 triệu đồng. Must + Should: 345,6 giờ, 93,68 triệu đồng. Toàn bộ phạm vi: 506,6 giờ, 136,98 triệu đồng, **vượt năng lực 360 giờ** |

Việc còn phải làm và người phụ trách được theo dõi tại một nơi duy nhất: [Pending tasks](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/decision-index.md#pending-tasks).

## Phạm vi sản phẩm

Hệ thống có hai nhóm người dùng: **Bạn đọc** (Reader) và **Nhân viên tại thư viện** (On-site Staff).

| Mã | Nhóm chức năng | Người dùng | Use case | Màn hình |
|---|---|---|---|---|
| F-01 | Vị trí sách và bản đồ thư viện | Bạn đọc | UC-01, 02 | S-F01-01, 02 |
| F-02 | Đánh giá sách và mã QR | Bạn đọc, Nhân viên | UC-04, 05, 06, 10, 13, 14 | S-F02-01 đến 04 |
| F-03 | Khám phá sách, lịch sử đọc và gợi ý | Bạn đọc | UC-03, 07, 08, 09, 12 | S-F03-01, 02, 03, 06, 07 |
| F-04 | Đăng nhập, phân quyền và vận hành | Tất cả | UC-11, 15 | S-F00-01 đến 03, S-F04-01 |

Mức ưu tiên của use case:

- **Must:** UC-01, 02, 04, 05, 06, 10, 11, 15
- **Should:** UC-03, 07, 12
- **Could:** UC-08, 09, 13, 14

**Không thuộc phạm vi:** mượn, trả và gia hạn sách; đọc sách trực tuyến ngay trên nền tảng; tìm kiếm theo từ khoá (OPAC đã có); tài khoản bạn đọc trực tuyến và đăng nhập Google; trang quản trị đầy đủ cho thủ thư. Danh sách đầy đủ và lý do nằm ở sheet `W0_Scope`, Bảng 3 của tệp Excel.

## Cấu trúc thư mục

```text
[DBIZ 2] GROUP H/
├── CVCA.pdf                     Quan hệ giá trị giữa các bên
├── Context diagram.pdf          Ranh giới hệ thống
├── Use case diagram.pdf         Sơ đồ use case
├── SEQUENCE DIAGRAM/            Sơ đồ tuần tự, từng luồng
├── GROUP-H_UC_FR_COST.xlsx      Use case, FR, ưu tiên, chi phí
├── ACTIVITY DIAGRAM/
│   ├── activity-index.md        Danh mục sơ đồ hoạt động
│   └── AD-UC-01 … AD-UC-15.md   Mỗi use case một sơ đồ
└── EXTERNAL DESIGN/
    ├── usage-flow.md            Luồng sử dụng
    ├── screen-list.md           Danh sách màn hình và hộp thoại
    ├── screen-transition.md     Sơ đồ chuyển màn hình
    ├── ui-conventions.md        Quy ước giao diện
    ├── decision-index.md        Sổ quyết định và việc còn lại
    └── screens/
        ├── specs/               Đặc tả từng màn hình
        ├── notes/               Ghi chú wireframe
        ├── img/                 Ảnh màn hình và các trạng thái
        └── src/                 Tệp nguồn wireframe
```

## Nên đọc theo thứ tự nào

1. **Hiểu bài toán:** [CVCA](%5BDBIZ%202%5D%20GROUP%20H/CVCA.pdf), [Context diagram](%5BDBIZ%202%5D%20GROUP%20H/Context%20diagram.pdf), [Use case diagram](%5BDBIZ%202%5D%20GROUP%20H/Use%20case%20diagram.pdf).
2. **Nắm phạm vi và yêu cầu:** [GROUP-H_UC_FR_COST.xlsx](%5BDBIZ%202%5D%20GROUP%20H/GROUP-H_UC_FR_COST.xlsx).
3. **Xem nghiệp vụ từng use case:** [activity-index.md](%5BDBIZ%202%5D%20GROUP%20H/ACTIVITY%20DIAGRAM/activity-index.md), rồi mở tệp `AD-UC-xx.md` cần xem.
4. **Xem người dùng đi qua sản phẩm thế nào:** [usage-flow.md](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/usage-flow.md), [screen-list.md](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screen-list.md), [screen-transition.md](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screen-transition.md).
5. **Xem chi tiết màn hình:** [ui-conventions.md](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/ui-conventions.md), rồi đặc tả trong [screens/specs/](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/screens/specs).
6. **Tra lý do của một quyết định:** [decision-index.md](%5BDBIZ%202%5D%20GROUP%20H/EXTERNAL%20DESIGN/decision-index.md), tìm theo mã được trích trong tài liệu, ví dụ `D7` hoặc `L8-01`.

## Quy ước đặt mã

| Mã | Ý nghĩa | Ví dụ |
|---|---|---|
| `UC-nn` | Use case | `UC-04` |
| `FR-<nhóm>-<nn>` | Yêu cầu chức năng | `FR-02-23` |
| `AD-UC-nn` | Sơ đồ hoạt động của một use case | `AD-UC-10` |
| `S-F<nhóm>-<nn>` | Màn hình. `S-F00` là màn hình đăng nhập dùng chung | `S-F01-02` |
| `M-F00-<nn>` | Hộp thoại dùng chung cho nhiều màn hình | `M-F00-01` |
| `M-<màn hình>-<nn>` | Hộp thoại của một màn hình | `M-F02-03-01` |
| `MSG-nn` | Thông báo chuẩn trong `ui-conventions.md` | `MSG-04` |
| `D<n>`, `UI Q<n>`, `L8-<nn>` | Quyết định trong `decision-index.md` | `D12` |

## Quy tắc khi cập nhật tài liệu

- **Đổi quyết định:** thêm một dòng mới có mã mới vào `decision-index.md` để thay dòng cũ. Không sửa yêu cầu trong tài liệu nếu chưa có dòng này.
- **Giá trị giao diện:** màu, cỡ chữ và mẫu câu chỉ định nghĩa một lần trong `ui-conventions.md`. Tệp `screens/src/ui-tokens.css` chép đúng từ mục 6 của tệp đó.
- **Màn hình và trạng thái:** thông báo lỗi, danh sách trống hay xác nhận là trạng thái của màn hình, không tách thành màn hình mới.
- **Mã đã bỏ:** không dùng lại, ví dụ `S-F03-04` và `S-F03-05`.
- **Ngôn ngữ:** tài liệu đặc tả viết bằng tiếng Anh, chữ trên giao diện viết bằng tiếng Việt có dấu.

## Xem sơ đồ và wireframe

- Sơ đồ trong các tệp `.md` viết bằng Mermaid. Sơ đồ hoạt động dùng dạng `swimlane-beta` và đã được kiểm tra hiển thị với Mermaid 12.3.0 trên Chrome. Trình xem dùng phiên bản cũ hơn có thể không vẽ được.
- Tệp `.html` trong `screens/src/` mở trực tiếp bằng trình duyệt.
- Tệp `.drawio` mở bằng [diagrams.net](https://app.diagrams.net).

## Thành viên và phân công

Người soát tài liệu của nhóm là **Chi**. Linh giữ tệp `ui-conventions.md`.

| Thành viên | Đặc tả màn hình phụ trách |
|---|---|
| Ha | S-F00-01, S-F00-02, S-F02-03 |
| Linh | S-F00-03, S-F03-01, S-F04-01 |
| Hoa | S-F02-01, S-F02-02, S-F02-04 |
| Nhi | S-F01-01, S-F01-02, S-F03-03 |
| Trieu | S-F03-02, S-F03-06, S-F03-07 |
