# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

### 📝 List bài toán của tôi:

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Xanh SM | Pain từ người khác (Stakeholder Pain) | Tài xế thường xuyên phàn nàn hệ thống điều vận (dispatch) gợi ý điểm đón khách sai vị trí thực tế hoặc quá xa, gây mất thời gian di chuyển và giảm số chuyến/giờ. |
| 2 | VinFast | Lặp lại (Repetitive) | Nhân viên kỹ thuật phải thủ công đối chiếu hàng trăm log cảnh báo pin (battery alert logs) mỗi ngày để lọc ra cảnh báo thật cần xử lý và cảnh báo giả (false positive). |
| 3 | Vinhomes | Tốn thời gian (Time-consuming) | Nhân viên chăm sóc cư dân mất trung bình 8-10 phút để soạn một phản hồi cho mỗi đánh giá tiêu cực (1-2 sao) trên ứng dụng quản lý căn hộ, do phải đọc kỹ và cá nhân hóa từng phản hồi. |
| 4 | Vinmec | AI có thể tốt hơn (AI-upgrade) | Quy trình đặt lịch khám hiện tại qua tổng đài phản hồi chậm (khách phải chờ trung bình 5-7 phút), không kiểm tra được lịch trống bác sĩ theo thời gian thực ngay khi khách gọi vào. |
| 5 | Vinpearl / VinWonders | AI có thể tốt hơn (AI-upgrade) | Chatbot CSKH hiện tại trả lời rập khuôn theo kịch bản cố định, không xử lý được các câu hỏi phức tạp về combo vé/giờ mở cửa theo mùa, khiến khách phải chuyển sang gọi hotline. |
| 6 | VinFast | Stakeholder Pain | Đội ngũ vận hành trạm sạc nhận nhiều phản ánh từ khách hàng về tình trạng trạm sạc "báo còn chỗ" trên app nhưng thực tế đã kín hoặc hỏng, do dữ liệu trạng thái không được đồng bộ theo thời gian thực. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây.

## 🎴 QUICK PROBLEM CARD #1

**Bài toán (1 câu):** Hệ thống điều vận Xanh SM gợi ý điểm đón/trả khách không sát thực tế, khiến tài xế phải di chuyển thêm quãng đường không cần thiết.

**Công ty thành viên:** ☑ Xanh SM

**Ai đang đau (Actor)?** Tài xế xe điện Xanh SM và khách hàng đang chờ đón.

**Workflow thủ công hiện tại (3-5 bước):**
1. Khách đặt xe qua app → 2. Hệ thống gợi ý điểm đón dựa trên GPS thô → 3. Tài xế nhận điểm đón không chính xác (VD: cổng khác của tòa nhà, ngõ cụt) → 4. Tài xế gọi điện xác nhận lại vị trí với khách → 5. Điều chỉnh lộ trình thủ công, mất thêm thời gian chờ.

**Bước nào tốn thời gian/lỗi nhất?** Bước 3-4 (xác định điểm đón sai và phải gọi xác nhận lại) — ⏱ trung bình 3-4 phút/lượt.

**AI có thể nhảy vào hỗ trợ ở bước nào?** Bước 2 — dùng mô hình tối ưu điểm đón dựa trên lịch sử đón trả thành công tại khu vực đó (không chỉ tọa độ GPS thô) kết hợp dữ liệu bản đồ chi tiết (cổng ra vào, khu vực cấm dừng).

**Đo thành công bằng gì (Metric có số)?** Giảm tỷ lệ tài xế phải gọi xác nhận lại vị trí từ 35% xuống dưới 10% số chuyến; giảm thời gian chờ đón trung bình từ 4 phút xuống dưới 2 phút.

**Quick Architecture:** ☑ LLM Feature (kết hợp rule-based cho khu vực cấm dừng)

---

## 🎴 QUICK PROBLEM CARD #2

**Bài toán (1 câu):** Nhân viên chăm sóc cư dân Vinhomes tốn nhiều thời gian soạn phản hồi cá nhân hóa cho từng đánh giá tiêu cực trên ứng dụng.

**Công ty thành viên:** ☑ Vinhomes

**Ai đang đau (Actor)?** Nhân viên chăm sóc khách hàng (CSKH) khu vực quản lý căn hộ.

**Workflow thủ công hiện tại (3-5 bước):**
1. Cư dân để lại đánh giá 1-2 sao trên app → 2. Nhân viên CSKH đọc và phân loại mức độ nghiêm trọng → 3. Nhân viên soạn thảo phản hồi cá nhân hóa → 4. Trưởng nhóm duyệt trước khi đăng → 5. Đăng phản hồi công khai.

**Bước nào tốn thời gian/lỗi nhất?** Bước 3 (soạn thảo phản hồi) — ⏱ trung bình 8-10 phút/lượt.

**AI có thể nhảy vào hỗ trợ ở bước nào?** Bước 3 — LLM soạn nháp phản hồi dựa trên nội dung đánh giá và giọng văn thương hiệu, nhân viên chỉ cần chỉnh sửa nhẹ trước khi gửi duyệt.

**Đo thành công bằng gì (Metric có số)?** Giảm thời gian soạn phản hồi từ 10 phút xuống dưới 2 phút; duy trì tỷ lệ phản hồi được duyệt không chỉnh sửa (hoặc chỉnh sửa nhỏ) trên 80%.

**Quick Architecture:** ☑ LLM Feature (có Human-in-the-loop duyệt trước khi đăng)

---

## 🎴 QUICK PROBLEM CARD #3

**Bài toán (1 câu):** Nhân viên kỹ thuật VinFast phải thủ công lọc hàng trăm cảnh báo pin mỗi ngày để phân biệt cảnh báo thật và cảnh báo giả.

**Công ty thành viên:** ☑ VinFast

**Ai đang đau (Actor)?** Nhân viên kỹ thuật giám sát đội xe (fleet maintenance team).

**Workflow thủ công hiện tại (3-5 bước):**
1. Hệ thống telemetry gửi cảnh báo pin bất thường → 2. Nhân viên mở từng log để xem chi tiết thông số (nhiệt độ, điện áp, chu kỳ sạc) → 3. Nhân viên đối chiếu với ngưỡng an toàn để xác định cảnh báo thật/giả → 4. Nếu thật, tạo ticket bảo trì và liên hệ chủ xe/trạm dịch vụ.

**Bước nào tốn thời gian/lỗi nhất?** Bước 2-3 (đọc và đối chiếu log thủ công) — ⏱ trung bình 4-5 phút/cảnh báo, nhân với hàng trăm cảnh báo/ngày.

**AI có thể nhảy vào hỗ trợ ở bước nào?** Bước 2-3 — mô hình phân loại (classification model) tự động gắn nhãn mức độ ưu tiên và độ tin cậy của cảnh báo, chỉ đẩy lên nhân viên những case có xác suất cảnh báo thật cao.

**Đo thành công bằng gì (Metric có số)?** Giảm số lượng cảnh báo cần nhân viên xem xét thủ công từ 100% xuống còn 20-30% (nhờ lọc bớt false positive); giảm thời gian xử lý trung bình mỗi cảnh báo thật từ 5 phút xuống dưới 2 phút.

**Quick Architecture:** ☑ Rule + LLM kết hợp (Rule lọc ngưỡng cứng, LLM/model phân loại các case mơ hồ)