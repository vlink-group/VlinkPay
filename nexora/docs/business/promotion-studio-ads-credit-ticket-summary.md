## Nạp Ads Credit & chạy quảng cáo — Tổng quan kết nối

**Trạng thái:** Đang rà soát
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/promotion-studio-ads-credit-overview.md)
**Ticket:** [#1778](https://github.com/vlink-group/vlink-nexora/issues/1778) — Confirmed, chưa bắt đầu xử lý khi rà soát ngày 5 tháng 10 năm 2026.

### Mục tiêu:

Kết nối ưu đãi với quảng cáo và nguồn Ads Credit để Owner kiểm soát nội dung, ngân sách, chi phí và hiệu quả.

### Phạm vi

- **Đã có trong code staging:** Quản lý Promotion, banner, áp dụng tại POS; Ads Credit có tab riêng, nạp thẻ/ví, số dư, lịch sử và biên nhận.
- **Cần tích hợp:** Public approval, Paid Boost, campaign → nạp → quay lại, ghi chi phí quảng cáo, báo cáo và tự chạy lại khi đủ credit. Chưa thấy hành trình hoàn chỉnh trong hai repository FE/BE.
- **Phân chia:** #1747 quản lý Promotion/quảng cáo; #1749 quản lý Ads Credit. Tài liệu hai ticket đang In Progress/Testing được giữ nguyên.
- **Ngoài phạm vi:** Xây quy trình gửi tin, đối soát đối tác hoặc payout riêng; mặc định dùng Ads Credit thanh toán AI, SMS hay quảng cáo ngoài Nexora.

### Vai trò liên quan

- **Owner:** Xác nhận nội dung, kênh, ngân sách và thanh toán.
- **Người được phân quyền:** Chuẩn bị nội dung; quyền này không tự bao gồm chi tiền.
- **Admin:** Kiểm duyệt theo quyền; **Khách:** sử dụng ưu đãi; **Support:** tra cứu trạng thái.

### Luồng chính

1. Tạo Promotion, kiểm tra ưu đãi, lịch và banner.
2. Chọn Internal tại tiệm hoặc gửi Public để duyệt; lưu cờ gửi chưa phải được duyệt.
3. Thiết lập Paid Boost với đối tượng, vị trí, lịch, ngân sách và mô hình phí.
4. Chọn Ads Credit; 💰 nạp thẻ hoặc ví được hỗ trợ nếu thiếu. Theo dõi đơn cũ khi chưa rõ kết quả.
5. Chỉ phân phối khi đủ duyệt/quyền/lịch/ngân sách/credit; 💰 ghi phí theo hoạt động hợp lệ.
6. Thiếu credit thì dừng; sau nạp chỉ tự chạy lại campaign còn đủ điều kiện. Đây là yêu cầu tích hợp.
7. Theo dõi kết quả theo kênh; đối chiếu chi phí với Ads Credit.

### Quy tắc nghiệp vụ quan trọng

- Ngân sách là hạn mức, không phải khoản bị trừ toàn bộ khi tạo campaign.
- Internal không yêu cầu credit cho phí quảng cáo network; Public không tự bật Paid Boost.
- CPC/CPL/CPA/Sponsored Placement áp dụng theo mô hình chấp thuận.
- Credit không hết hạn, không tự nạp; nạp không thay duyệt hoặc tự bật campaign Owner đã dừng.
- Đơn nạp có Đang xử lý/Hoàn tất/Không thành công; chỉ xác nhận cấp credit mới cập nhật số dư, không cộng trùng.
- Banner check-in đang bật chưa chứng minh ưu đãi đủ điều kiện POS.

### Ngoại lệ và rủi ro chính

- Thanh toán timeout: tra cứu, đối chiếu; không tự trả lại lần nữa.
- Public bị từ chối, campaign hết lịch hoặc bị hạn chế: hiển thị đúng lý do.
- Chưa tích hợp kênh hoặc chưa có dữ liệu: không báo đã phân phối hay hiển thị số mẫu.

### Tiêu chí hoàn thành

- Giữ đúng Promotion/cấu hình khi đi nạp và quay lại.
- Phân biệt kết quả thanh toán, cấp credit và trạng thái campaign.
- Chỉ chạy/ghi phí khi đủ điều kiện; không vượt ngân sách hoặc khôi phục sai lý do.
- Báo cáo có dữ liệu thật, chi phí truy được nguồn.

### Tính năng liên quan

- **[Promotion Studio](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/promotion-publishing-ads.md):** Nội dung, kênh, duyệt và quảng cáo.
- **[Ads Credit](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/merchant-ads-credit.md) / [phạm vi triển khai](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/merchant-ads-credit-ticket.md):** Nạp, số dư và chi phí.
- **[OneQR Earnings](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/business-oneqr-earnings.md) / [Sponsor Override](https://raw.githubusercontent.com/vlink-group/VlinkPay/main/nexora/docs/business/oneqr-sponsor-override.md):** Thu nhập và payout từ sự kiện xác nhận.

**HTML thiết kế:** [Promotion](https://taxiq-nexora-touch.vercel.app/html/pages/reward-promotions.html) · [Ads Credit](https://taxiq-nexora-touch.vercel.app/html/pages/nexora-packages.html?tab=ads-credit)
