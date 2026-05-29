# Phase 6 — Reflection: AI Log (Nhật ký cá nhân)

**Thực hiện bởi:** Nhan Khánh Đình (2A202600673)
**Mục tiêu:** Phản ánh trung thực về quá trình sử dụng AI (ChatGPT, Gemini, Claude) làm trợ lý đồng hành (thought-partner) trong suốt buổi Lab 02.

---

## 🤖 AI giúp gì trong buổi Lab?

### 1. **Brainstorm Bài Toán (Phase 1 — SCAN)**

**Sử dụng:** ChatGPT + Gemini

**Cách làm:**

- Sử dụng **4 Lenses** (Repetitive, Time-consuming, AI-upgrade, Stakeholder Pain) để quét qua các hoạt động vận hành của Xanh SM và VinFast.
- Prompt AI gợi ý các bài toán thực tế dựa trên các Lens này để tìm ra các bottleneck trong vận hành.
- **Kết quả:** Xác định được 5 bài toán then chốt:
  1. Điều phối trạm sạc V-Green thông minh.
  2. Phát hiện gian lận GPS và trục lợi khuyến mãi.
  3. Phân loại và xử lý ticket hỗ trợ (quên đồ, thái độ tài xế).
  4. Bảo dưỡng tiên đoán qua dữ liệu Telematics.
  5. Giám sát tài xế chủ động qua Camera/Dữ liệu hành trình.
- **Giá trị:** Giúp hệ thống hóa các vấn đề tồn đọng và mở rộng tư duy về các giải pháp AI khả thi cho từng loại bottleneck.

---

### 2. **Hoàn thiện Quick Problem Cards (Phase 2)**

**Sử dụng:** Gemini, Claude

**Cách làm:**

- Chọn ra Top 3 bài toán (Trạm sạc, Gian lận GPS, Ticket hỗ trợ) để hoàn thiện các Problem Cards.
- Sử dụng AI để đóng vai trò "CFO khắt khe" phản biện về logic, metric và tính thực tế của giải pháp (tại sao không dùng Rule-based mà phải dùng AI).
- **Kết quả:**
  - Card #1 (Trạm sạc): Xác định AI hỗ trợ gợi ý trạm, giảm 30% thời gian chờ.
  - Card #2 (Gian lận GPS): Ưu tiên Rule-based kết hợp AI để phát hiện 95% trường hợp.
  - Card #3 (Ticket hỗ trợ): Dùng LLM để giảm thời gian xử lý từ 15 phút xuống dưới 3 phút.
- **Giá trị:** AI giúp làm sắc nét các Success Metric và xác định đúng kiến trúc kỹ thuật phù hợp cho từng bài toán.

---

### 3. **Thiết kế 6-field Problem Statement & Deep-Dive (Phase 3)**

**Sử dụng:** Gemini 2.5 Flash

**Cách làm:**

- Nhóm tập trung vào bài toán "Smart Dispatching" (tối ưu điểm đón dựa trên text và GPS). Viết bản thảo 6-field Problem Statement.
- Prompt AI kiểm tra tính chặt chẽ: (1) Bottleneck có đủ chi tiết không? (2) Business Impact có con số cụ thể không? (3) Success Metric có SMART không? (4) Operational Boundary có an toàn không?
- **Feedback AI:** Bổ sung các con số cụ thể cho Business Impact (ví dụ: "1000 phút lãng phí/ngày") và thắt chặt Operational Boundary (CẤM tuyệt đối tự động gán xe mà không có confirm).
- **Giá trị:** Nâng cao chất lượng báo cáo Deep-Dive, đảm bảo tính thực tế và khả thi.

---

### 4. **Tối ưu System Prompt cho Prototype (Phase 4)**

**Sử dụng:** Gemini 2.5 Flash

**Cách làm:**

- Dựa trên các Problem Cards và Operational Boundary đã xác định, yêu cầu AI thiết kế và tối ưu System Prompt cho công cụ điều vận.
- **Phản hồi AI:** Viết lại System Prompt bằng tiếng Anh chuyên nghiệp, tích hợp các ràng buộc về Confidence Score và quy trình Human-in-the-loop.
- **Giá trị:** Tạo ra nền tảng vững chắc cho phần code Prototype, đảm bảo AI hoạt động đúng ranh giới cho phép.

---

### 5. **Viết Justification cho quyết định GO/NO-GO (Phase 5)**

**Sử dụng:** Claude 3.5 Sonnet + Gemini

**Cách làm:**

- Prompt AI đóng vai trò Board Member để viết justification chi tiết cho quyết định đầu tư.
- **Phản hồi AI:** Tính toán ROI cụ thể (tiết kiệm ~$1,920/tháng, tăng doanh thu ~$7,500/tháng), xác định thời gian hoàn vốn (payback period ~3 tuần) và các rủi ro kỹ thuật.
- **Giá trị:** Biến các suy luận cảm tính thành các lập luận dựa trên dữ liệu (data-driven) và tư duy kinh doanh sắc bén.

---

## ⚠️ AI Sai Gì / Hallucination?

### 1. **Hallucination #1: Overestimate AI Capability**

- **Tình huống:** AI đề xuất hệ thống "multi-agent" cực kỳ phức tạp để giải quyết bài toán điều vận đơn giản.
- **Sai lầm:** Không đánh giá đúng độ phức tạp và nguồn lực triển khai (MVP cần 3-4 tháng thay vì 2 tuần).
- **Cách fix:** Ràng buộc scope bằng prompt: "Cần một LLM Feature đơn giản, không phải Agent phức tạp".

### 2. **Hallucination #2: Metric không thực tế**

- **Tình huống:** AI gợi ý giảm thời gian chờ từ 12 phút xuống dưới 30 giây.
- **Sai lầm:** Không tính đến thời gian tương tác của người dùng (nhập text, xác nhận).
- **Cách fix:** Yêu cầu AI breakdown step-by-step timeline để tự nhận ra sự phi lý.

### 3. **Hallucination #3: Operational Boundary lỏng lẻo**

- **Tình huống:** AI đề xuất tự động gán xe khi confidence > 90% mà không cần người xác nhận.
- **Sai lầm:** Bỏ qua rủi ro sai sót 10% trong dịch vụ khách hàng nhạy cảm.
- **Cách fix:** Prompt AI nghiên cứu tiêu chuẩn an toàn ngành vận chuyển và áp dụng cơ chế Human-in-the-loop.

---

## 🔧 Kỹ thuật Prompting hiệu quả

1. **Roleplay khắt khe:** Đóng vai CFO/CTO để review ngược lại các đề xuất của chính mình.
2. **Breakdown & Timeline:** Yêu cầu AI giải trình từng bước để kiểm tra tính khả thi của metric.
3. **Explicit Constraints:** Đưa ra các ràng buộc cứng về thời gian (MVP 2 tuần), ngân sách và độ trễ.
4. **Adversarial Prompting:** Yêu cầu AI tự tấn công và bảo vệ các Operational Boundary mình đã thiết lập.

---

## 📊 Tóm tắt: Vai trò của AI trong buổi Lab

| Aspect            | AI giúp                  | AI sai                              | Cách fix                          |
| ----------------- | ------------------------ | ----------------------------------- | --------------------------------- |
| **Brainstorm**    | ✅ Gợi ý ý tưởng đa dạng | ❌ Thiếu trọng tâm impact           | Tự filter bằng business sense     |
| **Metric**        | ✅ SMART-ify mục tiêu    | ❌ Quá tham vọng                    | Challenge bằng timeline breakdown |
| **Architecture**  | ✅ Gợi ý cấu trúc nhanh  | ❌ Over-engineer                    | Thiết lập constraint rõ ràng      |
| **Risk/Boundary** | ✅ Liệt kê rủi ro        | ❌ Đánh giá sai mức độ nghiêm trọng | Role-play chuyên gia              |
| **Justification** | ✅ Phân tích ROI sắc bén | ⭐ Tốt nhất                         | Không cần chỉnh sửa nhiều         |

---

## 🎓 Lesson Learned: AI là Thought-Partner, không phải Decision-Maker

**Kết luận của nhóm:**
Trong suốt buổi Lab, AI đã đóng vai trò là một người cộng sự đắc lực giúp mở rộng tư duy và phát hiện lỗi sớm. Tuy nhiên, AI chỉ thực sự hiệu quả khi chúng ta:

1. **Bộc lộ suy nghĩ rõ ràng:** Viết prompt tốt giúp chính chúng ta hiểu rõ logic bài toán hơn.
2. **Luôn đặt nghi vấn:** Không chấp nhận output của AI một cách mù quáng, luôn challenge các giả định "quá tốt để là thật".
3. **Ưu tiên Safety over Automation:** Trong các bài toán kinh doanh thực tế, sự an toàn và quyền kiểm soát của con người luôn quan trọng hơn sự tự động hóa hoàn toàn.

---

**Ngày hoàn thành:** 29/05/2026
