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

## Quy trình làm việc
- Danh sách việc: `docs/BACKLOG.md` (cột "Nhánh" cho tên nhánh đề xuất) và GitHub Issues (BL-xx). Thiết kế: `docs/designs/flash-sale-lab.md`.
- Mỗi task một issue, một nhánh tách từ `main`. Tên nhánh dạng `feat/...`, `fix/...`, `chore/...`, `docs/...`, `test/...`, `ci/...`.
- Không commit thẳng vào `main` (trừ thay đổi tài liệu rất nhỏ). Merge bằng PR, kiểu squash.
- Commit theo kiểu Conventional Commits: `feat: ...`, `fix: ...`, `docs: ...`, `chore: ...`, `test: ...`.
- Một PR chỉ làm một task và không sửa file không liên quan. Ghi `Closes #<số issue>` trong mô tả PR.
- Thay đổi hành vi phải kèm test. Trước khi mở PR: build và test xanh, chạy `/review`, rồi `/ship`.
- Không commit bí mật (`.env`, mật khẩu, khoá API, token). Dùng biến môi trường.
