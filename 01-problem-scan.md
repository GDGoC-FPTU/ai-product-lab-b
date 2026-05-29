# Lab 02 — 01-Problem-Scan (Cá nhân)

## Phase 1 — SCAN

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | Xanh SM | Tốn thời gian | Điều phối viên phải đọc tin nhắn tài xế, tra GPS và soạn hướng dẫn trạm sạc thủ công, tốn 10-15 phút/lượt. |
| 2 | VinFast | Lặp lại | Đối chiếu hóa đơn sạc điện đối tác với log trạm sạc hàng tuần, nhiều dòng dữ liệu và sai sót. |
| 3 | Vinhomes | AI-upgrade | Phân loại phản ánh cư dân (mất nước, ồn ào, hỏng đèn) và route tới ban quản lý, hiện tại phân loại chậm và sai. |
| 4 | Vinpearl | Pain từ người khác | Tổng hợp review khách sạn từ nhiều nền tảng, lọc phàn nàn khẩn cấp gửi Manager. |
| 5 | Vinmec | Tốn thời gian | Bác sĩ tốn 20-30 phút để tóm tắt bệnh án xuất viện từ nhiều nguồn thông tin. |
| 6 | Xanh SM | Stakeholder Pain | Khách hủy chuyến, điều phối viên phải đọc ghi chú/ghi âm để phân loại lý do và cải thiện hệ thống. |

---

## Phase 2 — QUICK-ASSESS (Top 3 Quick Problem Cards)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Hướng dẫn tài xế đến trạm sạc phù hợp trong giờ   │
│ cao điểm để giảm thời gian chờ đợi.                         │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)? Điều phối viên và tài xế               │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tài xế báo pin thấp qua tổng đài                        │
│   2. Điều phối viên tra GPS xe trên bản đồ                  │
│   3. Tra cứu trạm sạc còn chỗ trống và loại cổng sạc        │
│   4. Soạn tin nhắn hướng dẫn đường đi gửi tài xế            │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (10 phút/lượt)     │
│ AI có thể nhảy vào bước nào? Tự động gợi ý trạm sạc + draft │
│ tin nhắn hướng dẫn                                          │
│                                                             │
│ Metric có số? Giảm thời gian xử lý từ 12 phút -> dưới 3 phút│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tự động phân loại và chuyển tiếp phản ánh cư dân  │
│ đến đúng bộ phận vận hành.                                  │
│ Công ty thành viên: [x] Vinhomes                            │
│                                                             │
│ Ai đang đau (Actor)? CSKH tòa nhà, Ban quản lý              │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Cư dân gửi phản ánh trên app                            │
│   2. CSKH đọc nội dung và gán nhãn thủ công                 │
│   3. Chuyển về bộ phận kỹ thuật/vệ sinh/an ninh             │
│   4. Theo dõi và cập nhật trạng thái phản hồi               │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2 (8 phút/lượt)        │
│ AI có thể nhảy vào bước nào? Tự động phân loại + route       │
│                                                             │
│ Metric có số? 85% phản ánh được phân loại đúng trong < 30s   │
│                                                             │
│ Quick Architecture: [ ] No AI  [x] Rule  [ ] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Tóm tắt bệnh án xuất viện từ nhiều nguồn dữ liệu   │
│ để bác sĩ duyệt nhanh.                                      │
│ Công ty thành viên: [x] Vinmec                              │
│                                                             │
│ Ai đang đau (Actor)? Bác sĩ điều trị                        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Bác sĩ mở bệnh án điện tử và đọc kết quả XN             │
│   2. Tổng hợp triệu chứng, chẩn đoán, thuốc                  │
│   3. Soạn bản tóm tắt xuất viện                              │
│   4. Kiểm tra lại và ký duyệt                                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 2-3 (20-30 phút/ca)     │
│ AI có thể nhảy vào bước nào? Tự động rút trích + draft tóm tắt│
│                                                             │
│ Metric có số? Giảm thời gian soạn từ 25 phút -> dưới 8 phút  │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```
