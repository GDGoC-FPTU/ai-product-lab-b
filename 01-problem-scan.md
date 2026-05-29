# Phase 1 & 2 — SCAN & QUICK-ASSESS (Báo cáo cá nhân)

**Thực hiện bởi:** Lê Quốc Bảo (2A202600561)  
**Mục tiêu:** Xác định 5+ bài toán vận hành tại Xanh SM (GSM) dùng 4 Lenses, sau đó hoàn thiện 3 Quick Problem Cards chi tiết.

---

## 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Sử dụng **4 Lenses** để quét qua hoạt động vận hành của **Xanh SM (GSM)** — công ty vận tải xe taxi/xe máy điện thông minh thuộc Vingroup.

### 4 Lenses áp dụng:

1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại hằng ngày
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ hiện tại còn chậm/rập khuôn
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck gây phàn nàn khách/nhân viên

### 📝 List bài toán của tôi (Ít nhất 5 bài toán):

| #   | Subsidiary  | Lens               | Mô tả ngắn bài toán                                                                                                                             |
| --- | ----------- | ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Xanh SM** | AI-upgrade         | Tối ưu hóa điểm đón khách dựa trên phân tích tự nhiên từ tin nhắn tài xế và GPS thực tế thay vì chỉ phụ thuộc lựa chọn của khách hàng trên app. |
| 2   | **Xanh SM** | Tốn thời gian      | Điều phối viên xử lý thủ công các phản hồi khẩn cấp từ tài xế về sự cố sạc pin hoặc va chạm (mất 15-20 min/lượt).                               |
| 3   | **Xanh SM** | Lặp lại            | So khớp và phân bổ lại cuốc xe khi khách hàng yêu cầu thay đổi điểm đến giữa chừng chuyến đi.                                                   |
| 4   | **Xanh SM** | Pain từ người khác | Phân tích lý do khách hàng hủy chuyến từ cuộc gọi ghi âm và ghi chú của tài xế để tìm pattern lỗi hệ thống gây mất doanh thu.                   |
| 5   | **Xanh SM** | Lặp lại            | Đối chiếu dữ liệu tiêu thụ điện năng hằng tuần giữa hệ thống quản lý xe và hóa đơn từ các trạm sạc đối tác.                                     |

---

## 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách SCAN: **#1 (Smart Dispatching), #2 (Sự cố sạc pin), #4 (Hủy chuyến)** và hoàn thiện **3 Quick Problem Cards**.

### 📋 QUICK PROBLEM CARD #1 — Tối ưu hóa Điểm Đón (Smart Dispatching)

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Hệ thống điều vận hiện tại chỉ dựa trên vị trí     │
│ khách hàng chọn trên app mà không phân tích ngôn ngữ tự     │
│ nhiên từ tin nhắn tài xế (VD: "tôi ở cạnh hiệu thuốc Việt   │
│ Á, gần cầu thang bộ"). Dẫn đến tài xế phải gọi lại hoặc    │
│ lái vòng vèo, tốn thời gian và chi phí xăng.                │
│                                                             │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│ - Tài xế: Lái vòng vèo, tốn xăng, timeout cuốc              │
│ - Khách hàng: Chờ đợi lâu, trải nghiệm tệ, chi phí cao      │
│ - Dispatcher: Quá tải xử lý cuộc gọi lại                    │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hàng gữ GPS/tin nhắn trên App ────────────┐      │
│   2. Dispatcher gán xe gần nhất dựa vị trí GPS       │      │
│   3. Tài xế lái đến vị trí GPS (có thể sai vị trí)   │      │
│   4. Tài xế gọi/nhắn lại khách để xác nhận chính xác │      │
│                                                     ▼       │
│                                                   Sai vị trí│
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 ( 8-12 phút/lượt)               │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2: AI phân tích text từ tin nhắn, mô tả khách để       │
│ predict vị trí chính xác, sửa GPS của khách trước gán xe    │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ - Giảm tỉ lệ tài xế gọi lại khách: từ 25% ──> dưới 5%       │
│ - Giảm thời gian chờ đợi: từ 12 phút ──> 4 phút             │
│ - Tăng tỉ lệ khách hàng hài lòng: từ 70% ──> 90%            │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Phân tích text GPS)    │
└─────────────────────────────────────────────────────────────┘
```

---

### 📋 QUICK PROBLEM CARD #2 — Xử lý Sự cố Pin/Va chạm

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Tài xế báo hết pin hoặc va chạm giữa đường, cần   │
│ dispatcher xử lý sự cố cứu hộ hoặc tìm trạm sạc gần nhất.   │
│ Hiện tại dispatcher tra cứu thủ công bản đồ và danh sách    │
│ trạm, rất tốn thời gian.                                    │
│                                                             │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau?                                                │
│ - Tài xế: Chờ đợi lâu, stressful                            │
│ - Khách hàng (nếu đang chuyến): Chuyến bị cancel            │
│ - Dispatcher: Quá tải xử lý sự cố                           │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│   1. Tài xế gọi báo hết pin / va chạm                       │
│   2. Dispatcher tra cứu vị trí GPS của xe trên bản đồ       │
│   3. Tra cứu thủ công trạm sạc trống gần nhất (VinFast)    │
│   4. Viết tin nhắn chỉ dẫn đường đi cho tài xế              │
│   5. Gọi cứu hộ nếu pin dưới 5% hoặc va chạm cần cứu        │
│                                                             │
│ Bước nào tốn nhất? Bước 3-4 (⏱ 10-15 phút/lượt)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 3-4: Tự động soạn SMS chỉ dẫn dựa trên GPS và loại    │
│ trạm sạc phù hợp với dòng xe (VF5/VFe34/VF8)               │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ - Giảm thời gian xử lý: từ 15 phút ──> dưới 3 phút          │
│ - Tỉ lệ hướng dẫn chính xác đạt 98%                        │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Soạn SMS tự động)      │
└─────────────────────────────────────────────────────────────┘
```

---

### 📋 QUICK PROBLEM CARD #3 — Phân tích Lý do Hủy chuyến

```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Khách hàng hủy chuyến vì lý do đa dạng (xe muộn,  │
│ giá quá cao, driver không lịch sự, v.v). Hiện tại Xanh SM   │
│ chỉ lưu ghi chú text của tài xế mà không phân loại          │
│ thành pattern, dẫn đến không biết root cause chính.         │
│                                                             │
│ Công ty thành viên: [x] Xanh SM (GSM)                       │
│                                                             │
│ Ai đang đau?                                                │
│ - Ban quản lý: Không biết lý do mất khách, không cải thiện  │
│ - Tài xế: Không nhận feedback cụ thể nào                    │
│ - Khách hàng: Trải nghiệm tệ, không quay lại               │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Khách hủy cuốc, ghi ghi chú text tự do trên app        │
│   2. Tài xế nhận notification hủy (không có chi tiết)       │
│   3. Dispatcher lưu ghi chú vào CRM                         │
│   4. Quản lý export dữ liệu hàng tuần để phân tích thủ công  │
│                                                             │
│ Bước nào tốn nhất? Bước 4 (⏱ 20-30 phút phân tích/tuần)    │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 1-3: Tự động phân loại ghi chú thành 10 category       │
│ (xe muộn, giá cao, driver tệ, sự cố kỹ thuật, v.v)        │
│                                                             │
│ Đo thành công bằng gì?                                      │
│ - Tỉ lệ phân loại chính xác: 90% category đúng              │
│ - Thời gian phân tích từ 30 phút ──> 2 phút (real-time)    │
│ - Tăng tỉ lệ chuyến được giữ lại: từ 75% ──> 85%           │
│                                                             │
│ Quick Architecture: [x] LLM Feature (Phân loại text)        │
└─────────────────────────────────────────────────────────────┘
```

---

## 🗳️ Quyết định lựa chọn bài toán cho Phase 3 Deep-Dive

**Nhóm quyết định chọn:** **Card #1 — Tối ưu hóa Điểm Đón (Smart Dispatching)**

### Lý do lựa chọn:

- **Card #1 (Smart Dispatching):** ✅ Ảnh hưởng trực tiếp đến hiệu suất vận hành real-time, có metric rõ ràng (giảm tỉ lệ gọi lại từ 25% → 5%), AI có thể tạo giá trị cao ngay từ MVP.
- **Card #2 (Sự cố pin):** Mặc dù cũng tốn thời gian nhưng là bài toán phối hợp tích hợp APIs nhiều (GPS, trạm sạc, SMS), phức tạp hơn. Sẽ xem xét ở giai đoạn II.
- **Card #3 (Hủy chuyến):** Đây là tác vụ phân tích offline (back-office), không ảnh hưởng trực tiếp đến revenue real-time. Ưu tiên thấp hơn.

---

## 📊 Tóm tắt Phase 1 & 2:

- ✅ Liệt kê 5+ bài toán Xanh SM sử dụng 4 Lenses (Lặp lại, Tốn thời gian, AI-upgrade, Pain)
- ✅ Hoàn thiện 3 Quick Problem Cards chi tiết với metric cụ thể
- ✅ Chọn bài toán **Smart Dispatching** cho Phase 3 Deep-Dive (ảnh hưởng cao, metric rõ, rủi ro kiểm soát được)
