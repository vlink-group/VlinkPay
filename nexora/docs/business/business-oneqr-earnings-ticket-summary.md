## Business OneQR — Kiếm tiền từ QR, đối soát và nhận tiền

**Trạng thái:** Đang rà soát
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/business-oneqr-earnings.md)
**Ticket:** [#1599](https://github.com/vlink-group/vlink-nexora/issues/1599) — Confirmed, chưa bắt đầu xử lý khi rà soát ngày 5 tháng 10 năm 2026.

### Mục tiêu:

Business Owner kiểm soát thu nhập từ QR, đối soát và nhận tiền vào ví VlinkPay SSO của Business.

### Phạm vi

- **Cần triển khai/xác minh:** Bật/tắt, nguồn thu, đối soát, dự phòng, thu hồi, lịch sử và payout theo phân bổ Admin cấu hình.
- **Code staging đã có:** OneQR/menu/tracking, Promotion/POS, KYB và Ads Credit. Chưa tìm thấy luồng FE/endpoint BE đầy đủ cho Earnings OneQR trong phạm vi đối chiếu.
- **Ngoài phạm vi:** Personal, Sponsor, nạp quảng cáo, xây mới Discovery/KYB, voucher trả trước, rút về ngân hàng, portal Admin đầy đủ.

### Vai trò liên quan

- **Owner:** Đồng ý điều khoản, hoàn thiện hồ sơ, bật/tắt và đối chiếu tiền.
- **Admin:** Cấu hình chính sách, xử lý giữ khoản/điều chỉnh theo quyền.
- **Nexora/VlinkPay:** Xác minh hoạt động, ghi thu nhập và xác nhận ghi có; **Support:** tra cứu.

### Luồng chính

1. Kiểm tra KYB/thuế/ví và consent; Owner bật khi đủ điều kiện.
2. Xác minh nguồn QR, campaign và hoạt động hợp lệ; ghi khoản chờ đối soát.
3. Sau đối soát, 💰 trích dự phòng một lần; phần còn lại khả dụng.
4. 💰 Xử lý điều chỉnh; dùng dự phòng → khả dụng → thu nhập kỳ sau cho phần đã trả cần thu hồi.
5. 💰 Giải phóng dự phòng đến hạn không bị giữ; xét ngưỡng/kỳ chi.
6. Phân bổ theo chính sách đã chốt; 💰 chuyển từng phần vào đúng ví Business.
7. Ghi đã nhận khi ví xác nhận; Owner xem từng phần, điều chỉnh và công nợ.

### Tính năng liên quan

- **[Promotion](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/promotion-publishing-ads.md):** Cung cấp hoạt động và điều chỉnh.
- **[Ads Credit](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/merchant-ads-credit.md):** Nguồn quảng cáo, tách thu nhập.
- **[Sponsor](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/oneqr-sponsor-override.md):** Thu nhập giới thiệu riêng.
- **OneQR/Discovery, KYB, ví SSO:** Nguồn, điều kiện và nơi nhận; chưa có tài liệu đi kèm.

**Tài liệu mẫu từ PO:** [Ads/Referral Policy](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Ads-Referral-Revenue-Policy.html) · [Menu Placement](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Menu-Placement.html) · [Monetization Terms](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Monetization-Sponsor-Terms.html) · [KYB](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Business-Verification-KYB.html) · [Pilot](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Five-Part-Pilot.html)
**HTML thiết kế:** [OneQR Earnings](https://taxiq-nexora-touch.vercel.app/html/pages/oneqr-earnings.html)
