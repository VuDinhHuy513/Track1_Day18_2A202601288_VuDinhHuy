# Three-option Design Sheet — Nhóm AI Tutor

**Case:** AI Tutor — Diagnostic Refresher  
**Thành viên:** Nguyễn Minh Quân · Vũ Đình Huy · Đào Văn Đạt  
**Trạng thái:** Design complete · Prototype links added · User tests completed

## 1. Evidence Snapshot từ Day 17

| Practice Note | User đã thực sự làm/nói gì? | Điều nhóm đang diễn giải |
|---|---|---|
| P01 | User nói mình “không biết hổng chỗ nào để đi vá”; tra “RRF reranking là gì” nhưng sau đó vẫn không giải thích được lý do chọn top-k. | Có tín hiệu user biết đoạn đang tắc nhưng chưa định vị được phần nền cần bổ sung. |
| P02 | User nói việc cố gắng tìm hiểu có thể khiến mình bỏ lỡ phần bài sau. | Có tín hiệu chi phí gián đoạn là một barrier riêng. |
| P03 | User đưa nội dung slide vào ChatGPT để hỏi Harness; mất khoảng 5 phút và lớp đi trước 5 slide. | Có workaround và consequence quan sát được; nghiêng nhẹ về chi phí gián đoạn. |

### Pattern và mâu thuẫn

- Cả ba đều gặp điểm không hiểu trong khi bài học vẫn đang tiếp tục.
- P01 và P03 đều rời luồng học hiện tại để dùng nguồn bên ngoài.
- P02 và P03 cho tín hiệu về mất mạch hoặc chậm tiến độ.
- P01 nghiêng về khó chẩn đoán phần nền; P02/P03 cho thấy ngay cả khi biết điểm vướng, chi phí xử lý vẫn có thể là barrier.
- Hypothesis C về AI Tutor hiện có chưa được kiểm tra trực tiếp trong ba Practice Notes.

## 2. Hypothesis Problem

> Khi **đang học một bài mới trên VLearn và gặp một đoạn hoặc khái niệm không hiểu**, **học viên** gặp khó khăn trong việc **gỡ điểm vướng để tiếp tục bài học** vì **họ không thể nhanh chóng xác định và bổ sung phần kiến thức liên quan ngay trong mạch học**, dẫn đến **phải rời bài đi tra cứu, mất mạch, bị chậm so với lớp hoặc tiếp tục khi chưa hiểu chắc nội dung**.

### Evidence ban đầu hỗ trợ

P01 phải tra cứu RRF nhưng vẫn không giải thích được top-k; P02 nêu rủi ro bỏ lỡ bài sau khi dừng lại tìm hiểu; P03 mất khoảng 5 phút tra cứu Harness và lớp đi trước 5 slide. Evidence cho thấy situation, workaround và consequence có tồn tại ở các trường hợp được luyện tập.

### Still Unproven

- Barrier chính là không xác định được kiến thức nền hay chi phí gián đoạn.
- AI chẩn đoán có chính xác hơn user tự chọn điểm khó hay không.
- Giải thích trong bài có giúp user hiểu, không chỉ giúp trả lời ngay hay không.
- User có chấp nhận AI chủ động dùng lịch sử học để đề xuất hay không.
- Problem prevalence, product value, learning outcome và market demand chưa được chứng minh.

## 3. Comparison Contract — Những thứ giữ nguyên

| Thành phần | Quyết định chung cho A/B/C |
|---|---|
| Target user | Học viên trong khóa đang học một bài mới trên VLearn |
| Situation | Học viên gặp đoạn RRF/top-k không hiểu trong khi bài học vẫn tiếp tục |
| Task | Hiểu RRF làm gì và giải thích được vì sao hệ thống vẫn chọn top-k sau fusion |
| Desired outcome | Học viên trả lời được câu hỏi kiểm tra và quay lại đúng vị trí đang học mà không phải tra cứu bên ngoài |
| Content/data fixture | Cùng đoạn bài RRF, câu trả lời gần đây chưa chính xác và lịch sử học tập mẫu |
| Visual contract | Cùng context screen, typography, components, panel width và vị trí nút quay lại/reset |

### Content/data fixture dùng chung

**Đoạn bài học:**

> “Reciprocal Rank Fusion — RRF — kết hợp nhiều danh sách kết quả đã được xếp hạng. Điểm của mỗi tài liệu được tính dựa trên vị trí của tài liệu trong từng danh sách. Sau khi fusion, hệ thống giữ lại top-k tài liệu để chuyển sang bước tiếp theo.”

**Câu hỏi kiểm tra:**

> “RRF có vai trò gì và vì sao hệ thống vẫn cần chọn top-k sau khi fusion?”

**Câu trả lời gần đây của học viên:**

> “RRF cộng các điểm cosine similarity để chọn top-k.”

**Lịch sử học tập mẫu:**

- Đã hoàn thành Embeddings và Vector Retrieval.
- Chưa hoàn thành Ranking và Reranking.

Fixture trên là dữ liệu giả lập phục vụ prototype, không phải interview evidence.

## 4. Three Solution Options

| Thành phần | Option A — User-led Inline Explain | Option B — Collaborative Diagnosis | Option C — AI-led Recovery Path |
|---|---|---|---|
| Solution mechanism | User chọn chính xác điểm khó và kiểu giải thích; AI không tự suy luận nguyên nhân. | User và AI cùng xác định kiến thức nền qua hai câu hỏi ngắn. | AI dùng câu trả lời gần đây và tiến độ học để chủ động đề xuất lộ trình ôn. |
| User làm gì? | Bôi đen `RRF` hoặc `top-k`; chọn định nghĩa, ví dụ hoặc giải thích từng bước. | Báo chưa hiểu, trả lời hai câu và xác nhận hoặc sửa đề xuất. | Xem evidence, chấp nhận, đổi khái niệm, dismiss hoặc yêu cầu hỗ trợ từ người thật. |
| AI làm gì? | Chỉ giải thích phần user chọn dựa trên bài hiện tại. | Hỏi, phân tích câu trả lời, đề xuất một phần nền và tạo refresher sau khi user xác nhận. | Phân tích câu trả lời sai và trạng thái hoàn thành; đề xuất bản đồ kiến thức cùng mức chắc chắn. |
| Trigger | User bôi đen nội dung và yêu cầu giải thích. | User bấm “Tôi vẫn chưa hiểu”. | Sau câu trả lời sai ở checkpoint, AI hiển thị suggestion card nhưng không tự chuyển bài. |
| Trade-off chính | Nhanh, ít suy luận, kiểm soát cao; có thể chỉ xử lý triệu chứng bề mặt. | Có thể tìm đúng nguyên nhân hơn; thêm thao tác và thời gian. | Ít thao tác; có rủi ro suy luận sai, gây phiền hoặc giảm agency. |

### Solution hypotheses

- **A:** Nếu user chọn đúng điểm khó và nhận giải thích ngay trong bài, họ có thể gỡ điểm vướng nhanh mà không cần AI suy luận về kiến thức nền.
- **B:** Nếu AI và user cùng chẩn đoán trước khi giải thích, phần hỗ trợ có thể xử lý nguyên nhân sâu hơn thay vì chỉ diễn giải lại đoạn hiện tại.
- **C:** Nếu AI chủ động nhận biết tín hiệu mắc kẹt và đưa lộ trình có evidence, user có thể tìm đường ôn với ít thao tác hơn.

## 5. Distance Check

- **A khác B vì:** A giả định user biết điểm cần hỏi và AI chỉ giải thích phần được chọn; B cùng user chẩn đoán nguyên nhân trước.
- **B khác C vì:** B chỉ bắt đầu khi user yêu cầu; C chủ động đưa đề xuất từ dữ liệu học tập để user review.
- **A khác C vì:** A không dùng lịch sử và không tự suy luận; C dùng câu trả lời gần đây cùng tiến độ để đề xuất lộ trình.

```text
Option A: USER INITIATES — AI RESPONDS
→ Option B: USER + AI CO-DIAGNOSE
→ Option C: AI INITIATES — USER REVIEWS
```

## 6. Human–AI Decision Table

| Human–AI decision | Option A | Option B | Option C |
|---|---|---|---|
| User làm gì? AI làm gì? | User chọn đoạn và kiểu giải thích; AI phản hồi đúng phạm vi được chọn. | User trả lời hai câu; AI đề xuất phần nền; user xác nhận trước khi AI tạo refresher. | AI hiển thị suggestion card; user xem evidence và quyết định chấp nhận, đổi hoặc dismiss. |
| AI Act / Ask / Don't Act? Vì sao? | **Act** sau yêu cầu rõ; **Don’t Act** nếu user chưa chọn nội dung. | **Ask** trước, sau đó mới **Act** khi user xác nhận. | **Ask bằng đề xuất chủ động**, không tự điều hướng hoặc thay đổi tiến trình. |
| User hiểu capability/limit bằng gì? | “AI chỉ giải thích phần bạn chọn dựa trên bài hiện tại; không chẩn đoán toàn bộ kiến thức nền.” | “Hai câu sau giúp ước lượng phần có thể cần ôn; kết quả là đề xuất, không phải kết luận chắc chắn.” | “Đề xuất dựa trên câu trả lời gần đây và tiến độ; AI có thể suy luận sai và không tự đổi lộ trình.” |
| Evidence/uncertainty thể hiện thế nào? | Hiển thị đoạn được chọn và nguồn bài hiện tại; nếu thiếu context, AI nói chưa đủ thông tin. | Hiển thị câu trả lời nào dẫn đến đề xuất; dùng “có thể/khả năng” và yêu cầu user xác nhận. | Hiển thị hai tín hiệu được dùng, mức chắc chắn định tính và nút “Vì sao tôi thấy đề xuất này?”. |
| User kiểm soát và recovery thế nào? | Đổi đoạn, đổi kiểu giải thích, đóng panel hoặc quay lại đúng vị trí. | Bỏ qua chẩn đoán, sửa câu trả lời, bác bỏ khái niệm, chọn phần khác hoặc quay lại bài. | Chấp nhận, dismiss, chọn đường khác, chỉ dùng câu trả lời hiện tại, tắt gợi ý hoặc hỏi giảng viên. |

## 7. Feedback and Data Check

| Nội dung | Option A | Option B | Option C |
|---|---|---|---|
| Dữ liệu dùng | Đoạn user chọn và trang hiện tại | Trang hiện tại và hai câu trả lời chẩn đoán | Trang hiện tại, câu trả lời gần đây và trạng thái hoàn thành bài |
| Ảnh hưởng của feedback | Chỉ phiên hiện tại | Sửa đề xuất trong phiên hiện tại | Bác bỏ đề xuất sẽ dừng lộ trình hiện tại |
| Ghi nhớ mặc định | Không | Không | Không nếu user chưa đồng ý |
| Rút quyền | Đóng phần giải thích | Dừng chẩn đoán và bỏ câu trả lời phiên | “Chỉ dùng câu trả lời hiện tại” hoặc “Tắt đề xuất chủ động” |

Prototype không giả định dữ liệu được dùng để huấn luyện hoặc cá nhân hóa cho lần sau.

## 8. Scope ba Micro-prototype

Mỗi option gồm đúng ba trạng thái:

```text
COMMON CONTEXT
→ CRITICAL INTERACTION
→ RESULT / USER DECISION
```

| Option | Common Context | Critical Interaction | Result/User Decision |
|---|---|---|---|
| A | Đọc đoạn RRF và câu trả lời gần đây | Bôi đen `RRF`/`top-k`, chọn định nghĩa/ví dụ/từng bước | Đọc giải thích; đổi kiểu, chọn đoạn khác, đóng hoặc quay lại câu hỏi |
| B | Đọc cùng đoạn và bấm “Tôi vẫn chưa hiểu” | Trả lời hai câu chẩn đoán | Xem đề xuất cùng evidence; xác nhận, sửa, bỏ qua hoặc quay lại |
| C | Sau câu trả lời sai, suggestion card xuất hiện | Mở lý do và xem các đường ôn tập | Chấp nhận, đổi đường, dismiss, tắt gợi ý hoặc hỏi người thật |

### Shared components và reset

- Cùng header VLearn, tên bài, tiến độ, nội dung, câu hỏi và câu trả lời gần đây.
- Cùng panel width, typography, màu, nút “Quay lại bài” và “Bắt đầu lại”.
- Reset xóa lựa chọn/câu trả lời trong phiên và đưa tester về Common Context.

## 9. Prototype Annotation

### Option A

```text
OPTION A
We expect the tester to: chọn điểm khó, chọn kiểu giải thích và quay lại câu hỏi.
Watch for: tester có nhận ra phải chọn nội dung không; có đổi cách giải thích không.
Do not explain: không chỉ từ cần chọn và không giải thích đáp án RRF/top-k.
```

### Option B

```text
OPTION B
We expect the tester to: trả lời hai câu, đọc lý do và chấp nhận hoặc bác bỏ đề xuất.
Watch for: hai câu có gây tốn công không; tester có hiểu đây chỉ là đề xuất không.
Do not explain: không nói đáp án đúng và không khuyến khích chấp nhận chẩn đoán.
```

### Option C

```text
OPTION C
We expect the tester to: nhận thấy đề xuất, kiểm tra evidence và quyết định accept/change/dismiss.
Watch for: suggestion có gây phiền không; tester có tìm thấy data control và dismiss không.
Do not explain: không nói vì sao AI xuất hiện và không chỉ vị trí nút dismiss.
```

## 10. Definition of Testable

- [x] A/B/C bắt đầu từ cùng context, task và fixture.
- [x] Mỗi option có tối đa ba trạng thái chính.
- [x] Option A thể hiện user-led/no-inference.
- [x] Option B thể hiện user–AI co-diagnosis.
- [x] Option C thể hiện proactive suggestion và user review.
- [x] Mỗi option có control/recovery được thiết kế.
- [x] Có reset path chung trong thiết kế.
- [x] Tester có thể mở và thao tác flow prototype được phân công.
- [x] Ba prototype đã được nhóm review trong cùng file Figma.
- [x] Link thiết kế và demo dùng chung cho A/B/C đã được điền trong `prototype-link.md`.

Ba điều kiện cuối đã được xác nhận sau khi prototype hoàn thành và được đưa vào test.