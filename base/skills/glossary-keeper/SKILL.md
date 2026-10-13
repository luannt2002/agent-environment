---
name: glossary-keeper
description: Giữ ngôn ngữ chung của dự án trong GLOSSARY.md và ghi quyết định khó đảo ngược thành ADR. Dùng khi thiết kế hoặc brainstorm một tính năng, khi đang bàn hoặc chốt thuật ngữ nghiệp vụ, khi một từ nghiệp vụ bị dùng mơ hồ hoặc lệch với glossary, hoặc khi viết/sửa GLOSSARY.md hay ADR.
metadata:
  source: "Chuyển thể từ skill domain-modeling của mattpocock/skills (MIT, Copyright (c) 2026 Matt Pocock) — https://github.com/mattpocock/skills"
---

# Glossary keeper — giữ ngôn ngữ chung của dự án

Mỗi dự án có bộ từ riêng. Skill này giữ bộ từ đó **trong repo**, để phiên sau, người khác và công cụ khác cùng hiểu một nghĩa. Đây là việc chủ động: chất vấn từ, thử bằng tình huống cụ thể, ghi ngay khi chốt. Chỉ đọc `GLOSSARY.md` để lấy từ thì không cần skill này.

## Tệp nằm ở đâu

- Một ngữ cảnh (đa số repo): `GLOSSARY.md` ở gốc repo, ADR ở `docs/adr/`.
- Nhiều ngữ cảnh: `GLOSSARY-MAP.md` ở gốc liệt kê từng ngữ cảnh, nơi đặt `GLOSSARY.md` của nó và quan hệ giữa chúng. ADR toàn hệ thống vẫn ở `docs/adr/` gốc; ADR riêng của một ngữ cảnh nằm ở `<ngữ-cảnh>/docs/adr/`. Chủ đề đang bàn thuộc ngữ cảnh nào không rõ thì hỏi.
- Tạo tệp khi có thuật ngữ hoặc quyết định đầu tiên cần ghi.
- Đang trong phiên bàn thiết kế hoặc thuật ngữ: ghi `GLOSSARY.md` ngay khi chốt. Đang làm việc khác (sửa lỗi, triển khai một ticket): đề xuất thuật ngữ cần ghi, người dùng đồng ý mới ghi.
- `CLAUDE.md` của dự án chỉ trỏ tới hai nơi này (mục P7 nếu dự án dùng template project-local), không chép nội dung sang.

## Trong phiên

- **Lệch glossary:** một từ được dùng khác nghĩa đã ghi → nêu ngay: "Glossary định nghĩa *huỷ đơn* là X, ở đây đang dùng theo nghĩa Y. Nghĩa nào đúng?"
- **Từ mơ hồ:** một từ gánh nhiều nghĩa → đề xuất từ chuẩn: "*Tài khoản* ở đây là Customer hay User?"
- **Tình huống biên:** khi bàn quan hệ giữa các khái niệm, tự đặt tình huống cụ thể để ép ranh giới giữa chúng rõ ra.
- **Đối chiếu code:** lời mô tả và code nói khác nhau → nêu chỗ khác kèm tệp/symbol, hỏi bên nào đúng.
- **Ghi khi chốt**, không gom tới cuối phiên (theo quy tắc ghi ở mục trên).

## GLOSSARY.md chỉ là bảng thuật ngữ

```md
# {Tên ngữ cảnh}

{Một hai câu: ngữ cảnh này là gì, tồn tại để làm gì.}

## Thuật ngữ

**Đơn hàng (Order)**:
Yêu cầu mua của khách, tính từ lúc xác nhận tới lúc giao xong.
_Tránh_: giao dịch, purchase
```

- Định nghĩa 1–2 câu, nói nó **là gì**. Nhiều từ cho một khái niệm → chọn một, các từ còn lại đưa vào `_Tránh_`.
- Chỉ ghi khái niệm riêng của dự án. Khái niệm lập trình chung (timeout, retry, cache) không thuộc về đây.
- Glossary chỉ giữ định nghĩa. Chi tiết cài đặt, spec, quyết định và ghi chú làm việc có chỗ khác. Glossary dài ra mà đọc giống spec là dấu hiệu đang lẫn: cắt về định nghĩa.
- Nhóm thuật ngữ theo tiêu đề con khi có cụm rõ ràng. Định nghĩa sai theo thời gian thì sửa tại chỗ.

## ADR chỉ khi đủ ba điều kiện

Đề nghị ghi ADR khi một quyết định **cùng lúc**:
1. **khó đảo ngược** — đổi ý sau này tốn kém thật;
2. **gây bất ngờ nếu thiếu bối cảnh** — người đọc code sau sẽ hỏi "sao lại làm thế này?";
3. **là đánh đổi thật** — có phương án khác hợp lý và đã chọn vì lý do cụ thể.

Thiếu một điều kiện thì không ghi. Người dùng đồng ý mới ghi.

```md
# {Tiêu đề ngắn của quyết định}

{1–3 câu: bối cảnh, đã chọn gì, vì sao.}
```

Đánh số tiếp theo số lớn nhất trong `docs/adr/`: `0001-slug.md`, `0002-slug.md`… Chỉ thêm mục *Trạng thái*, *Phương án đã cân nhắc*, *Hệ quả* khi chúng thật sự giúp người đọc sau.

Loại quyết định đáng ghi: hình dạng kiến trúc · cách các ngữ cảnh giao tiếp với nhau · công nghệ khó thay · ranh giới sở hữu dữ liệu · chỗ cố ý đi khác lối thông thường · ràng buộc không nhìn thấy trong code · phương án bị loại với lý do không hiển nhiên.
