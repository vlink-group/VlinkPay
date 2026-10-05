## Bộ tiêu chuẩn vận hành và Sổ tay nhân viên

**Trạng thái:** Define
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/pos-operating-standards-staff-handbook.md)

### Mục tiêu:

Cung cấp nơi để Owner/Manager tạo, quản lý và công bố tài liệu vận hành của tiệm. Staff đọc nội dung đã công bố qua Staff Handbook, giúp tiệm thống nhất nội quy và quy trình làm việc. Tiệm tự chuẩn bị nội dung phù hợp và dùng mẫu hệ thống làm điểm bắt đầu.

### Phạm vi

- **Trong phạm vi:** Quản lý tại Salon Settings → Operating Standards; thư viện System Templates; tạo mới/từ mẫu, editor, tìm kiếm/lọc, publish/unpublish, in và xóa; Staff Handbook; Recently Deleted, khôi phục và xóa vĩnh viễn.
- **Ngoài phạm vi:** Lịch sử phiên bản trên giao diện; ký điện tử và xác nhận đã đọc; theo dõi tiến độ checklist; AI tự sinh nội dung; đồng bộ tự động với cấu hình turn; trạng thái Archive.
- Đây là yêu cầu cần triển khai từ ticket và HTML. Code staging được rà soát chưa có phần Operating Standards/Staff Handbook và contract chuyên biệt cho tài liệu của tiệm.

### Vai trò liên quan

- **Owner/Manager:** Chuẩn bị và quản lý tài liệu của tiệm; công bố/ngừng công bố, in, xóa và khôi phục.
- **Staff:** Đọc và in nội dung đã công bố trong Staff Handbook của business được phép truy cập.
- **Hệ thống:** Lưu và phục vụ nội dung theo quyền/business, quản lý bản soạn và nội dung công bố.

### Luồng chính

1. Owner/Manager mở **Salon Settings → Operating Standards**, tìm tài liệu hoặc chọn tạo mới.
2. Chọn tài liệu trống hoặc **Use template** từ thư viện mẫu hệ thống.
3. Soạn tên, loại, mô tả, các mục và nội dung bằng ngôn ngữ tiệm sử dụng.
4. Lưu bản **Draft** để tiếp tục chuẩn bị và kiểm tra nội dung.
5. Owner/Manager **publish** nội dung đã kiểm tra.
6. Staff mở **Staff Handbook**, chọn tài liệu đang công bố để đọc hoặc in.
7. Owner/Manager quản lý cập nhật tiếp theo: sửa bản soạn, unpublish hoặc xóa; vào **Recently Deleted** khi cần khôi phục hay xử lý tài liệu đã xóa.

### Tính năng liên quan

- **Salon Settings:** Là điểm vào quản lý Operating Standards của tiệm. Chưa có tài liệu đi kèm cho điểm vào này.
- **Quyền và vai trò POS:** Xác định phạm vi quản lý của Owner/Manager và phạm vi đọc/in của Staff theo business. Chưa có tài liệu đi kèm cho phân quyền của tính năng mới.
- **Staff Handbook:** Giao diện đọc cùng bộ tài liệu đã công bố, được mô tả trong bản tài liệu đầy đủ phía trên.

<img width="933" height="665" alt="Image" src="https://github.com/user-attachments/assets/b228ff6a-9aa7-45cd-b7a0-f5bb4fcd10d9" />
<img width="836" height="1179" alt="Image" src="https://github.com/user-attachments/assets/240c703c-cd91-46d1-8883-f3e558733630" />

**Tài liệu mẫu từ PO:** [TurnBoardBanMau.html](https://github.com/user-attachments/files/31445416/TurnBoardBanMau.html)
**HTML thiết kế:** [Tiệm — Operating Standards](https://taxiq-nexora-touch.vercel.app/html/pages/pos-operating-standards.html) · [Thợ — Staff Handbook](https://taxiq-nexora-touch.vercel.app/html/pages/staff-handbook.html)
