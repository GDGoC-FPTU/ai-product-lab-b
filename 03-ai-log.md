# Phase 6 — Reflection: AI Log (Nhật ký cá nhân)

**Thực hiện bởi:** Lê Quốc Bảo (2A202600561)  
**Mục tiêu:** Phản ánh trung thực về quá trình sử dụng AI (ChatGPT, Gemini, Claude) làm trợ lý đồng hành (thought-partner) trong suốt buổi Lab 02.

---

## 🤖 AI giúp gì trong buổi Lab?

### 1. **Brainstorm Bài Toán (Phase 1 — SCAN)**

**Sử dụng:** ChatGPT + Gemini

**Cách làm:**

- Tôi prompt: _"Tôi là AI Engineer tại Vin Smart Future. Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng Xanh SM (taxi điện Hà Nội). Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."_
- **Kết quả:** AI trả về 8 bài toán rất tốt, bao gồm: Smart Dispatching, Xử lý sự cố pin, Phân tích hủy chuyến, Đối chiếu chi phí xăng, Lên lịch bảo trì xe, v.v. Tôi chọn 3 bài toán tốt nhất từ danh sách AI gợi ý.
- **Giá trị:** Tiết kiệm ~30 phút brainstorm, giúp tôi có 5+ bài toán chất lượng để đưa vào Phase 2.

---

### 2. **Hoàn thiện Quick Problem Cards (Phase 2)**

**Sử dụng:** Gemini, Claude

**Cách làm:**

- Tôi draft sơ bộ Card #1 (Smart Dispatching) với thông tin: Actor, Workflow, Bottleneck
- Prompt: _"Đây là một thẻ bài toán vận hành tôi đề xuất cho Xanh SM. Hãy đóng vai trò là CFO cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích tại sao rule-based code có thể giải quyết bài toán này tốt hơn là dùng AI. [Dán nội dung card]"_
- **Phản hồi từ Claude:** AI chỉ ra 3 điểm:
  1. **Metric không cụ thể:** "Giảm gọi lại" không nói được từ bao nhiêu % → bao nhiêu %. → **Tôi bổ sung: 25% → 5%**
  2. **Rule-based có thể đủ:** "Tôi có thể dùng regex/fuzzy matching để match text vs danh sách địa danh Hà Nội" → **Tôi thêm phần so sánh Rule vs LLM**
  3. **Confidence score không được định nghĩa:** "Nếu LLM confidence < X%, làm gì?" → **Tôi bổ sung fallback khi < 70%**
- **Giá trị:** AI giúp tôi làm sắc nét bài toán trước khi đưa vào Phase 3, tránh các sai lầm logic từ đầu.

---

### 3. **Thiết kế 6-field Problem Statement & Future-State Flow (Phase 3)**

**Sử dụng:** Gemini 2.5 Flash

**Cách làm:**

- Tôi viết draft 6-field Problem Statement (nội dung hơi sơ sài)
- Prompt AI: _"Tôi vừa hoàn thiện 6-field Problem Statement cho bài toán Smart Dispatching của Xanh SM. Hãy kiểm tra xem các field có chặt chẽ và cụ thể không? Cụ thể kiểm tra: (1) Bottleneck có đủ chi tiết không? (2) Business Impact có con số cụ thể không? (3) Success Metric có SMART không? (4) Operational Boundary có cover hết rủi ro an toàn không? [Dán nội dung]"_
- **Feedback AI:**
  - ✅ Bottleneck chi tiết tốt
  - ⚠️ **Business Impact cần bổ sung con số cụ thể:** "1000 phút lãng phí/ngày" (tôi đã thêm)
  - ✅ Success Metric rất SMART
  - ⚠️ **Operational Boundary thiếu:** "CẤM tự động gán xe mà không có confirm" (tôi đã bổ sung rõ ràng)
- **Giá trị:** Giúp tôi polish báo cáo, từ 80% quality lên 95%.

---

### 4. **Viết Justification cho quyết định GO/NO-GO (Phase 5)**

**Sử dụng:** Claude 3.5 Sonnet + Gemini

**Cách làm:**

- Tôi viết sơ bộ: "Quyết định GO vì bài toán rõ ràng, metric có số, AI fit phù hợp"
- Prompt AI: _"Tôi là startup CFO đang quyết định có nên đầu tư vào dự án AI này không. Hãy viết một justification chi tiết (kỹ thuật + kinh tế) cho quyết định GO/NOT-YET/NO-GO mà một board member khắt khe sẽ thuyết phục. Cân nhắc: ROI, payback period, rủi ro, competitive advantage."_
- **Phản hồi AI:**
  - Giúp tôi tính ROI cụ thể: $1,920/tháng tiết kiệm dispatcher + $7,500/tháng doanh thu thêm = $9,420/tháng
  - Giúp tôi tính payback: API cost ~$1,500/tháng → payback ~3 tuần ✅
  - Giúp tôi identify risks rõ ràng: "Confidence score < 70% → fallback thủ công"
- **Giá trị:** Justification của tôi từ "reasoning lung tung" lên "driven by data & business acumen".

### 5. **Tùy chỉnh và tối ưu System Prompt**

**Sử dụng:** Gemini 2.5 Flash
**Cách làm:**

- Prompt AI: _"Từ phần SYSTEM_PROMPT và nội dung cho sẵn sau [phần Quick Problem Cards], viết lại SYSTEM_PROMPT cho phù hợp, ngôn ngữ sử dụng là tiếng Anh"_
- **Phản hồi AI:**
  - Viết lại phần code cho SYSTEM_PROMPT để tối ưu theo phần phân tích đã có

---

## ⚠️ AI Sai Gì / Hallucination?

### 1. **Hallucination #1: Overestimate AI Capability**

**Tình huống:** Khi tôi prompt ChatGPT về xây dựng "multi-agent system để Smart Dispatching", AI trả lại một proposal về agent kiểm soát cuốc xe real-time, predict tài xế tốt nhất, tối ưu route tất cả cùng lúc (rất phức tạp).

**Sai lầm của AI:**

- Không assess độ phức tạp của bài toán
- Không nhân viên của tôi không có kiến thức ML advanced
- **Vấn đề:** Nếu tôi theo proposal này, MVP sẽ mất 3-4 tháng để xây dựng, quá dài.

**Cách tôi fix:**

- Tôi prompt lại: _"Cái tôi cần là một **LLM Feature đơn giản** (không phải Agent phức tạp), chỉ merge GPS + text để predict vị trí chính xác trong < 1 giây. Hãy suggest một architecture đơn giản nhất mà vẫn giải quyết được bài toán."_
- **AI sửa lại tốt hơn:** Simple pipeline: Input (GPS + text) → Gemini LLM embedding → fuzzy match with Hanoi landmarks DB → return top-3 locations with confidence scores.
- **Lesson learned:** Phải ràng buộc scope khi prompt AI, nếu không AI có xu hướng over-engineer.

---

### 2. **Hallucination #2: Metric không thực tế**

**Tình huống:** Khi tôi prompt "Success Metric cho Smart Dispatching", AI trả về: _"Giảm thời gian chờ đợi từ 12 phút xuống **dưới 30 giây**"_.

**Sai lầm của AI:**

- Metric quá tham vọng (unrealistic 96% improvement)
- Không assess được rằng khách phải mất thời gian để nhập text mô tả, confirm AI gợi ý, v.v. Thực tế không thể xuống 30 giây.

**Cách tôi fix:**

- Tôi challenge AI: _"Làm sao có thể 30 giây khi khách phải mất thời gian nhập text & confirm vị trí? Hãy bổ sung step-by-step timeline để chứng minh."_
- **AI nhận ra lỗi:** AI đồng ý rằng metric phải là "dưới 4-5 phút" thay vì 30 giây, vì phải tính thêm user interaction time.
- **Lesson learned:** Luôn luôn challenge metric "quá tốt để có thể có" của AI bằng cách yêu cầu breakdown step-by-step.

---

### 3. **Hallucination #3: Operational Boundary không đủ chặt chẽ**

**Tình huống:** Khi tôi prompt AI về "Operational Boundary", AI trả về: _"AI được tự động gán xe khi confidence > 90%"_.

**Sai lầm của AI:**

- **Rủi ro cao:** Ngay cả 90% confidence, vẫn có 1 trong 10 cuốc bị assign sai mà **không có human confirm**
- Đối với dịch vụ customer-facing như taxi, điều này không chấp nhận được (khách hàng sẽ phàn nàn)

**Cách tôi fix:**

- Tôi prompt lại: _"Trong ngành taxi/vận chuyển, standard nào để tự động assign vs cần human confirm? Hãy research và suggest boundary that is both safe and scalable."_
- **AI sửa lại tốt hơn:** AI suggest "Bắt buộc Human-in-the-loop ở bước confirm vị trí trước gán xe. Confidence score chỉ dùng để decide có recommend tự động hay ask manual."
- **Lesson learned:** Với các bài toán customer-facing hoặc có impact tài chính, **luôn luôn ưu tiên safety over automation**.

---

## 🔧 Cách tôi Sửa Đổi / Điều Chỉnh Prompt để Ép AI Trả Đúng

### Kỹ thuật 1: **Roleplay cực kỳ khắt khe (CFO, CTO)**

Thay vì: _"Hãy suggest metric"_  
→ **Dùng:** _"Hãy đóng vai CFO khắt khe đang review project này. Metric của tôi có bị gọi là 'unrealistic' không? Tại sao?"_

**Kết quả:** AI tự check lại logic của tôi và thường chỉ ra lỗi mà nó vừa tạo ra.

---

### Kỹ thuật 2: **Ask for breakdown + timeline**

Thay vì: _"Giảm thời gian từ 12 phút → 4 phút?"_  
→ **Dùng:** _"Giảm từ 12 phút → 4 phút. Hãy viết ra step-by-step timeline (khách nhập text: X giây, AI process: Y giây, khách confirm: Z giây, gán xe: W giây) để chứng minh metric này."_

**Kết quả:** AI sẽ lộ ra không thể đạt được metric quá tham vọng, hoặc adjust lại metric phù hợp.

---

### Kỹ thuật 3: **Explicit constraint + success criteria**

Thay vì: _"Hãy suggest architecture"_  
→ **Dùng:** _"Hãy suggest architecture với constraints: (1) < 1 second latency, (2) MVP trong 2 tuần, (3) không cần ML team, (4) confidence score bắt buộc > 70%."_

**Kết quả:** AI sẽ constraint scope và suggest solution phù hợp thực tế hơn.

---

### Kỹ thuật 4: **Adversarial prompting để test ranh giới**

Thay vì: _"Viết operational boundary"_  
→ **Dùng:** _"Viết operational boundary. Sau đó, hãy tự tấn công prompt của chính bạn bằng cách suggest: 'Nếu AI confidence 95%, có thể tự động assign mà không xin confirm được không?' Hãy defend boundary của bạn."_

**Kết quả:** AI sẽ stress-test riêng boundary và làm nó chắc chắn hơn.

---

## 📊 Tóm tắt: Vai trò của AI trong buổi Lab

| Aspect                   | AI giúp                              | AI sai                                                 | Cách fix                          |
| ------------------------ | ------------------------------------ | ------------------------------------------------------ | --------------------------------- |
| **Brainstorm**           | ✅ Rất tốt, gợi ý 8 bài toán đa dạng | ❌ Không tự ưu tiên theo impact/feasibility            | Tôi tự filter dựa business sense  |
| **Metric**               | ✅ Giúp SMART-ify                    | ❌ Có xu hướng quá tham vọng                           | Challenge bằng timeline breakdown |
| **Architectural design** | ✅ Hữu ích                           | ❌ Over-engineer (multi-agent instead of LLM feature)  | Scope rõ constraint từ đầu        |
| **Risk/Boundary**        | ✅ Giúp list ra                      | ❌ Không assess severity đúng                          | Role-play khắt khe (CFO, CTO)     |
| **Justification**        | ✅ Rất tốt, có data-driven           | ⭐ Tốt nhất, AI excel ở việc synthesize lý do phức tạp | Không cần fix bước này            |

---

## 🎓 Lesson Learned: AI là Thought-Partner, không phải Decision-Maker

**Kết luận cá nhân:**
Trong buổi Lab này, AI (ChatGPT, Gemini, Claude) đã giúp tôi **10 lần tốt hơn** vì sao? Không phải vì AI thông minh hơn tôi, mà vì:

1. **AI giúp bộc lộ suy nghĩ:** Khi tôi prompt AI, tôi bắt buộc phải express logic của mình bằng ngôn ngữ rõ ràng → phát hiện lỗi sớm.
2. **AI challenge giả định:** AI không "đồng ý" với tôi = tôi phải defend hoặc sửa lại logic.
3. **AI nhanh:** 30 phút brainstorm × 8 ý tưởng / AI 2 phút, = tiết kiệm 28 phút.
4. **AI không bị ego block:** AI không bảo vệ idea sai của mình, nó sửa lại liền khi tôi challenge.

**Lưu ý quan trọng:** AI là **thought-partner, không phải decision-maker**. Tôi không bao giờ chấp nhận 100% output của AI mà không critical thinking. Lúc nào cũng phải challenge, verify data, assess feasibility riêng.

---

**Ký tên:** Lê Quốc Bảo  
**Ngày hoàn thành:** 29/05/2026
