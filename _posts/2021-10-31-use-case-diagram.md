---
title: "Note: Use case diagram"
excerpt: "something about use-case"
show_date: true
tags:
  - use-case
categories:
  - UML
toc: true
---

# Tài liệu

- https://thinhnotes.com/chuyen-nghe-ba/use-case-diagram-va-5-sai-lam-thuong-gap/

# Use-case diagram

Nên vẽ sao cho khách hàng nhìn dễ hiểu nhất có thể. Các use-case không được chung chung, phải cụ thể

## Thành phần

1. Actor
    Đặt tên bằng danh từ

2. Use-case
    Tên rõ ràng, rành mạch: Verb + Noun

3. Relationship

4. System Boundary

## Relationship

### Include

Thể hiện quan hệ bắt buộc phải có

Ký hiệu: nét đứt và << include >> trên đường nối

        A --------> B (A include B)


Use case A include use case B, C, ... ý nghĩa là để xảy ra A thì trước đó các use case B, C, ... phải đạt được 

Ví dụ: Để post bài trên facebook (A) thì cần đăng nhập (B) và soạn thảo nội dung (C). 

Chỉ nên tách use-case nhỏ ra bằng include nếu nó quá phức tạp và những use-case tách ra đó có thể được sử dụng ở các Use-case khác ở sau này.


### Extend

Thể hiện mối quan hệ mở rộng (không bắt buộc).

Ký hiệu: nét đứt và << extend >>, ngoài ra còn có một note (optional) cho biết điều kiện xảy ra gọi là Extension point

Ví dụ: Người dùng muốn xem hướng dẫn sử dụng app ở màn hình chính thì bấm vào button help, vậy điều kiện là bấm vào button help, xảy ra khi người dùng muốn xem hướng dẫn. (Màn hình chính) <--- << extend >> ----- (Hướng dẫn sử dụng)

### Generalization

Thể hiện quan hệ cha con giữa các use-case hoặc actor với nhau

Ký hiệu: đường liền mũi tên tam giác trắng

    Old Customer -ᐅ Customer

Ví dụ: người dùng sử dụng app đặt hàng, có thể đặt qua phone hoặc web, chúng đều là con của đặt hàng.
             
              
