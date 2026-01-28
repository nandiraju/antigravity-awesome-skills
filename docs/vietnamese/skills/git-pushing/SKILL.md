---
name: git-pushing
description: Stage, commit, và push các thay đổi git với thông điệp commit theo chuẩn (conventional commit messages). Sử dụng khi người dùng muốn commit và push thay đổi, đề cập đến việc đẩy lên remote, hoặc yêu cầu lưu và đẩy công việc của họ. Cũng kích hoạt khi người dùng nói "push changes", "commit and push", "push this", "push to github", hoặc các yêu cầu quy trình công việc git tương tự.
---

# Quy trình Git Push

Stage tất cả thay đổi, tạo một commit theo chuẩn, và đẩy lên nhánh remote.

## Khi nào nên sử dụng

Tự động kích hoạt khi người dùng:

- Yêu cầu đẩy các thay đổi một cách rõ ràng ("push cái này", "commit và push")
- Đề cập đến việc lưu công việc lên remote ("lưu lên github", "push lên remote")
- Hoàn thành một tính năng và muốn chia sẻ nó
- Nói các cụm từ như "hãy push cái này lên" hoặc "commit những thay đổi này"

## Quy trình làm việc

**LUÔN LUÔN sử dụng script** - KHÔNG sử dụng các lệnh git thủ công:

```bash
bash skills/git-pushing/scripts/smart_commit.sh
```

Với thông điệp tùy chỉnh:

```bash
bash skills/git-pushing/scripts/smart_commit.sh "feat: them tinh nang"
```

Script sẽ xử lý: staging, thông điệp commit theo chuẩn, footer của Claude, và push với cờ -u.
