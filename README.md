# mini-project

Monorepo gồm frontend Next.js (`mini-project`) và backend Express (`mini-project-be`). Mỗi phần có `docker-compose.yml` riêng; chạy cả hai bằng lệnh `docker compose up --build` trong từng thư mục.

## Yêu cầu

Docker và Docker Compose đã cài trên máy.

## Chuẩn bị biến môi trường

**Backend** (`mini-project-be/.env`): tạo file `.env` trong thư mục `mini-project-be` với các biến mà ứng dụng cần (ví dụ `PORT`, thông tin kết nối database hoặc Supabase). Không commit file này lên Git.

**Frontend** (`mini-project/.env`): tạo file `.env` trong thư mục `mini-project` với tối thiểu:

- `NEXT_PUBLIC_BASE_URL`: URL API backend, phải có đuôi `/api` (ví dụ khi chạy backend trong Docker mặc định là `http://localhost:3002/api`).
- `POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`: dùng cho service Postgres trong compose của frontend.

Compose sẽ đọc `.env` cùng thư mục để truyền biến vào container và vào bước build Next.js.

## Chạy bằng Docker Compose

Chạy backend trước (frontend cần gọi API qua cổng backend).

1. Mở terminal, vào thư mục backend:

   `cd mini-project-be`

   Chạy:

   `docker compose up --build`

   Backend lắng nghe cổng **3002** (theo cấu hình mặc định trong project).

2. Mở terminal thứ hai, vào thư mục frontend:

   `cd mini-project`

   Chạy:

   `docker compose up --build`

   Frontend: **http://localhost:4000**  
   Postgres (từ compose frontend): cổng host **5433** (map vào 5432 trong container).

Dừng: trong mỗi terminal nhấn `Ctrl+C`, hoặc chạy `docker compose down` trong từng thư mục tương ứng.

## Ghi chú

Nếu build frontend báo thiếu `NEXT_PUBLIC_BASE_URL`, kiểm tra `mini-project/.env` rồi chạy lại `docker compose up --build`.
