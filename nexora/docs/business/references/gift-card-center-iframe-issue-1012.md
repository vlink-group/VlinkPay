## Salon – Đưa Gift Card Center vào NexoraTouch bằng iframe

**Trạng thái:** Define
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/enhance/1012-gift-card-center-docs/nexora/docs/business/references/gift-card-center-iframe-issue-1012.md)

**Nguồn:** [Ticket #1012](https://github.com/vlink-group/vlink-nexora/issues/1012). Bản lưu nội dung đầy đủ ngày 28 tháng 9 năm 2026; giữ nguyên yêu cầu nguồn, chỉ bổ sung thông tin xuất bản. Đây không phải xác nhận chức năng đã triển khai.

**Mục tiêu:** Cho phép Owner/Staff của salon sử dụng các chức năng cần thiết của Gift Card Center ngay trong NexoraTouch, không mở tab mới hoặc chuyển toàn bộ sang Merchant Portal.

### Hiện trạng

Khi người dùng chọn Gift Card Center trên NexoraTouch, hệ thống thực hiện SSO và mở Merchant Portal trong tab mới.

Luồng hiện tại làm gián đoạn thao tác và khiến người dùng rời khỏi giao diện quản lý salon.

### Kết quả mong muốn

Hiển thị các chức năng cần thiết của Gift Card Center trong vùng nội dung NexoraTouch bằng iframe:

- Giữ nguyên sidebar và header của NexoraTouch.
- Ẩn sidebar, header và navigation của Merchant Portal trong iframe.
- Đăng nhập thông qua ecosystem SSO hiện có.
- Điều hướng giữa các màn hình tiếp tục diễn ra bên trong iframe.
- Không mở tab hoặc cửa sổ mới.

## Cấu trúc menu

    Gift Card Center
    ├── Gift Card
    ├── Membership Card
    ├── Card Management
    ├── Membership Program
    └── Reports

### Hành vi của menu cha

- Chọn **Gift Card Center** sẽ mở rộng hoặc thu gọn danh sách submenu.
- Nếu người dùng truy cập trực tiếp route Gift Card Center mà chưa chọn submenu:
  - Mặc định mở submenu **Gift Card**.
  - Hiển thị màn hình Issue Card.
  - Tự động chọn Product Line là Gift Card.

## 1. Gift Card

Submenu Gift Card sử dụng màn hình **Issue Card** của Merchant Portal.

**UI title:** Issue Card  
**Description:** Issue a card in store and sell it directly to a customer.

### Hành vi

- Mở màn hình Issue Card trong iframe.
- Tự động chọn **Gift Card** tại phần **Select Product Line**.
- Submenu Gift Card được đánh dấu active.
- Người dùng vẫn có thể chuyển sang loại card khác trong màn hình Issue Card nếu có quyền.

### Chức năng

- Chọn hoặc nhập thông tin khách hàng.
- Tìm kiếm và sử dụng lại thông tin khách hàng cũ.
- Thiết kế card, chọn màu nền và hình nền.
- Chọn hoặc tải logo doanh nghiệp.
- Nhập thông tin doanh nghiệp và thông tin liên hệ.
- Thiết lập thời hạn.
- Nhập mệnh giá.
- Cấu hình discount nếu có.
- Chọn phương thức thanh toán.
- Xem trước card.
- Xác nhận phát hành và bán card cho khách.
- Gửi card qua email/SMS nếu luồng hiện tại hỗ trợ.
- Sau khi phát hành thành công, cho phép:
  - Mở chi tiết card.
  - Quay về Card Management.

## 2. Membership Card

Submenu Membership Card sử dụng chung màn hình **Issue Card** của Merchant Portal.

**UI title:** Issue Card  
**Description:** Issue a membership card in store and sell it directly to a customer.

### Hành vi

- Mở màn hình Issue Card trong iframe.
- Tự động chọn **Membership** tại phần **Select Product Line**.
- Submenu Membership Card được đánh dấu active.
- Hiển thị các membership tier/package hiện có để người dùng lựa chọn.
- Người dùng vẫn có thể chuyển sang loại card khác trong màn hình Issue Card nếu có quyền.

### Chức năng

- Chọn membership tier hoặc membership package.
- Chọn hoặc nhập thông tin khách hàng.
- Nhập tên, ngày sinh, email, số điện thoại và địa chỉ theo yêu cầu hiện có.
- Chọn benefit áp dụng.
- Thiết lập thời hạn membership.
- Nhập giá bán.
- Cấu hình discount nếu có.
- Thiết kế card và thông tin thương hiệu.
- Chọn phương thức thanh toán.
- Xem trước và xác nhận phát hành.
- Gửi Membership Card cho khách qua email/SMS nếu luồng hiện tại hỗ trợ.
- Sau khi phát hành thành công, cho phép:
  - Mở chi tiết Membership Card.
  - Quay về Card Management.

## 3. Card Management

**UI title:** Card Management  
**Description:** Manage cards issued in store and sold directly to customers.

Màn hình hiển thị và quản lý các card salon đã phát hành.

### Loại card

- Gift Card.
- Crypto Card.
- Membership Card.
- Promotion Card.
- Discount Card.
- Prepaid Card.

### Chức năng

- Tìm kiếm theo số card hoặc thông tin khách hàng.
- Lọc theo:
  - Loại card.
  - Ngày tạo.
  - Product Status.
  - Card Locked Status.
- Hiển thị:
  - Khách hàng.
  - Email và số điện thoại.
  - Số card.
  - Ngày phát hành.
  - Số dư.
  - Phương thức thanh toán.
  - Trạng thái.
- Xem chi tiết card.
- Khóa hoặc mở khóa card theo quyền.
- Nạp thêm số dư nếu loại card hỗ trợ.
- Thực hiện các thao tác quản lý hiện có theo quyền Owner/Staff.

### Chi tiết card

Màn chi tiết card bao gồm:

- Card Information.
- Card Transaction History.
- Product/Action History.

Tất cả màn chi tiết và thao tác quay lại phải tiếp tục nằm bên trong iframe.

## 4. Membership Program

**UI title:** Membership Program  
**Description:** Configure membership benefits and packages for your customers.

Màn hình gồm hai tab.

### Benefits

- Danh sách benefit.
- Tìm kiếm theo Benefit ID hoặc tên.
- Lọc theo trạng thái.
- Xem chi tiết benefit.
- Bật hoặc tắt benefit.
- Nút **Create New Benefit**.
- Hỗ trợ các Benefit Unit hiện có:
  - Currency.
  - Percentage.
  - Time Used.

### Membership Packages

- Danh sách membership package.
- Tìm kiếm theo Package ID hoặc tên.
- Lọc theo trạng thái.
- Hiển thị:
  - Package ID.
  - Package Name.
  - Price.
  - Currency.
  - Billing Cycle.
  - Benefit Count.
  - Approval Status.
  - Sale Status.
  - Created Date.
- Xem hoặc chỉnh sửa chi tiết package.
- Nút **Create Membership Package**.

### Quy tắc liên kết

- Membership Package chỉ có thể được bán khi đáp ứng trạng thái cho phép của hệ thống hiện tại.
- Sau khi package được tạo và kích hoạt, package phải xuất hiện trong luồng:
  - Membership Card.
  - Issue Card.
  - Select Product Line: Membership.
- Benefit được tạo và kích hoạt phải có thể được chọn khi cấu hình Membership Package hoặc phát hành Membership Card theo nghiệp vụ hiện có.

## 5. Reports

**UI title:** Reports  
**Description:** Review sales, membership activity, card payments, and expiring cards.

Reports bao gồm các màn hình sau.

### Sales Orders

- Danh sách đơn bán hoặc phát hành card.
- Tìm kiếm theo Order ID, card hoặc ngày.
- Lọc theo:
  - Start Date.
  - End Date.
  - Status.
  - Payment Method.
- Hiển thị thông tin đơn hàng, sản phẩm, số card, số lượng, số tiền, trạng thái, phí và người thực hiện.
- Xem chi tiết đơn hàng.
- Export dữ liệu.

### Membership Report

Gồm hai tab:

- Member Card Report.
- Membership Package Report.

Cho phép:

- Tìm kiếm theo số card hoặc package.
- Lọc theo khoảng thời gian.
- Theo dõi:
  - Package.
  - Thời hạn.
  - Giá bán.
  - Platform fee.
  - Discount.
  - Doanh thu.

### Gift Card Payment History

- Hiển thị các giao dịch:
  - Redeem.
  - Purchase.
  - Top-up.
  - Reload.
  - Refund.
- Tìm kiếm theo card holder, số card hoặc transaction.
- Lọc theo:
  - Start Date.
  - End Date.
  - Transaction Type.
  - Status.
- Hiển thị:
  - Transaction Date.
  - Type.
  - Amount.
  - Product.
  - Card Information.
  - Status.
  - Transaction ID.
  - Balance After.
  - Người thực hiện.
- Export dữ liệu.

### Crypto Payment History

- Chỉ hiển thị khi merchant có quyền hoặc được bật tính năng Crypto.
- Lọc theo khoảng thời gian.
- Hiển thị:
  - Date/Time.
  - Crypto.
  - Invoice.
  - Net Received.
  - Fee.
  - Status.
  - Transaction ID.
  - Người thực hiện.
- Cho phép xem chi tiết giao dịch nếu luồng hiện tại hỗ trợ.

### Expiring Cards

Gồm hai tab:

- Card List.
- Automatic Sending.

Cho phép:

- Tìm kiếm theo số card hoặc khách hàng.
- Lọc theo Card Type.
- Lọc theo thời gian sắp hết hạn.
- Hiển thị:
  - Loại card.
  - Khách hàng.
  - Số card.
  - Số dư.
  - Ngày hết hạn.
  - Trạng thái.
  - Trạng thái gửi email.
- Gửi email/SMS reminder riêng lẻ.
- Gửi reminder hàng loạt.
- Cấu hình tự động gửi thông báo sắp hết hạn.

## Quy tắc active menu

- Chọn **Gift Card**:
  - Active submenu Gift Card.
  - Mở Issue Card.
  - Product Line mặc định là Gift Card.

- Chọn **Membership Card**:
  - Active submenu Membership Card.
  - Mở Issue Card.
  - Product Line mặc định là Membership.

- Chọn **Card Management**:
  - Active submenu Card Management.
  - Mở danh sách card đã phát hành.

- Chọn **Membership Program**:
  - Active submenu Membership Program.
  - Mở Membership Program với tab mặc định theo cấu hình đã thống nhất.

- Chọn **Reports**:
  - Active submenu Reports.
  - Mở màn hình báo cáo mặc định hoặc tab báo cáo được lưu trong URL.

- Trạng thái active phải được xác định từ route của NexoraTouch, không phụ thuộc hoàn toàn vào URL nội bộ của iframe.
- Khi người dùng điều hướng bên trong iframe, submenu tương ứng vẫn giữ trạng thái active.
- Khi reload hoặc sử dụng Back/Forward, hệ thống phải khôi phục đúng submenu, màn hình iframe và loại card mặc định.

## Yêu cầu iframe và SSO

- Giữ sidebar và header của NexoraTouch.
- Merchant Portal phải chạy ở embedded mode.
- Không hiển thị sidebar, header hoặc navigation của Merchant Portal.
- Không mở tab hoặc cửa sổ mới.
- Sử dụng ecosystem SSO hiện có.
- Một phiên SSO hợp lệ phải được sử dụng lại khi chuyển giữa các submenu.
- Token hoặc thông tin xác thực không được đưa vào log hoặc hiển thị trên giao diện.
- Chỉ cho phép iframe tải từ Merchant Portal URL đã được cấu hình và xác thực.
- Điều hướng tạo mới, chi tiết và quay lại danh sách phải tiếp tục nằm trong iframe.

## Phân quyền

- Owner được truy cập các chức năng theo quyền hiện có.
- Staff chỉ nhìn thấy và truy cập những menu/màn hình được cấp quyền.
- Người dùng không có quyền không được truy cập màn hình bằng URL trực tiếp.
- Crypto Payment History chỉ hiển thị khi merchant có tính năng và quyền phù hợp.
- Quyền phải được kiểm tra ở Merchant Portal, không chỉ ẩn menu phía NexoraTouch.

## Loading và xử lý lỗi

- Hiển thị loading khi:
  - Đang lấy Merchant Portal configuration.
  - Đang thực hiện SSO.
  - Đang tải iframe.
- Khi SSO hoặc iframe thất bại:
  - Hiển thị thông báo lỗi trong NexoraTouch.
  - Cung cấp nút Retry.
  - Không tự động mở Merchant Portal trong tab mới.
- Khi phiên đăng nhập hết hạn:
  - Thực hiện lại SSO nếu có thể.
  - Nếu không thể, hiển thị lỗi và yêu cầu người dùng thử lại.
- Nếu một route không được phép nhúng, hiển thị lỗi thay vì trang trắng.

## Responsive

- Hoạt động trên desktop và mobile.
- Iframe sử dụng toàn bộ chiều rộng vùng nội dung.
- Không tạo cuộn ngang cho toàn bộ NexoraTouch.
- Các bảng bên trong iframe giữ hành vi responsive hiện có.
- Mobile menu phải đóng sau khi người dùng chọn submenu.
- Khi quay lại mobile menu, submenu hiện tại vẫn được đánh dấu active.

## Ngoài phạm vi

- Các menu khác của Merchant Portal như Homepage, Dashboard, Marketing Tools, Staff Management, Payment Settings và Sign Out.
- Xây dựng màn Customers/Card Holders riêng.
- Thay đổi nghiệp vụ phát hành, thanh toán hoặc tính phí hiện có.
- Đồng bộ hoặc xây dựng lại dữ liệu Gift Card trong NexoraTouch.
- Thay thế các API hiện có của Merchant Portal.
- Thay đổi nội dung hoặc nghiệp vụ của các màn hình được nhúng, trừ các điều chỉnh cần thiết để hỗ trợ embedded mode.

## Tiêu chí hoàn thành

- Gift Card Center hiển thị đúng năm submenu theo thứ tự:
  1. Gift Card.
  2. Membership Card.
  3. Card Management.
  4. Membership Program.
  5. Reports.
- Chọn Gift Card Center mặc định mở Gift Card nếu chưa có submenu được chọn.
- Gift Card và Membership Card sử dụng chung màn hình Issue Card.
- Gift Card tự động chọn Product Line Gift Card.
- Membership Card tự động chọn Product Line Membership.
- Người dùng vẫn có thể chuyển Product Line trong Issue Card nếu có quyền.
- Card Management hiển thị danh sách card đã phát hành và mở được chi tiết card.
- Membership Program hiển thị Benefits và Membership Packages.
- Create New Benefit hoạt động trong iframe.
- Create Membership Package hoạt động trong iframe.
- Reports truy cập được:
  - Sales Orders.
  - Membership Report.
  - Gift Card Payment History.
  - Crypto Payment History theo quyền.
  - Expiring Cards.
- Tất cả màn hình trong phạm vi được hiển thị trong iframe.
- Merchant Portal không hiển thị sidebar/header trong embedded mode.
- Không có thao tác nào trong phạm vi tự động mở tab mới.
- Owner/Staff chỉ truy cập được chức năng theo quyền.
- Điều hướng danh sách, tạo mới, chi tiết và quay lại hoạt động trong iframe.
- Reload và Back/Forward khôi phục đúng submenu và màn hình.
- Loading, lỗi và Retry hoạt động đúng.
- Giao diện sử dụng được trên desktop và mobile.
