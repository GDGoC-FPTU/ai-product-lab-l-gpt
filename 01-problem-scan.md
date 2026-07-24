### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
| 1 |** Vinhomes** |Stakeholder Pain |Cư dân và nhân viên kỹ thuật bị ảnh hưởng khi sự cố thang máy, máy bơm, điều hòa hoặc hệ thống điện chỉ được phát hiện sau khi thiết bị đã hỏng. |
| 2 |** Vinhomes** |Time-consuming | Đội an ninh phải theo dõi số lượng lớn camera để phát hiện xâm nhập, tụ tập bất thường, đỗ xe sai vị trí hoặc đồ vật bị bỏ quên. Đôi lúc khi xảy ra mất mát sẽ tốn rất nhiều thời gian|
| 3 |**Vinhomes** | AI-upgrade|Các báo cáo tiêu thụ điện, nước và điều hòa chủ yếu phản ánh dữ liệu quá khứ, chưa chủ động cảnh báo khu vực tiêu thụ bất thường hoặc có nguy cơ rò rỉ. |
| 4 |**Vinmec** |Time-consuming | Khi xảy ra tai nạn cần cấp cứu gấp, đều sẽ phải dựa vào bác sĩ trưởng khoa trực để phân loại bệnh nhân trước khi đưa đi điều trị. Có thể gây đến thương tổn về mạng người |
| 5 |**Vinmec** |Repetative | Nhân viên thường xuyên thực hiện các bước lặp lại như đặt lịch, xác nhận lịch, đổi lịch, nhắc lịch và điều phối bệnh nhân tới đúng phòng khám.|

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #01                                      │
│                                                             │
│ Bài toán (1 câu): Phát hiện sớm nguy cơ hỏng hóc của thang  │
│ máy, máy bơm, điều hòa và hệ thống điện trước khi sự cố ảnh │
│ hưởng đến cư dân.                                           │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Cư dân, nhân viên kỹ thuật và ban quản │
│ lý vận hành tòa nhà.                                        │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Kiểm tra định kỳ ──> 2. Nhận phản ánh từ cư dân ──>    │
│   3. Kỹ thuật viên kiểm tra ──> 4. Xác định lỗi và sửa chữa │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Kiểm tra và xác định nguyên│
│ nhân sự cố sau khi thiết bị đã hỏng (⏱ 45-120 phút/lượt).  │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Phân tích dữ liệu cảm │
│ biến, lịch sử bảo trì và cảnh báo bất thường trước bước 2.  │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm sự cố ngoài kế hoạch ít nhất 20%; giảm thời gian sửa │
│   chữa trung bình từ 90 phút xuống dưới 45 phút; cảnh báo   │
│   nguy cơ hỏng thiết bị trước ít nhất 24 giờ.               │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #02                                      │
│                                                             │
│ Bài toán (1 câu): Tự động phát hiện và truy xuất các đoạn   │
│ camera có sự kiện bất thường để giảm thời gian điều tra mất │
│ mát và sự cố an ninh tại khu đô thị.                        │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên an ninh, ban quản lý và cư   │
│ dân cần xác minh sự cố hoặc tài sản bị mất.                 │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận báo cáo sự cố ──> 2. Xác định camera và thời gian │
│   ──> 3. Xem lại video ──> 4. Trích xuất bằng chứng ──>     │
│   5. Lập biên bản xử lý                                     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Tìm kiếm và xem lại nhiều  │
│ đoạn video liên tục (⏱ 30-120 phút/vụ việc).               │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Phát hiện sự kiện,    │
│ khoanh vùng thời gian, tìm đối tượng và tóm tắt clip tại    │
│ bước 2-3; nhân viên an ninh xác nhận kết quả cuối cùng.     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian tìm video từ 60 phút xuống dưới 10 phút;   │
│   phát hiện đúng ít nhất 95% nhóm sự kiện đã định nghĩa;    │
│   100% bằng chứng được con người xác nhận trước khi sử dụng.│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #03                                      │
│                                                             │
│ Bài toán (1 câu): Chủ động phát hiện khu vực tiêu thụ điện, │
│ nước hoặc điều hòa bất thường thay vì chỉ phản ánh dữ liệu  │
│ trong báo cáo quá khứ.                                      │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [x] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Ban quản lý vận hành, nhân viên kỹ     │
│ thuật, kế toán vận hành và cư dân.                          │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Thu thập số công tơ ──> 2. Tổng hợp dữ liệu ──>        │
│   3. So sánh với kỳ trước ──> 4. Tìm điểm bất thường ──>    │
│   5. Tạo yêu cầu kiểm tra                                   │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Tổng hợp và đối chiếu dữ   │
│ liệu từ nhiều tòa nhà, đồng hồ và kỳ báo cáo                │
│ (⏱ 120-240 phút/báo cáo).                                  │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Tự động chuẩn hóa dữ  │
│ liệu, phát hiện xu hướng bất thường và ưu tiên vị trí cần   │
│ kiểm tra tại bước 2-4.                                      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian lập báo cáo từ 180 phút xuống dưới 30 phút;│
│   giảm ít nhất 10% mức tiêu thụ bất thường; phát hiện ít    │
│   nhất 90% trường hợp rò rỉ đã được xác nhận.               │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #04                                      │
│                                                             │
│ Bài toán (1 câu): Hỗ trợ đội cấp cứu phân loại nhanh mức độ │
│ ưu tiên của bệnh nhân dựa trên triệu chứng, dấu hiệu sinh   │
│ tồn và quy trình chuyên môn, nhưng không thay thế quyết định│
│ của bác sĩ hoặc điều dưỡng phân loại.                       │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Bệnh nhân cấp cứu, điều dưỡng phân     │
│ loại, bác sĩ trực và đội điều phối phòng cấp cứu.           │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tiếp nhận bệnh nhân ──> 2. Đo dấu hiệu sinh tồn ──>    │
│   3. Thu thập triệu chứng ──> 4. Nhân viên y tế phân loại   │
│   ──> 5. Chuyển tới khu vực điều trị phù hợp                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Tổng hợp nhanh triệu chứng,│
│ tiền sử và dấu hiệu sinh tồn khi có nhiều bệnh nhân đến cùng│
│ lúc (⏱ 5-15 phút/bệnh nhân).                               │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Trích xuất thông tin, │
│ phát hiện dấu hiệu cảnh báo và đề xuất mức ưu tiên tại bước │
│ 2-4; quyết định cuối cùng bắt buộc thuộc về nhân viên y tế. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian phân loại từ 8 phút xuống dưới 3 phút; đặt │
│   mục tiêu độ nhạy với ca nguy kịch ≥99%; 100% đề xuất phải │
│   được bác sĩ hoặc điều dưỡng có thẩm quyền xác nhận.       │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #05                                      │
│                                                             │
│ Bài toán (1 câu): Tự động hóa việc đặt lịch, xác nhận, nhắc │
│ lịch và xử lý yêu cầu đổi lịch khám của bệnh nhân.          │
│                                                             │
│ Công ty thành viên: [ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  │
│                     [x] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên tổng đài, lễ tân, điều phối  │
│ phòng khám, bác sĩ và bệnh nhân.                            │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận yêu cầu ──> 2. Xác định chuyên khoa ──>           │
│   3. Kiểm tra lịch trống ──> 4. Xác nhận và nhắc lịch ──>   │
│   5. Xử lý đổi hoặc hủy lịch                                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Tra cứu lịch, đối chiếu yêu│
│ cầu và liên hệ lại với bệnh nhân (⏱ 5-10 phút/yêu cầu).    │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Thu thập nhu cầu bằng │
│ ngôn ngữ tự nhiên, gợi ý chuyên khoa, tìm khung giờ phù hợp │
│ và tạo nội dung xác nhận tại bước 1-4.                      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│   Giảm thời gian đặt lịch từ 8 phút xuống dưới 2 phút; giảm │
│   tỷ lệ bệnh nhân không đến ít nhất 15%; duy trì tỷ lệ đặt  │
│   sai lịch dưới 1%.                                         │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
