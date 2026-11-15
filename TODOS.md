# TODOS

## Booking

### Mua nhiều ghế trong một order

**What:** Cho phép một order giữ 2–6 ghế theo kiểu tất cả hoặc không: `RedisSeatGate.tryHoldAll(keys, owner, expiresAt)` bằng Lua, cộng bảng `order_item`.

**Why:** Web bán vé thật thường mua nhiều ghế cạnh nhau. Đây cũng là một câu chuyện phỏng vấn hay về giữ nhiều khóa nguyên tử trong Redis.

**Pros:** Giống sản phẩm thật hơn; thêm một bài Redis/Lua nâng cao.
**Cons:** Đổi API của `RedisSeatGate`, hợp đồng dùng chung duy nhất (eng review D2); thêm migration `order_item`; partial unique index (D17) phải áp dụng cho từng ghế.

**Context:** Bị hoãn ở eng review D20 (2026-11-15). Lý do: giai đoạn Redis đầu tiên chỉ nên có một thứ mới. Bản hiện tại là 1 ghế/order (docs/designs/flash-sale-lab.md, mục "Luồng đặt vé thật"). Bắt đầu từ `RedisSeatGate` và test giữ ghế hai tab.

**Effort:** M
**Priority:** P3
**Depends on:** Giai đoạn 6 (checkout thật) xong.

## Infrastructure

### Chốt công cụ build và thư viện đo độ trễ

**What:** Chọn Gradle (Kotlin DSL) hay Maven, và HdrHistogram hay Micrometer Timer cho p50/p99 của Lab.

**Why:** Bản thiết kế cần một cách đo độ trễ nhất quán (D8 thêm cột "p99 gồm timeout"), và việc khởi tạo repo cần chọn công cụ build.

**Pros:** Bỏ một điểm còn mơ hồ trước khi viết code (minor R2-11).
**Cons:** Không đáng kể.

**Context:** Chọn lúc khởi tạo repo bằng Spring Initializr (Java 25 + Spring Boot 4, eng review D12). HdrHistogram cho phân vị chính xác trên từng lượt; Micrometer tiện nếu muốn đưa ra Actuator.

**Effort:** S
**Priority:** P2
**Depends on:** None

### Cập nhật PROJECT_BRIEF và chốt tên nhánh chính

**What:** Cập nhật docs/PROJECT_BRIEF.md theo lộ trình mới (strategy + test bất biến dời lên giai đoạn 3, Lab MVP ở giai đoạn 4, trạng thái "đã có Git") và chốt `main` hay `master` làm nhánh chính cho CI/deploy.

**Why:** Brief vẫn ghi lộ trình cũ và "chưa có Git"; Distribution Plan ghi "nhánh chính" chung chung (minor R2-12).

**Pros:** Một nguồn sự thật duy nhất cho lộ trình.
**Cons:** Không đáng kể.

**Context:** Lộ trình mới nằm trong docs/designs/flash-sale-lab.md, mục "Lộ trình xếp lại". Repo hiện ở nhánh `master`, chưa có commit.

**Effort:** S
**Priority:** P2
**Depends on:** None

## Completed
