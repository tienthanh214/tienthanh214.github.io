---
title: "System Design"
excerpt: "Some little things about System Design"
show_date: true
tags:
  - use-case
categories:
  - 
toc: true
---

## Problem statement

Bắt đầu tuần training về technical đầu tiên ở công ty, mình được giao bài tập đầu tiên về chủ đề System Design. Với yêu cầu như sau:
*Thiết kế  hệ thống cho blog phục vụ lên đến 10k người truy cập*

Dưới góc nhìn của một newbie mới tìm hiểu cấp tốc về chủ đề này, mình xin được chia sẻ những gì đã đọc và học được. Bài viết sẽ còn được cập nhật trong tương lai, cũng như theo sự hiểu biết sâu hơn về chủ đề này cảu mình.

## Analysis

**Những vấn đề với trang web có lượng truy cập lớn**
- Tương tác với hệ thống bị chậm, thời gian tải lâu, thậm chí sập luôn cả hệ thống. Không có tính khả dụng (availability)

**Nguyên nhân**
- Nhiều nguồn truy cập, yêu cầu nhiều tác vụ lên hệ thống như tương tác với giao diện, xử lý logic, truy cấp database, ... mà hệ thống không thể đáp ứng được
 

## Solution

### Horizontal scaling
Tăng thêm thiết bị phần cứng cho hệ thống. Còn gọi là scale-out.

### Vertical scaling
Khác với horizontal scaling, vertical scaling hay còn gọi là scale-up là nâng cấp cho nguồn lực hiện tại, ví dụ như tăng RAM, CPU, thay HDD sang SSD để tăng hiệu năng, .... Phương pháp scale này đơn giản, không cần phải thay đổi kiến trúc website, tuy nhiên tài nguyên luôn có giới hạn nâng cấp nhất định.

### Load balancing
Khi website có quá nhiều truy cập, không thể chỉ sử dụng một server, ta cần thêm nhiều server để đảm bảo tính khả dụng đề phòng khi server gặp sự cố. 

Tuy nhiên, vấn đề là truy vấn từ client sẽ được gửi đến server nào, load balancer sẽ điều phối để đảm bảo lưu lượng truy cập đồng đều, giảm thiểu sự quá tải hoặc nhàn rỗi cho các server, hoặc xử lý khi có sự cố xảy ra trên một server bất kỳ. 

### Cache
Cache giúp tăng tốc độ tải của website, giảm thời gian chờ do truy cập database. 

Bằng cách lưu lại những key/value có thể sẽ truy cập thường xuyên mà không cần phải thực hiện lại truy vấn lên server tốn nhiều thời gian. Một hệ thống cache phổ biến và hiệu quả ngày nay là Redis.

### Database replication
Đối với website thường xuyên có nhiều truy cập, nếu chỉ sử dụng một database duy nhất, khi có sự cố xảy ra như mất mát dữ liệu, hỏng cả database, dữ liệu sẽ không thể hồi phục, và website cũng sẽ bị sập.

Để giải quyết, duy trì các bản sao database trên nhiều server khác nhau. 

Có một số phương pháp database replication như Master-slave replication, Master-master replication, .... Ví dụ về Master-slave replication, tất cả các truy vấn sẽ đều thực hiện ở database Master, các database Slave chỉ sao chép lại dữ liệu từ Master, hiệu quả với website blog yêu cầu truy vấn READ nhiều hơn WRITE.

### Content Delivery Network
Là mạng lưới gôm nhiều server đặt tại nhiều vị trí địa lý khác nhau, cùng làm công việc phân phối nội dung. Tương tự như cache nhưng CDN mang tính khả dụng về mặt địa lý. Giúp cho người dùng truy cập nhanh hơn vào dữ liệu server gần nhất thay vì phải truy cập vào server trung tâm.

## References
[System Design Primer](https://github.com/donnemartin/system-design-primer)
             
              
