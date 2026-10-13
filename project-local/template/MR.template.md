<!-- Khuôn mô tả MR/PR. Người duyệt đọc phần này thay vì đọc toàn bộ diff.
     GitHub: chép thành .github/pull_request_template.md · GitLab: .gitlab/merge_request_templates/Default.md -->

## 1. Đổi gì
<!-- 2–3 câu, cho người không theo dõi việc này -->

## 2. Vì sao
<!-- việc gốc, đánh đổi đã chọn, phương án bị loại -->

## 3. Bằng chứng
<!-- Lệnh chạy lại được kèm output thật. "Đã test, pass hết" không tính. -->

Đối chứng ngược (bản hỏng phải đỏ, ca đúng vẫn qua):
<!-- lệnh kèm output -->

## 4. Rủi ro
- Vùng 🔴 bị chạm: <!-- quyền, tiền, xoá/migration, secret, đồng thời, API ra ngoài; không có thì ghi "không" -->
- Đường lùi: <!-- git revert <sha> · tắt cờ · rollback migration -->

## 5. Điều tôi không kiểm được
<!-- Bắt buộc có nội dung cụ thể: phép kiểm nào, vì sao. Để trống là dấu hiệu xấu. -->
