# Phase 1 — SCAN: Tìm kiếm cơ hội (Cá nhân)

Dùng 4 lenses để quét qua hoạt động vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **Xanh SM** | Lặp lại | Điều phối viên phải lặp lại thao tác tìm lại trạm sạc và soạn tin nhắn hướng dẫn cho từng tài xế khi xe báo pin yếu. |
| 2 | **Xanh SM** | Tốn thời gian | Tài xế báo sự cố pin trên đường, đội điều vận phải tra cứu vị trí, kiểm tra trạm sạc, và viết hướng dẫn thủ công mất 10–15 phút mỗi lượt. |
| 3 | **Vinmec** | Tốn thời gian | Bác sĩ hoặc nhân viên y tế phải tóm tắt hồ sơ bệnh án xuất viện thủ công, mất 20–30 phút mỗi bệnh nhân. |
| 4 | **Vinhomes** | AI-upgrade | Hệ thống chat nội bộ nhận khiếu nại và phản hồi cư dân đang xử lý theo template rập khuôn, phản hồi chậm và thiếu cá nhân hóa. |
| 5 | **VinFast** | Stakeholder Pain | Nhân viên vận hành trạm sạc phải so khớp hóa đơn/biên lai sạc và đối chiếu với dữ liệu đối tác theo định kỳ, dễ sai sót và kéo dài. |

---

# Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards (Cá nhân)

Chọn top 3 bài toán từ danh sách SCAN.

## Quick Problem Card #1 — Xanh SM: Xử lý sự cố pin thực địa

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Tài xế Xanh SM báo xe đang ở điểm nào đó hết pin │
│ và cần được hướng dẫn đến trạm sạc gần nhất.               │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)? Tài xế và điều phối viên               │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tài xế gọi báo sự cố pin                               │
│   → 2. Điều phối viên tra cứu vị trí xe                     │
│   → 3. Tra cứu trạm sạc gần nhất và phù hợp                 │
│   → 4. Soạn tin nhắn hướng dẫn gửi lại cho tài xế           │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–4 (⏱ 12 phút/lượt) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–4              │
│ (Tự động pull dữ liệu và draft tin nhắn)                    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian xử lý sự cố từ 12 phút xuống dưới 3 phút.   │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #2 — Vinmec: Tóm tắt hồ sơ bệnh án xuất viện

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Bác sĩ phải tóm tắt hồ sơ bệnh án xuất viện bằng  │
│ văn bản ngắn gọn và rõ ràng cho theo dõi tiếp.              │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ, nhân viên y tế                  │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Đọc nhiều phần hồ sơ bệnh án                           │
│   → 2. Chọn thông tin quan trọng                            │
│   → 3. Viết bản tóm tắt bằng tay                            │
│   → 4. Gửi cho khoa/phòng liên quan                         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 1–3 (⏱ 25 phút/bệnh nhân) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3              │
│ (Tóm tắt, trích xuất thông tin và gợi ý câu văn)            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian viết tóm tắt từ 25 phút xuống còn dưới 5 phút. │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

## Quick Problem Card #3 — Vinhomes: Phản hồi khiếu nại cư dân

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Nhân viên CSKH Vinhomes phải trả lời các khiếu nại │
│ và hỏi đáp cư dân trên app, thường lặp lại template.        │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH, cư dân                 │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tiếp nhận khiếu nại / câu hỏi                         │
│   → 2. Đọc lịch sử trao đổi và tài liệu tham khảo           │
│   → 3. Viết phản hồi theo template                          │
│   → 4. Chuyển cho quản lý kiểm duyệt nếu cần                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2–3 (⏱ 10 phút/lượt) │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2–3              │
│ (Tự động gợi ý bài phản hồi và rút gọn tài liệu)            │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian phản hồi từ 10 phút xuống còn dưới 3 phút. │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

---

## Lựa chọn ưu tiên cá nhân

Trong 3 bài toán trên, bài toán tôi thấy có độ phù hợp cao nhất để mang vào nhóm là:

- **Xanh SM — Xử lý sự cố pin thực địa**

Lý do:
- Tác vụ có tính lặp lại và thời gian xử lý rõ ràng.
- Có thể đo bằng thời gian xử lý/lượt.
- Dễ xây dựng prompt prototype với ranh giới an toàn rõ ràng.
- Rủi ro sai sót có thể được kiểm soát bằng Human-in-the-loop.
