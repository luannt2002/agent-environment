---
name: retro
description: Nhìn lại một phiên làm việc và đề xuất sửa môi trường của agent (điều hướng, check tự động, chuẩn code, steering file, công cụ) để lần sau làm tốt hơn.
disable-model-invocation: true
metadata:
  source: "Chuyển thể từ skill retro của mattpocock/skills (MIT, Copyright (c) 2026 Matt Pocock) — https://github.com/mattpocock/skills"
---

# Retro — học từ phiên vừa rồi

Retro đề xuất sửa **môi trường**, không sửa code: tìm thứ trong repo hoặc trong bộ skill đã khiến agent vướng, để lỗi lần này không lặp lại lần sau. Đây là dạng chạy được của luật "sửa ở tầng cao nhất": bài học chưa thành tệp mà máy tự nạp thì coi như chưa học.

## Các bước

1. **Chọn phiên.** Mặc định là phiên hiện tại. Người dùng chỉ phiên khác thì đọc log của phiên đó (Claude Code lưu dưới `~/.claude/projects/`, mỗi dự án một thư mục đặt tên theo đường dẫn đã mã hoá, mỗi phiên một tệp `.jsonl`).
2. **Tìm chỗ vướng.** Mỗi đề xuất trỏ về một khoảnh khắc cụ thể trong phiên: lệnh nào, lượt nào, tốn bao nhiêu bước. Phiên trơn tru thì báo là không có gì đáng sửa — đó là kết quả hợp lệ.
3. **Rà theo bảy nhóm** ở bảng dưới.
4. **Phân loại** từng chỗ vướng trước khi đề xuất cách sửa.
5. **Trình bày** theo mức nghiêm trọng, nặng trước. Chỉ đề xuất; người dùng chọn cái nào thì mới sửa cái đó.

## Bảy nhóm

| Nhóm | Dấu hiệu trong phiên | Sửa bằng |
|---|---|---|
| Điều hướng | Mất nhiều lượt mới tìm ra tệp hoặc thông tin | Con trỏ điều hướng từ tệp agent đã đọc (`CLAUDE.md` của dự án, README); tìm docs có sẵn trước khi viết docs mới |
| Check tự động | Agent mắc lỗi mà một check bắt được | Lint rule, kiểu dữ liệu, test, hook, CI job |
| Chuẩn code | Khâu soát bỏ lọt một lỗi cần phán đoán | Thêm hoặc sửa luật trong `CODING_STANDARDS.md` |
| Steering file | `CLAUDE.md`/`AGENTS.md` dài, chứa lời dặn đáng là một check | Chuyển sang check hoặc chuẩn code, chỉ giữ con trỏ |
| Công cụ | Lệnh gọi tốn kém so với thứ nó trả về | Thu gọn lệnh, viết script, đổi công cụ |
| Câu thừa (no-op) | Câu trong steering file mà agent vẫn làm như mặc định | Xoá cả câu |
| Thiếu thông tin | Agent cần một dữ kiện mà không với tới | Ghi log dev server ra tệp, cấp quyền chỉ đọc vào dịch vụ |

## Phân loại

- **Lỗi máy móc** (mẫu cú pháp cố định, API bị cấm, kiểu import, vị trí tệp) → **check tất định**. Đọc lệnh check sẵn có của repo trước (`package.json`, Makefile, cấu hình CI): check đã có mà chưa nối vào, hoặc đã hỏng âm thầm, thì đề xuất nối/sửa nó, không viết mới. Mỗi check đề xuất kèm cách phá thử để chứng minh nó chặn được.
- **Lỗi cần phán đoán** (nhất quán giữa nhiều tệp, khớp phong cách xung quanh) → luật trong `CODING_STANDARDS.md`, khâu soát đọc khi review. Chuẩn code giao cho khâu soát vì khâu viết đã chịu áp lực ngữ cảnh lớn nhất (khảo sát, viết, debug), còn khâu soát chỉ cầm diff nên có chỗ để áp luật.
- **`CLAUDE.md`** chỉ giữ con trỏ điều hướng và điều không suy ra được từ repo. Nó nạp vào mọi phiên, nên mỗi dòng thêm vào đều tốn ở mọi phiên.
- Repo không có cổng nào (không pre-commit, không CI chạy lint/test) là một phát hiện riêng.

## Đặt đề xuất ở đâu

Đề xuất đúng cho mọi dự án → base (`~/.claude/CLAUDE.md` hoặc một skill base). Chỉ đúng cho repo này → project-local (`CLAUDE.md` dự án, `.claude/skills/`, CI của repo). Sửa base là một việc riêng, không làm lẫn trong task của dự án.
