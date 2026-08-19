# Prototype Links — Nhóm AI Tutor
## A/B/C Prototype Index

| Option | Người phụ trách | Link prototype | Critical interaction cần test | Trạng thái |
|---|---|---|---|---|
| **A — User-led Inline Explain** | Nguyễn Minh Quân | [Figma design](https://www.figma.com/design/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1) · [Demo prototype](https://www.figma.com/proto/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1) | User bôi đen `RRF`/`top-k`, chọn kiểu giải thích và lấy lại control bằng đổi lựa chọn/đóng/quay lại | Đã test |
| **B — Collaborative Diagnosis** | Vũ Đình Huy | [Figma design](https://www.figma.com/design/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1) · [Demo prototype](https://www.figma.com/proto/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1) | User trả lời hai câu chẩn đoán, xem evidence và xác nhận hoặc bác bỏ kiến thức nền AI đề xuất | Đã test |
| **C — AI-led Recovery Path** | Đào Văn Đạt | [Figma design](https://www.figma.com/design/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1) · [Demo prototype](https://www.figma.com/proto/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1) | AI hiển thị suggestion card; user xem lý do rồi accept/change/dismiss/tắt gợi ý | Đã test |

## Common Test Contract

| Thành phần | Nội dung giữ nguyên cho A/B/C |
|---|---|
| Target user | Học viên trong khóa đang học một bài mới trên VLearn |
| Situation | Gặp đoạn RRF/top-k không hiểu trong khi bài học vẫn tiếp tục |
| Task | Hiểu RRF làm gì và vì sao hệ thống vẫn chọn top-k sau fusion |
| Desired outcome | Trả lời được câu hỏi kiểm tra và quay lại đúng vị trí đang học |
| Fixture | Cùng đoạn RRF, câu trả lời sai về cosine similarity và lịch sử học Ranking/Reranking |

## Hướng dẫn mở prototype Figma

1. Mở [Demo prototype](https://www.figma.com/proto/sHzj89Xc3Jjm8e34Sfle2J/Lab18?node-id=0-1&t=yb5FmfSP3w6cEWo9-1).
2. Trong thanh **Flows** bên trái, chọn option cần test: 
    - **Option A — User-led Inline Explain**
    - **Option B — Collaborative Diagnosis** 
    - **Option C — AI-led Recovery Path**
3. Tại màn hình VLearn của **Bài 19 · Day08**, đọc slide **Hybrid Search + RRF** và thực hiện câu hỏi kiểm tra hiển thị bên dưới. Facilitator chỉ quan sát, không giải thích UI hoặc gợi ý đáp án.

## Reset Path chung

- Nút **Bắt đầu lại** nằm ở góc trên bên phải màn hình prototype.
- Khi cần thực hiện lại một option, chọn **Bắt đầu lại**, sau đó kiểm tra màn hình trở về slide RRF và câu hỏi kiểm tra ban đầu của option đang chọn.
- Muốn đổi option, chọn flow A/B/C trong thanh bên trái rồi thực hiện lại task.

## Kiểm tra trước khi test

- [x] Ba option A/B/C dùng chung một link demo; quyền chia sẻ đã được kiểm tra để tester, giảng viên và TA có thể truy cập.
- [x] Các flow A/B/C mở được từ thanh **Flows** và dùng chung context, task cùng dữ liệu mẫu.
- [x] Demo prototype trên Figma hoạt động mượt khi chuyển flow và thực hiện các tương tác chính.
- [x] Nút **Bắt đầu lại** hoạt động để khởi động lại quy trình khi gặp sự cố.

## Cập nhật sau test

Hiện chưa có bản cập nhật prototype nào được triển khai sau các phiên test.

**Future work:**

- Cải thiện thao tác **bôi đen** thuật ngữ/đoạn khó trong Option A để dễ nhận biết và phản hồi rõ hơn.
- Bổ sung **summary slide** tóm tắt nội dung RRF và lý do chọn top-k, giúp học viên ôn lại trước hoặc sau khi thực hiện task.