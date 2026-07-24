# Phase 6 — AI Log & Reflection (Cá nhân)

Trong buổi lab, tôi đã sử dụng AI như một “thought-partner” để hỗ trợ quá trình khám phá bài toán và kiểm tra prompt boundary.

## 1. AI giúp gì?

AI đã giúp tôi rất nhiều ở 3 bước chính:

1. **Brainstorm ý tưởng bài toán**
   - Tôi dùng AI để xem xét các pain point thực tế ở các mảng như Xanh SM, Vinmec và Vinhomes.
   - AI giúp tôi chuyển từ những ý tưởng mơ hồ thành các bài toán có tính vận hành rõ hơn.

2. **Stress-test quick card**
   - Tôi đặt bài toán vào prompt và yêu cầu AI đóng vai trò là CFO / trưởng vận hành để phản biện.
   - Điều này giúp tôi thấy đâu là bài toán nên chọn và đâu là bài toán dễ bị “đẹp” quá nhưng thiếu thực tế.

3. **Rà soát ranh giới an toàn của prompt prototype**
   - Tôi đã dùng AI để kiểm tra xem prompt có đủ chặt để tránh bypass hay hành vi vượt quyền.
   - Đây là bước rất quan trọng vì trong bài lab, AI không chỉ giải quyết vấn đề mà còn phải được kiểm soát chặt chẽ.

## 2. AI sai gì?

Một điểm AI làm tôi thấy rõ là nó dễ “trả lời đẹp nhưng không đúng hoàn toàn” nếu không được chặn kỹ.

Ví dụ:
- Khi tôi đề cập đến bài toán xử lý sự cố pin của tài xế, AI có xu hướng đề xuất cách chỉ đường tự động và “gửi luôn” mà không nhấn mạnh bước phê duyệt của người vận hành.
- Nếu tôi không yêu cầu rõ ràng, AI sẽ bỏ qua yếu tố người dùng có thể gây ra rủi ro an toàn.

Điều này cho thấy AI chưa phải là một “decision maker” hoàn toàn; nó chỉ là một trợ lý mạnh nếu ta đặt ranh giới và quy tắc rất rõ ràng.

## 3. Sửa đổi ra sao?

Tôi đã điều chỉnh cách sử dụng AI theo hướng chặt chẽ hơn:

- Không chỉ hỏi “đề xuất giải pháp”, mà còn yêu cầu AI đánh giá theo tiêu chí:
  - business impact
  - metric
  - operational boundary
  - mức độ an toàn
- Khi xây dựng prototype, tôi bắt buộc AI phải trả về định dạng có kiểm soát và phải tuân theo các quy tắc như:
  - bắt buộc có tag `[DRAFT_ONLY]`
  - nếu pin dưới 5% thì không đề xuất trạm xa quá 5km
  - phải ưu tiên phương án cứu hộ / mobile charger

## 4. Bài học rút ra

Từ buổi hôm nay, tôi nhận ra rằng AI không phải là “phương án thay thế con người”, mà là công cụ giúp con người làm việc nhanh hơn nếu được đặt đúng phạm vi. Một sản phẩm AI tốt không chỉ cần câu trả lời hay, mà còn cần:

- metric rõ
- workflow rõ
- ranh giới rõ
- human review rõ
- fallback rõ

Vì vậy, phần quan trọng nhất của bài lab không chỉ là làm prompt đẹp, mà là làm cho prompt biết “được làm gì” và “không được làm gì”.
