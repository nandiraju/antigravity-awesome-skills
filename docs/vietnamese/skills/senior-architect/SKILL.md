---
name: senior-architect
description: Kỹ năng kiến trúc phần mềm toàn diện để thiết kế các hệ thống có khả năng mở rộng, dễ bảo trì sử dụng ReactJS, NextJS, NodeJS, Express, React Native, Swift, Kotlin, Flutter, Postgres, GraphQL, Go, Python. Bao gồm tạo sơ đồ kiến trúc, các mẫu thiết kế hệ thống, khung quyết định về tech stack và phân tích phụ thuộc. Sử dụng khi thiết kế kiến trúc hệ thống, đưa ra các quyết định kỹ thuật, tạo sơ đồ kiến trúc, đánh giá sự đánh đổi hoặc xác định các mẫu tích hợp.
---

# Kiến trúc sư Cao cấp (Senior Architect)

Bộ công cụ hoàn chỉnh cho kiến trúc sư cao cấp với các công cụ hiện đại và thực hành tốt nhất.

## Khởi động Nhanh

### Các Khả năng Chính

Kỹ năng này cung cấp ba khả năng cốt lõi thông qua các script tự động:

```bash
# Script 1: Trình tạo Sơ đồ Kiến trúc
python scripts/architecture_diagram_generator.py [options]

# Script 2: Kiến trúc sư Dự án
python scripts/project_architect.py [options]

# Script 3: Bộ phân tích Phụ thuộc
python scripts/dependency_analyzer.py [options]
```

## Các Khả năng Cốt lõi

### 1. Trình tạo Sơ đồ Kiến trúc (Architecture Diagram Generator)

Công cụ tự động cho các tác vụ tạo sơ đồ kiến trúc.

**Tính năng:**
- Dựng khung (scaffolding) tự động
- Tích hợp sẵn thực hành tốt nhất
- Mẫu có thể cấu hình
- Kiểm tra chất lượng

**Cách dùng:**
```bash
python scripts/architecture_diagram_generator.py <project-path> [options]
```

### 2. Kiến trúc sư Dự án (Project Architect)

Công cụ phân tích và tối ưu hóa toàn diện.

**Tính năng:**
- Phân tích sâu
- Chỉ số hiệu năng
- Đề xuất
- Tự động sửa lỗi

**Cách dùng:**
```bash
python scripts/project_architect.py <target-path> [--verbose]
```

### 3. Bộ phân tích Phụ thuộc (Dependency Analyzer)

Công cụ nâng cao cho các tác vụ chuyên biệt.

**Tính năng:**
- Tự động hóa cấp độ chuyên gia
- Cấu hình tùy chỉnh
- Sẵn sàng tích hợp
- Đầu ra chuẩn production

**Cách dùng:**
```bash
python scripts/dependency_analyzer.py [arguments] [options]
```

## Tài liệu Tham khảo

### Các Mẫu Kiến trúc

Hướng dẫn toàn diện có sẵn tại `references/architecture_patterns.md`:

- Các mẫu và cách thực hành chi tiết
- Ví dụ code
- Thực hành tốt nhất
- Các anti-patterns cần tránh
- Các kịch bản thực tế

### Quy trình Thiết kế Hệ thống

Tài liệu quy trình hoàn chỉnh tại `references/system_design_workflows.md`:

- Quy trình từng bước
- Chiến lược tối ưu hóa
- Tích hợp công cụ
- Tinh chỉnh hiệu năng
- Hướng dẫn khắc phục sự cố

### Hướng dẫn Quyết định Kỹ thuật

Hướng dẫn tham chiếu kỹ thuật tại `references/tech_decision_guide.md`:

- Chi tiết về tech stack
- Ví dụ cấu hình
- Các mẫu tích hợp
- Các cân nhắc về bảo mật
- Hướng dẫn về khả năng mở rộng

## Tech Stack

**Ngôn ngữ:** TypeScript, JavaScript, Python, Go, Swift, Kotlin
**Frontend:** React, Next.js, React Native, Flutter
**Backend:** Node.js, Express, GraphQL, REST APIs
**Cơ sở dữ liệu:** PostgreSQL, Prisma, NeonDB, Supabase
**DevOps:** Docker, Kubernetes, Terraform, GitHub Actions, CircleCI
**Cloud:** AWS, GCP, Azure

## Quy trình Phát triển

### 1. Thiết lập và Cấu hình

```bash
# Cài đặt dependencies
npm install
# hoặc
pip install -r requirements.txt

# Cấu hình môi trường
cp .env.example .env
```

### 2. Chạy Kiểm tra Chất lượng

```bash
# Sử dụng script phân tích
python scripts/project_architect.py .

# Xem xét các đề xuất
# Áp dụng các bản sửa lỗi
```

### 3. Triển khai Thực hành Tốt nhất

Tuân theo các mẫu và thực hành được tài liệu hóa trong:
- `references/architecture_patterns.md`
- `references/system_design_workflows.md`
- `references/tech_decision_guide.md`

## Tóm tắt Thực hành Tốt nhất

### Chất lượng Code
- Tuân theo các mẫu đã được thiết lập
- Viết bài kiểm tra toàn diện
- Tài liệu hóa các quyết định
- Review thường xuyên

### Hiệu năng
- Đo lường trước khi tối ưu hóa
- Sử dụng bộ nhớ đệm (caching) phù hợp
- Tối ưu hóa các đường dẫn quan trọng (critical paths)
- Giám sát trên production

### Bảo mật
- Validate tất cả đầu vào
- Sử dụng parameterized queries
- Triển khai xác thực (authentication) đúng cách
- Giữ các dependencies luôn cập nhật

### Khả năng Bảo trì
- Viết code rõ ràng
- Sử dụng cách đặt tên nhất quán
- Thêm comment hữu ích
- Giữ cho mọi thứ đơn giản

## Các Lệnh Phổ biến

```bash
# Phát triển
npm run dev
npm run build
npm run test
npm run lint

# Phân tích
python scripts/project_architect.py .
python scripts/dependency_analyzer.py --analyze

# Triển khai
docker build -t app:latest .
docker-compose up -d
kubectl apply -f k8s/
```

## Khắc phục Sự cố

### Các Vấn đề Phổ biến

Kiểm tra phần khắc phục sự cố toàn diện trong `references/tech_decision_guide.md`.

### Nhận Trợ giúp

- Xem lại tài liệu tham khảo
- Kiểm tra thông báo đầu ra của script
- Tham khảo tài liệu của tech stack
- Xem lại nhật ký lỗi (error logs)

## Tài nguyên

- Tham chiếu Mẫu: `references/architecture_patterns.md`
- Hướng dẫn Quy trình: `references/system_design_workflows.md`
- Hướng dẫn Kỹ thuật: `references/tech_decision_guide.md`
- Tool Scripts: Thư mục `scripts/`
