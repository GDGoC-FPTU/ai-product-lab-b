# Lab 02 — Problem Scan (Cá nhân)

**Mảng tôi chọn:** Xanh SM (GSM)

---

# 🔍 Phase 1 — SCAN (Cá nhân)

Hãy sử dụng 4 Lenses dưới đây để quét qua hoạt động vận hành của Xanh SM và các công ty thành viên liên quan. Tôi chọn tập trung vào các pain point có thể đo được bằng thời gian xử lý, tỷ lệ lỗi, hoặc SLA vận hành.

### 4 Lenses tôi ưu tiên khi quét bài toán
1. **Lặp lại (Repetitive):** Những tác vụ dispatch/đối soát/lập báo cáo diễn ra nhiều lần mỗi ngày.
2. **Tốn thời gian (Time-consuming):** Những bước điều phối thủ công khiến tổng thời gian xử lý tăng mạnh.
3. **AI-upgrade:** Những tác vụ CSKH hoặc tóm tắt thông tin có thể tốt hơn nếu có AI hỗ trợ.
4. **Stakeholder Pain:** Những vấn đề làm tài xế, điều phối viên, hoặc khách hàng phàn nàn trực tiếp.

### 📝 List bài toán của tôi
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Xanh SM | Lặp lại | Điều phối viên phải ghép lại cuốc xe khi khách đổi điểm đón/điểm đến, thao tác lặp đi lặp lại trên dashboard điều vận. |
| 2 | Xanh SM | Tốn thời gian | Xử lý thủ công các báo cáo sự cố pin yếu hoặc xe hỏng giữa đường từ tài xế, phải tra GPS và liên hệ cứu hộ. |
| 3 | Xanh SM | AI-upgrade | Tóm tắt nội dung cuộc gọi/tin nhắn của tài xế để phân loại lý do hủy chuyến hoặc chậm nhận cuốc. |
| 4 | Xanh SM | Stakeholder Pain | Gợi ý điểm đón khách chưa chính xác làm tài xế mất thời gian tìm khách và khách phải chờ lâu. |
| 5 | Xanh SM | Tốn thời gian | Đối soát thủ công các khiếu nại về cước phí và hoàn tiền sau chuyến, cần đọc log và so sánh nhiều nguồn dữ liệu. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân)

Tôi chọn 3 bài toán tiềm năng nhất từ danh sách trên để đánh giá nhanh: **#2 (Sự cố pin yếu/xe hỏng giữa đường), #4 (Gợi ý điểm đón không chính xác), #5 (Đối soát khiếu nại cước phí).**

## QUICK PROBLEM CARD #1

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán (1 câu): Xử lý sự cố pin yếu hoặc xe hỏng giữa     │
│ đường của tài xế Xanh SM để điều phối cứu hộ hoặc trạm sạc. │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau (Actor)? Điều phối viên và tài xế               │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Tài xế gọi tổng đài báo sự cố                           │
│   -> 2. Điều phối viên tra cứu vị trí xe trên bản đồ        │
│   -> 3. Tra cứu trạm sạc/cứu hộ phù hợp                      │
│   -> 4. Soạn hướng dẫn và gửi cho tài xế                    │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3 (⏱ 5-7 phút/lượt)   │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3 và 4           │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian xử lý sự cố từ 15 phút xuống dưới 3 phút.    │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## QUICK PROBLEM CARD #2

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán (1 câu): Gợi ý lại điểm đón khách khi tài xế không │
│ tìm thấy khách hoặc điểm đón ban đầu quá khó tiếp cận.      │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau (Actor)? Tài xế và khách hàng                   │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Khách tạo cuốc trên app                                │
│   -> 2. Tài xế di chuyển đến điểm đón                       │
│   -> 3. Tài xế không tìm thấy khách / điểm đón sai          │
│   -> 4. Gọi điện hoặc chat qua app để đổi vị trí            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (⏱ 4-6 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm tỷ lệ cuốc phải gọi lại do điểm đón sai từ 18% xuống   │
│ dưới 8%.                                                     │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

## QUICK PROBLEM CARD #3

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán (1 câu): Đối soát và phản hồi nhanh các khiếu nại  │
│ về cước phí/hoàn tiền sau chuyến của khách Xanh SM.         │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau (Actor)? Nhân viên CSKH và bộ phận đối soát     │
│                                                             │
│ Workflow thủ công hiện tại (3-5 bước):                      │
│   1. Nhận khiếu nại từ khách                                │
│   -> 2. Mở lịch sử chuyến và log thanh toán                 │
│   -> 3. So khớp chính sách cước với từng trường hợp         │
│   -> 4. Soạn phản hồi hoặc đề xuất hoàn tiền                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (⏱ 8-10 phút/lượt)│
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 3-4              │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian xử lý mỗi khiếu nại từ 12 phút xuống dưới 4  │
│ phút, đồng thời giữ tỷ lệ phản hồi đúng chính sách trên 95%.│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

---

# Ghi chú ngắn

Tôi ưu tiên Xanh SM vì các quy trình điều vận và CSKH ở đây có tần suất cao, ranh giới vận hành rõ, và dễ đo hiệu quả bằng thời gian xử lý/lượt cũng như tỷ lệ lỗi.