# TicketHub: tóm tắt dự án

**Là gì:** Web đặt vé sự kiện (concert, hội thảo, phim). Người dùng chọn ghế, thanh toán và nhận vé điện tử có mã QR. Ban tổ chức tạo sự kiện, quản lý vé và xem doanh thu.

**Vì sao chọn:** Đề tài có nhiều bài toán backend thật: chống hai người đặt trùng một ghế, giữ ghế tạm thời, thanh toán, gửi email nền. Giao diện đủ đa dạng (sơ đồ chọn ghế, checkout, dashboard) để luyện lên fullstack.

## Công nghệ
- Backend: Java 25, Spring Boot 4, Spring Security + JWT, JPA
- Dữ liệu: PostgreSQL + Flyway, Redis (cache, giữ ghế), RabbitMQ (tác vụ nền)
- Frontend: Next.js/React + TypeScript, Tailwind, TanStack Query
- Chất lượng và triển khai: JUnit + Testcontainers, Docker, GitHub Actions, deploy lên Render/Railway

## Lộ trình 8 giai đoạn
1. Chuẩn bị: yêu cầu, ERD, wireframe
2. Nền móng backend: CRUD sự kiện, migration, xử lý lỗi
3. Xác thực và phân quyền: JWT, vai trò
4. Nghiệp vụ đặt vé: giữ ghế bằng Redis, khóa lạc quan/bi quan (trọng tâm)
5. Thanh toán sandbox, webhook idempotent, email vé qua queue
6. Hiệu năng và test: cache, index, test tích hợp
7. Frontend: các trang chính, sơ đồ ghế, dashboard
8. DevOps, deploy và README kèm ghi chú quyết định kỹ thuật

## Kết quả mong muốn
Một sản phẩm chạy online, repo gọn gàng, có tài liệu API, và có những câu chuyện kỹ thuật (concurrency, idempotency, cache) để kể khi phỏng vấn.

## Trạng thái hiện tại
Giai đoạn 1 (chuẩn bị). Thư mục mới có Main.java mẫu, chưa có Git và chưa có code dự án.
