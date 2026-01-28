---
name: architecture
description: Khung ra quyết định kiến trúc. Phân tích yêu cầu, đánh giá đánh đổi, tài liệu hóa ADR. Sử dụng khi đưa ra các quyết định kiến trúc hoặc phân tích thiết kế hệ thống.
allowed-tools: Read, Glob, Grep
---

# Khung Quyết định Kiến trúc (Architecture Decision Framework)

> "Yêu cầu thúc đẩy kiến trúc. Sự đánh đổi định hình quyết định. ADRs lưu giữ lý do."

## 🎯 Quy tắc Đọc Chọn lọc

**CHỈ ĐỌC các file liên quan đến yêu cầu!** Kiểm tra bản đồ nội dung, tìm thứ bạn cần.

| File | Mô tả | Khi nào đọc |
|------|-------------|--------------|
| `context-discovery.md` | Các câu hỏi cần đặt ra, phân loại dự án | Bắt đầu thiết kế kiến trúc |
| `trade-off-analysis.md` | Mẫu ADR, khung phân tích đánh đổi | Tài liệu hóa quyết định |
| `pattern-selection.md` | Cây quyết định, anti-patterns | Lựa chọn mẫu (patterns) |
| `examples.md` | Ví dụ MVP, SaaS, Doanh nghiệp lớn | Tham chiếu triển khai |
| `patterns-reference.md` | Tra cứu nhanh các mẫu | So sánh các mẫu |

---

## 🔗 Các Kỹ năng Liên quan

| Kỹ năng | Dùng cho |
|-------|---------|
| `@[skills/database-design]` | Thiết kế schema cơ sở dữ liệu |
| `@[skills/api-patterns]` | Các mẫu thiết kế API |
| `@[skills/deployment-procedures]` | Kiến trúc triển khai |

---

## Nguyên tắc Cốt lõi

**"Đơn giản là đỉnh cao của sự tinh tế."**

- Bắt đầu đơn giản
- CHỈ thêm độ phức tạp khi đã chứng minh là cần thiết
- Bạn luôn có thể thêm các mẫu sau này
- Loại bỏ độ phức tạp khó hơn RẤT NHIỀU so với việc thêm vào

---

## Checklist Xác thực

Trước khi chốt kiến trúc:

- [ ] Các yêu cầu đã được hiểu rõ ràng
- [ ] Các ràng buộc đã được xác định
- [ ] Mỗi quyết định đều có phân tích đánh đổi
- [ ] Các phương án thay thế đơn giản hơn đã được xem xét
- [ ] ADRs đã được viết cho các quyết định quan trọng
- [ ] Chuyên môn của đội ngũ phù hợp với các mẫu được chọn
