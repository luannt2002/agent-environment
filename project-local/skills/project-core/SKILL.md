---
name: project-core
description: Tạo hoặc cập nhật CLAUDE.md từ bằng chứng trong repo và template chuẩn; dùng khi thiết lập thông tin/quy tắc dự án, không tự sửa code hoặc cài base.
---

# Project core — viết CLAUDE.md từ bằng chứng trong repo

1. Đọc luật repo, CLAUDE.md hiện có, README, manifest/lockfile, entry point, config mẫu, test, CI và decision record liên quan.
2. Xác định mục tiêu, quyền và quyết định đã chốt. Phân biệt HIỆN TRẠNG / MỤC TIÊU / ĐỀ XUẤT; không biến đề xuất thành quyết định.
3. Dùng template `.claude/CLAUDE.template.md` trong repo (chép từ `project-local/template/` của agent-environment). Không thấy tệp đó thì dừng và hỏi người dùng đường dẫn template; không tự đi tìm template ở nơi khác trên máy và không tự dựng khung.
4. Giữ CORE, cụ thể hoá P1–P8 bằng dữ kiện/path/symbol thật. Thiếu thông tin ghi CHƯA XÁC MINH + cách kiểm; không để placeholder hay lời hướng dẫn điền trong bản cuối.
5. Quy tắc quan trọng từ bản cũ phải có nơi chuyển tới; mâu thuẫn ảnh hưởng yêu cầu/quyền thì nêu để quyết định, không âm thầm bỏ.
6. Chỉ sửa file tài liệu được giao. Không tự tạo tài liệu phụ, sửa `.gitignore`, skill kỹ thuật, code hoặc cài plugin để hoàn thiện hồ sơ.
7. Kiểm nguồn/link, đủ tám mục, lệnh có điều kiện chạy và trạng thái; tách cổng trên giấy/cấu hình/đã kiểm hoạt động. Lệnh tồn tại không có nghĩa đã chạy.
8. Báo diff, quy tắc đã giữ/chuyển, bằng chứng và điều chưa biết. Sau task code, chỉ cập nhật CLAUDE.md nếu thông tin dự án bị lệch.
