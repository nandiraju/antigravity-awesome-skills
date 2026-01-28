---
name: concise-planning
description: Sử dụng khi người dùng yêu cầu lập kế hoạch cho một tác vụ lập trình, nhằm tạo ra một danh sách kiểm tra (checklist) rõ ràng, khả thi và chia nhỏ (atomic).
---

# Lập Kế hoạch Súc tích (Concise Planning)

## Mục tiêu

Biến yêu cầu của người dùng thành một **kế hoạch hành động duy nhất** với các bước nhỏ, cụ thể (atomic steps).

## Quy trình làm việc

### 1. Quét Bối cảnh (Scan Context)

- Đọc `README.md`, tài liệu và các file code liên quan.
- Xác định các ràng buộc (ngôn ngữ, frameworks, kiểm thử).

### 2. Tương tác Tối thiểu

- Hỏi **tối đa 1–2 câu hỏi** và chỉ hỏi nếu thực sự bị chặn (blocking).
- Đưa ra các giả định hợp lý cho những ẩn số không gây cản trở.

### 3. Tạo Kế hoạch

Sử dụng cấu trúc sau:

- **Cách tiếp cận (Approach)**: 1-3 câu về cái gì và tại sao.
- **Phạm vi (Scope)**: Các gạch đầu dòng cho "Trong phạm vi" (In) và "Ngoài phạm vi" (Out).
- **Hạng mục Hành động (Action Items)**: Một danh sách gồm 6-10 tác vụ nhỏ, được sắp xếp theo thứ tự (Bắt đầu bằng động từ).
- **Xác thực (Validation)**: Ít nhất một mục dành cho việc kiểm thử.

## Mẫu Kế hoạch

```markdown
# Kế hoạch

<Cách tiếp cận cấp cao>

## Phạm vi (Scope)

- Trong phạm vi (In):
- Ngoài phạm vi (Out):

## Hạng mục Hành động (Action Items)

[ ] <Bước 1: Khám phá/Tìm hiểu>
[ ] <Bước 2: Triển khai>
[ ] <Bước 3: Triển khai>
[ ] <Bước 4: Xác thực/Kiểm thử>
[ ] <Bước 5: Triển khai/Commit>

## Câu hỏi Mở

- <Câu hỏi 1 (tối đa 3)>
```

## Hướng dẫn Checklist

- **Tính nguyên tử (Atomic)**: Mỗi bước nên là một đơn vị công việc logic duy nhất.
- **Bắt đầu bằng động từ (Verb-first)**: "Thêm...", "Tái cấu trúc (Refactor)...", "Xác minh...".
- **Cụ thể (Concrete)**: Nêu tên các file hoặc module cụ thể khi có thể.
