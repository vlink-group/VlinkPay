## OneQR — Mở rộng mẫu theo nhiều ngành nghề

**Trạng thái:** Bản nháp — cần chốt các mục “Cần làm rõ” trước khi phát triển
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/oneqr-multi-industry-templates.md)

### Mục tiêu:

Mở rộng OneQR từ salon sang nhiều loại hình kinh doanh. Chủ doanh nghiệp chọn ngành, tùy chỉnh bộ hành động Customer rồi áp dụng. Nâng cấp bổ sung **Danh thiếp · Contact Card**, dùng lại hồ sơ doanh nghiệp và cho phép khách lưu vCard.

### Phạm vi

- Đây là phạm vi nâng cấp: code staging có Builder và lưu module, chưa có mẫu ngành hoặc Contact Card riêng.
- **Trong phạm vi:** 115 ngành/14 nhóm; tìm kiếm VI/EN; preview, sắp xếp và áp dụng template; đổi/reset nhưng giữ hành động tùy chỉnh; Contact Card, quyền riêng tư và vCard; quản trị phiên bản/audit.
- **Ngoài phạm vi:** thay đổi Staff/Owner/AIVoice; danh thiếp nhân viên; Google Business import; Wallet, trao đổi liên hệ, CRM, auto-sync; các epic khác trong handoff tổng.

### Vai trò liên quan

- **Chủ doanh nghiệp/người quản lý:** chọn, áp dụng template và cấu hình Contact Card.
- **Khách quét QR:** dùng hành động Customer và lưu vCard.
- **Admin:** quản lý ngành, module, nội dung VI/EN, phiên bản và audit.

### Luồng chính

1. Từ `QR Stations > OneQR`, người dùng chọn **Choose Industry Template** hoặc **Change industry**; không có tab Industry Templates riêng.
2. Người dùng tìm/chọn một trong 115 ngành trên màn hình picker rồi được đưa trở lại OneQR Builder.
3. Builder dựng bản nháp Customer, giữ hành động tùy chỉnh và chưa thay đổi trang live.
4. Người dùng thêm/bỏ, bật/tắt và sắp xếp trong Modules; live preview phía khách hàng cập nhật ngay.
5. Người dùng mở Contact Card ngay tại thanh công cụ Modules; dữ liệu lấy sẵn từ Business Profile và tuân theo quyền hiển thị.
6. Người dùng chọn **Save Settings**; hệ thống áp dụng nguyên tử chỉ cho Customer.
7. Builder hiển thị cấu hình mới; QR, slug, hồ sơ và analytics không đổi.

### Tính năng liên quan

- **OneQR Builder:** quản lý module sau khi áp dụng. Chưa có tài liệu đi kèm.
- **Trang OneQR công khai:** hiển thị Customer và Contact Card. Chưa có tài liệu đi kèm.
- **Business Profile:** nguồn dữ liệu Contact Card. Chưa có tài liệu đi kèm.
- **OneQR Analytics:** giữ lịch sử khi đổi template. Chưa có tài liệu đi kèm.

**Tài liệu mẫu từ PO:** [Bàn giao OneQR](https://github.com/user-attachments/files/32448615/OneQR-ban-giao-BA-Dev-QC.docx) · [Prototype v25](https://github.com/user-attachments/files/32448617/OneQR-prototype-v25.html) · [Handoff Dev/BA/QC](https://github.com/user-attachments/files/32448616/OneQR-Nexora-Handoff-Dev-BA-QC.docx) · [HTML mẫu ngành trước đây](https://taxiq-nexora-touch.vercel.app/html/pages/oneqr-industry-templates.html)
**HTML thiết kế:** [OneQR Builder](https://taxiq-nexora-touch.vercel.app/html/pages/qr-stations.html?tab=one-qr) · [Chọn ngành](https://taxiq-nexora-touch.vercel.app/html/pages/oneqr-industry-picker.html)
