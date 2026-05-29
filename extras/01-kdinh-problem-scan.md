# Phase 1 & 2 — SCAN & QUICK-ASSESS (Báo cáo cá nhân)

**Thực hiện bởi:** Nhan Khánh Đình (2A202600673)  
**Mục tiêu:** Xác định 5 bài toán có thể vận hành tại Xanh SM (GSM) dùng 4 Lenses, sau đó hoàn thiện 3 Quick Problem Cards.

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:

1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

### 📝 List bài toán của tôi:

| #   | Subsidiary | Lens             | Mô tả ngắn bài toán                                                                                                                                |
| :-- | :--------- | :--------------- | :------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | Xanh SM    | Stakeholder Pain | Tài xế tự tìm trạm sạc thủ công gây kẹt trạm V-Green giờ cao điểm; khách hàng phàn nàn vì khó gọi xe.                                              |
| 2   | Xanh SM    | Repetitive       | Đội Ops dùng Rule-based và rà soát Excel/Log thủ công lặp đi lặp lại hàng ngày để bắt gian lận GPS, trục lợi khuyến mãi.                           |
| 3   | Xanh SM    | Time-consuming   | CS Agent phải đọc từng ticket (quên đồ, thái độ tài xế), phân loại và tra cứu hành trình thủ công để xử lý.                                        |
| 4   | Xanh SM    | AI-upgrade       | Hiện tại bảo dưỡng cứng nhắc theo số km hoặc đợi xe hỏng (đặc biệt hệ thống tản nhiệt pin), trong khi AI có thể dự báo trước sự cố qua Telematics. |
| 5   | Xanh SM    | Stakeholder Pain | Chỉ trích xuất camera/dữ liệu khi có khách phàn nàn hoặc tai nạn; thiếu giám sát chủ động khiến tài xế lái ẩu, phanh gấp.                          |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Điều phối trạm sạc V-Green thông minh để  │
│ giảm ùn tắc và tối ưu thời gian chờ của tài xế.             │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Tài xế Xanh SM                         │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Xe hết pin ──> 2. Tài xế tự tìm trạm gần nhất ──> 3.   │
│   Đến trạm thấy đông ──> 4. Chờ đợi hoặc tìm trạm khác      │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 & 4 (30-60 phút)    │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 (Gợi ý trạm)   │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian chờ sạc│
│ trung bình của tài xế 30%.                                  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [ ] LLM  [x] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Tự động phát hiện gian lận GPS và trục lợi│
│ khuyến mãi từ dữ liệu hành trình của tài xế.                │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Đội ngũ Vận hành (Ops Team)            │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Xuất log hành trình ──> 2. Rà soát bằng Excel/Rule ──> │
│   3. Xác minh thủ công ──> 4. Ra quyết định xử phạt         │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 ( 20 phút/ca)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 (Phát hiện)    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Phát hiện 95% các     │
│ trường hợp gian lận tinh vi trong dưới 5 phút.              │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Phân loại và xử lý ticket hỗ trợ (quên đồ,│
│ thái độ tài xế) tự động để tăng tốc độ phản hồi khách hàng. │
│ Công ty thành viên: [ ] VinFast  [x] Xanh SM  [ ] Vinhomes  │
│                     [ ] Vinmec   [ ] Khác (Ghi rõ)________  │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH (CS Agent)              │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận ticket ──> 2. Đọc nội dung ──> 3. Phân loại & Tra │
│   cứu thông tin ──> 4. Draft câu trả lời                    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 & 3 (10 phút/tkt)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2, 3 & 4         │
│                                                             │
│ Đo thành công bằng gì (Metric có số)? Giảm thời gian xử lý  │
│ ticket từ 15 phút ──> dưới 3 phút.                          │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```
