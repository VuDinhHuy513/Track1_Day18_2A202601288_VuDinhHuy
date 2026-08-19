# AI Support Log — Vũ Đình Huy · 2A202601288

**Track 1 · Day 18 — Multiple Prototypes & Human–AI Design**
Nhóm ABC · Case: AI Tutor — Diagnostic Refresher · Phụ trách **Option A — User-led Inline Explain**

| Mục | Nội dung |
|---|---|
| Công cụ | Claude (Claude Code) |
| Ngày | 19/08/2026 |
| Phạm vi dùng AI | Đọc tài liệu lab · gợi ý cơ chế A/B/C · sinh canned content · viết code prototype (HTML + Figma Plugin API) · rà soát tính nhất quán giữa các artifact |
| **Không dùng AI cho** | Tạo quote, observation hoặc feedback của tester · viết thay phần reflection cá nhân · suy diễn dữ liệu người dùng chưa nói |

---

## 1. AI đã giúp tôi ở đâu?

### 1.1 Đọc và giải mã tài liệu lab

Tài liệu Day 18 là **14 ảnh slide** và **9 file PDF chụp màn hình** trang codelab — PDF dạng ảnh nên `pdftotext` trả về rỗng. AI cài `pymupdf`, trích ảnh nhúng ở độ phân giải gốc, cắt thành lát đọc được, rồi tóm tắt lại 6 chặng, 5 gate và yêu cầu nộp bài.

Tự phát hiện và báo rõ **bản chụp thiếu mục 9–10 của codelab và slide 15/15**, thay vì lấp bằng suy đoán.

### 1.2 Xác định lại Hypothesis Problem từ evidence Day 17

AI đối chiếu ba Interview Record (P01, P02, P03) và chỉ ra mâu thuẫn nội tại trong README Day 17: mục 2.7 chốt barrier A, nhưng mục 4 lại ghi 1 lượt nghiêng A và 2 lượt nghiêng B.

Một phát hiện có giá trị: **P03 không phải tín hiệu B thuần**. P03 hỏi ChatGPT *"Harness là gì?"* — tra tên khái niệm **trong bài**, trùng khuôn với P01 tra *"RRF reranking là gì"*. Theo đúng tiêu chí nhóm tự đăng ký ở mục 2.6 Day 17, đó là **tín hiệu A**; phần nghiêng B nằm ở consequence (mất 5 phút, lớp đi trước 5 slide), không nằm ở barrier.

### 1.3 Dựng và kiểm thử prototype

| Việc | Kết quả |
|---|---|
| Prototype HTML Option A | Dựng đầy đủ giao diện VLearn, **AI tự test 15 chức năng** trong trình duyệt và báo cáo từng mục |
| Script Figma Plugin API | 8 script Scripter: dựng frame, sửa highlight, thêm nhánh top-k, sửa logo, tách Section, dọn flow, dựng Option B, dựng Option C |
| Kiểm cú pháp | Mọi script được `node --check` trước khi giao |

### 1.4 Soạn nội dung thiết kế

Ba Solution Options với Comparison Contract, Distance Check, Human–AI Decision Table; hai bản PLAN bàn giao cho Huy (Option B) và Đạt (Option C); toàn bộ canned content giải thích RRF và top-k.

---

## 2. AI sai, hời hợt hoặc làm các option giống nhau ở đâu?

Đây là phần dài nhất, và cố ý như vậy. Trong buổi này AI sai nhiều hơn đúng ở khâu thiết kế.

### 2.1 ❗ Làm Option A lẫn sang Option B — lỗi nghiêm trọng nhất

AI đề xuất Option A là *"chú giải nền nội tuyến: hover thuật ngữ → định nghĩa + dòng **Phần này giả định bạn đã biết: [X]** + nút **Mở phần nền**"*.

**Đó chính là chẩn đoán kiến thức nền** — việc của Option B. Nếu làm theo, A và B cùng đề xuất phần nền, chỉ khác ai bấm trước → **Distance Check sụp, trượt Gate 2**.

Bản đúng là bản nhóm đã chốt trong `prototype-link.md`: user bôi đen → **chọn kiểu giải thích** (Định nghĩa / Ví dụ / Từng bước) → AI **chỉ giải thích đúng phần được chọn**, không suy đoán gì thêm.

### 2.2 ❗ Option C thiếu "lộ trình / bản đồ kiến thức"

Spec nhóm ghi rõ AI đề xuất **lộ trình ôn tập** và **bản đồ kiến thức**. AI dựng C chỉ đề xuất **một khái niệm đơn lẻ** — giống hệt B về mặt đầu ra, khác mỗi chuyện ai bấm trước.

Lại là lỗi làm hai option giống nhau. Phải sửa C3 thành lộ trình 2 bước có đánh số và thêm frame C4b để đi hết lộ trình.

### 2.3 Thẻ gợi ý gọi tên khái niệm mà user chưa biết

Lời thẻ ban đầu: *"Có vẻ phần **thứ hạng khác điểm số** đang gây vướng."*

Vòng luẩn quẩn: nếu user đã hiểu cụm đó nghĩa là gì thì họ đã không trả lời sai. Phải viết lại để neo vào chính câu user vừa viết: *"Câu trả lời vừa rồi của bạn dùng **điểm số**, nhưng RRF dùng **thứ hạng**."*

### 2.4 Đếm sót và làm hỏng test-ready

| Lỗi | Hệ quả |
|---|---|
| Đếm chữ `RRF` trong slide còn **3**, thực tế **4** — quên tiêu đề `Hybrid Search + RRF` | Thiếu vùng bấm |
| Chỉ dựng highlight cho **1 trong 4** chỗ | Tester bấm 3 chỗ kia **không có phản hồi** → vi phạm *Definition of Test-Ready* |
| `top-k` không có vùng bấm nào | Cùng lỗi trên |
| **Hardcode toạ độ** highlight `x=481` thay vì đo | Vệt vàng lệch khỏi chữ |

### 2.5 Sai về công cụ — 5 lần

| # | Sai gì | Hậu quả |
|---|---|---|
| 1 | Dùng **object spread** `{...}` trong script Option B | Scripter không hỗ trợ ES2018 → script **không chạy được** |
| 2 | Script tạo **4 page** | Gói Figma Starter chỉ cho **3 page** → chết giữa chừng, để lại 2 page rỗng |
| 3 | Không biết **clone frame starting point sẽ đẻ thêm flow** | Option B ra **6 flow trùng tên** thay vì 1 |
| 4 | `figma-fix-logo.js` chỉ quét `currentPage` | Sau khi tách page chỉ sửa được 1 trong 3 page |
| 5 | Khẳng định *"flow starting point theo từng page nên phải tách page"* | **Sai** — một page chứa được nhiều flow. Lập luận này suýt khiến nhóm tách page không cần thiết trong khi đang bị giới hạn 3 page |

### 2.6 Sai khi đọc hiểu và khi tự kiểm

- Hiểu nhầm câu *"đã làm xong page 1"* thành *"đã tách page xong"*, trong khi script tách page **chưa hề chạy**
- Lệnh quét object spread báo **false positive** cho 6 file — nhầm spread mảng `[...arr]` (ES2015, chạy được) với spread object (ES2018, không chạy được)
- Để file `figma-setup-pages.js` ở thư mục khác các script còn lại mà không nói rõ → tôi tưởng thiếu file

---

## 3. Tôi đã tự sửa hoặc quyết định lại điều gì?

### 3.1 Bác bỏ thiết kế Option A của AI

Tôi giữ bản nhóm đã chốt — **chọn kiểu giải thích, AI không chẩn đoán** — thay vì bản AI đề xuất có gợi ý kiến thức nền. Đây là quyết định giữ được khoảng cách giữa A và B.

### 3.2 Tự phát hiện lỗi trong sản phẩm AI dựng

- Phát hiện **2 chữ `RRF` chưa có highlight** mà AI đã báo là xong
- Phát hiện **6 flow trùng** cho Option B khi mở dropdown Present
- Đối chiếu Option C với spec nhóm và chỉ ra **thiếu lộ trình / bản đồ kiến thức**
- Nói rõ **không hiểu nội dung thẻ gợi ý tự động** — chính phản hồi này dẫn tới việc viết lại lời thẻ

### 3.3 Quyết định về công cụ và cấu trúc

| Quyết định | Lý do |
|---|---|
| **Chọn Figma, không dùng HTML** | Cần prototype chạy được có chuyển động và action để demo; bản HTML chỉ giữ làm đối chiếu |
| **Chọn cách 2 — 1 page + 3 Section + 3 flow** | Tiết kiệm hạn mức page, và ba option nằm cạnh nhau thì lệch chỗ nào nhìn thấy ngay — giữ Gate 4 |
| **Chọn phương án (a) cho `top-k`** — thêm 3 frame riêng | Phương án rẻ hơn là cho `top-k` dẫn về giải thích `RRF`; tôi loại vì bấm ra sai nội dung còn tệ hơn không bấm được |
| **Không nâng gói Figma** | Đối chiếu nhu cầu thật với hạn mức free: đủ dùng. Quota MCP đã hết thì đi đường Scripter, không tốn tiền |

### 3.4 Điều tôi giữ lại để quyết định sau khi test

AI đề xuất chuỗi *"Option A không xong thì chuyển sang Option B"*. Tôi đã hỏi và xác nhận lại: **không xây chuỗi này vào prototype**, vì nối A→B thì mất khả năng so sánh và nhiễm thứ tự khi test.

Ý tưởng đó được giữ lại làm **ứng viên Next Change**, chỉ chốt sau khi có evidence từ ba phiên test — đúng như codelab cho phép: *"Kết hợp hai options nhưng giữ một cơ chế chính rõ ràng."*