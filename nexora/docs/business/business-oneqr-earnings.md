## Business OneQR — Kiếm tiền từ QR, đối soát và nhận tiền

**Cập nhật lần cuối:** 24 tháng 9 năm 2026

**Đối tượng đọc:** Chủ doanh nghiệp (Business Owner), quản trị viên vận hành, người phụ trách sản phẩm, BA, QA, bộ phận hỗ trợ, đội phát triển

**Trạng thái:** Đang rà soát

**Bản chia sẻ:** [Tài liệu trên GitHub](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/business-oneqr-earnings.md)

### Tổng quan

Business OneQR — Kiếm tiền từ QR, đối soát và nhận tiền giúp doanh nghiệp tạo và kiểm soát thu nhập từ hoạt động quảng cáo hoặc giao dịch đủ điều kiện được QR giới thiệu. Hệ thống ghi nhận thu nhập, đối soát, giữ dự phòng hoàn tiền/tranh chấp, khấu trừ nghĩa vụ thu hồi và chi phần đủ điều kiện vào ví VlinkPay liên kết SSO của Business. Admin vận hành cấu hình thời gian đối soát, chính sách dự phòng, loại tiền nhận và tỷ lệ từng loại; Business Owner bật/tắt kiếm tiền, theo dõi nguồn thu và đối chiếu tiền thực nhận.

**Phạm vi và mức độ chốt:** Phạm vi và quyết định nghiệp vụ đã được ghi nhận; các thông số chưa chốt và phụ thuộc tích hợp được nêu tại cuối tài liệu.

**Nhu cầu chính:** Là Business Owner, tôi muốn bật kiếm tiền cho OneQR, theo dõi thu nhập và đối soát, rồi nhận tiền vào ví VlinkPay của tài khoản Business, để biết QR tạo ra thu nhập từ đâu và số tiền thực tế tôi nhận được.

#### Phạm vi áp dụng

**Trong phạm vi:** đăng ký/bật/tắt kiếm tiền; kế thừa KYB và yêu cầu thuế; ghi nhận nguồn và thu nhập trực tiếp của Business; đối soát; trích giữ, sử dụng và giải phóng khoản dự phòng hoàn tiền/tranh chấp; lịch sử; Admin cấu hình loại tiền nhận và tỷ lệ từng loại; chi trả vào ví VlinkPay SSO theo phân bổ; khấu trừ khoản đã trả cần thu hồi, chuyển phần chưa bù hết sang thu nhập các kỳ sau.

**Ngoài phạm vi:** Personal; Sponsor Override và cấp Sponsor; nạp Ads Credit; xây Campaign Manager, Discovery, bộ lọc ngành hoặc hệ thống KYB mới; mua voucher trả trước; rút tiền từ VlinkPay về ngân hàng. Các hệ thống campaign, discovery, xác minh và ví là phần liên quan được tích hợp.

#### Quyết định đã chốt và thứ tự ưu tiên

| Nội dung | Quyết định áp dụng |
| :--- | :--- |
| Chủ thể | Chỉ Business; Business Owner quản lý kiếm tiền và xem thu nhập của doanh nghiệp trong phạm vi này. |
| Nguồn chính sách | Dùng **Chính sách Ads/Referral ngày 21 tháng 9 năm 2026** (mã phiên bản: ONEQR-ADS-REF-REV-2026-09-21-v1), bản mới nhất có mã phiên bản trong bộ HTML. Không trộn tỷ lệ 70% của chính sách ngày 20/09 hoặc tỷ lệ minh họa từ các prototype khác vào bản này. |
| Xác minh | Kế thừa KYB hiện có và yêu cầu thuế áp dụng cho Business; hiển thị các điều kiện còn thiếu. Không xây lại KYB trong story. |
| Nơi nhận tiền | Ví VlinkPay của tài khoản Business, xác định qua liên kết SSO được hệ thống xác nhận. Quyết định này thay phần chọn phương thức nhận tiền tổng quát trong HTML. |
| Loại tiền nhận | Admin vận hành cấu hình một hoặc nhiều loại tiền VlinkPay hỗ trợ và tỷ lệ mỗi loại; tổng bằng 100%. Phân bổ trên giá trị đủ chi sau dự phòng và khấu trừ. Business Owner chỉ xem; danh sách tiền và tỷ lệ thực tế chưa được chốt. |
| Đối soát và kỳ chi | Thời gian đối soát mặc định **14 ngày**, áp dụng cả click quảng cáo và thưởng dịch vụ. **Admin vận hành hệ thống cấu hình số ngày**; Business Owner không được sửa. Hết thời gian và không có hold mới phân bổ dự phòng/khả dụng; xét chi thứ Ba tại 00:00 America/Chicago, số dư đủ chi sau dự phòng và khấu trừ tối thiểu $25. |
| Dự phòng hoàn tiền/tranh chấp | Giữ lại một phần Publisher Share sau đối soát trên Nexora, chưa chuyển phần này vào ví VlinkPay. Admin vận hành cấu hình tỷ lệ, thời hạn và phạm vi Business/nhóm rủi ro áp dụng; công khai cho Owner. Đã chọn cơ chế, chưa chốt tỷ lệ và số ngày cụ thể. |
| Thu hồi sau payout | Ưu tiên dùng dự phòng còn lại được phép sử dụng của cùng Business, rồi thu nhập khả dụng chưa chi; chỉ phần thiếu mới bù vào thu nhập các kỳ sau. Mọi lần sử dụng đều liên kết khoản phải thu hồi và không thu trùng. |
| Sponsor | Không xây luồng Sponsor. Phần Publisher Share của Business vẫn theo chính sách mới; không tự cộng phần Sponsor vào thu nhập Business vì story không triển khai Sponsor. |

### Khái niệm chính

| Thuật ngữ | Ý nghĩa |
| :--- | :--- |
| Chủ QR / QR Host / Publisher | Business sở hữu QR hoặc nguồn truy cập hợp lệ dẫn khách đến hoạt động đủ điều kiện. |
| Nhà quảng cáo / Advertiser | Doanh nghiệp trả phí theo campaign; có thể là Business khác với chủ QR. |
| Publisher Share | Phần thu nhập trực tiếp của chủ QR từ phí quảng cáo/giao dịch hợp lệ, không phải toàn bộ giá trị dịch vụ khách thanh toán. |
| Thu nhập chờ đối soát | Khoản đã ghi nhận nhưng chưa đủ điều kiện chi trả. |
| Thu nhập khả dụng | Phần đã qua đối soát, không nằm trong dự phòng hoặc hold và chưa đưa vào một đợt chi trả; có thể dùng bù khoản cần thu hồi trước khi chi. |
| Khoản dự phòng / Reserve | Một phần thu nhập được trích giữ theo chính sách để xử lý hoàn tiền/tranh chấp. Có nguồn, số tiền còn lại và ngày dự kiến giải phóng; chưa ở ví VlinkPay và không phải phí mất đi. |
| Hold do tranh chấp | Tạm giữ khoản cụ thể đang cần kiểm tra; khác với tỷ lệ dự phòng định kỳ. Chưa có kết luận thì chưa ghi là khoản thu hồi cuối cùng. |
| Khoản cần thu hồi | Phần thưởng đã trả nhưng được xác nhận mất điều kiện hưởng; bù từ dự phòng hợp lệ, thu nhập khả dụng hoặc thu nhập tương lai. |
| Giá trị đủ chi | Phần khả dụng còn lại sau xử lý nghĩa vụ thu hồi, không bao gồm dự phòng/hold; xét ngưỡng $25 trước khi phân bổ loại tiền. |
| Phân bổ loại tiền nhận | Chia giá trị đủ chi theo tỷ lệ Admin cấu hình, tổng 100%; khác tỷ lệ Publisher Share và tỷ lệ dự phòng. |
| Số tiền thực nhận | Số đơn vị từng loại tiền thực tế được VlinkPay xác nhận ghi có, sau quy đổi và phí nếu có; không cộng trực tiếp số đơn vị của các loại tiền khác nhau. |
| Ví VlinkPay SSO | Ví nhận tiền thuộc đúng tài khoản Business đã liên kết; không suy ví nhận chỉ từ email hoặc địa chỉ ví nhập tự do. |

### Vai trò người dùng

| Vai trò | Trách nhiệm |
| :--- | :--- |
| Chủ doanh nghiệp (Business Owner) | Đồng ý điều khoản, hoàn thiện điều kiện, bật/tắt kiếm tiền và kiểm tra thu nhập/payout của doanh nghiệp. |
| Khách quét QR | Tạo hoạt động có nguồn được ghi nhận; không cần biết cơ chế chia tiền để sử dụng tiện ích. |
| Nexora Operations / Support | Admin được phân quyền cấu hình đối soát, dự phòng, loại tiền nhận và tỷ lệ phân bổ; vận hành xử lý xét duyệt, hold, gian lận, điều chỉnh và khiếu nại theo quyền. Support không mặc nhiên có quyền sửa cấu hình tiền. Không xây toàn bộ portal Admin trong story này. |
| VlinkPay | Xác nhận ví nhận, các loại tiền được hỗ trợ và kết quả ghi có từng phần theo tích hợp SSO/payout. |

### Luồng nghiệp vụ đầu cuối

#### Luồng: Đăng ký và bật/tắt kiếm tiền

**Người thực hiện chính:** Business Owner.

**Điểm bắt đầu:** Owner mở mục kiếm tiền trong OneQR.

**Kết quả:** Business đủ điều kiện có thể chủ động bật kiếm tiền; trạng thái và bước cần hoàn thiện rõ ràng.

**Nhu cầu người dùng:**

- **Là** Business Owner, **tôi muốn** xem điều kiện tham gia và sử dụng kết quả KYB hiện có **để** hoàn thiện hồ sơ mà không làm lại bước đã được chấp thuận.
- **Là** Business Owner, **tôi muốn** chủ động bật/tắt kiếm tiền và thấy ảnh hưởng tới khoản đã ghi nhận, **để** kiểm soát việc tham gia mà vẫn theo dõi được quyền lợi còn lại.
- **Là** Business Owner, **tôi muốn** thấy lý do và cách bổ sung khi hồ sơ chưa đủ hoặc bị từ chối, **để** hoàn thiện điều kiện tham gia.

| Bước | Người thực hiện | Hành động | Phản hồi hệ thống | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Owner | Mở OneQR → Kiếm tiền. | Hiển thị Business, trạng thái tham gia, chính sách và điều kiện còn thiếu. | Chỉ Business trong quyền Owner. |
| 2 | Owner / hệ thống | Kiểm tra KYB, thông tin thuế, quyền sở hữu nguồn QR, điều kiện bảo mật và liên kết ví. | Kế thừa kết quả xác minh; dẫn tới luồng hiện có nếu cần bổ sung. SSO đăng nhập thành công không tự được coi là ví đủ điều kiện nhận tiền. | Dùng luồng xác minh hiện có. |
| 3 | Owner | Đọc và chủ động đồng ý điều khoản. | Hiển thị cả tỷ lệ/thời hạn dự phòng, ngày giải phóng dự kiến và thứ tự xử lý thu hồi. Ghi nhận người chấp thuận, thời điểm và phiên bản chính sách; ô đồng ý không được chọn sẵn. | Owner chủ động chấp thuận. |
| 4 | Nexora / Owner | Xét điều kiện; Owner bật khi đủ điều kiện. | Hiển thị đã bật, chờ xét hoặc cần bổ sung/từ chối cùng lý do phù hợp. | Chưa đủ điều kiện thì chưa bật. |
| 5 | Owner | Tắt kiếm tiền. | Không ẩn Nearby/Search hoặc làm mất tiện ích OneQR; giữ các khoản thưởng đã khóa hợp lệ để xử lý theo chính sách đã ghi nhận. | Không mất quyền lợi đã khóa hợp lệ. |

```mermaid
flowchart TD
    A([Owner mở kiếm tiền]) --> B[Kiểm tra điều kiện]
    B --> C{Đã đủ hồ sơ?}
    C -- Chưa --> D[Hiển thị phần còn thiếu]
    D --> B
    C -- Đủ --> E[Chấp thuận điều khoản]
    E --> F[Xét điều kiện tham gia]
    F --> G{Được phép bật?}
    G -- Chưa --> D
    G -- Có --> H[Owner bật kiếm tiền]
    H --> I([Ghi nhận hoạt động mới])
```

#### Luồng: Ghi nhận nguồn và đối soát thu nhập

**Người thực hiện chính:** Business Owner theo dõi kết quả; khách tạo hoạt động, hệ thống đối soát.

**Điểm bắt đầu:** Khách từ OneQR của Business tạo hoạt động đủ điều kiện.

**Kết quả:** Thu nhập đúng nguồn, đúng chính sách và truy được lý do của mỗi thay đổi.

**Nhu cầu người dùng:**

- **Là** Business Owner, **tôi muốn** biết hoạt động nào từ QR tạo thu nhập và trạng thái từng khoản, **để** đánh giá hiệu quả QR và dự kiến tiền được nhận.
- **Là** Business Owner, **tôi muốn** thấy lý do khoản thu bị giữ, loại hoặc điều chỉnh **để** đối chiếu được kết quả.

| Bước | Người thực hiện | Hành động | Phản hồi hệ thống | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Khách | Quét QR, khám phá và mở quảng cáo/deal phù hợp. | Giữ nguồn Business trong hành trình; scan và mở menu không tự tạo tiền. | Scan không tự tạo tiền. |
| 2 | Hệ thống | Kiểm tra hoạt động, campaign, nguồn, quyền hưởng và gian lận. | Loại hoạt động trùng/không hợp lệ; không tạo thu nhập nếu không có nguồn hợp lệ của Business. | Không ghi nhận trùng. |
| 3 | Hệ thống | Với dịch vụ, khóa nguồn khi booking/order được xác nhận. | Giữ nguồn và phiên bản chính sách của giao dịch; quét QR khác sau đó không thay nguồn đã khóa. Booking chưa hoàn tất chưa tạo thưởng dịch vụ. | Nguồn đã khóa không đổi. |
| 4 | Hệ thống | 💰 Ghi nhận Publisher Share khi đủ điều kiện. | Tạo khoản chờ đối soát gắn hoạt động, campaign, nguồn và cách tính; chưa ghi có ví VlinkPay. | Chưa phải tiền trong ví. |
| 5 | Hệ thống / vận hành | 💰 Đối soát, phân bổ hoặc điều chỉnh khoản thu. | Khoản hợp lệ được phân bổ thành dự phòng và phần khả dụng theo chính sách. Khoản sai có lý do và bút toán điều chỉnh, không sửa/xóa lịch sử gốc. | Giữ lịch sử gốc. |
| 6 | Owner | Xem tổng quan và chi tiết. | Phân biệt hoạt động, khoản chờ, dự phòng, khả dụng, hold, đã chi và điều chỉnh; chỉ hiển thị dữ liệu thuộc Business, không lộ hồ sơ khách/hóa đơn ngoài quyền. | Dữ liệu trong quyền Business. |

```mermaid
flowchart TD
    A([Khách đến từ QR]) --> B[Hoạt động có nguồn]
    B --> C{Đủ điều kiện hưởng?}
    C -- Không --> D([Không tạo thu nhập])
    C -- Có --> E[💰 Ghi thu nhập chờ]
    E --> F[Đối soát hoạt động]
    F --> G{Kết quả đối soát}
    G -- Hợp lệ --> H([💰 Phân bổ khoản thu])
    G -- Cần kiểm tra --> I[Giữ khoản thu]
    I --> F
    G -- Không hợp lệ --> J[💰 Ghi khoản điều chỉnh]
```

#### Luồng: Dự phòng, khấu trừ và nhận tiền vào ví VlinkPay

**Người thực hiện chính:** Business Owner.

**Điểm bắt đầu:** Khoản thu hoàn tất đối soát, phát sinh hoàn tiền/tranh chấp, dự phòng đến hạn giải phóng hoặc đến kỳ xét chi trả.

**Kết quả:** Có khoản dự phòng để giảm rủi ro hoàn tiền/tranh chấp sau payout; Owner thấy rõ tiền đang giữ, ngày giải phóng, khoản khấu trừ và tiền thực nhận vào đúng ví Business.

**Nhu cầu người dùng:**

- **Là** Business Owner, **tôi muốn** nhận khoản đủ điều kiện vào ví VlinkPay SSO của doanh nghiệp và xem lịch sử, **để** đối chiếu thu nhập Nexora với tiền trong ví.
- **Là** Business Owner, **tôi muốn** biết mình nhận bằng loại tiền nào, tỷ lệ mỗi loại, giá trị phân bổ, tỷ giá/phí và số đơn vị thực nhận **để** đối chiếu với ví.
- **Là** Business Owner, **tôi muốn** biết số tiền được giữ dự phòng, lý do, tỷ lệ và ngày dự kiến giải phóng **để** chủ động theo dõi khoản mình sẽ nhận.
- **Là** Business Owner, **tôi muốn** khoản dự phòng còn lại được giải phóng khi hết hạn và đủ điều kiện, **để** số tiền này được xét chi mà không bị trích dự phòng lần nữa.
- **Là** Business Owner, **tôi muốn** xem rõ khoản thưởng bị điều chỉnh, phần dự phòng đã sử dụng, khoản khấu trừ và số còn phải bù **để** đối chiếu thu nhập thực nhận.
- **Là** Business Owner, **tôi muốn** thấy kết quả từng phần khi chuyển tiền thất bại hoặc chưa rõ kết quả, **để** biết phần đã nhận và phần cần xử lý mà không bị trả trùng.

| Bước | Người thực hiện | Hành động | Phản hồi hệ thống | Ghi chú |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Hệ thống | 💰 Phân bổ khoản thu mới hoàn tất đối soát. | Theo chính sách đã lưu cho khoản thu, trích một phần làm dự phòng và chuyển phần còn lại thành khả dụng. Ghi thời điểm bắt đầu giữ và ngày dự kiến giải phóng; chỉ trích một lần. | Trích dự phòng một lần. |
| 2 | Hệ thống / vận hành | 💰 Xét hoàn tiền/tranh chấp và điều chỉnh khi có kết luận. | Với tranh chấp chưa kết luận, giữ phần liên quan và hiển thị lý do. Khi đã xác nhận mất điều kiện hưởng, tách phần chưa trả để đảo trực tiếp và phần đã trả cần thu hồi; không tính cùng một khoản hai lần. | Hold chưa phải thu hồi cuối cùng. |
| 3 | Hệ thống | 💰 Xử lý phần đã trả cần thu hồi. | Dùng dự phòng còn lại được phép sử dụng của cùng Business trước, rồi thu nhập khả dụng chưa chi. Phần thiếu ghi công nợ để bù kỳ sau; vận hành theo dõi số tiền/thời gian tồn đọng. Mỗi lần sử dụng dự phòng/khấu trừ truy được khoản điều chỉnh gốc. | Không tự trừ ví VlinkPay. |
| 4 | Hệ thống | 💰 Giải phóng dự phòng đến hạn. | Sau khi xử lý nghĩa vụ đã xác nhận, chuyển phần còn lại không bị hold sang khả dụng. Nếu còn tranh chấp, giữ phần liên quan với lý do; phần không liên quan vẫn được xét giải phóng. | Chỉ giữ phần còn tranh chấp. |
| 5 | Hệ thống | Xét kỳ thứ Ba lúc 00:00 America/Chicago. | Lấy số dư khả dụng hiện tại đã phản ánh phần chuyển kỳ, thu nhập mới sau trích dự phòng, dự phòng đã giải phóng và các lần bù; xử lý nghĩa vụ còn thiếu, không cộng/trừ lại bút toán đã ghi. Không tính phần dự phòng còn giữ, hold, đã chi hoặc đang chuyển. Kiểm tra hồ sơ và ví nhận. | Không cộng/trừ lại khoản đã ghi. |
| 6 | Hệ thống | Kiểm tra số đủ chi. | Đạt tối thiểu $25 thì đưa vào kỳ chi; thấp hơn thì giữ sang kỳ sau. Không trích dự phòng lại trên số dư chuyển kỳ hoặc khoản dự phòng vừa giải phóng. | Xét ngưỡng trên tổng USD. |
| 7 | Hệ thống | Phân bổ giá trị đủ chi theo loại tiền nhận. | Chọn chính sách có hiệu lực khi tạo payout, tổng tỷ lệ 100%; kiểm tra ví Business nhận được các loại tiền đó. Lưu phiên bản, tỷ lệ, giá trị USD của từng phần, tỷ giá/thời điểm quy đổi, phí và số đơn vị dự kiến. Thiếu căn cứ quy đổi hoặc cấu hình hợp lệ thì giữ chờ với lý do, không tự chọn loại tiền thay thế. | Chốt chính sách theo payout. |
| 8 | Hệ thống / VlinkPay | 💰 Chuyển từng phần vào ví Business liên kết SSO. | Mỗi phần có loại tiền, số đơn vị, trạng thái và tham chiếu riêng, liên kết cùng payout. Không cho số tiền đã phân bổ tham gia payout khác; không trích dự phòng lại. | Mỗi phần có tham chiếu riêng. |
| 9 | VlinkPay / Nexora | 💰 Xác nhận ghi có từng phần. | Chỉ phần đã xác nhận ghi có mới là đã nhận. Một phần thành công thì payout là đã trả một phần; tất cả thành công mới là đã trả. Đối chiếu phần chưa rõ trước khi thử lại; chỉ thử lại phần xác nhận chưa chi, không chuyển lại phần thành công. | Không thử lại phần đã nhận. |
| 10 | Owner | Xem chi tiết thu nhập và kỳ chi. | Hiển thị thu nhập mới, dự phòng mới giữ/còn lại/đã dùng/đã giải phóng, ngày giải phóng, khấu trừ, giá trị đủ chi, công nợ còn lại; từng loại tiền có tỷ lệ, quy đổi/phí, số đơn vị dự kiến/thực nhận và giao dịch ví. | Không cộng số đơn vị khác loại. |

```mermaid
flowchart TD
    A([Thu nhập qua đối soát]) --> B[💰 Tách dự phòng và khả dụng]
    B --> C{Có nghĩa vụ thu hồi?}
    C -- Có --> D[💰 Dùng dự phòng hợp lệ]
    D --> E[💰 Bù tiếp từ khả dụng]
    E --> F[Ghi công nợ còn thiếu]
    C -- Không --> G[Xét dự phòng đến hạn]
    F --> G
    G --> H[💰 Giải phóng phần đủ điều kiện]
    H --> I[Đến kỳ xét chi]
    I --> J{Còn đủ 25 USD?}
    J -- Chưa --> K([Chuyển tiếp kỳ sau])
    J -- Có --> L{Hồ sơ và ví hợp lệ?}
    L -- Không --> M([Giữ chờ xử lý])
    L -- Có --> R{Phân bổ và quy đổi hợp lệ?}
    R -- Không --> M
    R -- Có --> S[💰 Phân bổ từng loại tiền]
    S --> N[💰 Chuyển từng phần vào VlinkPay]
    N --> O{Kết quả ghi có}
    O -- Tất cả thành công --> P([Đã trả])
    O -- Một phần thành công --> T[Đã trả một phần]
    O -- Chưa xác nhận --> Q[Đối chiếu phần chưa trả]
    T --> Q
    Q --> U{Xác nhận chưa chi?}
    U -- Có --> V[Thử lại phần chưa chi]
    V --> N
    U -- Chưa rõ --> W([Chờ kết quả đối chiếu])
    U -- Đã chi --> O
```

**Phân biệt hai thời hạn:** đối soát mặc định 14 ngày vẫn giữ nguyên. Thời hạn dự phòng là thời gian giữ thêm cho phần được trích sau đối soát, không khóa tiếp toàn bộ thu nhập. Mỗi phần dự phòng có ngày bắt đầu và ngày giải phóng riêng; hết hạn không đồng nghĩa tự chuyển ví ngay, mà chuyển sang khả dụng để xét kỳ chi.

**Ví dụ minh họa, không phải cấu hình đã chốt:** $100 Publisher Share qua đối soát, tỷ lệ dự phòng 20%, giữ thêm 30 ngày → giữ $20 dự phòng, $80 khả dụng để xét payout. Sau 30 ngày, nếu không có hold/thu hồi, $20 chuyển thành khả dụng và cộng với số khác để xét ngưỡng $25; không bị trích thêm 20% lần nữa.

### Cấu hình và quản trị

- **Là** Admin vận hành hệ thống, **tôi muốn** cấu hình số ngày đối soát, mặc định 14 ngày cho cả click quảng cáo và thưởng dịch vụ, **để** điều chỉnh thời gian chờ theo chính sách vận hành.
- **Là** Admin vận hành hệ thống, **tôi muốn** cấu hình tỷ lệ trích dự phòng, số ngày giữ thêm sau đối soát, nhóm Business áp dụng và thời điểm hiệu lực, **để** kiểm soát rủi ro hoàn tiền/tranh chấp mà vẫn công khai ngày dự kiến nhận tiền.
- **Là** Admin vận hành hệ thống, **tôi muốn** chọn loại tiền Business nhận qua VlinkPay và tỷ lệ của từng loại, xem trước phân bổ và đặt ngày hiệu lực, **để** quản lý chính sách chi trả thống nhất.
- **Là** người vận hành, **tôi muốn** thấy công nợ chưa bù theo Business, số tiền và thời gian tồn đọng, **để** xử lý khoản có nguy cơ không thu hồi được thay vì chờ thu nhập tương lai vô thời hạn.
- **Là** người vận hành được phân quyền, **tôi muốn** quản lý phiên bản chính sách, ngưỡng/kỳ chi và lý do hold **để** xử lý nhất quán.
- **Là** người vận hành, **tôi muốn** tra cứu cùng một hoạt động và giao dịch ví qua các lần ghi nhận, điều chỉnh và chi trả **để** xử lý khiếu nại mà không sửa lịch sử.
- Thay đổi chính sách không tự tính lại giao dịch đã khóa theo phiên bản cũ. Các màn hình quản trị đầy đủ thuộc phần triển khai liên quan, không mặc định nằm trong FE Business của story.

**Cấu hình số ngày đối soát:** mặc định 14 ngày ở cấp hệ thống. Chỉ Admin vận hành có quyền mới được thay đổi; lưu người sửa, giá trị trước/sau và thời điểm có hiệu lực. Khoản thu mới lưu số ngày và ngày dự kiến đủ điều kiện theo cấu hình hiệu lực khi ghi nhận; khoản đã ghi nhận giữ thời hạn cũ. FE Business đọc và hiển thị thời hạn từ hệ thống, không hardcode 14 ngày. Chức năng cấu hình phía Admin là yêu cầu phụ thuộc cần triển khai hoặc xác nhận có sẵn ở hệ thống vận hành.

**Cấu hình dự phòng:** Admin vận hành cấu hình tỷ lệ trên Publisher Share của Business, thời gian giữ thêm sau đối soát, phạm vi Business/nhóm rủi ro và ngày hiệu lực. Không tính tỷ lệ trên toàn bộ doanh thu dịch vụ hoặc tiền nạp Ads. Lưu phiên bản chính sách với từng khoản thu khi ghi nhận; thay đổi chỉ tác động khoản thu mới. Business Owner được xem tỷ lệ, thời hạn, điều kiện sử dụng/giải phóng và điều khoản áp dụng, nhưng không được sửa. Giảm/tắt chính sách cho khoản mới không tự giải phóng khoản cũ; khoản cũ tiếp tục theo lịch đã lưu. Mọi sửa đổi, hold hoặc xử lý thủ công có lý do và lịch sử người thực hiện. Tỷ lệ/thời hạn cụ thể chưa được user chốt, không mặc định lấy 20%/30 ngày từ ví dụ.

#### Cấu hình loại tiền nhận và tỷ lệ phân bổ

Đây là cấu hình phía Admin vận hành cho payout Business, không phải lựa chọn phương thức rút tiền của Owner. Nơi nhận vẫn là ví VlinkPay SSO của đúng Business.

| Trường/chức năng | Yêu cầu |
| :--- | :--- |
| Loại tiền nhận | Chọn một hoặc nhiều loại từ danh mục VlinkPay hỗ trợ cho chương trình; dùng mã định danh rõ ràng, không nhập tên tùy ý hoặc chọn trùng. Danh mục thực tế cần xác nhận qua tích hợp. |
| Tỷ lệ mỗi loại | Mỗi loại được chọn có tỷ lệ lớn hơn 0 và không vượt 100%; tổng phải đúng 100%. Nhận một loại thì tỷ lệ là 100%; bỏ một loại phải phân bổ lại phần còn lại trước khi áp dụng. |
| Căn cứ phân bổ | Giá trị đủ chi bằng USD sau dự phòng, hold và khấu trừ; xét ngưỡng $25 trên tổng này trước khi chia. Không áp ngưỡng $25 riêng cho từng loại và không tính phần trăm trên doanh thu gốc. |
| Phạm vi và hiệu lực | Cấu hình cho chương trình Business, có ngày/giờ hiệu lực và phiên bản. Nếu hỗ trợ nhiều nhóm Business, phải xác định phạm vi và thứ tự ưu tiên để mỗi payout chỉ áp dụng một chính sách. |
| Xem trước và kiểm tra | Admin nhập giá trị đủ chi mẫu để xem tỷ lệ/tổng phân bổ, quy đổi/phí nếu đã có dữ liệu. Không cho áp dụng cấu hình thiếu loại tiền, sai tổng, tỷ lệ không hợp lệ hoặc loại tiền không được hỗ trợ; nêu lỗi cụ thể. |
| Quyền và lịch sử | Chỉ Admin vận hành được phân quyền được sửa/áp dụng; lưu người thao tác, lý do, giá trị trước/sau và hiệu lực. Owner chỉ xem chính sách áp dụng và lịch sử payout. |

**Thời điểm áp dụng:** khác chính sách đối soát/dự phòng lưu theo khoản thu, cấu hình loại tiền được chốt khi tạo payout. Payout mới lấy bản đang hiệu lực; payout đã tạo giữ bản đã chốt, kể cả khi thử lại phần thất bại. Đổi cấu hình không đổi khoản đã nhận hoặc tự chia lại phần chưa trả của payout cũ.

**Quy đổi và phí:** phân bổ giá trị USD trước, sau đó xác định số đơn vị từng loại theo tỷ giá, thời điểm chốt, độ chính xác và phí được tích hợp xác nhận. Lưu đủ căn cứ để đối chiếu; không mặc định các loại tiền có tỷ giá 1:1. Quy tắc phí, làm tròn, phần lẻ và hiệu lực báo giá cần chốt trước phát hành; không làm mất phần lẻ hoặc tự trừ phí không có chính sách. Nếu báo giá hết hiệu lực khi thử lại, phần chưa trả cần xử lý theo quy tắc quy đổi đã được duyệt, lưu lịch sử thay đổi và không đổi giá trị phân bổ/tỷ lệ gốc hay phần đã trả.

**Cấu hình hoặc khả năng nhận chưa đủ:** nếu chưa có chính sách hợp lệ, giữ payout chờ cấu hình với lý do; không tự đặt một loại tiền mặc định. Nếu một loại bị ngừng hỗ trợ hoặc ví không nhận được, giữ phần chưa chi liên quan để vận hành xử lý; không tự chuyển tỷ lệ sang loại khác hoặc đánh dấu đã trả. Việc chờ payout không tự tắt ghi nhận thu nhập hay làm mất số dư.

### Vòng đời trạng thái

Các nhãn dưới đây là trạng thái nghiệp vụ cần biểu đạt, chưa phải tên trạng thái API đã được xác nhận. Trạng thái bật kiếm tiền, khoản thu, phần dự phòng và payout được theo dõi riêng. Một khoản thu có thể đồng thời có phần khả dụng và phần dự phòng; không gộp cả khoản thành một trạng thái khiến Owner không biết số được chi.

#### Trạng thái tham gia kiếm tiền

| Trạng thái hiện tại | Tác nhân chuyển trạng thái | Trạng thái mới | Ghi chú |
| :--- | :--- | :--- | :--- |
| Chưa đủ điều kiện | Hoàn thiện và được xác nhận hồ sơ/điều kiện | Đủ điều kiện | Kế thừa KYB hiện có. |
| Đủ điều kiện | Owner bật kiếm tiền | Đang bật | Đã chấp thuận điều khoản. |
| Đang bật | Owner tắt kiếm tiền | Đã tắt | Khoản đã khóa vẫn được xử lý. |
| Đã tắt | Owner bật lại khi còn đủ điều kiện | Đang bật | Không cộng hồi tố click lúc tắt. |
| Đang bật | Mất điều kiện tham gia | Chưa đủ điều kiện | Hiển thị lý do và bước bổ sung. |

```mermaid
stateDiagram-v2
    state "Chưa đủ điều kiện" as Ineligible
    state "Đủ điều kiện" as Eligible
    state "Đang bật" as Enabled
    state "Đã tắt" as Disabled
    [*] --> Ineligible : Bắt đầu xét điều kiện
    Ineligible --> Eligible : Hoàn tất điều kiện
    Eligible --> Enabled : Owner bật
    Enabled --> Disabled : Owner tắt
    Disabled --> Enabled : Bật lại khi đủ điều kiện
    Enabled --> Ineligible : Mất điều kiện tham gia
```

#### Trạng thái khoản thu

| Trạng thái hiện tại | Tác nhân chuyển trạng thái | Trạng thái mới | Ghi chú |
| :--- | :--- | :--- | :--- |
| Chưa ghi nhận | Hoạt động đủ điều kiện hưởng | Chờ đối soát | Lưu nguồn và chính sách áp dụng. |
| Chờ đối soát | Hoàn tất đối soát hợp lệ | Phân bổ dự phòng và khả dụng | 💰 Trích một lần; hai phần được theo dõi riêng. |
| Chờ đối soát / Khả dụng | Phát hiện vấn đề cần xác minh | Bị giữ | Có lý do hold. |
| Bị giữ | Gỡ hold | Chờ đối soát / Khả dụng | Trở về đúng giai đoạn trước hold. |
| Chờ đối soát / Khả dụng / Bị giữ | Xác nhận mất quyền hưởng | Điều chỉnh một phần/toàn bộ | 💰 Có bút toán liên kết; không xóa lịch sử. |
| Khả dụng | Bù nghĩa vụ thu hồi được xác nhận | Khả dụng còn lại | 💰 Chỉ dùng phần chưa phân bổ cho payout. |
| Phần dự phòng | Đến hạn, đủ điều kiện giải phóng | Khả dụng | 💰 Không trích dự phòng lại. |
| Khả dụng | Đạt điều kiện kỳ chi | Đã phân bổ cho kỳ chi | Theo dõi kết quả ở payout; không đưa cùng tiền vào hai kỳ chi. |

```mermaid
stateDiagram-v2
    state "Chờ đối soát" as Pending
    state "Phân bổ theo chính sách" as Allocation
    state "Phần dự phòng" as ReservedPart
    state "Khả dụng" as Available
    state "Bị giữ" as Held
    state "Đã phân bổ cho kỳ chi" as Allocated
    state "Đã điều chỉnh toàn bộ" as Reversed
    [*] --> Pending : Ghi nhận hoạt động hợp lệ
    Pending --> Allocation : Đối soát đạt
    Allocation --> Available : 💰 Phần không trích dự phòng
    Allocation --> ReservedPart : 💰 Phần trích dự phòng
    Pending --> Held : Cần kiểm tra
    Available --> Held : Có vấn đề cần kiểm tra
    Held --> Pending : Gỡ hold cho phần chưa phân bổ
    Held --> Available : Gỡ hold cho phần đã phân bổ
    ReservedPart --> Available : 💰 Giải phóng phần đến hạn
    Pending --> Reversed : 💰 Đảo toàn bộ
    Available --> Reversed : 💰 Đảo toàn bộ
    Held --> Reversed : Xác nhận không hợp lệ
    Pending --> Pending : Điều chỉnh một phần
    Available --> Available : Điều chỉnh hoặc bù một phần
    Available --> Allocated : 💰 Phân bổ khoản đủ chi
```

#### Trạng thái phần dự phòng

| Trạng thái hiện tại | Tác nhân chuyển trạng thái | Trạng thái mới | Ghi chú |
| :--- | :--- | :--- | :--- |
| Chưa trích | Khoản thu qua đối soát | Đang giữ dự phòng | 💰 Lưu số tiền và lịch giải phóng. |
| Đang giữ dự phòng | Dùng bù nghĩa vụ hoặc giải phóng một phần | Đang giữ phần còn lại | 💰 Theo dõi riêng số đã dùng và đã giải phóng. |
| Đang giữ dự phòng | Phát sinh tranh chấp | Bị giữ do tranh chấp | Chỉ giữ phần liên quan. |
| Bị giữ do tranh chấp | Gỡ hold | Tiếp tục xét lịch dự phòng | Không khởi động lại thời hạn giữ. |
| Đang giữ / Bị giữ do tranh chấp | Sử dụng/đảo hết phần còn lại theo kết luận, hoặc giải phóng hết khi đủ điều kiện | Đã xử lý hết | 💰 Số còn giữ bằng 0; lưu lịch sử. |

```mermaid
stateDiagram-v2
    state "Đang giữ dự phòng" as Reserved
    state "Bị giữ do tranh chấp" as Disputed
    state "Đã xử lý hết" as Closed
    [*] --> Reserved : 💰 Trích giữ một lần
    Reserved --> Reserved : 💰 Dùng hoặc giải phóng một phần
    Reserved --> Disputed : Giữ phần đang tranh chấp
    Disputed --> Reserved : Gỡ hold và xét lịch giải phóng
    Disputed --> Closed : Xác nhận dùng hết phần còn lại
    Reserved --> Closed : 💰 Dùng hoặc giải phóng hết
    Closed --> [*] : Kết thúc theo dõi số dư
```

#### Trạng thái kỳ chi trả

| Trạng thái hiện tại | Tác nhân chuyển trạng thái | Trạng thái mới | Ghi chú |
| :--- | :--- | :--- | :--- |
| Chờ cấu hình hoặc điều kiện | Có chính sách, quy đổi và ví hợp lệ | Đang chuyển | Chốt phiên bản phân bổ cho payout. |
| Đang chuyển / Cần đối chiếu | Xác nhận tất cả phần ghi có | Đã trả | 💰 Chỉ xác nhận tiền nhận từ VlinkPay. |
| Đang chuyển / Cần đối chiếu | Xác nhận một số phần ghi có | Đã trả một phần | Phần chưa trả có trạng thái riêng. |
| Đang chuyển | Chưa phần nào xác nhận ghi có, còn kết quả chưa rõ | Cần đối chiếu | Timeout không có nghĩa chưa chi. |
| Đang chuyển / Cần đối chiếu | Xác nhận tất cả phần thất bại | Thất bại | Chưa có phần đã nhận. |
| Thất bại | Thử lại sau khi xác nhận chưa chi | Đang chuyển | Không đổi tỷ lệ đã chốt. |
| Đã trả một phần | Đối chiếu/thử lại phần còn lại | Đã trả một phần / Đã trả | Không gửi lại phần đã ghi có. |
| Đã trả | Hoàn/đảo sau chi được xác nhận | Giữ lịch sử đã trả | Tạo khoản cần thu hồi riêng. |

```mermaid
stateDiagram-v2
    state "Chờ cấu hình hoặc điều kiện" as Waiting
    state "Đang chuyển" as Sending
    state "Cần đối chiếu" as Reconciling
    state "Thất bại" as Failed
    state "Đã trả một phần" as Partial
    state "Đã trả" as Paid
    [*] --> Waiting : Xét khoản đủ chi
    Waiting --> Sending : Đủ điều kiện và chốt phân bổ
    Sending --> Paid : 💰 Xác nhận ghi có tất cả
    Sending --> Partial : 💰 Xác nhận ghi có một phần
    Sending --> Reconciling : Chưa nhận tiền, kết quả chưa rõ
    Sending --> Failed : Tất cả phần xác nhận thất bại
    Reconciling --> Paid : 💰 Xác nhận tất cả đã ghi có
    Reconciling --> Partial : 💰 Xác nhận một số phần đã ghi có
    Reconciling --> Failed : Xác nhận tất cả thất bại
    Failed --> Sending : 💰 Thử lại không chi trùng
    Partial --> Partial : Đối chiếu hoặc thử lại phần chưa trả
    Partial --> Paid : Xác nhận đủ các phần còn lại
    Paid --> Paid : Hoàn sau chi tạo khoản thu hồi riêng
```

#### Trạng thái phần chi theo loại tiền

| Trạng thái hiện tại | Tác nhân chuyển trạng thái | Trạng thái mới | Ghi chú |
| :--- | :--- | :--- | :--- |
| Chưa gửi | Đủ điều kiện gửi yêu cầu chi | Đang chuyển | 💰 Mỗi phần có tham chiếu riêng. |
| Đang chuyển / Cần đối chiếu | VlinkPay xác nhận ghi có | Đã trả | 💰 Lưu số đơn vị thực nhận. |
| Đang chuyển | Kết quả chưa rõ | Cần đối chiếu | Chưa được thử lại. |
| Đang chuyển / Cần đối chiếu | Xác nhận không chi và yêu cầu đã thất bại | Thất bại | Giữ phần tiền chờ xử lý. |
| Thất bại | Thử lại hợp lệ | Đang chuyển | 💰 Không gửi lại phần khác đã thành công. |

```mermaid
stateDiagram-v2
    state "Đang chuyển" as Sending
    state "Cần đối chiếu" as Reconciling
    state "Thất bại" as Failed
    state "Đã trả" as Paid
    [*] --> Sending : 💰 Gửi phần chi hợp lệ
    Sending --> Reconciling : Kết quả chưa rõ
    Sending --> Failed : Xác nhận không chi
    Sending --> Paid : 💰 Xác nhận ghi có
    Reconciling --> Failed : Xác nhận không chi
    Reconciling --> Paid : 💰 Xác nhận ghi có
    Failed --> Sending : 💰 Thử lại không trả trùng
    Paid --> [*] : Hoàn tất phần chi
```

#### Trạng thái khoản cần thu hồi

| Trạng thái hiện tại | Tác nhân chuyển trạng thái | Trạng thái mới | Ghi chú |
| :--- | :--- | :--- | :--- |
| Chưa có nghĩa vụ xác nhận | Kết luận phần đã trả mất điều kiện hưởng | Chưa bù đủ | Không tạo công nợ chỉ từ khiếu nại chưa kết luận. |
| Chưa bù đủ | Dùng dự phòng hợp lệ hoặc thu nhập khả dụng | Đã bù một phần / Đã bù đủ | 💰 Ưu tiên dự phòng, rồi khả dụng; phần thiếu chuyển tiếp. |
| Đã bù một phần | Có thu nhập đủ điều kiện tiếp theo | Đã bù một phần / Đã bù đủ | 💰 Không thu lại số đã bù. |
| Chưa bù đủ / Đã bù một phần / Đã bù đủ | Quyết định thu hồi được hủy hoặc đính chính | Hủy / Điều chỉnh nghĩa vụ | 💰 Hoàn nguyên đúng nguồn khi cần; giữ dấu vết gốc. |

```mermaid
stateDiagram-v2
    state "Chưa bù đủ" as Outstanding
    state "Đã bù một phần" as Partial
    state "Đã bù đủ" as Settled
    state "Đã hủy nghĩa vụ" as Cancelled
    [*] --> Outstanding : Xác nhận cần thu hồi
    Outstanding --> Partial : Bù một phần nghĩa vụ
    Outstanding --> Settled : Bù đủ nghĩa vụ
    Partial --> Partial : Bù thêm nhưng còn thiếu
    Partial --> Settled : Bù đủ phần còn lại
    Outstanding --> Outstanding : Đính chính nghĩa vụ còn thiếu
    Partial --> Outstanding : Đính chính và đối chiếu lại
    Settled --> Outstanding : Đính chính còn nghĩa vụ
    Outstanding --> Cancelled : Hủy quyết định thu hồi
    Partial --> Cancelled : Hủy và hoàn nguyên
    Settled --> Cancelled : Hủy và hoàn nguyên
    Cancelled --> [*] : Hoàn tất xử lý hủy
```

### Quy tắc nghiệp vụ

1. **Quyền và nguồn tiền:** thu nhập, consent, điều chỉnh và payout thuộc đúng Business. Không gộp hoặc bù chéo với Personal, Business khác, tiền tip hoặc Ads Credit.
2. **Bật kiếm tiền là tùy chọn:** không yêu cầu Business phải mua quảng cáo hoặc giới thiệu thêm tài khoản mới để nhận thu nhập trực tiếp. Scan, mở menu, xem danh sách và impression không tự tạo tiền.
3. **Hoạt động được hưởng:** phải có nguồn QR hợp lệ, campaign đủ điều kiện/ngân sách, Business có quyền hưởng và hoạt động vượt kiểm tra trùng lặp/gian lận. Nội dung Internal của chính chủ QR và click Public organic không tạo Publisher Share từ CPC.
4. **Bộ lọc bảo vệ:** quảng cáo trả phí cũng không được vượt bộ lọc đối thủ trong phiên OneQR doanh nghiệp. Story nhận kết quả phân phối hợp lệ từ phần discovery/campaign liên quan.
5. **Nguồn giao dịch:** với dịch vụ, kế thừa mẫu nguồn hợp lệ cuối trong 30 ngày trước khi khóa booking/order và tối đa 60 ngày từ khóa tới hoàn tất/thanh toán. Đây là cửa sổ nguồn dịch vụ, khác cửa sổ chống click trùng và thời gian đối soát.
6. **Tắt kiếm tiền:** không xóa thưởng đã khóa hợp lệ hoặc công nợ còn thiếu; tiếp tục đối soát và xử lý hoàn/đảo theo chính sách gốc. Dự phòng không được giải phóng sớm chỉ vì Owner tắt kiếm tiền; vẫn giải phóng đúng lịch khi đủ điều kiện, kể cả Business không còn thu nhập mới. Click phát sinh lúc tắt không được cộng hồi tố sau khi bật lại.
7. **Đối soát:** thời gian chờ mặc định **14 ngày**, dùng chung cho click quảng cáo và thưởng dịch vụ; Admin vận hành hệ thống cấu hình số ngày. Thời gian tính từ lúc khoản thu đủ điều kiện được ghi nhận chờ đối soát: click sau xác nhận hợp lệ, dịch vụ sau khi đã hoàn tất và thanh toán quyết toán được xác nhận. Đổi cấu hình chỉ áp dụng cho khoản ghi nhận mới; không đổi thời hạn của khoản đã ghi nhận. Hết thời gian chờ không tự giải phóng hold hoặc bỏ qua điều kiện khác.
8. **💰 Kỳ chi:** thứ Ba, mốc 00:00 America/Chicago; phần khả dụng còn lại sau trích dự phòng và bù nghĩa vụ thu hồi phải đạt $25. Dự phòng đến hạn được cộng vào khả dụng một lần, không trích dự phòng lại. Ngày hết đối soát hoặc giải phóng dự phòng không phải cam kết tiền về ví ngay.
9. **💰 Ví nhận:** dùng ví VlinkPay liên kết SSO của tài khoản Business. Hiển thị ví đủ để Owner nhận biết; hệ thống xác nhận quyền sở hữu và điều kiện nhận tiền. Chưa xác định được ví thì giữ khoản chi và báo lý do, không chuyển sang một tài khoản suy đoán.
10. **💰 Hoàn/đảo phần chưa trả:** khi xác nhận mất điều kiện hưởng, xác định phần thưởng phải điều chỉnh theo giao dịch gốc. Đảo phần chưa chi liên quan trước, gồm dự phòng của chính khoản thu và phần khả dụng chưa chi. Không vừa đảo phần này vừa ghi cùng số tiền thành công nợ phải thu hồi. Hoàn một phần chỉ điều chỉnh phần thưởng tương ứng, không thu hồi toàn bộ giá trị hóa đơn của khách.
11. **💰 Hoàn/đảo phần đã trả:** giữ lịch sử payout; chỉ phần nghĩa vụ còn thiếu sau khi xử lý phần chưa chi mới là khoản cần thu hồi. Dùng dự phòng còn lại được phép sử dụng của cùng Business trước, sau đó thu nhập khả dụng chưa chi; phần thiếu mới chuyển sang thu nhập đủ điều kiện các kỳ sau. Mỗi lần bù có số tiền, lý do, giao dịch gốc, nguồn bù, kỳ bù và số còn thiếu. Không tự trừ lại số dư ví VlinkPay đã nhận tiền hoặc dùng số đã phân bổ vào payout đang chuyển mà chưa đối chiếu kết quả.
12. **Không ghi nhận trùng:** gửi lại sự kiện, xác nhận ví hoặc thao tác kiểm tra trạng thái không được tạo thêm thu nhập, lần trích/sử dụng/giải phóng dự phòng, khoản thu hồi, khấu trừ hoặc payout cho cùng nghĩa vụ.
13. **💰 Trích dự phòng một lần:** trên mỗi khoản Publisher Share mới qua đối soát, trích theo tỷ lệ đã lưu; phần còn lại mới khả dụng. Thời gian giữ thêm tính từ lúc trích sau đối soát. Không trích trên số dư đã chuyển kỳ, phần dự phòng vừa giải phóng hoặc payout thử lại. Cả tỷ lệ và ngày giải phóng phải hiển thị cho Owner; tiền dự phòng vẫn ở phần theo dõi thu nhập Nexora, chưa chuyển vào số dư sử dụng được của ví VlinkPay.
14. **💰 Giải phóng dự phòng:** tới hạn, xử lý nghĩa vụ đã xác nhận rồi chuyển phần còn lại không bị hold sang khả dụng. Chỉ phần đang cần kiểm tra tiếp tục bị giữ, kèm lý do và lịch sử cập nhật; không gia hạn toàn bộ dự phòng vô thời hạn vì một khoản tranh chấp nhỏ. Mỗi khoản phải đối chiếu được: số đã trích = số còn giữ + số đã sử dụng/đảo + số đã giải phóng.
15. **Tranh chấp và thu hồi:** khi mới nhận khiếu nại, giữ phần liên quan để kiểm tra, chưa ghi giảm cuối cùng hoặc công nợ đã xác nhận. Nếu khoản thu hồi bị hủy/đính chính, tạo bút toán hoàn nguyên liên kết giao dịch gốc; số đã bù được khôi phục vào đúng phần dự phòng/khả dụng theo thời hạn còn hiệu lực và không bị trích dự phòng mới.
16. **Rủi ro còn lại:** dự phòng không bảo đảm luôn đủ để bù mọi khoản thu hồi. Công nợ chưa bù phải có số tiền, ngày phát sinh, tuổi nợ và trạng thái xử lý cho vận hành; cảnh báo theo ngưỡng được cấu hình. Không tự xóa công nợ khi Business tắt kiếm tiền hoặc không có thu nhập mới.
17. **💰 Loại tiền và tỷ lệ:** Admin chọn các loại tiền VlinkPay hỗ trợ, tỷ lệ mỗi loại lớn hơn 0 và tổng bằng 100%; một loại thì 100%. Phân bổ trên giá trị đủ chi sau dự phòng/khấu trừ, không thay công thức Publisher Share. Kiểm tra ngưỡng $25 trên tổng USD trước phân bổ, không kiểm tra lại riêng từng loại.
18. **💰 Đối chiếu phân bổ:** tổng giá trị USD phân bổ cho các loại phải khớp giá trị đủ chi. Số đơn vị thực nhận phụ thuộc tỷ giá và phí đã công khai; mọi chênh lệch làm tròn phải được giải thích và xử lý theo chính sách được duyệt. Không cộng trực tiếp số đơn vị khác loại hoặc dùng tỷ giá hiện tại để sửa lịch sử giá trị gốc.
19. **💰 Chi trả từng phần:** mỗi phần tiền có tham chiếu và kết quả riêng. Khi một phần đã ghi có, chỉ số đó là đã nhận; giữ phần còn lại để xử lý, không đưa vào kỳ chi khác đồng thời. Thử lại không đổi phiên bản/tỷ lệ phân bổ, không gửi lại phần thành công và không coi timeout là đã thất bại. Thu hồi sau chi căn cứ phần thưởng gốc mất điều kiện hưởng, không tự tính công nợ theo biến động giá loại tiền đã nhận.

#### Cách tính theo chính sách ngày 21/09

Các giá trị sau lấy từ bản user chọn làm nguồn chuẩn cho story; lưu theo phiên bản chính sách/campaign, không hardcode vào FE.

| Hoạt động | Phí của Advertiser | Publisher Share của Business |
| :--- | :--- | :--- |
| Click banner tài trợ hợp lệ | $0.40/click | 40% phí hợp lệ; ví dụ $0.16. |
| Click card tài trợ Nearby/Explore | $0.25/click | 35% phí hợp lệ. |
| Click card tài trợ Search Deals | $0.30/click | 35% phí hợp lệ. |
| Dịch vụ hoàn tất và thanh toán — khách mới đủ điều kiện | 10% giá trị dịch vụ sau giảm giá đủ điều kiện | 50% performance fee. |
| Dịch vụ — khách quay lại sau ít nhất 90 ngày | 5% nếu campaign bật điều kiện này | 50% performance fee. |
| Mở menu, impression, click organic hoặc Internal | Không tính phí mạng tương ứng | Không phát sinh thưởng từ những hoạt động này. |

Giá trị dịch vụ tính phí không gồm thuế, tip, phụ phí, retail, gift card lúc bán hoặc phần đã hoàn. Một số tỷ lệ tạo phần lẻ dưới một cent; FE hiển thị giá trị đã được hệ thống đối soát xác nhận. Quy tắc làm tròn/tích lũy cần xác nhận trong contract trước phát hành. Không mặc định cộng phí click và phí dịch vụ trên cùng hành trình nếu campaign chưa chấp thuận mô hình tương ứng. Bán voucher trả trước là giai đoạn sau, ngoài phạm vi.

Cửa sổ click mẫu của bản 21/09: banner tối đa một valid click mỗi khách/phiên × advertiser × 24 giờ; sponsored card tối đa một valid click mỗi khách/phiên × deal × 24 giờ. Hoạt động service dùng booking/order để chống ghi nhận trùng. Cách nhận diện khách qua guest/login được xử lý trong tích hợp tracking.

#### Ví dụ dự phòng, khấu trừ và ngưỡng nhận tiền

Tỷ lệ **20%** và thời gian **30 ngày giữ thêm** dưới đây chỉ để minh họa; Admin cần cấu hình giá trị được duyệt trước phát hành. Các ví dụ là những tình huống độc lập. “Khả dụng” đã loại phần dự phòng/hold; không trích thêm dự phòng trên số đó.

| Trường hợp | Kết quả |
| :--- | :--- |
| Khoản thu $100 qua đối soát, dự phòng 20%, chưa có công nợ | 💰 Trích $20, còn $80 khả dụng để xét chi. Dự phòng $20 chưa vào ví; có ngày dự kiến giải phóng sau 30 ngày giữ thêm. |
| $20 dự phòng đến hạn, không có hold/công nợ và chưa có số khả dụng khác | 💰 Giải phóng $20 thành khả dụng; chưa chi vì dưới $25, không trích lại 20%. Có thêm $10 khả dụng thì xét chi $30 ở kỳ tiếp theo. |
| Có $20 dự phòng hợp lệ và $80 khả dụng; cần thu hồi $30 từ khoản cũ đã trả | 💰 Dùng $20 dự phòng + $10 khả dụng; còn $70 xét chi. Công nợ về $0; không lấy thêm $30 lần nữa. |
| Khoản $100 đã trả $80, còn $20 dự phòng; xác nhận $50 phần thưởng gốc mất điều kiện | 💰 Đảo $20 chưa trả của khoản gốc; phần đã trả cần thu hồi còn $30. Không ghi công nợ $50 rồi dùng lại cùng $20 lần thứ hai. |
| Cần thu hồi $4; không còn dự phòng; kỳ sau có $30 khả dụng | 💰 Bù $4; còn $26, đủ ngưỡng xét chi vào ví VlinkPay. |
| Cần thu hồi $4; không còn dự phòng; kỳ sau có $3 khả dụng | 💰 Bù $3; không chi kỳ này; còn $1 cần bù ở kỳ sau. |
| Cần thu hồi $4; không còn dự phòng; kỳ sau có $27 khả dụng | 💰 Bù $4; còn $23, giữ sang kỳ tiếp theo vì chưa đạt $25. |
| $20 dự phòng đến hạn; $5 đang bị hold vì tranh chấp chưa kết luận | Giữ riêng $5 có lý do; 💰 giải phóng $15 còn lại nếu không có nghĩa vụ khác. Chưa coi $5 là khoản mất quyền hưởng cuối cùng. |
| Business tắt kiếm tiền và chưa có thu nhập mới | Dự phòng tiếp tục theo lịch; dùng/giải phóng theo chính sách. Công nợ chưa bù vẫn hiển thị và được vận hành theo dõi; không tự trừ ví VlinkPay. |

#### Ví dụ phân bổ loại tiền nhận

**Chỉ minh họa, chưa phải danh mục hoặc tỷ lệ được chốt:** Admin cấu hình loại tiền A **70%**, loại tiền B **30%**; cả hai phải được VlinkPay hỗ trợ. Giả sử chưa có công nợ và phí quy đổi bằng 0 trong ví dụ.

| Bước | Kết quả |
| :--- | :--- |
| Publisher Share $100 qua đối soát, giữ dự phòng 20% | Giữ $20; $80 đủ ngưỡng chi. Tỷ lệ dự phòng 20% độc lập với tỷ lệ tiền nhận 70%/30%. |
| Phân bổ $80 đủ chi | Loại A nhận giá trị tương đương $56; loại B tương đương $24. Không giữ riêng phần B vì dưới $25, vì tổng payout $80 đã đạt ngưỡng. |
| Quy đổi minh họa: 1 đơn vị A = $2, 1 đơn vị B = $0.50 | Dự kiến ghi có 28 A và 48 B. Không gọi tổng là “76 tiền”; giá trị phân bổ gốc vẫn là $80. Các tỷ giá chỉ là giả định tính toán. |
| 28 A thành công, phần 48 B thất bại được xác nhận | Payout đã trả một phần: 28 A đã nhận, 48 B chờ xử lý. Thử lại chỉ phần B; không trích dự phòng lại và không gửi lại 28 A. |
| Admin đổi phân bổ sang A 60% / B 40% | Áp dụng cho payout mới từ thời điểm hiệu lực; payout $80 đã tạo vẫn giữ phân bổ A $56 / B $24. |

#### Tiêu chí nghiệm thu

1. Business Owner chỉ xem/thao tác trên Business mình có quyền; Personal và Sponsor không xuất hiện trong luồng này.
2. Hiển thị trạng thái KYB, điều kiện tham gia, thuế, liên kết ví và chính sách dự phòng áp dụng; kế thừa kết quả xác minh hiện có. Chỉ bật khi hệ thống xác nhận đủ điều kiện; consent có người đồng ý, thời điểm và phiên bản.
3. Bật/tắt không làm mất tiện ích OneQR hoặc tắt bộ lọc đối thủ. Khoản đã khóa hợp lệ không bị xóa khi tắt; click lúc tắt không được cộng hồi tố.
4. Scan, mở menu, impression, click organic và Internal không tạo thu nhập trái chính sách. Hoạt động trùng, tự giao dịch, gian lận hoặc campaign không đủ điều kiện không được cộng thưởng.
5. Khoản thu hiển thị loại hoạt động, nguồn QR, campaign, thời điểm, căn cứ/phần chia, trạng thái và lý do giữ/điều chỉnh khi có; chỉ hiển thị dữ liệu khách trong quyền được phép.
6. Booking/order khóa nguồn; việc quét QR khác không thay nguồn đã khóa. Thưởng dịch vụ chỉ phát sinh khi hoàn tất và thanh toán được xác minh.
7. Tổng quan phân biệt chờ đối soát, dự phòng còn giữ, khả dụng, hold do tranh chấp, đang chi, đã trả và điều chỉnh. Không cộng hai lần khoản vừa thuộc dự phòng vừa bị hold. Số tiền đã chuyển ví chỉ hiển thị khi có xác nhận ghi có.
8. Cả click quảng cáo và thưởng dịch vụ dùng thời gian đối soát mặc định 14 ngày do Admin vận hành cấu hình. Lưu thời hạn áp dụng cho từng khoản thu; đổi cấu hình không tính lại khoản cũ. Sau đối soát, trích dự phòng theo chính sách của khoản thu. Kiểm tra $25 trên phần khả dụng còn lại sau xử lý công nợ; không dùng phần dự phòng chưa giải phóng, chờ đối soát, hold hoặc đang chi để trả tiếp.
9. Payout gửi vào đúng ví VlinkPay SSO của Business. Thiếu ví hợp lệ, ví bị hạn chế hoặc hồ sơ chưa đủ phải có lý do và bước xử lý; không mất số tiền đang chờ chi.
10. Điều chỉnh được xác nhận phải tách phần chưa trả để đảo trực tiếp và phần đã trả cần thu hồi. Dùng dự phòng hợp lệ còn lại cùng Business, rồi khả dụng, sau cùng chuyển tiếp phần thiếu sang kỳ sau. Không ghi hoặc thu hai lần cùng nghĩa vụ; không đổi lịch sử đã trả và không tự trừ ví VlinkPay.
11. Chi tiết đối soát hiển thị thu nhập kỳ này, dự phòng mới trích/còn giữ/đã dùng/đã giải phóng, ngày giải phóng, khấu trừ, số thực nhận và số còn phải bù; mỗi thay đổi truy được giao dịch gốc. Các ví dụ phía trên phải cho kết quả tương ứng.
12. Payout lỗi/chưa rõ kết quả có trạng thái riêng và đối chiếu trước khi thử lại; sự kiện lặp không chi, trích dự phòng, giải phóng hoặc khấu trừ trùng.
13. Lịch sử lưu mã giao dịch Nexora/VlinkPay khi có, thời điểm, trạng thái và số tiền; Owner có thể lọc kỳ và mở chi tiết để đối chiếu.
14. Giao diện dùng được trên điện thoại và desktop, có EN/VI; ngày tiếng Việt viết đầy đủ “tháng”. Chưa có dữ liệu, đang tải hoặc lỗi kết nối có trạng thái rõ ràng.
15. Business Owner không sửa được số ngày đối soát. Thay đổi của Admin vận hành có lịch sử người sửa, giá trị trước/sau, thời điểm hiệu lực; FE Business hiển thị ngày dự kiến đủ điều kiện do hệ thống xác nhận.
16. Admin vận hành được phân quyền cấu hình tỷ lệ dự phòng, số ngày giữ thêm, phạm vi áp dụng và ngày hiệu lực; Owner chỉ xem. Lưu chính sách với từng khoản thu khi ghi nhận; thay đổi/giảm/tắt cấu hình cho khoản mới không tính lại hay giải phóng sớm khoản cũ.
17. Dự phòng chỉ trích một lần trên Publisher Share mới qua đối soát. Không trích lại trên tiền chuyển kỳ, dự phòng được giải phóng hoặc payout thử lại. Tổng dự phòng trích phải bằng còn giữ + đã dùng/đảo + đã giải phóng.
18. Đến hạn, hệ thống giải phóng phần dự phòng không còn nghĩa vụ/hold vào khả dụng; chưa đủ $25 thì chuyển kỳ. Phần bị hold có lý do; không giữ cả số tiền không liên quan. Tắt kiếm tiền không ngừng giải phóng khoản đủ điều kiện theo lịch.
19. Tranh chấp chưa kết luận chỉ tạo hold; khi xác nhận mới điều chỉnh/thu hồi. Nếu quyết định thu hồi được hủy, có bút toán hoàn nguyên đúng nguồn và lịch sử, không tạo thu nhập hay lần dự phòng mới.
20. Công nợ chưa bù hiển thị số tiền, ngày phát sinh và tuổi nợ cho vận hành; có cảnh báo theo ngưỡng cấu hình. Dự phòng không đủ hoặc Business ngừng hoạt động không làm công nợ tự biến mất.
21. Admin được phân quyền có thể chọn loại tiền VlinkPay hỗ trợ, nhập tỷ lệ, xem trước phân bổ và đặt hiệu lực. Chặn áp dụng nếu tổng khác 100%, thiếu/trùng loại tiền, tỷ lệ không hợp lệ hoặc loại không được hỗ trợ. Business Owner không sửa được cấu hình.
22. Payout lưu phiên bản, loại tiền, tỷ lệ, giá trị USD từng phần, căn cứ quy đổi, phí, số đơn vị và tham chiếu. Đổi cấu hình chỉ tác động payout mới từ ngày hiệu lực; không tính lại payout đã tạo, kể cả phần đang chờ thử lại. Thay đổi có lịch sử Admin và giá trị trước/sau.
23. Phân bổ đúng trên giá trị đủ chi sau dự phòng/khấu trừ, tổng tỷ lệ 100%; ngưỡng $25 áp dụng trên tổng USD trước chia. Ví dụ $80 chia 70%/30% phải cho $56/$24; không chặn riêng phần $24 hoặc trích thêm dự phòng.
24. Lịch sử và chi tiết hiển thị từng loại tiền, tỷ lệ, giá trị phân bổ, tỷ giá/phí, số đơn vị dự kiến/đã nhận và trạng thái. Một phần thành công phải hiển thị đã trả một phần; chỉ tất cả phần được xác nhận ghi có mới đánh dấu payout đã trả. Không cộng trực tiếp số đơn vị khác loại.
25. Khi một phần thất bại/chưa rõ kết quả, đối chiếu và chỉ thử lại phần xác nhận chưa chi. Không chuyển lại phần thành công, đổi tỷ lệ theo cấu hình mới, trích thêm dự phòng hoặc phân bổ cùng tiền vào payout khác. Báo giá hết hạn được xử lý theo chính sách quy đổi đã duyệt và có lịch sử.
26. Chưa có cấu hình hợp lệ, thiếu tỷ giá/phí cần thiết hoặc ví không nhận được loại tiền cấu hình phải có trạng thái/lý do chờ và bên xử lý. Không mất số dư, tự đổi loại tiền/tỷ lệ hoặc tắt toàn bộ ghi nhận thu nhập; phần đã trả giữ nguyên lịch sử.

### Tình huống ngoại lệ và cách xử lý

| Tình huống | Cách xử lý | Bên xử lý |
| :--- | :--- | :--- |
| KYB/hồ sơ chưa đạt hoặc bị yêu cầu bổ sung | Hiển thị phần thiếu/lý do; dẫn tới luồng xác minh hiện có. | Owner / xác minh |
| Mất liên kết ví hoặc ví chưa đủ điều kiện nhận | Giữ khoản chi, hiển thị lý do; xác nhận lại đúng ví Business trước khi trả. | Owner / VlinkPay / vận hành |
| Booking hủy, no-show, hết hạn trước hoàn tất | Không tạo thưởng dịch vụ; giải phóng giữ chỗ qua nghiệp vụ campaign liên quan. | Hệ thống |
| Hoàn một phần/toàn bộ trước hoặc sau payout | Đảo phần chưa trả đúng một lần; phần đã trả cần thu hồi dùng dự phòng hợp lệ, khả dụng và chuyển tiếp phần thiếu. Chỉ điều chỉnh phần thưởng mất điều kiện hưởng. | Hệ thống / vận hành |
| Dự phòng đến hạn khi vẫn có tranh chấp | Giải phóng phần không liên quan; giữ phần liên quan với lý do cho đến khi có kết quả. | Hệ thống / vận hành |
| Payout chưa đủ ngưỡng sau trích dự phòng/khấu trừ | Giữ phần khả dụng sang kỳ tiếp theo, không trích dự phòng lại. | Hệ thống |
| Business tắt kiếm tiền | Không giải phóng dự phòng sớm; không trì hoãn phần đến hạn đủ điều kiện. Tiếp tục theo dõi công nợ. | Hệ thống / vận hành |
| Công nợ vượt ngưỡng hoặc lâu không bù được | Cảnh báo vận hành và theo dõi xử lý; không tự xóa nợ hoặc tự lấy tiền từ ví VlinkPay. | Vận hành |
| Điều chỉnh thu hồi bị hủy/đính chính | Hoàn nguyên khoản đã dùng/khấu trừ bằng bút toán liên kết; trở lại dự phòng/khả dụng theo thời hạn áp dụng. | Hệ thống / vận hành |
| Thu nhập thấp hơn ngưỡng hoặc khoản cần thu hồi | Chuyển tiếp số dư/khoản còn thiếu; hiển thị riêng từng loại. | Hệ thống |
| Payout chậm, thất bại hoặc không rõ kết quả | Giữ dấu vết giao dịch, đối chiếu VlinkPay; không coi timeout là chắc chắn chưa chuyển tiền. | VlinkPay / vận hành |
| Cấu hình loại tiền thiếu, tỷ lệ sai tổng hoặc loại tiền không được hỗ trợ | Chặn áp dụng cấu hình sai. Khi không có chính sách hợp lệ để chi, giữ payout chờ với lý do; không tự đặt loại tiền hoặc tỷ lệ thay thế. | Admin vận hành |
| Ví không nhận được một loại tiền hoặc thiếu căn cứ quy đổi | Kiểm tra trước khi gửi; giữ phần chưa chi cần xử lý, không tự phân bổ sang loại khác. Nếu đã có phần ghi có thì giữ trạng thái đã trả một phần và lịch sử tương ứng. | VlinkPay / vận hành |
| Một loại tiền thành công, loại khác thất bại/chưa rõ | Theo dõi từng phần; đối chiếu phần chưa rõ rồi chỉ thử lại phần xác nhận chưa chi. Không chuyển lại toàn bộ payout. | VlinkPay / vận hành |
| Admin đổi tỷ lệ khi payout đang chuyển | Giữ phiên bản đã chốt cho payout đó; bản mới áp dụng cho payout tạo sau thời điểm hiệu lực. | Hệ thống |
| Hoạt động nghi gian lận | Giữ khoản liên quan và hiển thị lý do phù hợp; xử lý theo kết quả xác minh. | Vận hành |
| Owner thắc mắc khoản điều chỉnh | Tra cứu hoạt động, chính sách và lịch sử; dùng kênh hỗ trợ hiện có. | Support |

### Câu hỏi thường gặp

**Quét QR là có tiền ngay?**

Không. Chỉ hoạt động đủ điều kiện của campaign và có nguồn hợp lệ mới được xét thưởng.

**Phải nạp Ads Credit hoặc mời người khác mới được bật kiếm tiền?**

Không. Đây là thu nhập trực tiếp của QR Host; mua quảng cáo và Sponsor là nghiệp vụ khác.

**Tiền chờ đối soát hoặc giữ dự phòng có nằm trong ví VlinkPay chưa?**

Chưa. Chỉ khoản đã được VlinkPay xác nhận ghi có mới là tiền đã nhận vào ví.

**Tắt kiếm tiền có mất khoản đang chờ không?**

Không xóa khoản đã khóa hợp lệ; khoản đó vẫn chịu điều kiện đối soát, dự phòng, hoàn/đảo và khấu trừ. Dự phòng vẫn được xét giải phóng đúng lịch dù Owner đã tắt kiếm tiền.

**Dự phòng có phải phí bị trừ mất không?**

Không. Đây là phần thu nhập tạm giữ trên Nexora để bảo đảm nghĩa vụ hoàn tiền/tranh chấp. Phần không sử dụng được giải phóng theo lịch vào khả dụng rồi xét kỳ chi; Owner thấy số tiền, lý do và ngày dự kiến giải phóng.

**Đã chờ đối soát 14 ngày thì còn chờ thêm bao lâu?**

Chỉ phần trích dự phòng chờ thêm theo số ngày Admin cấu hình; phần còn lại có thể được xét chi ngay kỳ đủ điều kiện. Ví dụ 20%/30 ngày trong tài liệu chỉ minh họa, chưa phải mức mặc định đã chốt.

**Đã nhận tiền nhưng sau đó khách được hoàn thì sao?**

Sau khi xác nhận, hệ thống điều chỉnh phần thưởng mất điều kiện hưởng, ưu tiên xử lý phần chưa trả; phần đã trả còn phải thu hồi dùng dự phòng hợp lệ, rồi khả dụng, rồi thu nhập các kỳ sau cho phần thiếu. Mỗi lần dùng tiền có lý do và lịch sử; không tự trừ số dư ví VlinkPay đã nhận.

**Ai quyết định nhận bằng loại tiền nào và bao nhiêu phần trăm?**

Admin vận hành cấu hình từ danh mục VlinkPay hỗ trợ, tổng tỷ lệ 100%; Owner chỉ xem. Ví dụ A 70% / B 30% không phải cấu hình mặc định. Tỷ lệ áp dụng trên giá trị đủ chi sau dự phòng và khấu trừ, không phải toàn bộ doanh thu.

**Một loại tiền đã vào ví, loại còn lại chưa vào thì sao?**

Payout hiển thị đã trả một phần, kèm kết quả từng loại. Phần còn lại được đối chiếu/xử lý riêng; hệ thống không chuyển lại phần đã nhận hoặc tự đổi sang loại tiền khác.

### Tính năng liên quan

| Tính năng | Mối liên hệ với tài liệu này |
| :--- | :--- |
| [Promotion và quảng cáo](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/promotion-publishing-ads.md) | Cung cấp hoạt động quảng cáo hoặc giao dịch đủ điều kiện, cùng các điều chỉnh, để làm căn cứ ghi nhận thu nhập cho doanh nghiệp giới thiệu. |
| [Ads Credit](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/merchant-ads-credit.md) | Là nguồn tiền quảng cáo của doanh nghiệp chạy quảng cáo. Số dư nạp quảng cáo và thu nhập OneQR được quản lý riêng. |
| OneQR và Discovery | Xác định nguồn giới thiệu và nơi phân phối nội dung phù hợp. Quét QR hoặc mở menu không tự tạo thu nhập. |
| Xác minh doanh nghiệp (KYB) | Cung cấp kết quả xác minh để xét điều kiện tham gia và nhận tiền; kế thừa quy trình xác minh hiện có. |
| Ví VlinkPay liên kết SSO | Nhận phần thu nhập đủ điều kiện vào đúng ví của tài khoản Business; trả kết quả để đối chiếu từng phần chi. |
| [Sponsor Override](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/oneqr-sponsor-override.md) | Quản lý phần thu nhập theo quan hệ giới thiệu và cấp Sponsor. Thu nhập này có chính sách riêng, ngoài phạm vi thu nhập trực tiếp của Business. |

#### Tài liệu nguồn đi kèm

Các file HTML nguồn có nhắc đến `NEXORA-Promotion-Owner-Guide.html`, `NEXORA-Salon-Research-and-Template-Brief.md` hoặc `OneQR-2.2-Prototype.html`, nhưng các file này chưa có trong bộ nguồn được cung cấp. Không coi các liên kết đó là tài liệu đã xuất bản.

Các tài liệu nguồn có liên kết dưới đây được đính kèm trong thư mục references để đối chiếu. Đây là các bản mẫu, không phải bằng chứng chức năng đã triển khai. Nội dung nghiệp vụ và các quyết định áp dụng được trình bày trong tài liệu này; những nguồn chưa tìm thấy được ghi rõ riêng.

- [Chính sách Ads/Referral 21/09 — nguồn tính thu nhập](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Ads-Referral-Revenue-Policy.html).
- [Menu Placement — onboarding, payout và hành vi tắt](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Menu-Placement.html): chỉ lấy phần không mâu thuẫn chính sách 21/09 và quyết định user; không áp dụng tỷ lệ 70% của phần chính sách cũ trong file.
- [Monetization & Sponsor Terms — điều kiện QR Host](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Monetization-Sponsor-Terms.html): không lấy tỷ lệ minh họa làm tỷ lệ của story; Sponsor ngoài phạm vi.
- [Business Verification / KYB — bối cảnh xác minh](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Business-Verification-KYB.html): các level là đề xuất; không đồng nhất trực tiếp với trạng thái KYB đang chạy.
- [Five-Part Pilot — không cộng hồi tố click lúc tắt](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Five-Part-Pilot.html): tỷ lệ demo không thay thế chính sách 21/09.

#### Hiện trạng và phụ thuộc tích hợp — tham chiếu nội bộ

Đối chiếu mã giao diện trên nhánh `staging`, mã phiên bản `58c41d9352b604209d375ab8dfab7c24763b8def`, ngày 24 tháng 9 năm 2026: đã có OneQR (tệp `src/data/repositories/merchantOneQr.ts`, tham chiếu nội bộ), tracking bấm menu (tệp `src/data/repositories/publicOneQr.ts`, tham chiếu nội bộ), KYB (tệp `src/components/settings/tabs/KybTab.tsx`, tham chiếu nội bộ) và khai báo mở Wallet qua hồ sơ SSO (tệp `src/data/repositories/profileSettings.ts`, tham chiếu nội bộ). Những phần này chưa chứng minh có tích hợp payout earnings OneQR vào VlinkPay. Không lấy payout Tips hoặc trường địa chỉ crypto của phương thức thanh toán làm bằng chứng cho cơ chế ghi có ví SSO.

Các điểm cần xác nhận trước tích hợp/phát hành, không tự đặt giá trị trong story:

| Phụ thuộc | Cần xác nhận |
| :--- | :--- |
| Contract kiếm tiền | Trạng thái/điều kiện, consent, bật/tắt, tổng quan, chi tiết thu nhập, dự phòng, điều chỉnh, công nợ và lịch sử payout; chưa xác nhận API triển khai trong công việc tài liệu này. |
| VlinkPay | Định danh Business/ví qua SSO, danh mục loại tiền được hỗ trợ và khả năng nhận của ví, nguồn tỷ giá/thời điểm chốt/hiệu lực báo giá, phí nếu có, độ chính xác từng loại, mã và trạng thái từng phần chi, cơ chế chống trùng/đối chiếu. Không tự chọn USDV hoặc USDT chỉ vì FE có phương thức crypto. |
| Cấu hình loại tiền nhận | Đã chốt Admin vận hành cấu hình loại tiền và tỷ lệ mỗi loại, tổng 100%. Cần xác nhận danh mục và tỷ lệ thực tế, phạm vi/ưu tiên chính sách, quyền Admin và contract lưu phiên bản theo payout, xem trước, hiệu lực, lịch sử. A 70% / B 30% chỉ là ví dụ; chưa xác nhận chức năng này đã có sẵn. |
| Tích hợp cấu hình đối soát | Đã chốt mặc định 14 ngày, gồm cả click, Admin vận hành cấu hình. Contract cần cung cấp thời hạn của từng khoản thu, quyền cấu hình và lịch sử thay đổi; xác nhận giới hạn giá trị cấu hình hợp lệ trước triển khai. |
| Chính sách và tích hợp dự phòng | Cơ chế đã được user chọn. Cần chốt tỷ lệ, số ngày giữ thêm, nhóm Business áp dụng và ngưỡng cảnh báo công nợ; 20%/30 ngày chỉ là ví dụ. Contract cần cung cấp chính sách đã lưu, ngày giải phóng từng khoản, lịch sử trích/dùng/đảo/giải phóng và hold; không mặc định VlinkPay đã có chức năng reserve. |
| Làm tròn | Quy tắc phần chia lẻ dưới một cent của thu nhập; độ chính xác tỷ lệ phân bổ và đơn vị từng loại tiền, xử lý phần lẻ/phần quy đổi dưới mức tối thiểu VlinkPay cho phép, phí và đối soát để tổng giá trị khớp. Không tự làm mất phần lẻ hoặc coi phần chưa ghi có là đã trả. |
| Eligibility | Mapping KYB hiện có với quyền bật kiếm tiền/payout, yêu cầu thuế và 2FA trong mẫu; thời điểm tái xác minh/giữ chi khi điều kiện thay đổi. |
| Hoàn tiền khi đang chuyển | Phối hợp trạng thái chuyển ví và adjustment để quyết định giảm phần chưa trả hay tạo khoản thu hồi cho phần đã trả, không vừa giảm vừa thu hồi cùng một khoản. |

Phạm vi công việc hiện tại là tài liệu nghiệp vụ; chưa sửa FE/BE, chưa gọi giao dịch tiền thật và chưa xác nhận tính sẵn sàng của API trên staging.
