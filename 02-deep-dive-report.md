# 📄 02-deep-dive-report.md — Báo cáo Deep-Dive (Bài nhóm)

**Nhóm:** L-GPT
**Thành viên:** 
1.Nguyễn Hoài Nam - 2A202602016
2.Nguyễn Anh Tú - 2A202601825
3.Trần đoàn Quang Vũ - 2A202601999
4.phan trần tường vy-2A202601701
5.Nguyễn Quang vinh - 2A2002601517
6.nguyễn minh hiếu - 2A202601685
---

## ✅ Quyết định lựa chọn bài toán Deep-Dive

Sau khi thảo luận, cả nhóm thống nhất chọn bài toán:

> **"Hệ thống dispatcher gợi ý trạm sạc / xử lý tình huống khẩn cấp khi pin xe điện Xanh SM ở mức nguy hiểm (Critical Battery Dispatch Co-Pilot)"** thuộc mảng **Xanh SM (GSM)**.

**Lý do chọn:** Đây là bài toán có ranh giới an toàn (safety boundary) rõ ràng, ảnh hưởng trực tiếp đến trải nghiệm và an toàn của tài xế/khách hàng, đồng thời phù hợp để prototype bằng LLM có Operational Boundary nghiêm ngặt — khớp với phần Technical Prompt Prototype (`prompt_prototype.py`) nhóm đã xây dựng ở Phase 4.

---

## 🏗️ Phase 3 — DEEP-DIVE

### 3.2. Problem Statement (6-field) & Metrics

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Tài xế xe điện Xanh SM (VinFast VF8, VF9, Feliz S...) đang vận hành trên đường, và nhân viên tổng đài điều vận (dispatcher) hỗ trợ xử lý tình huống khẩn cấp. |
| **2. Current Workflow** | Khi pin xe xuống thấp, tài xế tự tra cứu bản đồ trạm sạc gần nhất trên app riêng lẻ (không tích hợp với hệ thống điều vận), tự ước lượng quãng đường còn lại có đủ pin để tới trạm hay không, và tự gọi hotline nếu cần hỗ trợ khẩn cấp. Toàn bộ quá trình xử lý thủ công, không có cảnh báo chủ động từ hệ thống trung tâm. |
| **3. Bottleneck** | Không có bước tự động đánh giá mức độ khẩn cấp theo % pin thực tế và khoảng cách tới trạm sạc; tài xế có thể tự ý chọn trạm quá xa dẫn đến hết pin giữa đường (chết máy), hoặc tổng đài phản hồi chậm khi tài xế gọi khẩn cấp. |
| **4. Business Impact** | Xe hết pin giữa đường gây gián đoạn dịch vụ, ảnh hưởng SLA đón/trả khách, tốn chi phí điều xe cứu hộ/sạc di động phát sinh ngoài kế hoạch, và ảnh hưởng tiêu cực đến uy tín thương hiệu Xanh SM nếu khách hàng bị ảnh hưởng bởi sự cố. |
| **5. Success Metric** | 100% các trường hợp pin < 5% được hệ thống tự động phát hiện và phản hồi trong vòng dưới 10 giây; giảm số ca xe hết pin giữa đường (không tới được điểm sạc) xuống gần 0% trong các trường hợp hệ thống được kích hoạt đúng. |
| **6. Operational Boundary** | AI **được phép**: soạn draft tin nhắn hướng dẫn tài xế, đề xuất trạm sạc trong bán kính an toàn, kích hoạt yêu cầu điều xe sạc di động (mobile charger) khi pin < 5%. AI **tuyệt đối không được phép**: tự động gửi tin nhắn mà không qua tag `[DRAFT_ONLY]` để con người duyệt, và không được đề xuất trạm sạc xa hơn 5km khi pin ở mức nguy hiểm (< 5%) dù người dùng có yêu cầu. Mọi hành động thực tế (gửi tin, điều xe) đều cần con người xác nhận trước khi thực thi. |

### 3.3. Future-State Flow & AI Fit

**AI-Fit Matrix:** ☑ **LLM Feature** (kết hợp Rule cứng cho ngưỡng an toàn pin < 5%, không dùng Agentic Loop vì cần kiểm soát chặt chẽ hành động thực thi).

**Future-State Flow (text-diagram):**

```
[Tài xế báo % pin + vị trí GPS]
            │
            ▼
   🔵 AI Step: Phân tích % pin + tính khoảng cách tới các trạm sạc gần nhất
            │
            ▼
     Pin ≥ 5%? ──── Có ──▶ 🔵 AI Step: Soạn draft gợi ý trạm sạc phù hợp
            │                          (kèm tag [DRAFT_ONLY])
            │ Không (Pin < 5%, Critical)              │
            ▼                                          ▼
   🔵 AI Step: Trigger JSON                   🟢 Human Step (HITL):
   {"action": "dispatch_mobile_charger",       Dispatcher xem draft,
    "reason": "..."}                           duyệt & gửi cho tài xế
            │                                          │
            ▼                                          ▼
   🟢 Human Step (HITL): Dispatcher xác nhận     Tài xế nhận hướng dẫn
   điều xe sạc di động thực tế                    di chuyển tới trạm
            │
            ▼
   ↩️ Fallback: Nếu AI không chắc chắn về vị trí/khoảng cách
      (dữ liệu GPS lỗi, thiếu thông tin trạm) → tự động chuyển
      thẳng qua tổng đài viên con người xử lý, không tự suy đoán.
```

- 🔵 **AI Step:** Phân tích mức pin, tính khoảng cách, soạn draft tin nhắn/JSON dispatch.
- 🟢 **Human Step (HITL):** Dispatcher luôn là người xác nhận cuối cùng trước khi gửi tin hoặc điều xe sạc di động thực tế — AI không tự động thực thi hành động.
- ↩️ **Fallback:** Khi thiếu dữ liệu đáng tin cậy (GPS không chính xác, không có trạm sạc nào trong bán kính an toàn), hệ thống chuyển ngay sang xử lý bởi con người thay vì để AI tự đoán.

---

## 🏁 Phase 5 — EVALUATE

### AI Readiness Checklist:
1. [x] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test? — *Có dữ liệu log cảnh báo pin và vị trí GPS lịch sử từ đội xe Xanh SM để làm dữ liệu test ban đầu.*
2. [x] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)? — *Có, nhờ cơ chế `[DRAFT_ONLY]` bắt buộc và Fallback chuyển sang người khi không chắc chắn, mọi hành động thực thi đều qua con người duyệt.*
3. [x] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ? — *Đội ngũ điều vận và tài xế đã quen thao tác qua app, việc thêm một bước gợi ý tự động từ AI không làm thay đổi lớn quy trình hiện có.*

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

☑ **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**

> Bài toán có ranh giới an toàn rõ ràng và có thể kiểm soát rủi ro tốt thông qua thiết kế Operational Boundary nghiêm ngặt (đã được stress-test qua 3+ adversarial test cases trong `prompt_prototype.py`, bao gồm cả các kịch bản cố tình yêu cầu bỏ qua tag `[DRAFT_ONLY]` hoặc đề xuất trạm sạc xa khi pin nguy hiểm). Chi phí triển khai ban đầu thấp vì chỉ cần một LLM feature xử lý văn bản/JSON đơn giản, không cần xây dựng Agentic Loop phức tạp hay tự động hóa hành động thực (gửi tin/điều xe vẫn qua con người xác nhận). Rủi ro kỹ thuật chính (AI đề xuất sai trạm sạc, bỏ qua ngưỡng an toàn) đã được kiểm chứng có thể chặn được bằng system prompt và test case cụ thể. Vì vậy nhóm đề xuất **GO** với phạm vi hẹp: chỉ triển khai thí điểm cho các trường hợp pin < 5% trước, sau đó mở rộng dần sang các mức pin khác khi đã có đủ dữ liệu thực tế để tinh chỉnh ngưỡng khoảng cách và độ chính xác gợi ý trạm sạc.