# TicketHub

Web đặt vé sự kiện (concert, hội thảo, phim): chọn ghế, thanh toán, nhận vé điện tử có mã QR. Ban tổ chức tạo sự kiện, quản lý vé, xem doanh thu.
Mô tả đầy đủ và lộ trình 8 giai đoạn: docs/PROJECT_BRIEF.md

## Công nghệ
- Backend: Java 25, Spring Boot 4, Spring Security + JWT, JPA
- Dữ liệu: PostgreSQL + Flyway, Redis (cache, giữ ghế), RabbitMQ (tác vụ nền)
- Frontend: Next.js/React + TypeScript, Tailwind, TanStack Query
- Chất lượng/triển khai: JUnit + Testcontainers, Docker, GitHub Actions, Render/Railway

## gstack
Use /browse from gstack for all web browsing. Never use mcp__claude-in-chrome__* tools.
