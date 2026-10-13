---
name: code-en-doc-vi
description: Viết code với identifier tiếng Anh, giải thích và docs/comment tiếng Việt, giữ keyword kỹ thuật tiếng Anh; không đổi API hay mã bên thứ ba chỉ để dịch.
---

- Identifier mới dùng tiếng Anh, theo naming convention repo; không dùng tên tiếng Việt không dấu.
- Giải thích cho chủ dự án, comment, docstring và tài liệu tự viết dùng tiếng Việt có dấu.
- Giữ keyword kỹ thuật EN, giải nghĩa VI khi cần: `idempotency (tính lặp an toàn)`; không bắt lặp giải nghĩa ở mọi câu.
- Giữ tên symbol, command, path, config key, error code và tên sản phẩm để tra cứu được.
- Comment nói lý do, invariant và chỗ dễ sai; không diễn lại từng dòng code.
- Không rename API/schema/identifier có sẵn chỉ vì ngôn ngữ. Rename được giao phải kiểm caller/contract.
- Mã bên thứ ba/generated giữ nguyên; sửa nguồn theo quy trình nếu cần. Chuỗi UI/tài liệu có yêu cầu ngôn ngữ riêng theo repo.
- Skill chỉ quyết ngôn ngữ, không thêm quyền triển khai hoặc bỏ qua test/review.
