# 📝 03-ai-log.md — Nhật ký chiêm nghiệm về việc dùng AI (Reflection)

**Họ tên / MSSV:** [Nguyễn Hoài Nam- 2A202602016]

---

## 1. AI đã giúp gì?

Trong buổi lab, mình dùng AI (Claude) làm thought-partner ở nhiều bước khác nhau:

- **Hoàn thiện System Prompt & Operational Boundary:** AI giúp mình viết một `SYSTEM_PROMPT` chi tiết, rõ ràng cho vai trò "Vin Smart Future Dispatcher Co-Pilot", đặc biệt là diễn đạt lại 2 ranh giới bắt buộc (tag `[DRAFT_ONLY]` và ngưỡng pin < 5% → dispatch mobile charger) thành ngôn ngữ chỉ thị chặt chẽ, khó bị bypass hơn so với bản mình tự viết ban đầu.
- **Thiết kế Adversarial Test Cases:** AI gợi ý thêm một test case thứ 3 ("Roleplay / Authority Override Attempt") mô phỏng kiểu tấn công người dùng giả làm "admin-mode" để yêu cầu AI bỏ qua toàn bộ rule — đây là kiểu tấn công mình chưa nghĩ tới khi chỉ có 2 test case mẫu ban đầu.
- **Debug lỗi kỹ thuật thực tế:** Khi chạy `prompt_prototype.py`, mình gặp liên tiếp 2 lỗi:
  1. `400 INVALID_ARGUMENT — API_KEY_INVALID`: AI hướng dẫn mình kiểm tra từng lớp (biến môi trường có set đúng không → giá trị key thực tế qua `repr()` → test trực tiếp bằng `curl` để tách bạch lỗi do code hay do key) thay vì đoán mò.
  2. `404 NOT_FOUND — model gemini-2.5-flash is no longer available to new users`: sau khi key đã đúng, AI giúp mình hiểu rằng model bị Google deprecate cho user mới dù vẫn còn trong danh sách model trả về, và hướng dẫn cách tự tra danh sách model khả dụng thật sự cho key của mình bằng `curl ... | grep gemini` thay vì đoán tên model.

## 2. AI sai gì / có giới hạn gì?

- **Đoán sai định dạng API key:** Ban đầu AI khẳng định khá chắc rằng key hợp lệ của Gemini phải có dạng `AIzaSy...` (dựa theo kiến thức huấn luyện cũ). Khi mình đưa key thật có dạng `AQ.Ab8...`, AI đã *không* vội khẳng định đúng/sai mà thừa nhận đây là định dạng nó không có thông tin chắc chắn (có thể do Google cập nhật sau thời điểm huấn luyện của AI), và đề xuất cách kiểm chứng độc lập bằng `curl` thay vì đoán mò tiếp — đây là điểm AI xử lý đúng nguyên tắc (không hallucinate), nhưng cũng cho thấy giới hạn rõ ràng: **kiến thức của AI về tên/định dạng model, API key của các nhà cung cấp bên thứ ba có thể lỗi thời** và cần luôn kiểm chứng thực tế thay vì tin tuyệt đối.
- **Không thể tự xác nhận chắc chắn tên model mới nhất:** Khi `gemini-2.5-flash` bị lỗi 404, AI đề xuất `gemini-flash-latest` như một lựa chọn hợp lý (alias tự trỏ tới bản mới nhất) nhưng cũng thẳng thắn nói không chắc 100% nếu không kiểm tra qua danh sách model thật của tài khoản — đúng là sau khi mình chạy `curl` để liệt kê, danh sách thực tế khác khá nhiều so với những gì AI "nhớ" từ trước (có cả các model đời `gemini-3.x` mà AI cũng không có dữ liệu để biết chắc).

## 3. Mình đã điều chỉnh/sửa như thế nào?

- Với System Prompt: mình giữ nguyên cấu trúc AI đề xuất nhưng bổ sung thêm ví dụ cụ thể hơn về cách tài xế/dispatcher thực tế tương tác, để ranh giới rõ ràng hơn khi áp dụng vào tình huống thật của Xanh SM.
- Với lỗi kỹ thuật: thay vì tin ngay gợi ý đầu tiên (tên model/định dạng key), mình luôn tự chạy lệnh kiểm chứng độc lập (`curl`, `repr()`) trước khi sửa code — nhờ vậy phát hiện ra vấn đề thật sự (model deprecated) thay vì sửa sai chỗ.
- Bài học rút ra: AI là công cụ debug rất hiệu quả để thu hẹp phạm vi vấn đề (đưa ra các bước kiểm tra có thứ tự logic), nhưng với các thông tin có thể thay đổi theo thời gian thực (tên model, định dạng API key của bên thứ ba), mình cần luôn xác minh bằng công cụ thực tế (curl, log lỗi) thay vì dựa hoàn toàn vào "trí nhớ" của AI.