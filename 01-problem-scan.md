# Lab 02 — 01-Problem-Scan (Cá nhân)

## Phase 1 — SCAN

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | Xanh SM | Tốn thời gian | Điều phối viên xử lý sự cố pin/va chạm, phải tra GPS và tìm trạm sạc thủ công, mất 10-15 phút/lượt. |
| 2 | Xanh SM | Lặp lại | Phân bổ lại cuốc xe khi khách đổi điểm đến giữa chuyến, thao tác lặp lại nhiều lần mỗi ngày. |
| 3 | Xanh SM | AI-upgrade | Tối ưu điểm đón dựa trên mô tả văn bản của tài xế/khách (ví dụ “cạnh hiệu thuốc”), giảm sai vị trí GPS. |
| 4 | Xanh SM | Stakeholder Pain | Khách hủy chuyến, cần phân loại lý do từ ghi chú/ghi âm để giảm rò rỉ doanh thu. |
| 5 | Xanh SM | Lặp lại | Đối chiếu dữ liệu sạc điện hằng tuần giữa hệ thống xe và hóa đơn trạm sạc đối tác. |

---

## Phase 2 — QUICK-ASSESS (Top 3 Quick Problem Cards)
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Xử lý sự cố pin/va chạm của tài xế nhanh hơn bằng │
│ cách tự động gợi ý trạm sạc phù hợp.                         │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)? Điều phối viên và tài xế               │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế gọi báo hết pin/va chạm                          │
│   2. Điều phối viên tra GPS xe trên bản đồ                  │
│   3. Tra cứu trạm sạc trống + loại cổng sạc                  │
│   4. Soạn tin nhắn hướng dẫn đường đi gửi tài xế            │
│   5. Gọi cứu hộ nếu pin quá thấp                             │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (10-15 phút/lượt)  │
│ AI có thể nhảy vào bước nào? Tự động gợi ý trạm sạc + draft │
│ tin nhắn hướng dẫn                                          │
│                                                             │
│ Metric có số? Giảm thời gian xử lý từ 15 phút -> dưới 3 phút│
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tối ưu điểm đón khách từ mô tả văn bản và GPS để  │
│ giảm sai vị trí và gọi lại.                                 │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)? Tài xế, khách hàng, điều phối viên     │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách gửi vị trí/GPS và mô tả qua app                  │
│   2. Điều phối viên gán xe dựa trên GPS                     │
│   3. Tài xế đến vị trí, đôi khi sai điểm đón                │
│   4. Tài xế gọi lại khách để xác nhận                        │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (8-12 phút/lượt)   │
│ AI có thể nhảy vào bước nào? Phân tích mô tả + sửa điểm đón │
│                                                             │
│ Metric có số? Giảm tỉ lệ gọi lại từ 25% -> dưới 5%           │
│ và giảm thời gian chờ từ 12 phút -> dưới 4 phút              │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Phân loại lý do hủy chuyến để giảm rò rỉ doanh thu │
│ và tối ưu quy trình vận hành.                               │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)? Quản lý vận hành, điều phối viên        │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hủy chuyến, để lại ghi chú tự do                  │
│   2. Điều phối viên lưu ghi chú vào CRM                      │
│   3. Quản lý export dữ liệu theo tuần                        │
│   4. Phân tích thủ công để tìm pattern                       │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3-4 (20-30 phút/tuần)   │
│ AI có thể nhảy vào bước nào? Tự động phân loại lý do hủy     │
│                                                             │
│ Metric có số? 90% phân loại đúng, phân tích từ 30 -> 2 phút  │
│ và tăng tỉ lệ chuyến giữ lại từ 75% -> 85%                   │
│                                                             │
│ Quick Architecture: [ ] No AI  [ ] Rule  [x] LLM  [ ] Agent │
└─────────────────────────────────────────────────────────────┘
```

