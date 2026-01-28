---
name: lint-and-validate
description: "Quy trình kiểm soát chất lượng tự động, linting và phân tích tĩnh. Sử dụng sau mỗi lần sửa đổi code để đảm bảo tính đúng đắn của cú pháp và các tiêu chuẩn dự án. Kích hoạt với từ khóa: lint, format, check, validate, types, static analysis."
allowed-tools: Read, Glob, Grep, Bash
---

# Kỹ năng Kiểm tra lỗi và Xác thực (Lint and Validate)

> **BẮT BUỘC:** Chạy các công cụ xác thực phù hợp sau MỖI lần thay đổi code. Không được hoàn thành tác vụ cho đến khi code không còn lỗi.

### Quy trình theo Hệ sinh thái

#### Node.js / TypeScript
1. **Lint/Sửa lỗi:** `npm run lint` hoặc `npx eslint "đường_dẫn" --fix`
2. **Kiểu dữ liệu (Types):** `npx tsc --noEmit`
3. **Bảo mật:** `npm audit --audit-level=high`

#### Python
1. **Linter (Ruff):** `ruff check "đường_dẫn" --fix` (Nhanh & Hiện đại)
2. **Bảo mật (Bandit):** `bandit -r "đường_dẫn" -ll`
3. **Kiểu dữ liệu (MyPy):** `mypy "đường_dẫn"`

## Vòng lặp Chất lượng
1. **Viết/Sửa Code**
2. **Chạy Kiểm tra (Audit):** `npm run lint && npx tsc --noEmit`
3. **Phân tích Báo cáo:** Kiểm tra phần "BÁO CÁO KIỂM TRA CUỐI CÙNG" (FINAL AUDIT REPORT).
4. **Sửa & Lặp lại:** Việc gửi code có lỗi trong "KIỂM TRA CUỐI CÙNG" là KHÔNG được phép.

## Xử lý Lỗi
- Nếu `lint` thất bại: Sửa ngay các lỗi về phong cách (style) hoặc cú pháp.
- Nếu `tsc` thất bại: Sửa các lỗi không khớp kiểu dữ liệu trước khi tiếp tục.
- Nếu không có công cụ nào được cấu hình: Kiểm tra thư mục gốc dự án xem có `.eslintrc`, `tsconfig.json`, `pyproject.toml` không và đề xuất tạo mới.

---
**Quy tắc Nghiêm ngặt:** Không được commit hoặc báo cáo code là "hoàn thành" nếu chưa vượt qua các kiểm tra này.

---

## Scripts

| Script | Mục đích | Lệnh |
|--------|---------|---------|
| `scripts/lint_runner.py` | Kiểm tra lint hợp nhất | `python scripts/lint_runner.py <project_path>` |
| `scripts/type_coverage.py` | Phân tích độ bao phủ kiểu dữ liệu | `python scripts/type_coverage.py <project_path>` |
