# Ngày 1 — Bài Tập & Phản Ánh
## Nền Tảng LLM API | Phiếu Thực Hành

**Thời lượng:** 1:30 giờ  
**Cấu trúc:** Lập trình cốt lõi (60 phút) → Bài tập mở rộng (30 phút)

---

## Phần 1 — Lập Trình Cốt Lõi (0:00–1:00)

Chạy các ví dụ trong Google Colab tại: https://colab.research.google.com/drive/172zCiXpLr1FEXMRCAbmZoqTrKiSkUERm?usp=sharing

Triển khai tất cả TODO trong `template.py`. Chạy `pytest tests/` để kiểm tra tiến độ.

**Điểm kiểm tra:** Sau khi hoàn thành 4 nhiệm vụ, chạy:
```bash
python template.py
```
Bạn sẽ thấy output so sánh phản hồi của GPT-4o và GPT-4o-mini.

---
## Phần 2 — Bài Tập Mở Rộng (1:00–1:30)

### Bài tập 2.1 — Độ Nhạy Của Temperature
Gọi `call_openai` với các giá trị temperature 0.0, 0.5, 1.0 và 1.5 sử dụng prompt **"Hãy kể cho tôi một sự thật thú vị về Việt Nam."**

**Bạn nhận thấy quy luật gì qua bốn phản hồi?** (2–3 câu)
> Khi temperature bằng 0.0, phản hồi mang tính xác định cao, cấu trúc câu chữ trang trọng, lặp lại giống nhau giữa các lần chạy. Khi tăng lên 0.5 và 1.0, nội dung trở nên đa dạng, sinh động và sử dụng nhiều từ vựng tự nhiên hơn. Tuy nhiên, khi tăng lên mức 1.5, câu trả lời bắt đầu xuất hiện các lỗi diễn đạt, mất tính mạch lạc và có thể sinh ra thông tin không chính xác (hallucination).

**Bạn sẽ đặt temperature bao nhiêu cho chatbot hỗ trợ khách hàng, và tại sao?**
> Tôi sẽ đặt temperature ở mức thấp, từ **0.0 đến 0.2** (hoặc tối đa là 0.3). Lý do là chatbot hỗ trợ khách hàng cần sự chính xác, nhất quán và đáng tin cậy tuyệt đối về thông tin (như chính sách, điều khoản, giá cả) thay vì sự sáng tạo hay ngẫu hứng từ ngữ có thể gây hiểu lầm cho khách hàng.

---

### Bài tập 2.2 — Đánh Đổi Chi Phí
Xem xét kịch bản: 10.000 người dùng hoạt động mỗi ngày, mỗi người thực hiện 3 lần gọi API, mỗi lần trung bình ~350 token.

**Ước tính xem GPT-4o đắt hơn GPT-4o-mini bao nhiêu lần cho workload này:**
> GPT-4o đắt hơn GPT-4o-mini **33.33 lần**. Cụ thể, tỷ lệ giá của Input ($5.00 / $0.150) và Output ($20.00 / $0.600) đều là 33.33 lần, vì vậy tổng chi phí cho bất kỳ tỷ lệ phân bổ input/output nào cũng sẽ đắt hơn đúng 33.33 lần.

**Mô tả một trường hợp mà chi phí cao hơn của GPT-4o là xứng đáng, và một trường hợp GPT-4o-mini là lựa chọn tốt hơn:**
> - GPT-4o xứng đáng: Khi cần giải quyết các bài toán suy luận logic phức tạp, viết code/gỡ lỗi lập trình nâng cao, phân tích tài liệu tài chính/pháp lý học thuật chuyên sâu hoặc các tác vụ xử lý đa phương thức (multimodal) đòi hỏi độ chính xác tuyệt đối.
> - GPT-4o-mini tốt hơn: Khi triển khai các tác vụ quy mô lớn, lặp đi lặp lại có cấu trúc đơn giản như phân loại văn bản, phân tích cảm xúc (sentiment analysis), lọc thư rác, tóm tắt nhanh hoặc các cuộc hội thoại thông thường có ngân sách giới hạn.

---

### Bài tập 2.3 — Trải Nghiệm Người Dùng với Streaming
**Streaming quan trọng nhất trong trường hợp nào, và khi nào thì non-streaming lại phù hợp hơn?** (1 đoạn văn)
> Streaming quan trọng nhất trong các ứng dụng hội thoại thời gian thực tương tác trực tiếp với người dùng (như ChatGPT, trợ lý ảo, chat hỗ trợ khách hàng). Việc hiển thị từng từ ngay khi được sinh ra giúp giảm độ trễ cảm nhận (perceived latency) của người dùng, mang lại trải nghiệm mượt mà và tự nhiên. Ngược lại, non-streaming phù hợp hơn đối với các tác vụ xử lý ngầm (background processing), gọi hàm (tool calling/function calling), trích xuất dữ liệu cấu trúc (như trả về chuỗi JSON để parse), hoặc khi hệ thống trung gian cần kiểm duyệt hoặc xử lý hậu kỳ toàn bộ nội dung phản hồi trước khi hiển thị.

## Danh Sách Kiểm Tra Nộp Bài
- [x] Tất cả tests pass: `pytest tests/ -v`
- [x] `call_openai` đã triển khai và kiểm thử
- [x] `call_openai_mini` đã triển khai và kiểm thử
- [x] `compare_models` đã triển khai và kiểm thử
- [x] `streaming_chatbot` đã triển khai và kiểm thử
- [x] `retry_with_backoff` đã triển khai và kiểm thử
- [x] `batch_compare` đã triển khai và kiểm thử
- [x] `format_comparison_table` đã triển khai và kiểm thử
- [x] `exercises.md` đã điền đầy đủ
- [x] Sao chép bài làm vào folder `solution` và đặt tên theo quy định 

