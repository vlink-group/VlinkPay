# Spec: Check-In 1-Page dùng chung (Kiosk + POS Front Desk)

**Ngày chốt:** 2026-08-17
**Nguồn:** phiên `/brainstorm` với TL, 14 câu hỏi; mockup do PO cung cấp
**Trạng thái:** Implemented 2026-08-18 — đã live-test cả 2 bề mặt (chưa commit)
**Thay thế:** phần Create mode của `PosOrderWorkspace` và bố cục wizard của `SelfCheckInFlow`

---

## 1. Bối cảnh — vì sao có spec này

Tab Check-in của POS và màn self check-in của khách được xây riêng, nên trôi xa nhau. Ba lần chỉnh "cho giống" đều thất bại vì mỗi lần chỉ chạm phần vỏ:

1. Lần 1 — copy class Tailwind sang POS. Khung giống, ruột khác.
2. Lần 2 — tách `CheckInStepFrame` dùng chung. Khung giống thật, nhưng ruột mỗi bước vẫn là component riêng của POS.
3. Lần 3 — POS render trực tiếp `CustomerNameStep` / `SelectTechnicianStep` / `SelectServicesStep` của kiosk. Gần đúng, nhưng vẫn là "sửa cho giống".

Kết luận của TL: **thay thế**, không sửa tiếp. Giữa phiên, PO đổi hướng thêm một lần nữa — **không dùng wizard, dùng 1-page**.

> ⚠️ Bài học ghi lại: khi yêu cầu là "hai màn phải giống hệt", giải pháp duy nhất bền vững là **cùng một component**, không phải hai component được canh cho khớp.

---

## 2. Quyết định đã chốt

| # | Câu hỏi | Chốt | Ghi chú |
|---|---------|------|---------|
| 1 | Tính năng chỉ POS có | Bỏ hết | *Đảo một phần ở câu 10 — xem mục 8* |
| 2 | Bán sản phẩm rời (product-only checkout) | **Chấp nhận mất** | Không còn đường bán khi khách không check-in |
| 3 | Sau khi Check In | Màn cảm ơn có số thứ tự, **đứng yên** tới khi bấm Done | Kiosk vẫn tự về — cờ duy nhất giữa 2 bề mặt |
| 4 | Nguồn danh sách thợ | Theo luật kiosk: clock-in **và** có ≥1 skill | Không dùng Turn Board nữa |
| 5 | Cảnh báo lượt đang mở | Mang sang nguyên vẹn, kể cả chữ 2 nút | Vị trí chốt ở câu 14 |
| 6 | Kiến trúc | Một component chung, bề mặt tối thiểu | |
| 7 | Cắt chuyển | Thay thẳng | *Đảo ở câu 9 — giữ code cũ làm module* |
| 8 | Kiosk có đổi sang 1-page không | **Có** | Giữ được cam kết "một component chung" |
| 9 | Code wizard cũ | **Giữ**, bật/tắt bằng **setting per-business** | |
| 10 | Khối nào ẩn với khách | **Không ẩn gì** | Khách thấy cả badge bận lẫn ô Note |
| 11 | Name bắt buộc | **Cả hai bề mặt** | |
| 12 | Checkbox SMS | **Tick sẵn + bắt buộc** | ⚠️ xem cảnh báo mục 7 |
| 13 | Số điện thoại trên trang | Trong card đầu + link **Đổi số** | Mockup thiếu, đã bổ sung |
| 14 | Vị trí cảnh báo lượt mở | **Màn chặn riêng**, xen giữa bàn phím và trang | |
| — | Nút Cancel | Góc trên phải trang, xoá nháp về bàn phím | TL bổ sung |

---

## 3. Kiến trúc module

```
src/components/checkin/
  layouts/
    WizardCheckInLayout.tsx        ← flow từng bước hiện tại; GIỮ NGUYÊN, không mặc định
    SinglePageCheckInLayout.tsx    ← mặc định mới, theo mockup PO
  parts/                           ← dùng chung cho cả hai layout
    CustomerIdentityCard.tsx       ← phone + Đổi số + Name + checkbox SMS
    TechnicianPickerGrid.tsx       ← (đã có) thêm badge available/busy
    ServiceCatalogSection.tsx      ← chip danh mục + lưới thẻ + Note
    SelectedServicesSummary.tsx    ← chip đã chọn + Services/Total time/Total
    ActiveVisitInterstitial.tsx    ← màn chặn 2 nút
    ThankYouScreen.tsx             ← số thứ tự + Done
    CheckInStepFrame.tsx           ← (đã có) chỉ wizard dùng
  useCheckInSession.ts             ← toàn bộ state + submit; KHÔNG biết layout nào đang vẽ
```

**Nguyên tắc:** cả hai layout nhận cùng `useCheckInSession` + cùng nguồn dữ liệu tiêm từ ngoài. Kiosk tiêm hook device-auth, POS tiêm hook merchant Bearer. Đổi layout không đụng một dòng logic nào.

**Lý do đặt tên `Wizard*` / `SinglePage*`:** để lần sau thêm mode thứ ba thì chỗ cần đọc là hiển nhiên, và không ai phải đoán "file nào là cái đang chạy".

---

## 4. Bố cục 1-page

### Bước 1 — bàn phím số điện thoại
Đủ 10 số tự chuyển, không cần nút. Dùng lại `PhoneCheckInStep` hiện có.

### Bước 1.5 — chặn nếu đang có lượt mở
Chỉ hiện khi số đó có order `Waiting`/`InService`. Hai nút: *"That's me — I'm all set"* (thoát) / *"Check in another guest"* (đi tiếp).

### Bước 2 — một trang duy nhất

| Card | Nội dung |
|------|----------|
| **Nice to meet you!** | số điện thoại + link **Đổi số** · ô **Name (bắt buộc)** · checkbox SMS (tick sẵn, bắt buộc) |
| **Technician** — *optional, "First available" is fastest* | lưới thẻ: First available (*shortest wait*) + từng thợ kèm badge `available` / `busy now` |
| **Choose services** — *Optional: tap a category chip, then tap a service card…* | chip danh mục có số đếm → lưới thẻ dịch vụ (giá, thời lượng, View details, badge `add-on`) → ô **Note** gập được → **Selected services** dạng chip có nút xoá → hàng tổng: **Services** / **Total time** / **Total** |
| **CTA** | `Check me in (N selected)` — nút gradient chạy hết bề ngang |

Nút **Cancel** ở góc trên phải trang.

### Sau khi submit
Màn cảm ơn với số thứ tự cỡ lớn.
- **POS:** đứng yên tới khi nhân viên bấm `Done`.
- **Kiosk:** tự về bàn phím sau đếm ngược (máy đặt ở cửa, không ai bấm hộ).

---

## 5. Khác biệt giữa hai bề mặt

Chỉ còn **một** cờ hành vi:

| Cờ | Kiosk | POS |
|---|---|---|
| `autoReturnSeconds` | có | không (đứng yên tới khi bấm Done) |

Ngoài ra khác nhau **chỉ ở nguồn dữ liệu tiêm vào**. Không có cờ nào cho nội dung hiển thị.

---

## 6. Backend

| Việc | Chi tiết |
|------|----------|
| 2 field cấu hình | `KioskCheckInLayout`, `FrontDeskCheckInLayout` — enum `Wizard \| SinglePage`, mặc định `SinglePage` |
| UI cấu hình | POS General Settings, 2 lựa chọn tách biệt |
| Endpoint mới | `GET /merchant/pos/{businessId}/checkin/technicians` — bản Bearer của query kiosk: thợ clock-in + có ≥1 skill, kèm `serviceIds` **và `isBusy`** |
| Endpoint mới | `GET /merchant/pos/{businessId}/checkin/active-visit?phone=` — bản Bearer |
| Mở rộng | endpoint technicians của kiosk trả thêm `isBusy` (câu 10: khách cũng thấy) |
| Kiosk đọc layout | qua `GET /pos-device/self-checkin/context` (kiosk không có phiên merchant) |
| Dùng lại nguyên | `CheckInOrderCommand` · `CheckInBookingCommand` (đã có `Items`/`CustomerName`/`CustomerEmail`) · catalog dịch vụ · customer lookup · booking list/detail |

---

## 7. Business rules

- **Name bắt buộc** ở cả hai bề mặt.
- **Checkbox SMS tick sẵn và bắt buộc.**
  > ⚠️ **Rủi ro pháp lý đã được nêu và TL vẫn giữ nguyên lựa chọn.** Theo TCPA, tick sẵn không tính là đồng ý chủ động, và ép đồng ý nhận **marketing** ("offers, reminders & rewards") mới được phục vụ là phương án rủi ro nhất trong 3 phương án đã trình bày. Đây là quyết định có ý thức, không phải sơ suất. Quyết định 2026-08-12 (consent transactional tick sẵn + bắt buộc) vẫn giữ nguyên giá trị và không mâu thuẫn.
- Thợ chọn trước chỉ **tự gán** cho dịch vụ họ có skill; dịch vụ còn lại để `null` cho quầy xử lý. Không chặn khách chọn dịch vụ thợ đó không làm được.
- Khách **có booking hôm nay** → prefill thẳng vào trang; `Check me in` **chuyển đổi booking** (đổi `Status`, cấp `OrderNumber`) chứ không tạo order thứ hai.
- Không còn tab Products, không còn ô Email, không còn bán sản phẩm rời.

---

## 8. Những chỗ đảo hướng trong phiên

| Chốt sớm | Bị thay bởi | Vì sao |
|---|---|---|
| Bỏ ô Note, bỏ badge bận | Câu 10 — hiện cho cả khách | Mockup PO có cả hai |
| Xoá code cũ, thay thẳng | Câu 9 — giữ wizard làm module + setting | Phòng PO đổi ý, và để thêm mode sau này |
| Wizard 4 bước | Câu 8 — 1-page 2 bước | PO không muốn wizard |

---

## 9. Việc đã làm sẵn trước phiên này (dùng lại được)

- `CheckInStepFrame`, `TechnicianPickerGrid`, `CheckInServiceLineRow` trong `src/components/checkin/` — đã tách và đang được kiosk dùng.
- `CheckInBookingCommand` đã nhận `Items` / `CustomerName` / `CustomerEmail` optional; `PosOrderDraftLines` tách dùng chung với `CheckInOrderCommand`.
- Tab Check-in của POS **đã** chuyển đổi booking thay vì tạo order trùng (`useCheckInBookingWithDraft`).
- Prefill từ booking hôm nay đã chạy ở cả hai bề mặt.

---

## 10. Success criteria

1. Cùng một layout render ở `/self-checkin` và tab Check-in; ảnh chụp chỉ khác phần chrome quanh tab.
2. Đổi setting sang `Wizard` → layout cũ chạy lại nguyên vẹn, **không sửa dòng code nào**.
3. Walk-in ở POS → order `Waiting` đúng thợ đã chọn.
4. Khách có booking → **1** order duy nhất, cùng `Id` với booking; tab Bookings hiện `Checked In`.
5. Bỏ trống Name hoặc bỏ tick SMS → `Check me in` không bấm được, ở cả hai bề mặt.
6. Gõ nhầm số → thấy số trên trang và sửa được qua link **Đổi số**.
7. Số đang có lượt mở → hiện màn chặn trước khi vào trang.

---

## 11. Việc còn treo / rủi ro

- ~~**Add-on**~~ — đã xác minh từ catalog khi implement: add-on là **một category** ("Add-ons"), không phải cờ trên từng dịch vụ. Nên hiển thị như dịch vụ thường dưới chip category của nó, không badge riêng, không ràng buộc "phải kèm dịch vụ chính". Không cần hỏi PO.
- **Checkbox SMS chưa có nơi lưu trên nhánh này.** Bảng consent nằm ở nhánh `feature/booking-consent`, chưa merge — nên checkbox hiện chỉ chặn nút `Check me in` ở FE, không ghi xuống DB. Khi nhánh kia merge phải nối vào `useCheckInSession.smsConsent`.
- **Không có test tự động cho POS** — toàn bộ đảm bảo dựa vào kiểm thử tay, và từ nay là **hai** layout phải kiểm mỗi lần sửa. Đây là chi phí trực tiếp của quyết định câu 9.
- **Mất đường bán sản phẩm rời** là mất tính năng đang chạy, không phải dọn code thừa.
- **Mất ô Email** ở luồng check-in — receipt hiện chỉ còn SMS hoặc không.
