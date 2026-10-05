## POS — Cấu hình Steps và Materials cho dịch vụ

**Trạng thái:** Đang rà soát
**Bản chia sẻ:** [Bản tài liệu đầy đủ](https://github.com/vlink-group/VlinkPay/blob/docs/promotion-code-skill-audit/nexora/docs/business/pos-service-steps-materials.md)

### Mục tiêu:

Chuẩn hóa hướng dẫn dịch vụ thành các bước có ảnh và phần nguyên vật liệu riêng; cập nhật mà không mất nội dung cũ.

### Phạm vi

- **Trong phạm vi:** Cấu hình Steps và Materials trong Edit Service; thêm/xóa/sắp xếp bước, chụp/chọn/thay/xóa ảnh; lưu/hủy cùng dịch vụ; chuyển nội dung cũ để quản lý tự phân chia lại; giữ khóa chỉnh sửa với Custom service.
- **Ngoài phạm vi:** Màn hình hướng dẫn riêng cho nhân viên/khách; tồn kho/định mức; tự tính Supply Fee; quy trình duyệt hướng dẫn riêng.
- Code staging hiện chỉ lưu một mô tả chung và ảnh dịch vụ. Steps/Materials là yêu cầu mới; cần chốt contract máy chủ và đồng bộ thiết bị. Cách lưu trong HTML là hành vi prototype.

### Vai trò liên quan

- **Người quản lý cấu hình dịch vụ:** Dùng quyền chỉnh sửa dịch vụ hiện có để soạn/lưu/hủy hướng dẫn. Không cấp thêm quyền cho nhân viên/khách.

### Luồng chính

1. Mở **POS → Salon Settings → Services → View / Edit**. Steps nằm sau Require approval; Materials nằm dưới Add step.
2. Hiển thị các bước đã lưu hoặc một bước trống. Nhập **Title** và **Description** cho từng bước.
3. Dùng **Take photo / Choose image** để gắn ảnh vào đúng bước; xem trước, thay hoặc **Remove image** khi cần.
4. **Add step** thêm cuối danh sách; **Remove** xóa cả bước. Kéo tay nắm hoặc dùng **Alt + ↑/↓** để đổi thứ tự, giữ ảnh/nội dung đi cùng bước.
5. Nhập **Materials** có định dạng dùng chung cho toàn bộ dịch vụ, không phải cho từng bước.
6. **Save changes** lưu cùng thông tin dịch vụ khi biểu mẫu hợp lệ và ảnh xử lý xong; **Cancel/đóng form** bỏ thay đổi chưa lưu.
7. Mở lại đúng nội dung/thứ tự đã lưu, kể cả mở dịch vụ từ category khác. Lưu thất bại thì giữ bản đang nhập để thử lại.

### Tính năng liên quan

Các phần dưới đây chưa có tài liệu riêng đi kèm trong nguồn:

- **Salon Settings / Services:** Nơi quản lý dịch vụ và mở biểu mẫu hướng dẫn.
- **Edit Service:** Lưu/hủy Steps và Materials cùng thông tin dịch vụ.
- **Categories:** Một dịch vụ thuộc nhiều nhóm nhưng dùng chung hướng dẫn.
- **Service image:** Ảnh đại diện độc lập với ảnh từng Step.
- **Supply Fee:** Phí cấu hình riêng, không tính từ Materials.
- **Require approval:** Thiết lập sẵn có, không tạo quy trình duyệt hướng dẫn riêng.

**HTML thiết kế:** [Mở Salon Settings / Services — chọn View / Edit của dịch vụ](https://taxiq-nexora-touch.vercel.app/html/pages/pos-salon-settings.html?section=services)
