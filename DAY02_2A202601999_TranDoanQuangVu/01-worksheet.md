# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4 | | | |
| 5 | | | |

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | VinFast | Repetitive | Tự động so khớp hóa đơn, giấy tờ bảo trì và chi phí phụ tùng giữa hệ thống sản xuất và kho vận hàng ngày. |
| 2 | Xanh SM | Time-consuming | Điều phối lại lộ trình tài xế khi có kẹt xe hoặc hủy chuyến, cần xử lý thủ công với nhiều cuộc gọi và cập nhật. |
| 3 | Vinhomes | AI-upgrade | Soạn thảo và phân loại phản hồi cho đánh giá 1-star của cư dân, hiện tại vẫn do nhân viên CSKH làm thủ công. |
| 4 | Vinmec | Stakeholder Pain | Quản lý lại lịch hẹn khám và nhắc bệnh nhân đến khám, giảm tình trạng hủy/không đến và quá tải phòng khám. |
| 5 | Khác (Vinpearl) | AI-upgrade | Dự đoán lưu lượng khách và phân bổ nhân sự/phòng chờ nhằm giảm thời gian xếp hàng và tăng trải nghiệm du lịch. |
---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #___                                     │
│                                                             │
│ Bài toán (1 câu): ________________________________________  │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? ______________________________________ │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. ___ ──> 2. ___ ──> 3. ___ ──> 4. ___                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? ___ (⏱ ___ phút/lượt)      │
│ AI có thể nhảy vào hỗ trợ ở bước nào? _____________________ │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? ______________________ │
│   VD: "Giảm thời gian soạn phản hồi từ 10 min ──> under 2 min"│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

### Quick Problem Card #1
Bài toán (1 câu): Tự động so khớp hoá đơn bảo trì, phiếu xuất kho và chứng từ phụ tùng giữa nhà máy VinFast và kho vận mỗi ngày.
Công ty thành viên: [x] VinFast  [ ] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)________
Ai đang đau (Actor)? Nhân viên kế toán và quản lý kho phụ tùng.
Workflow thủ công hiện tại (3-5 bước):
  1. Thu thập hoá đơn, phiếu xuất kho, và đề nghị bảo trì.
  2. So sánh thủ công từng mục phụ tùng với dữ liệu ERP.
  3. Xác nhận chênh lệch và yêu cầu làm rõ từ nhà máy/kho.
  4. Cập nhật lại hệ thống và phát hành lệnh thanh toán.
Bước nào tốn thời gian/lỗi nhất? So sánh dữ liệu thủ công và phát hiện chênh lệch (⏱ 15-25 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Bước so sánh và xác định chênh lệch giữa hoá đơn, phiếu xuất kho và dép dụng cụ.
Đo thành công bằng gì (Metric có số)? Giảm thời gian kiểm tra từ ~20 phút/lượt xuống dưới 5 phút; giảm sai sót đối chiếu xuống dưới 5%.
Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

### Quick Problem Card #2
Bài toán (1 câu): Điều chỉnh lộ trình và ưu tiên phân bổ tài xế Xanh SM khi có kẹt xe, hủy chuyến hoặc yêu cầu đặc biệt của khách.
Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)________
Ai đang đau (Actor)? Điều phối viên trung tâm điều vận và tài xế.
Workflow thủ công hiện tại (3-5 bước):
  1. Nhận báo cáo kẹt xe/hủy chuyến từ tài xế hoặc khách.
  2. Gọi điện hoặc nhắn tin cho tài xế khác để điều chuyển.
  3. Chỉnh sửa lộ trình thủ công trong hệ thống điều độ.
  4. Thông báo lại cho khách và tài xế về lịch trình mới.
Bước nào tốn thời gian/lỗi nhất? Điều chỉnh lộ trình và tìm tài xế thay thế (⏱ 10-15 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Phân tích tình huống, đề xuất lộ trình thay thế và tài xế phù hợp tự động.
Đo thành công bằng gì (Metric có số)? Giảm thời gian điều phối xuống dưới 5 phút; tăng tỷ lệ chấp nhận điều phối mới lên 80%.
Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

### Quick Problem Card #3
Bài toán (1 câu): Soạn thảo và phân loại phản hồi cho đánh giá 1-star của cư dân Vinhomes để giảm thời gian xử lý và tăng chuẩn xác.
Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  [ ] Vinmec  [ ] Khác (Ghi rõ)________
Ai đang đau (Actor)? Nhân viên chăm sóc khách hàng Vinhomes.
Workflow thủ công hiện tại (3-5 bước):
  1. Nhận đánh giá 1-star từ nền tảng quản lý cư dân.
  2. Đọc nội dung đánh giá và phân loại vấn đề.
  3. Viết phản hồi thủ công hoặc chuyển sang bộ phận liên quan.
  4. Gửi phản hồi và theo dõi hành động khắc phục.
Bước nào tốn thời gian/lỗi nhất? Đọc, phân loại và soạn thảo phản hồi phù hợp (⏱ 12-18 phút/lượt).
AI có thể nhảy vào hỗ trợ ở bước nào? Phân tích nội dung đánh giá, phân loại nguyên nhân và sinh phản hồi mẫu theo chính sách.
Đo thành công bằng gì (Metric có số)? Giảm thời gian soạn trả lời từ 15 phút xuống còn 3 phút; đạt 90% phản hồi phù hợp với kịch bản CSKH.
Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent

> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
