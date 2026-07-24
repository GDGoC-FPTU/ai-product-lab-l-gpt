# Lab 02 — Problem Scan & Quick Problem Cards

##phan trần tường vy 2A202601701

# Phase 1 — SCAN

## Danh sách bài toán vận hành

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---:|---|---|---|
| 1 | Vinhomes | Tốn thời gian | Nhân viên CSKH phải đọc, phân loại và chuyển thủ công phản ánh của cư dân đến đúng bộ phận như kỹ thuật, an ninh, vệ sinh hoặc kế toán. Nội dung phản ánh thường dài, thiếu cấu trúc và có thể chứa nhiều vấn đề trong cùng một yêu cầu. |
| 2 | Xanh SM | Pain từ người khác | Tài xế phản ánh rằng một số điểm đón khách không chính xác hoặc khó tiếp cận. Nhân viên điều vận phải đọc nội dung, kiểm tra vị trí và quyết định có cần đổi điểm đón hay không. |
| 3 | VinFast | Lặp lại | Kỹ thuật viên phải tổng hợp lịch sử lỗi, thông tin bảo dưỡng và mô tả của khách hàng trước khi kiểm tra xe. Công việc này lặp lại với mỗi lượt tiếp nhận và dễ bỏ sót thông tin quan trọng. |
| 4 | Vinpearl / VinWonders | AI có thể tốt hơn | Chatbot CSKH hiện tại có thể trả lời tốt các câu hỏi đơn giản nhưng khó xử lý yêu cầu nhiều điều kiện như đổi ngày vé, chính sách trẻ em, combo dịch vụ và trường hợp ngoại lệ. |
| 5 | Vinmec | Tốn thời gian | Nhân viên tiếp nhận phải đọc nội dung yêu cầu đặt khám, xác định chuyên khoa phù hợp và chuyển thông tin đến bộ phận liên quan. Các mô tả của bệnh nhân thường không theo mẫu và có thể thiếu dữ liệu cần thiết. |

---

## Đánh giá nhanh 5 bài toán

| Bài toán | Dữ liệu đầu vào | Output mong muốn | Rủi ro khi AI sai | Khả năng làm prototype |
|---|---|---|---|---|
| Phân loại phản ánh cư dân Vinhomes | Văn bản phản ánh | Loại vấn đề, mức khẩn cấp, bộ phận xử lý, phản hồi nháp | Trung bình; có thể kiểm soát bằng human review | Cao |
| Triage phản ánh điểm đón Xanh SM | Văn bản, tọa độ, ảnh bản đồ | Loại lỗi, mức độ ảnh hưởng, đề xuất xử lý | Trung bình; quyết định cuối vẫn do điều vận | Trung bình |
| Tóm tắt hồ sơ bảo dưỡng VinFast | Lịch sử lỗi và ghi chú kỹ thuật | Bản tóm tắt có cấu trúc | Trung bình; có thể bỏ sót lỗi quan trọng | Cao |
| Chatbot xử lý yêu cầu phức tạp Vinpearl | Nội dung hội thoại và chính sách | Câu trả lời hoặc hướng dẫn chuyển người | Trung bình; có thể trả lời sai chính sách | Cao |
| Phân loại yêu cầu đặt khám Vinmec | Văn bản mô tả nhu cầu khám | Chuyên khoa gợi ý, dữ liệu còn thiếu | Cao; không được chẩn đoán bệnh | Trung bình |

---

# Phase 2 — QUICK-ASSESS

## QUICK PROBLEM CARD #1

### Bài toán

Hỗ trợ nhân viên CSKH Vinhomes phân loại phản ánh cư dân, xác định mức độ ưu tiên và soạn phản hồi nháp.

### Công ty thành viên

- [ ] VinFast
- [ ] Xanh SM
- [x] Vinhomes
- [ ] Vinmec
- [ ] Khác

### Ai đang đau?

- Nhân viên CSKH tiếp nhận phản ánh.
- Nhân viên vận hành phải nhận lại các ticket bị chuyển sai bộ phận.
- Cư dân phải chờ lâu khi phản ánh không được phân loại đúng ngay từ đầu.

### Workflow thủ công hiện tại

1. Cư dân gửi phản ánh qua ứng dụng, email hoặc hotline.
2. Nhân viên CSKH đọc toàn bộ nội dung.
3. Nhân viên xác định loại vấn đề và mức độ khẩn cấp.
4. Ticket được chuyển sang bộ phận kỹ thuật, an ninh, vệ sinh, kế toán hoặc ban quản lý.
5. Nhân viên soạn phản hồi xác nhận cho cư dân.

### Bước tốn thời gian hoặc lỗi nhất

- **Bước 2–4:** đọc, phân loại và chuyển đúng bộ phận.
- **Thời gian giả định:** khoảng 5–8 phút mỗi yêu cầu.
- Lỗi thường gặp là chuyển sai bộ phận, đánh giá thiếu mức độ khẩn cấp hoặc bỏ sót một vấn đề phụ trong nội dung dài.

### AI có thể hỗ trợ ở đâu?

AI có thể:

- Tóm tắt phản ánh.
- Gán category.
- Đề xuất mức độ khẩn cấp.
- Đề xuất bộ phận phụ trách.
- Soạn phản hồi xác nhận ban đầu.

AI không được:

- Tự gửi phản hồi.
- Tự cam kết bồi thường.
- Tự kết luận sự cố đã được xử lý.
- Tự đóng ticket.
- Tự xử lý tình huống liên quan đến an toàn mà không có con người kiểm tra.

### Metric có số

- Ít nhất **90% ticket** được gán đúng nhóm xử lý trong tập test nội bộ.
- Thời gian phân loại trung bình giảm từ **6 phút xuống dưới 1 phút**.
- **100% phản hồi nháp** phải được nhân viên duyệt trước khi gửi.
- Các trường hợp có dấu hiệu cháy, điện, thang máy, bạo lực hoặc y tế phải được gắn cờ khẩn cấp với recall mục tiêu tối thiểu **95%**.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] LLM
- [ ] Agent

### Lý do chọn

LLM phù hợp vì đầu vào là ngôn ngữ tự nhiên, có nhiều cách diễn đạt và thường chứa nhiều ý trong một đoạn. Rule-based vẫn nên được dùng như lớp bảo vệ để phát hiện từ khóa khẩn cấp.

---

## QUICK PROBLEM CARD #2

### Bài toán

Hỗ trợ điều vận Xanh SM phân loại phản ánh của tài xế về điểm đón khách không chính xác hoặc khó tiếp cận.

### Công ty thành viên

- [ ] VinFast
- [x] Xanh SM
- [ ] Vinhomes
- [ ] Vinmec
- [ ] Khác

### Ai đang đau?

- Tài xế không tìm được vị trí đón thuận tiện.
- Khách hàng phải chờ lâu hoặc phải đi bộ xa.
- Nhân viên điều vận phải đọc và xử lý nhiều phản ánh tương tự.

### Workflow thủ công hiện tại

1. Tài xế gửi phản ánh kèm mô tả vị trí.
2. Nhân viên điều vận đọc nội dung.
3. Nhân viên kiểm tra tọa độ và bản đồ.
4. Nhân viên xác định nguyên nhân: sai ghim, đường cấm, không có điểm dừng hoặc mô tả thiếu.
5. Nhân viên đề xuất vị trí thay thế hoặc liên hệ tài xế.

### Bước tốn thời gian hoặc lỗi nhất

- **Bước 2–4:** hiểu phản ánh và xác định nguyên nhân.
- **Thời gian giả định:** khoảng 4–7 phút mỗi trường hợp.
- Một số trường hợp có thể bị xử lý chậm vì nội dung quá ngắn hoặc không có đủ thông tin.

### AI có thể hỗ trợ ở đâu?

AI có thể:

- Chuẩn hóa nội dung phản ánh.
- Phân loại loại lỗi điểm đón.
- Trích xuất địa danh, hướng tiếp cận và trở ngại.
- Yêu cầu bổ sung thông tin nếu dữ liệu chưa đủ.
- Đề xuất checklist để điều vận xác minh.

AI không được:

- Tự thay đổi điểm đón trên hệ thống sản xuất.
- Tự điều hướng tài xế vào đường cấm hoặc khu vực nguy hiểm.
- Tự kết luận vị trí mới là an toàn khi chưa có dữ liệu bản đồ xác nhận.

### Metric có số

- Ít nhất **85% phản ánh** được phân loại đúng nguyên nhân.
- Giảm thời gian đọc và chuẩn hóa nội dung từ **5 phút xuống dưới 1 phút**.
- Giảm ít nhất **30% số ticket** phải chuyển lại do thiếu thông tin.
- **100% thay đổi điểm đón** phải do nhân viên điều vận phê duyệt.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] LLM
- [ ] Agent

### Lý do chọn

LLM phù hợp cho bước hiểu nội dung tự do. Việc kiểm tra bản đồ và thay đổi điểm đón nên được xử lý bởi hệ thống rule, API bản đồ và con người thay vì giao toàn quyền cho LLM.

---

## QUICK PROBLEM CARD #3

### Bài toán

Tự động tóm tắt lịch sử lỗi và bảo dưỡng xe VinFast trước khi kỹ thuật viên bắt đầu kiểm tra.

### Công ty thành viên

- [x] VinFast
- [ ] Xanh SM
- [ ] Vinhomes
- [ ] Vinmec
- [ ] Khác

### Ai đang đau?

- Kỹ thuật viên phải đọc nhiều ghi chú cũ trước khi kiểm tra xe.
- Cố vấn dịch vụ mất thời gian tổng hợp thông tin từ nhiều nguồn.
- Khách hàng phải chờ lâu hơn tại bước tiếp nhận.

### Workflow thủ công hiện tại

1. Cố vấn dịch vụ tiếp nhận mô tả của khách hàng.
2. Nhân viên mở lịch sử bảo dưỡng và lỗi trước đó.
3. Nhân viên đọc từng ghi chú kỹ thuật.
4. Nhân viên tóm tắt lỗi lặp lại, hạng mục đã thay và cảnh báo quan trọng.
5. Kỹ thuật viên dùng bản tóm tắt để bắt đầu kiểm tra.

### Bước tốn thời gian hoặc lỗi nhất

- **Bước 2–4:** đọc và tổng hợp lịch sử.
- **Thời gian giả định:** khoảng 8–15 phút mỗi xe có lịch sử dài.
- Rủi ro lớn nhất là bỏ sót lỗi lặp lại hoặc nhầm một hạng mục đã được xử lý trước đó.

### AI có thể hỗ trợ ở đâu?

AI có thể:

- Tóm tắt lịch sử theo mốc thời gian.
- Nhóm các lỗi lặp lại.
- Trích xuất linh kiện đã thay.
- Đánh dấu thông tin còn mâu thuẫn.
- Sinh checklist để kỹ thuật viên kiểm tra.

AI không được:

- Tự chẩn đoán lỗi cuối cùng.
- Tự ra quyết định sửa chữa hoặc thay linh kiện.
- Xóa hoặc thay đổi hồ sơ gốc.
- Che giấu thông tin mâu thuẫn.
- Tạo chi tiết không tồn tại trong hồ sơ.

### Metric có số

- Giảm thời gian tổng hợp hồ sơ từ **10 phút xuống dưới 2 phút**.
- Ít nhất **95% lỗi đã xuất hiện trong hồ sơ** phải được giữ lại trong bản tóm tắt.
- Tỷ lệ hallucination phải dưới **1%** trên tập test đã gán nhãn.
- **100% bản tóm tắt** phải dẫn lại nguồn hoặc mốc ghi chú liên quan để kỹ thuật viên kiểm tra.

### Quick Architecture

- [ ] No AI
- [ ] Rule
- [x] LLM
- [ ] Agent

### Lý do chọn

LLM phù hợp cho việc tóm tắt và tái cấu trúc ghi chú kỹ thuật. Tuy nhiên, hệ thống chỉ đóng vai trò hỗ trợ thông tin; kỹ thuật viên vẫn là người đưa ra kết luận chuyên môn.

---

# So sánh và chọn bài toán ưu tiên

| Tiêu chí | Vinhomes CSKH | Xanh SM điểm đón | VinFast lịch sử lỗi |
|---|---:|---:|---:|
| Dữ liệu đầu vào dễ mô phỏng | 5/5 | 3/5 | 4/5 |
| Dễ xây dựng prompt prototype | 5/5 | 4/5 | 4/5 |
| Rủi ro khi AI sai có thể kiểm soát | 4/5 | 4/5 | 3/5 |
| Có metric rõ ràng | 5/5 | 4/5 | 5/5 |
| Phù hợp thời lượng Lab | 5/5 | 3/5 | 4/5 |
| **Tổng** | **24/25** | **18/25** | **20/25** |

## Bài toán được đề xuất cho phần Deep-Dive nhóm

**Hỗ trợ phân loại và soạn phản hồi nháp cho phản ánh cư dân Vinhomes.**

### Lý do

1. Đầu vào và đầu ra đều là văn bản nên dễ làm prototype bằng Gemini 2.5 Flash.
2. Có thể kiểm thử bằng nhiều tình huống bình thường và adversarial.
3. Có thể thiết lập boundary rõ ràng.
4. Human-in-the-loop giúp kiểm soát rủi ro.
5. Có thể so sánh trực tiếp Rule-based và LLM.
6. Không cần tích hợp hệ thống bên ngoài để chứng minh giá trị ban đầu.

---

# Kết luận cá nhân

Qua quá trình scan, các bài toán phù hợp nhất với LLM không phải là những bài toán yêu cầu AI tự đưa ra quyết định cuối cùng, mà là các tác vụ cần hiểu văn bản tự do, tóm tắt, phân loại và tạo bản nháp. Trong ba bài toán được đánh giá, bài toán Vinhomes có scope rõ nhất, rủi ro có thể kiểm soát bằng human review và phù hợp nhất để tiếp tục sang bước workflow mapping, problem statement, future-state flow và prompt prototype.
