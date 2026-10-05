## OneQR Sponsor — Quan hệ hưởng, cấp Sponsor và chi trả override

**Trạng thái:** Đang rà soát
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/oneqr-sponsor-override.md)

### Mục tiêu:

Cho phép Personal, Business và Staff/Partner nhận override từ hoạt động OneQR hợp lệ của B, theo đúng quan hệ, cấp Sponsor và kết quả ghi có vào ví VlinkPay SSO.

### Phạm vi

- Phần Sponsor là yêu cầu cần triển khai; code staging hiện có nền tảng giới thiệu và tích hợp ví, chưa có chương trình override chuyên biệt.
- **Trong phạm vi:** Quan hệ trực tiếp/trên cây; B active; cấp và quyền hưởng; tính, đối soát, điều chỉnh override; phân bổ nhiều loại tiền; chi qua ví VlinkPay SSO; giao diện Sponsor/Admin.
- **Ngoài phạm vi:** Đổi Sponsor; Ads Credit; quảng cáo, loyalty; xây lại affiliate, KYC/KYB hoặc ví; rút tiền ngân hàng. Thu nhập QR trực tiếp thuộc Business OneQR Earnings.

### Vai trò liên quan

- **Sponsor/B:** Sponsor theo dõi quyền và thu nhập; B tạo hoạt động hợp lệ nhưng không tự xác nhận thưởng.
- **Admin/Vận hành:** Cấu hình chính sách, hiệu lực, hồi tố và ngoại lệ.
- **Nexora/VlinkPay:** Nexora xác định quyền và điều phối; VlinkPay xác nhận ví và ghi có.

### Luồng chính

1. Admin phát hành chính sách về quan hệ hưởng, B active, cấp, công thức, giới hạn, hiệu lực và hồi tố.
2. Sponsor tham gia; B được ghi nhận qua nguồn hợp lệ hoặc cây affiliate. Người giới thiệu đã xác lập không thay đổi.
3. Hệ thống xét hoạt động thực tế của B và quyền Sponsor; đăng ký, nạp credit hoặc traffic đơn thuần không tạo thưởng.
4. Với sự kiện hợp lệ, hệ thống xác định người hưởng, xử lý trùng, áp dụng tỷ lệ/giới hạn và 💰 ghi override chờ đối soát.
5. Khoản hợp lệ được tách dự phòng/khả dụng; khoản mất điều kiện tạo điều chỉnh liên kết, không xóa lịch sử.
6. Đến kỳ chi, hệ thống xác minh ví SSO, phân bổ theo loại tiền và 💰 gửi từng phần. Chỉ phần VlinkPay xác nhận mới là đã nhận; kết quả chưa rõ phải đối chiếu trước khi thử lại.

### Tính năng liên quan

- **Affiliate — quan hệ giới thiệu:** Cung cấp người giới thiệu và cây làm căn cứ xét hưởng; quan hệ đã xác lập không được đổi. Chưa có tài liệu đi kèm.
- **[Promotion và quảng cáo](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/promotion-publishing-ads.md):** Cung cấp sự kiện đủ điều kiện và điều chỉnh liên quan; quyền và tiền Sponsor vẫn theo chính sách Sponsor.
- **[Business OneQR Earnings](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/business-oneqr-earnings.md):** Quản lý thu nhập QR trực tiếp; chỉ tham khảo mô hình đối soát, không tự dùng ngưỡng hoặc kỳ chi cho Sponsor.
- **[Ads Credit](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/merchant-ads-credit.md):** Là nguồn tiền quảng cáo; credit chưa sử dụng không tự tạo Sponsor Override.
- **Ví VlinkPay liên kết SSO:** Nhận tiền đúng tài khoản và xác nhận kết quả ghi có từng loại tiền. Chưa có tài liệu đi kèm.

**Tài liệu mẫu từ PO:** [Ads/Referral Revenue Policy](https://github.com/user-attachments/files/32545230/NEXORA-OneQR-Ads-Referral-Revenue-Policy.html) · [Sponsor Level Flow](https://github.com/user-attachments/files/32545236/NEXORA-OneQR-Sponsor-Level-Flow.html) · [Monetization & Sponsor Terms](https://github.com/user-attachments/files/32545251/NEXORA-OneQR-Monetization-Sponsor-Terms.html)  
**HTML thiết kế:** [Mở bản thiết kế Sponsor Level Flow](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Sponsor-Level-Flow.html)
