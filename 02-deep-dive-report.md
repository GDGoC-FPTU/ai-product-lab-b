# Phase 3 & 5 — DEEP-DIVE & EVALUATE (Báo cáo nhóm)

**Nhóm:** B

**Thành viên:** 
- Lê Quốc Bảo (2A202600561) 
- Mai Văn Thuyên (2A202600926) 
- Phan Quốc Anh (2A202600890)
- Nguyễn Tài Khoa (2A202600682)
- Nhan Khánh Đình (2A202600673)

**Công ty thành viên được chọn:** Xanh SM (GSM) — Vận tải xe taxi điện thông minh  
**Bài toán được chọn:** Tối ưu hóa Điểm Đón (Smart Dispatching)  
**Ngày:** 29/05/2026

---

## 🗳️ Quyết định lựa chọn của Ban Giám Đốc Vin Smart Future

Sau Phase 1 & 2, **nhóm quyết định chọn bài toán "Tối ưu hóa Điểm Đón (Smart Dispatching)"** của Xanh SM để thực hiện Deep-Dive vì:
- ✅ Ảnh hưởng trực tiếp đến hiệu suất vận hành real-time
- ✅ Metric rõ ràng: Giảm tỉ lệ gọi lại từ 25% → 5%, giảm thời gian chờ từ 12 phút → 4 phút
- ✅ Giải pháp công nghệ đơn giản (LLM Feature) mà hiệu quả
- ✅ Rủi ro kiểm soát được thông qua Human-in-the-loop

---

## 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

### 3.1. Current-State Workflow Mapping

**Quy trình xử lý yêu cầu đón xe hiện tại của điều phối viên/hệ thống Xanh SM:**

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách gữ     │     │ Hệ thống     │     │ Tài xế lái   │     │ Tài xế gọi   │
│ vị trí GPS   │ ──→ │ gán xe gần   │ ──→ │ đến GPS      │ ──→ │ lại hoặc     │
│ & tin nhắn   │     │ nhất (chỉ    │     │ (có thể sai) │     │ nhắn lại để  │
│ mô tả        │     │ dựa GPS)     │     │              │     │ xác nhận      │
│              │     │              │     │              │     │              │
│ Ai: Khách    │     │ Ai: Hệ      │     │ Ai: Tài xế   │     │ Ai: Tài xế   │
│ ⏱ 2 phút     │     │ ⏱ 1 phút     │     │ ⏱ 6 phút     │     │ ⏱ 3 phút     │
│ Input:       │     │ Input:       │     │ Input:       │     │ Input:       │
│ GPS + Text   │     │ Toạ độ GPS   │     │ GPS sai lệch │     │ GPS sai      │
│ Output:      │     │ Output:      │     │ Output:      │     │ Output:      │
│ Request log  │     │ Gán xe+vị trí│     │ Xe tới sai vị│     │ Xác nhận      │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Cuốc hoàn    │
                                                               │ thành (hoặc  │
                                                               │ delay nhiều) │
                                                               └──────────────┘

🔴 BOTTLENECK: Bước 2 & 3 — Hệ thống chỉ dựa GPS của khách mà không phân tích text mô tả vị trí, 
   dẫn đến tài xế phải gọi lại hoặc lái vòng vèo. Gây tốn thời gian 8-12 phút/lượt.

🔄 HANDOFF: Khách → Hệ thống (bước 1), Hệ thống → Tài xế (bước 2), Tài xế ↔ Khách (bước 3-4)

⏱ TỔNG THỜI GIAN: 2 + 1 + 6 + 3 = 12 phút/cuốc (khi tài xế phải gọi lại)
```

---

### 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Dispatcher (Điều phối viên) của Trung tâm Điều vận Xanh SM Hà Nội. Cũng gián tiếp ảnh hưởng đến tài xế và khách hàng. |
| **2. Current Workflow** | Khi khách hàng gữ yêu cầu đón xe trên app Xanh SM, khách input vị trí GPS và có thể viết tin nhắn mô tả chi tiết (VD: "tôi ở cạnh hiệu thuốc Việt Á, cạnh cầu thang bộ, áo đỏ"). Hệ thống hiện tại **chỉ dựa trên vị trí GPS** để gán xe gần nhất, bỏ qua thông tin text. Tài xế lái đến GPS nhưng nếu vị trí sai, phải gọi khách để xác nhận chính xác. Quy trình: 4 bước, hoàn toàn thủ công/tự động nhưng kém hiệu quả, mất 12+ phút/lượt khi có lỗi GPS. |
| **3. Bottleneck** | Hệ thống không phân tích dữ liệu text từ tin nhắn khách để **điều chỉnh/predict vị trí chính xác** trước khi gán xe. Dẫn đến: (a) Tài xế phải gọi lại hoặc lái vòng vèo, (b) Dispatcher quá tải cuộc gọi incoming, (c) Khách hàng chờ đợi lâu, (d) Rò rỉ doanh thu do timeout cuốc. |
| **4. Business Impact** | **Mỗi ngày:** ~500 cuốc tại Hà Nội có vấn đề GPS sai lệch. **Nếu 25% gọi lại (125 cuốc/ngày) × 8-12 phút gọi** = ~1000 phút (≈ 16 giờ) làm việc lãng phí của team điều vận. **Doanh thu mất:** ~15-20% cuốc bị cancel do chờ đợi lâu (= ~7.5k USD/tháng). **Thương hiệu:** Tài xế/khách phàn nàn trên social media. |
| **5. Success Metric** | 1. **Giảm tỉ lệ tài xế phải gọi lại khách:** Từ 25% (125 cuốc/ngày) ──> **dưới 5% (25 cuốc/ngày)**. <br> 2. **Giảm thời gian chờ đợi của khách:** Từ 12 phút ──> **dưới 4 phút (70% tăng tốc)**. <br> 3. **Tăng tỉ lệ khách hàng hài lòng** (measured by rating): Từ 70% (rating ≥4/5) ──> **90%**. <br> 4. **Giảm chi phí hoạt động:** 8 giờ/ngày × $12/giờ (Dispatcher salary) × 20 ngày = ~$1,920 tiết kiệm/tháng. |
| **6. Operational Boundary** | **AI được phép:** (a) Đọc text mô tả vị trí từ tin nhắn khách, (b) Kết hợp GPS + text để **predict vị trí chính xác** dùng embedding/fuzzy matching với danh sách địa danh Hà Nội, (c) **Điều chỉnh/gợi ý vị trí chính xác** (hiển thị cho khách để confirm trước gán xe), (d) Ghi log confidence score của AI để tracking. <br><br> **CẤM tuyệt đối:** (a) Tự động gán xe mà **không có khách/dispatcher confirm** lại vị trí chính xác, (b) Dùng AI để can thiệp chuyên tuyến tài xế (chỉ hỗ trợ điều chỉnh vị trí pickup), (c) Lưu trữ/chia sẻ text mô tả của khách cho bên thứ ba mà không consent, (d) Hoạt động nếu confidence score < 70% (phải fallback xin confirm khách thủ công). |

---

### 3.3. Future-State Flow & AI Fit

#### **AI Fit Classification:**
✅ Chọn **LLM Feature** (không cần Agentic Loop vì quy trình có structure cố định: input → text-GPS merge → predict → confirm → assign)

#### **Future-State Workflow:**

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách gữ     │     │ 🔵 AI merge  │     │ 🟢 Khách      │     │ Hệ thống     │
│ vị trí GPS   │ ──→ │ GPS + text   │ ──→ │ confirm hoặc │ ──→ │ gán xe gần   │
│ & tin nhắn   │     │ predict vị    │     │ sửa lại vị   │     │ nhất đã       │
│ mô tả        │     │ trí chính xác │     │ trí AI gợi ý │     │ xác nhận     │
│              │     │ + confidence  │     │              │     │              │
│              │     │ score         │     │              │     │              │
│ Ai: Khách    │     │ Ai: AI/LLM   │     │ Ai: Khách    │     │ Ai: Hệ      │
│ ⏱ 2 phút     │     │ ⏱ 15 giây    │     │ ⏱ 30 giây    │     │ ⏱ 1 phút     │
│ Input:       │     │ Input:       │     │ Input:       │     │ Input:       │
│ GPS + Text   │     │ GPS + Text   │     │ Gợi ý vị trí │     │ Vị trí       │
│ Output:      │     │ Output:      │     │ Output:      │     │ Output:      │
│ Request log  │     │ Vị trí dự    │     │ Xác nhận vị  │     │ Gán xe +     │
│              │     │ đoán + score │     │ trí chính xác│     │ notify       │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Tài xế lái   │
                                                               │ đến vị trí   │
                                                               │ chính xác    │
                                                               │ (rất ít gọi  │
                                                               │ lại)         │
                                                               └──────────────┘

↩️ FALLBACK (Nếu AI confidence < 70% hoặc khách click "Tôi không thấy vị trí"):
   → Hệ thống yêu cầu khách xác nhận thủ công qua bản đồ interactive
   → Dispatcher hỗ trợ gọi xác nhận (quay lại quy trình cũ)

🟢 HUMAN-IN-THE-LOOP (HITL):
   → Bước 3: Khách phải confirm/edit vị trí AI gợi ý trước khi gán xe
   → Mục đích: Đảm bảo không tự động gán xe sai vị trí mà không có confirm
```

#### **Tại sao chọn LLM Feature mà không phải Rule / Agent?**

| Phương án | Lợi điểm | Nhược điểm | Lựa chọn |
|-----------|---------|-----------|----------|
| **Rule-based** | Nhanh, đơn giản, dễ maintenance | Không xử lý được mô tả text linh hoạt, hạn chế địa danh | ❌ |
| **LLM Feature** (chọn) | Xử lý text tự nhiên tốt, flexible, confidence score rõ | Latency 0.5-1s, cần fallback khi < 70% confidence | ✅ Phù hợp nhất |
| **Agentic Loop** | Có thể iterate/refine vị trí | Quá phức tạp, rủi ro cao (agentic hallucination), latency dài, không cần cho bài toán này | ❌ |

---

## 🏁 Phase 5 — EVALUATE (Nhóm)

### AI Readiness Checklist:

- [ ] **1. Dữ liệu sẵn sàng:** Chúng tôi có sẵn dataset ≥ 5,000 cuốc xe thực tế với GPS + text mô tả để test/validate AI? 
  - 📊 **Kết quả:** Xanh SM có access đầy đủ vào logs cuốc xe (GPS, text, call history). ✅ **READY**

- [ ] **2. Rủi ro kiểm soát được:** Rủi ro khi AI sai (predict vị trí sai) có nằm trong tầm kiểm soát thông qua HITL hoặc Fallback? 
  - 🛡️ **Kết quả:** Có Human-in-the-loop (khách confirm bước 3) trước khi gán xe. Nếu AI < 70% confidence, fallback yêu cầu khách xác nhận thủ công. ✅ **MITIGATED**

- [ ] **3. Stakeholder sẵn sàng:** Dispatcher + Khách hàng có sẵn sàng thay đổi quy trình làm việc cũ (thêm bước confirm vị trí AI gợi ý)? 
  - 👥 **Kết quả:** Xanh SM management tán thành (nhân viên sẽ có 40 phút/ngày rảnh rỗi thay vì xử lý cuộc gọi lại; khách hàng hưởng chất lượng dịch vụ tốt hơn). ✅ **COMMITTED**

---

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:

#### **🟢 GO (Bắt đầu xây dựng Prototype)**

Quyết định **GO** với scope hẹp:

**Phase 1 (Ngay):** Xây dựng MVP bằng Gemini 2.5 Flash + Google Maps API để:
- Đọc GPS + text description từ request khách
- Predict vị trí pickup chính xác (confidence score > 70%)
- Return gợi ý vị trí cho khách confirm

**Phase 2 (Tháng 2):** 
- Deploy MVP để 5-10% cuốc Hà Nội (A/B test)
- Monitor metrics (tỉ lệ gọi lại, thời gian chờ, rating)
- Collect feedback

**Phase 3 (Tháng 3+):**
- Scale lên toàn thành phố nếu kết quả tích cực

---

### Justification (Lý giải chi tiết dựa trên bằng chứng kỹ thuật & chi phí):

**📊 Lý do Kỹ Thuật:**
1. **Độ khả thi cao:** LLM Feature là giải pháp proven technology (OpenAI GPT, Gemini đã xử lý tốt text-to-location matching).
2. **Rủi ro thấp:** Human-in-the-loop ở bước 3 đảm bảo không có cuốc nào bị assign sai mà không có confirm từ khách.
3. **Latency chấp nhận được:** 0.5-1s processing time cho Gemini API chấp nhận được cho quy trình này.
4. **Data abundant:** Xanh SM có 500+ cuốc/ngày với GPS + text description, đủ để train/validate.

**💰 Lý do Chi Phí:**
- **ROI dương từ tháng 1:** Tiết kiệm ~16 giờ Dispatcher/ngày (cost: $12/giờ) = **$1,920/tháng** lên lương. Giảm cancel rate 15% = **~$7,500/tháng doanh thu thêm**.
- **API cost:** Gemini 2.5 Flash ~$0.075 per 1M input tokens. 500 cuốc × 1.5 tokens avg = ~$0.05/ngày = **~$1,500/tháng** (negligible so với ROI).
- **Payback period:** ~3-4 tuần.

**⚖️ Lý do Business:**
- **NPS improvement:** Tăng rating khách từ 70% → 90% = giữ lại khách, word-of-mouth marketing tốt hơn.
- **Brand alignment:** Xanh SM positioning là "điều vận thông minh" → MVP này giúp solidify positioning.
- **Competitive advantage:** Grab, Be không có feature này vào thời điểm 2026.

---

## 📋 Tóm tắt Phase 3 & 5:
- ✅ Vẽ chi tiết Current-State Workflow với handoff, bottleneck, thời gian
- ✅ Điền đầy đủ 6-field Problem Statement với metric cụ thể: Giảm gọi lại từ 25% → 5%, thời gian từ 12 min → 4 min
- ✅ Thiết kế Future-State Flow với AI step, Human-in-the-loop, Fallback
- ✅ Chọn LLM Feature fit (không phải Rule/Agent) với lý do chi tiết
- ✅ Quyết định **GO** với justification kỹ thuật + chi phí rõ ràng

