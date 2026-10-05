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

### Quy tắc nghiệp vụ quan trọng

- Tracking menu, scan, impression, Internal và click organic không tự tạo tiền. Thanh toán Ads Credit từ ví khác với payout Earnings.
- Dùng chính sách ngày 21 tháng 9 năm 2026; lưu phiên bản, không trộn tỷ lệ cũ/demo hoặc hardcode.
- Dịch vụ lấy nguồn hợp lệ cuối trong 30 ngày trước khóa; tối đa 60 ngày từ khóa tới hoàn tất/thanh toán. Loại thuế, tip, phụ phí và phần hoàn khỏi căn cứ phí.
- Đối soát mặc định 14 ngày, Admin cấu hình; khoản cũ giữ thời hạn. Không trích dự phòng lại khi chuyển kỳ, giải phóng hoặc thử lại.
- 💰 Xét chi thứ Ba lúc 00:00 America/Chicago; tối thiểu $25 trên tổng USD sau dự phòng/khấu trừ, trước phân bổ.
- Admin chọn loại tiền/tỷ lệ tổng 100%; Owner chỉ xem. Payout giữ phiên bản khi thử lại, không chuyển lại phần thành công.
- Tắt kiếm tiền giữ khoản đã khóa và công nợ; không hồi tố click lúc tắt, tự trừ ví hoặc bù chéo Business/Personal/Ads Credit/tip.

### Ngoại lệ và rủi ro chính

- Thiếu hồ sơ/ví/cấu hình/quy đổi: giữ khoản chi, nêu lý do; không chọn thay thế.
- Tranh chấp: giữ phần liên quan. Hoàn tiền: xử lý phần chưa trả trước, không thu trùng.
- Payout một phần/timeout: đối chiếu; chỉ thử lại phần xác nhận chưa chi.
- **Cần làm rõ:** Dự phòng, loại tiền/tỷ lệ, quy đổi/phí/làm tròn và mapping điều kiện. Ví dụ 20%/30 ngày hoặc 70%/30% chưa được chốt.

### Tiêu chí hoàn thành

- Đúng quyền/consent/điều kiện; truy được nguồn/chính sách.
- Phân biệt đối soát, dự phòng, khả dụng, đang chi và đã trả.
- Đúng thu hồi, ngưỡng/kỳ chi và phân bổ; không ghi/trích/chi trùng.
- Đối chiếu payout và số dư với xác nhận ví.

### Tính năng liên quan

- **[Promotion](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/promotion-publishing-ads.md):** Cung cấp hoạt động và điều chỉnh.
- **[Ads Credit](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/merchant-ads-credit.md):** Nguồn quảng cáo, tách thu nhập.
- **[Sponsor](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/oneqr-sponsor-override.md):** Thu nhập giới thiệu riêng.
- **OneQR/Discovery, KYB, ví SSO:** Nguồn, điều kiện và nơi nhận; chưa có tài liệu đi kèm.

**Tài liệu mẫu từ PO:** [Chính sách Ads/Referral](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/references/NEXORA-OneQR-Ads-Referral-Revenue-Policy.html)
**HTML thiết kế:** [OneQR Earnings](https://taxiq-nexora-touch.vercel.app/html/pages/oneqr-earnings.html)
