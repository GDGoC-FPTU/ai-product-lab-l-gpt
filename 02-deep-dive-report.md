# Lab 02 — Deep-Dive Report & Evaluation

## Thông tin nhóm

- **Tên nhóm:** L-GPT
- **Thành viên:**
  - Phan Trần Tường Vy — MSSV: 2A202601701

---

# Quyết định lựa chọn

Nhóm chọn bài toán: **Hỗ trợ phân loại và soạn phản hồi nháp cho phản ánh cư dân Vinhomes.**

## Lý do lựa chọn

- Đầu vào và đầu ra đều là văn bản nên dễ làm prototype bằng Gemini 2.5 Flash.
- Có thể kiểm thử bằng nhiều tình huống bình thường và adversarial.
- Có thể thiết lập operational boundary rõ ràng.
- Human-in-the-loop giúp kiểm soát rủi ro.
- Không cần tích hợp hệ thống bên ngoài để chứng minh giá trị ban đầu.

---

# Phase 3 — DEEP-DIVE

## 3.1. Current-State Workflow Mapping

Quy trình xử lý phản ánh cư dân hiện tại của nhân viên CSKH Vinhomes:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │     │ Bước 5       │
│ Nhận phản ánh│     │ Đọc toàn bộ  │     │ Phân loại    │     │ Chuyển ticket│     │ Soạn phản hồi│
│ từ cư dân    │ ──→ │ nội dung     │ ──→ │ vấn đề &     │ ──→ │ sang bộ phận │ ──→ │ xác nhận cho │
│              │     │              │     │ mức khẩn cấp │     │ phù hợp      │     │ cư dân       │
│ Ai: CSKH     │     │ Ai: CSKH     │     │ Ai: CSKH     │     │ Ai: CSKH     │     │ Ai: CSKH     │
│ ⏱ 1 phút     │     │ ⏱ 2 phút 🔴  │     │ ⏱ 2 phút 🔴  │     │ ⏱ 1 phút     │     │ ⏱ 2 phút     │
│ 🔄 Handoff   │     │              │     │              │     │ 🔄 Handoff   │     │              │
│ In: App/Email │     │ In: Nội dung │     │ In: Nội dung │     │ In: Category │     │ In: Mẫu text │
│ Out: Log tiếp│     │ Out: Hiểu    │     │ Out: Category│     │ Out: Ticket  │     │ Out: Email/SMS│
│     nhận     │     │     vấn đề   │     │     Urgency  │     │     assigned │     │     gửi cư dân│
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘

🔴 = Bottleneck (Bước 2–3: đọc, hiểu, phân loại)
🔄 = Handoff (Bước 1: cư dân → CSKH; Bước 4: CSKH → bộ phận kỹ thuật/an ninh/vệ sinh/kế toán)
⏱ Tổng thời gian xử lý thủ công: 8 phút/phản ánh
```

**Mô tả chi tiết:**
- **Bước 1:** Cư dân gửi phản ánh qua ứng dụng Vinhomes Resident, email hoặc hotline. Nhân viên CSKH tiếp nhận và tạo log.
- **Bước 2 (🔴 Bottleneck):** Nhân viên đọc toàn bộ nội dung, thường dài, thiếu cấu trúc và có thể chứa nhiều vấn đề.
- **Bước 3 (🔴 Bottleneck):** Nhân viên xác định loại vấn đề (kỹ thuật, an ninh, vệ sinh, kế toán) và mức độ khẩn cấp. Dễ bị sai khi nội dung mơ hồ hoặc chứa nhiều ý.
- **Bước 4 (🔄 Handoff):** Ticket được chuyển sang bộ phận phụ trách. Nếu chuyển sai, ticket phải quay lại gây lãng phí thời gian.
- **Bước 5:** Nhân viên soạn phản hồi xác nhận cho cư dân.

---

## 3.2. Problem Statement (6-field)

| Field | Nội dung |
|---|---|
| **1. Actor / Operator** | Nhân viên CSKH tiếp nhận phản ánh tại Trung tâm Quản lý Vinhomes. |
| **2. Current Workflow** | Khi cư dân gửi phản ánh qua app/email/hotline, nhân viên CSKH đọc toàn bộ nội dung, xác định loại vấn đề và mức độ khẩn cấp, chuyển ticket đến bộ phận kỹ thuật/an ninh/vệ sinh/kế toán, rồi soạn phản hồi xác nhận. 5 bước, hoàn toàn thủ công, mất khoảng 6–8 phút/phản ánh. |
| **3. Bottleneck** | Bước 2–3 (mất 4 phút): Đọc nội dung tự do, phân loại vấn đề khi nội dung chứa nhiều ý hoặc mơ hồ, xác định mức khẩn cấp. Lỗi thường gặp: chuyển sai bộ phận (~12% ticket), bỏ sót vấn đề phụ, đánh giá thiếu mức khẩn cấp cho sự cố an toàn. |
| **4. Business Impact** | Ước tính ~200 phản ánh/ngày tại một dự án lớn. Thời gian phân loại sai gây lãng phí 1.5 giờ/ngày do phải chuyển lại ticket. Cư dân phải chờ lâu, giảm chỉ số hài lòng (CSAT) và tăng tỉ lệ khiếu nại lặp lại. |
| **5. Success Metric** | 1. Ít nhất **90% ticket** được gán đúng bộ phận trong tập test (Accuracy).<br>2. Thời gian phân loại trung bình giảm từ **6 phút xuống dưới 1 phút** (Efficiency).<br>3. **100% phản hồi nháp** phải được nhân viên duyệt trước khi gửi (Safety).<br>4. Recall cho tình huống khẩn cấp (cháy, điện, thang máy, bạo lực, y tế) đạt tối thiểu **95%** (Critical Safety). |
| **6. Operational Boundary** | AI được phép: tóm tắt phản ánh, gán category, đề xuất mức khẩn cấp, đề xuất bộ phận phụ trách, soạn phản hồi nháp dạng `[DRAFT_ONLY]`.<br>**CẤM:** AI không được tự gửi phản hồi; không được cam kết bồi thường; không được tự kết luận sự cố đã giải quyết; không được tự đóng ticket; không được hạ mức ưu tiên tình huống an toàn; không được tạo thông tin không có trong input gốc. Bắt buộc Human-in-the-loop trước mọi hành động cuối cùng. |

---

## 3.3. Future-State Flow & AI Fit

### AI Fit Analysis

| Giải pháp | Phù hợp? | Lý do |
|---|---|---|
| **Rule / State-Machine** | Một phần | Phù hợp cho lớp guardrail: phát hiện từ khóa khẩn cấp (cháy, khói, mất điện, kẹt thang máy, bạo lực). Không đủ khả năng hiểu nội dung tự do, nhiều cách diễn đạt. |
| **LLM Feature** ✅ | **Phù hợp nhất** | Input là văn bản tự do, cần hiểu ngữ cảnh, phân loại đa chiều, tóm tắt và sinh nội dung. LLM có thể trả structured JSON output. |
| **Agentic Loop** | Quá mức | Quy trình có cấu trúc cố định, không cần AI tự lập kế hoạch hoặc gọi nhiều công cụ. Agent làm tăng độ phức tạp và rủi ro không cần thiết cho prototype. |

**Quyết định:** Chọn **LLM Feature** kết hợp **Rule-based guardrail**.

### Future-State Flow

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Nhận phản ánh│     │ 🔵 AI phân   │     │ 🟢 CSKH      │     │ Hệ thống gửi│
│ từ cư dân    │ ──→ │ loại, tóm tắt│ ──→ │ review &     │ ──→ │ phản hồi đã │
│              │     │ & draft reply│     │ phê duyệt    │     │ được duyệt  │
│ Ai: Hệ thống│     │ Ai: LLM      │     │ Ai: Con người│     │ Ai: Hệ thống│
│ ⏱ Tự động   │     │ ⏱ 5-10 giây  │     │ ⏱ 30 giây    │     │ ⏱ Tự động   │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                │
                                                ▼
                                         ↩️ Fallback:
                                         Nếu output AI không
                                         đúng schema hoặc
                                         confidence thấp,
                                         CSKH xử lý thủ công
                                         như quy trình cũ.

🔵 = AI Step (LLM xử lý)
🟢 = Human Step (HITL — bắt buộc con người phê duyệt)
↩️ = Fallback (kế hoạch dự phòng khi AI lỗi)
```

**Chi tiết bước AI (Bước 2):**
- Rule-based guardrail quét từ khóa khẩn cấp trước (cháy, khói, điện, thang máy, bạo lực, y tế) → nếu match, auto-flag urgency = critical.
- LLM nhận nội dung phản ánh + system prompt nghiêm ngặt.
- LLM trả structured JSON: `{ category, urgency, summary, department, draft_reply (bắt đầu bằng [DRAFT_ONLY]) }`.
- Nếu JSON không đúng schema hoặc LLM không tự tin → fallback cho CSKH xử lý thủ công.

**Human-in-the-loop (Bước 3):**
- Nhân viên CSKH xem kết quả phân loại, tóm tắt và phản hồi nháp.
- Nhân viên có thể chỉnh sửa, thay đổi category/urgency hoặc viết lại phản hồi.
- Chỉ sau khi nhân viên nhấn "Duyệt", hệ thống mới gửi phản hồi cho cư dân.

**Fallback:**
- Output không đúng JSON schema → nhân viên xử lý thủ công.
- Trường hợp khẩn cấp → chuyển ngay cho ban quản lý, không chờ AI.
- LLM timeout hoặc lỗi API → fallback hoàn toàn về quy trình cũ.

---

# Phase 5 — EVALUATE

## AI Readiness Checklist

| # | Tiêu chí | Đánh giá |
|---|---|---|
| 1 | Có sẵn dữ liệu mẫu/logs sạch để test? | ✅ Có thể tạo dữ liệu mẫu mô phỏng các phản ánh thực tế. Trong sản xuất, cần thu thập log từ App Vinhomes Resident. |
| 2 | Rủi ro khi AI sai có nằm trong tầm kiểm soát? | ✅ Có — phản hồi luôn ở dạng nháp `[DRAFT_ONLY]`, bắt buộc con người duyệt. Tình huống khẩn cấp có guardrail rule-based bổ sung. |
| 3 | Stakeholders sẵn sàng thay đổi quy trình? | ⚠️ Cần đào tạo nhân viên CSKH sử dụng giao diện mới. Tuy nhiên, quy trình không thay đổi triệt để — chỉ bổ sung công cụ hỗ trợ. |

## Quyết định cuối cùng

### ✅ GO — Bắt đầu xây dựng Prototype

**Justification (Lý giải quyết định):**

1. **Bài toán rõ ràng:** Bottleneck được xác định cụ thể (đọc, phân loại, soạn phản hồi), có metric đo lường định lượng.
2. **Rủi ro kiểm soát được:** AI chỉ tạo đề xuất dạng nháp, con người luôn là người ra quyết định cuối cùng. Tình huống khẩn cấp có rule-based guardrail bổ sung.
3. **Công nghệ phù hợp:** Gemini 2.5 Flash đủ khả năng xử lý phân loại văn bản tiếng Việt, tóm tắt và sinh structured JSON output. Không cần mô hình phức tạp hơn cho prototype.
4. **Chi phí hợp lý:** Gemini 2.5 Flash có giá thấp (~$0.15/1M input tokens). Ước tính 200 phản ánh/ngày × ~500 tokens/phản ánh = 100K tokens/ngày ≈ $0.015/ngày. Chi phí API không đáng kể so với tiết kiệm nhân sự.
5. **Scope hẹp và khả thi:** Prototype tập trung vào một tính năng LLM đơn lẻ, không yêu cầu tích hợp hệ thống phức tạp. Có thể hoàn thành trong thời gian Lab.
6. **Fallback an toàn:** Khi AI lỗi, hệ thống quay về quy trình thủ công hiện tại — không gây gián đoạn vận hành.

---

# Kết luận

Bài toán phân loại và soạn phản hồi nháp cho phản ánh cư dân Vinhomes đáp ứng đủ các tiêu chí để bắt đầu phát triển prototype: bottleneck rõ ràng, metric đo lường được, rủi ro kiểm soát qua HITL, chi phí hợp lý và fallback an toàn. Nhóm quyết định **GO** với scope prototype tập trung vào LLM Feature kết hợp rule-based guardrail.
