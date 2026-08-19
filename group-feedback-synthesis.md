# Group Feedback Synthesis

## Tổng hợp ba phiên test

| Nội dung | Tester 1 — Trần Thị Kiều Trang (2A202601498) · A: Inline Explain | Tester 2 — Nguyễn Quy Dũng (2A202601288) · B: Diagnosis | Tester 3 — Đồng Đại Huy (2A202601901) · C: Recovery Path | Pattern / khác biệt |
|---|---|---|---|---|
| First action | Chọn kiểu giải thích bằng ví dụ vì trực quan và có thể áp dụng ngay. | Trả lời câu hỏi chẩn đoán; chấp nhận bộ câu hỏi thay thế khi đề xuất đầu tiên chưa đúng. | Khi không hiểu/mất tập trung thường chuyển slide liên tục. | Cả ba cần một phản hồi phù hợp đúng thời điểm; cách khởi đầu khác nhau theo mức chủ động của AI. |
| Breakdown / hesitation | Chưa tự tin trả lời câu hỏi kiểm tra; trên lớp có thể bỏ qua để theo kịp. | Muốn được hỏi trước để chắc chắn về kiến thức cần ôn. | Không muốn chọn lộ trình ôn lại trên web; muốn tự nghiên cứu sâu hơn ở nguồn ngoài. | Sự gián đoạn vẫn xuất hiện khi thiếu tin tưởng hoặc luồng không khớp nhu cầu học sâu. |
| Evidence & uncertainty | Chỉ tin khoảng “50–50”; kiến thức sâu vẫn muốn kiểm tra thêm. | Thấy câu hỏi khá liên quan và cảm thấy được giúp đỡ, không bị kiểm tra. | Gợi ý giống thông báo; chấp nhận được khi thưa, khó chịu khi xuất hiện nhiều. | Niềm tin phụ thuộc vào tính liên quan, mức giải thích và tần suất can thiệp của AI. |
| Control & recovery | Có thể quay sang ChatGPT hoặc bỏ qua. | Có thể bác bỏ đề xuất và đi qua bộ câu hỏi khác. | Bỏ qua gợi ý, tìm hiểu từ nguồn bên ngoài. | User cần luôn có đường thoát, đổi hướng hoặc tự quyết định cách tiếp tục. |
| Option chọn và trade-off | Nhanh, trực quan nhưng chưa đủ cho nội dung phức tạp. | Tốn thêm thời gian trả lời, đổi lại tạo cảm giác kiểm chứng và tin tưởng hơn. | Ít thao tác ban đầu nhưng có nguy cơ sai trọng tâm và làm giảm agency. | B có tín hiệu tốt nhất về mức liên quan và cảm giác được hỗ trợ; chưa đủ dữ liệu để khẳng định B thắng A/C. |

## Group Next Change

Chưa có thay đổi nào được triển khai sau test. Vòng lặp tiếp theo sẽ tập trung vào hai việc: cải thiện thao tác **bôi đen** ở Option A để điểm chọn rõ ràng hơn và bổ sung **summary slide** dùng chung để tóm tắt RRF cùng lý do hệ thống vẫn chọn top-k.

## Evidence dẫn tới quyết định

**Facts:** Tester A thích ví dụ nhưng chỉ tin khoảng “50–50” và vẫn có thể dùng ChatGPT ngoài. Tester B thấy câu hỏi khá liên quan, muốn được hỏi trước, và cảm thấy đây là hỗ trợ chứ không phải kiểm tra. Tester C muốn tìm hiểu sâu ở nguồn ngoài và thấy gợi ý quá thường xuyên gây khó chịu.

**Diễn giải:** Tester cần thấy rõ điểm đang tương tác, giữ quyền đổi/bỏ qua và có một phần tóm tắt ngắn để củng cố kiến thức trước khi quay lại bài. Feedback hiện tại chưa đủ để tuyên bố một option thắng.

## Still unproven

- B có giúp học viên quay lại bài nhanh hơn và hiểu RRF/top-k tốt hơn tra cứu ngoài hay không.
- Hai câu chẩn đoán có phù hợp cho các mức độ khó và các khái niệm khác nhau hay không.
- Ba option chưa được so sánh trên cùng một tester trong cùng điều kiện, nên chưa thể kết luận B tốt hơn A hoặc C một cách nhân quả.
- Chưa có dữ liệu về thời gian hoàn thành task, tỉ lệ quay lại bài, hoặc mức độ hiểu sau test.