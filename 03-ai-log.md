# 03-ai-log.md — AI Log & Reflection

## AI giúp gì

Trong buổi học này, tôi dùng AI như một người đồng hành để brainstorm ý tưởng bài toán cho Xanh SM và kiểm tra xem một ý tưởng có đủ thực tế để đem đi làm tiếp hay không. Phần hữu ích nhất là khi tôi hỏi AI gợi ý các pain point vận hành có thể đo bằng thời gian xử lý, tỷ lệ lỗi hoặc SLA. Nhờ vậy tôi nhìn ra rõ hơn những việc lặp đi lặp lại như điều phối cuốc xe, xử lý sự cố giữa đường, gợi ý lại điểm đón và đối soát khiếu nại cước phí.

Tôi cũng dùng AI để phản biện lại chính các thẻ bài toán mình viết. Khi đưa prompt kiểu “đóng vai CFO và trưởng phòng vận hành”, AI giúp tôi nhìn ra chỗ nào còn quá chung chung, chỗ nào metric chưa đủ số, và chỗ nào đang cố dùng AI cho một việc mà rule-based có thể làm tốt hơn. Cách đó khiến tôi bớt bị cuốn theo ý tưởng và quay lại nhìn bài toán theo góc độ vận hành thật.

## AI sai gì

Tuy vậy, AI không phải lúc nào cũng đúng. Có lúc nó trả lời khá tự tin nhưng lại suy diễn quá rộng, ví dụ giả định rằng một quy trình CSKH nào đó chắc chắn cần LLM, trong khi thực tế chỉ cần rule hoặc form chuẩn hóa là đủ. Một số gợi ý ban đầu cũng hơi chung chung, thiếu ranh giới vận hành nên nếu làm theo ngay thì sẽ dễ biến thành một giải pháp phức tạp hơn mức cần thiết.

## Sửa đổi ra sao

Để sửa điều đó, tôi đã siết lại prompt bằng cách yêu cầu AI chỉ trả về các bài toán có đầu ra đo được, thêm ranh giới rõ ràng về việc AI được phép làm gì và không được phép làm gì, rồi yêu cầu nêu luôn fallback nếu AI không đủ tự tin. Khi cần kiểm tra tính khả thi, tôi cũng ép AI so sánh giữa No AI, Rule, LLM và Agent thay vì mặc định chọn LLM. Nhờ vậy kết quả thực tế hơn và dễ dùng hơn cho bài lab.

Nếu nhìn lại, AI giúp tôi đi nhanh hơn ở bước khám phá và phản biện ý tưởng, nhưng quyết định cuối cùng vẫn phải do tôi tự kiểm tra bằng logic vận hành. Phần quan trọng nhất của buổi học là hiểu rằng AI chỉ thật sự hữu ích khi mình đặt đúng câu hỏi, đặt đúng ranh giới, và chấp nhận loại bỏ những ý tưởng nghe hay nhưng không đủ chắc để triển khai.