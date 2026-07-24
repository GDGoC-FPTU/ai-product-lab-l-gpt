# Phase 3 — DEEP-DIVE (Nhóm)

## 1. Quyết định lựa chọn bài toán

Nhóm lựa chọn bài toán:

**“Xử lý sự cố pin thực địa của tài xế Xanh SM”**

Lý do lựa chọn:
- Bài toán có tính lặp lại và dễ mô tả quy trình vận hành.
- Bước xử lý chính là tra cứu trạm sạc và soạn tin nhắn hướng dẫn, dễ xác định bottleneck.
- Có thể đo được bằng thời gian xử lý/lượt.
- Rủi ro hành vi sai có thể kiểm soát bằng human-in-the-loop.

---

## 2. Problem Statement (6-field)

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Điều phối viên (Dispatcher) tại trung tâm điều vận Xanh SM. |
| **2. Current Workflow** | Khi tài xế báo sự cố pin yếu hoặc hết pin trên đường, điều phối viên phải tra cứu vị trí xe trên hệ thống định vị, tìm trạm sạc phù hợp, soạn tin nhắn chỉ dẫn và gửi thông tin qua kênh App. |
| **3. Bottleneck** | Bước tra cứu trạm sạc phù hợp và soạn thảo thông tin hướng dẫn cho tài xế là bước tốn thời gian nhất, mất khoảng 10–12 phút mỗi lần. |
| **4. Business Impact** | Mỗi sự cố không được xử lý kịp thời có thể kéo dài thời gian chờ của tài xế, làm giảm năng suất điều phối và ảnh hưởng doanh thu / SLA vận hành. |
| **5. Success Metric** | Giảm thời gian xử lý sự cố từ 12 phút xuống còn dưới 3 phút; đạt tỷ lệ hướng dẫn đúng địa điểm và trạm sạc phù hợp ≥ 98%. |
| **6. Operational Boundary** | AI được phép đề xuất trạm sạc và draft tin nhắn, nhưng không được tự gửi mà không có phê duyệt của điều phối viên. Nếu pin < 5%, AI phải ưu tiên đề xuất xe cứu hộ pin di động thay vì đề xuất trạm sạc xa. |

---

## 3. Future-State Flow & AI Fit

### AI Fit

Chọn mức độ: **LLM Feature**

Lý do:
- Đề bài có quy trình có cấu trúc rõ ràng.
- Không cần bắt đầu bằng một agent phức tạp với nhiều bước tự chủ.
- AI nên giúp ở giai đoạn “draft + recommend”, còn con người giữ quyền gửi và phê duyệt cuối cùng.

### Future-State Flow

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Tài xế báo    │ ──→ │ 🔵 AI pull   │ ──→ │ 🔵 AI draft  │ ──→ │ 🟢 Dispatcher│
│ sự cố pin    │     │ vị trí + trạm │     │ tin nhắn chỉ │     │ duyệt & gửi │
│              │     │ sạc phù hợp  │     │ đường         │     │ tài xế       │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ↩️ Fallback:
                                                               Nếu AI không chắc chắn,
                                                               dispatcher tự xử lý thủ công
                                                               như quy trình cũ.
```

---

## 4. Evaluate

### AI Readiness Checklist

1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test.
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát qua HITL và fallback.
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ.

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

[ ] **GO**
[ ] **NOT YET**
[x] **NO-GO**

### Justification

Bài toán này về mặt ý tưởng là hợp lý và phù hợp với AI, nhưng trong bối cảnh lab hiện tại, nhóm nên đánh giá đây là **NO-GO ở mức dự án nhóm** vì:
- phạm vi quá nhỏ và có thể giải quyết bằng rule-based hoặc workflow tối ưu đơn giản hơn.
- AI chỉ mang lại lợi ích trong việc draft nội dung, nhưng không tạo ra bước thay đổi cốt lõi cho quy trình.
- Nếu mục tiêu là hiệu quả tài chính và độ chắc chắn, giải pháp rule-based hoặc dashboard hỗ trợ manual sẽ an toàn và nhanh hơn.

Tuy nhiên, nếu mở rộng sang hệ thống “sự cố pin theo thời gian thực + mối tương tác GPS + hệ thống trạm sạc + điều phối xe cứu hộ”, bài toán này có thể chuyển sang **GO** ở mức sản phẩm thực tế.
