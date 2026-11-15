# TicketHub: backlog

Nguồn: `docs/designs/flash-sale-lab.md` (13 task T1–T13 từ eng review, lộ trình 8 giai đoạn, mục "Luồng đặt vé thật"), `TODOS.md`, và các task còn thiếu do mình bổ sung (đánh dấu **mới**).
Các task **mới** là bản nháp suy ra từ lộ trình trong doc, hãy đọc lại và chỉnh trước khi tạo issue.

Quy ước: mỗi task một nhánh từ `main`, merge bằng PR (squash). Ưu tiên P1 > P2 > P3. Cột "Nguồn": `T#` là task trong doc, `TODOS` là `TODOS.md`, `mới` là bổ sung.

## Giai đoạn 1: Chuẩn bị

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-01 | Commit tài liệu thiết kế, đổi `master` thành `main`, tạo repo GitHub và push. Kiểm tra `.gstack/` có cần ignore không trước khi commit | `chore/repo-setup` | P1 | — | mới |
| BL-02 | Quy trình repo: mẫu PR, nhãn P1/P2/P3, quy ước nhánh và commit, ghi quy tắc vào `CLAUDE.md` | `chore/workflow` | P1 | BL-01 | mới |
| BL-03 | Chốt Gradle (Kotlin DSL) hay Maven, và HdrHistogram hay Micrometer cho p50/p99 | `chore/build-tool-decision` | P2 | — | TODOS |
| BL-04 | Vẽ ERD giai đoạn đầu: `event`, `venue_seat`, `ticket`, `order`, schema `lab` | `docs/erd-phase1` | P1 | BL-01 | mới ("Next Steps" #2 của doc) |
| BL-05 | Cập nhật `PROJECT_BRIEF.md` theo lộ trình mới và chốt tên nhánh chính | `docs/update-brief` | P2 | — | TODOS |

## Giai đoạn 2: Nền móng

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-06 | Khởi tạo repo Java 25 + Spring Boot 4, khoá `pgjdbc ≥ 42.6.0`, xoá `Main.java`/`Main.class`, tạo `.gitignore`. Xong khi: ứng dụng khởi động, `java -version` = 25 | `feat/t1-init-repo` | P1 | BL-01, BL-03 | T1 |
| BL-07 | Docker Compose chạy Postgres và Redis cho môi trường local. Xong khi: một lệnh lên đủ hai dịch vụ | `chore/compose-local` | P1 | BL-06 | mới |
| BL-08 | Flyway: migration nền cho schema `public` và `lab` theo ERD. Xong khi: migrate sạch trên DB trống | `feat/db-baseline-migration` | P1 | BL-04, BL-06, BL-07 | mới |
| BL-09 | CRUD sự kiện và sơ đồ ghế, lỗi theo RFC 7807, Testcontainers Postgres. Xong khi: test tích hợp xanh | `feat/event-crud` | P1 | BL-08 | mới |
| BL-10 | GitHub Actions: build và test cho mỗi PR. Xong khi: PR hiện kết quả CI | `ci/github-actions` | P1 | BL-06 | mới |

## Giai đoạn 3: Chiến lược và test bất biến

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-11 | Hai pool Hikari và role `tickethub_lab` với timeout mức role | `feat/t2-lab-pools` | P1 | BL-08 | T2 |
| BL-12 | 5 chiến lược × 2 kịch bản và test bất biến (naive phải tái hiện bán vượt) | `feat/t3-lab-strategies` | P1 | BL-11 | T3 |
| BL-13 | Test JFR chống virtual thread bị pin trong CI | `test/t8-jfr-pinning` | P2 | BL-12, BL-10 | T8 |

## Giai đoạn 4: Redis, Lab MVP, deploy lần đầu

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-14 | `RedisSeatGate` với mốc hết hạn tuyệt đối và partial unique index | `feat/t5-redis-seat-gate` | P1 | BL-08 | T5 |
| BL-15 | Vòng đời một lượt chạy Lab: khoá, cờ dừng, ABORTED, dọn key | `feat/t6-lab-run-lifecycle` | P1 | BL-12, BL-14 | T6 |
| BL-16 | Endpoint polling `?since=version` và cột p99 gồm timeout | `feat/t7-lab-polling` | P2 | BL-15 | T7 |
| BL-17 | Ma trận đo pool 10/20/40 × số bot, chỉ số "chờ pool", viết lại bảng kỳ vọng | `feat/t4-pool-matrix` | P1 | BL-15 | T4 |
| BL-18 | Trang Lab theo wireframe và 3 test Playwright | `feat/t9-lab-page` | P2 | BL-16 | T9 |
| BL-19 | Bảng hosting, gọi thẳng backend, kiểm tra header IP thật | `chore/t11-hosting-ip-check` | P2 | BL-16 | T11 |
| BL-20 | Deploy lần đầu (backend, frontend, Lab). Xong khi: URL công khai chạy được lượt Lab | `chore/first-deploy` | P2 | BL-18, BL-19 | mới |

## Giai đoạn 5: Xác thực

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-21 | Auth: JWT, vai trò USER và ORGANIZER, migration `user/role`. Xong khi: endpoint tổ chức sự kiện chỉ ORGANIZER gọi được | `feat/auth` | P1 | BL-09 | mới |

## Giai đoạn 6: Checkout thật

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-22 | Giữ ghế thật: `order` HOLD, dùng `RedisSeatGate`, job xử lý hết hạn | `feat/booking-hold` | P1 | BL-14, BL-21 | mới |
| BL-23 | Authorize rồi capture, trạng thái AUTHORIZED/EXPIRED | `feat/t13-authorize-capture` | P1 | BL-22 | T13 |
| BL-24 | Xác thực chữ ký webhook, đối chiếu tiền, idempotent theo `processed_webhook` | `feat/t12-webhook-verify` | P1 | BL-23 | T12 |
| BL-25 | Bù trừ: trạng thái `REFUND_REQUIRED` và job hoàn tiền (outbox) | `feat/refund-job` | P1 | BL-24 | mới |
| BL-26 | Email vé có mã QR qua RabbitMQ | `feat/ticket-email-qr` | P2 | BL-24 | mới |

## Giai đoạn 7: Frontend đầy đủ và hiệu năng

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-27 | Sơ đồ chọn ghế, checkout, dashboard doanh thu cho ban tổ chức | `feat/frontend-booking` | P2 | BL-21, BL-22 | mới |
| BL-28 | Cache Redis cho trang sự kiện và index DB | `feat/cache-and-indexes` | P2 | BL-09 | mới |

## Giai đoạn 8: DevOps và kể chuyện

| ID | Việc | Nhánh | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|---|
| BL-29 | `docker compose up` một lệnh và GIF ở đầu README | `chore/t10-compose-gif` | P2 | BL-18 | T10 |
| BL-30 | CI xuất bảng benchmark vào README, ADR cho từng quyết định khoá, README hoàn chỉnh | `docs/adr-readme` | P2 | BL-17, BL-24 | mới |
| BL-31 | Deploy production | `chore/deploy-prod` | P2 | BL-27, BL-30 | mới |

## Hoãn lại

| ID | Việc | Ưu tiên | Phụ thuộc | Nguồn |
|---|---|---|---|---|
| BL-32 | Mua nhiều ghế trong một order (`tryHoldAll` bằng Lua, bảng `order_item`) | P3 | BL-25 | TODOS |

## Thứ tự làm đề xuất cho một người

BL-01 → BL-02 → BL-03 → BL-04 → BL-06 → BL-07 → BL-08 → BL-10 → BL-09 → BL-11 → BL-12 → BL-14 → BL-15 → BL-16. Các task còn lại đi theo cột "Phụ thuộc".
