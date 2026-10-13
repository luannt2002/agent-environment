# agent-environment

Cách mình dùng Claude Code: một `CLAUDE.md`, vài skill dùng chung cho mọi dự án (**base**), và vài skill chép vào từng dự án (**project-local**). Phần lớn là ghép lại từ bộ skill của người khác, cộng vài tệp mình tự viết. Ghi lại để tự dùng và chia sẻ.

## Hai tầng

| Thư mục | Đặt ở đâu | Áp dụng cho |
|---|---|---|
| `base/` | `~/.claude/` | Mọi dự án trên máy |
| `project-local/` | `<repo>/.claude/` (skill vào `skills/`, cộng tệp template) | Chỉ repo đó |

Cách xếp: chép sang dự án **nào** cũng đúng và cũng cần thì để ở base; chỉ đúng với một dự án, hoặc chỉ khi dự án có thứ gì đặc biệt, thì để ở project-local.

## Base

| Thành phần | Làm gì | Nguồn |
|---|---|---|
| [`base/CLAUDE.md`](base/CLAUDE.md) | Luật làm việc lõi: đòi lệnh chứ không nhận lời khai, người chấm khác người làm, sửa ở tầng cao nhất | Tự viết, có mượn ý (xem [Nguồn](#nguồn)) |
| superpowers | Quy trình: làm rõ yêu cầu, plan, TDD, debug, verify, review | [obra/superpowers](https://github.com/obra/superpowers) |
| ponytail | Lời giải đơn giản nhất còn chạy đúng: YAGNI, stdlib trước, viết ít code | [DietrichGebert/ponytail](https://github.com/DietrichGebert/ponytail) |
| [`code-en-doc-vi`](base/skills/code-en-doc-vi/SKILL.md) | Identifier tiếng Anh; comment, docs tiếng Việt | Tự viết |
| [`glossary-keeper`](base/skills/glossary-keeper/SKILL.md) | Giữ thuật ngữ dự án trong `GLOSSARY.md`, quyết định khó đảo ngược trong ADR | Chuyển thể từ `domain-modeling` của [mattpocock/skills](https://github.com/mattpocock/skills) |
| [`retro`](base/skills/retro/SKILL.md) | Gõ `/retro` sau phiên: đề xuất sửa môi trường (check, chuẩn code, steering file) thay vì sửa code | Chuyển thể từ `retro` của [mattpocock/skills](https://github.com/mattpocock/skills) |

## Luồng base trong một phiên

**Lúc mở phiên**, Claude Code tự nạp:
- `~/.claude/CLAUDE.md`;
- toàn văn skill `using-superpowers` (do hook của superpowers nạp): có skill hợp với việc thì dùng skill trước khi làm;
- bộ luật ponytail (do hook của ponytail nạp), kèm danh sách ngắn các hàm/class có sẵn trong thư mục đang làm để tái dùng thay vì viết lại (bản 5.x);
- tên và mô tả của các skill khác. Thân skill chỉ nạp khi skill được dùng. Riêng `retro` không nạp gì cho tới khi gõ `/retro`.

**Trong lúc làm**, agent tự gọi skill theo tình huống:

| Khi | Skill |
|---|---|
| Bắt đầu một tính năng hoặc thay đổi hành vi | `brainstorming` |
| Đang chốt thuật ngữ nghiệp vụ, một từ bị dùng mơ hồ | `glossary-keeper` |
| Có spec cho việc nhiều bước | `writing-plans` → `subagent-driven-development` hoặc `executing-plans` |
| Viết hoặc sửa logic | `test-driven-development`, cộng ponytail và `code-en-doc-vi` |
| Gặp lỗi, test đỏ | `systematic-debugging` |
| Sắp báo "xong" | `verification-before-completion`, rồi `requesting-code-review` |
| Xong nhánh | `finishing-a-development-branch`; người chọn merge, PR hay giữ |
| Muốn soát theo kiểu ponytail: code thừa, cộng lỗi, bảo mật, test còn thiếu | `ponytail-review` (một diff), `ponytail-audit` (cả repo) |

**Sau phiên** vất vả, gõ `/retro`. Lỗi máy móc thì thành check (lint, hook, CI); lỗi cần phán đoán thì thành luật trong chuẩn code; `CLAUDE.md` chỉ thêm con trỏ điều hướng. Bài học thành tệp, lần sau khỏi phải nhắc.

```
mở phiên ─► CLAUDE.md · using-superpowers · luật ponytail · mô tả skill
   │
nhận việc ─► "xong là gì" phải là một phép thử có thể TRƯỢT
   │
việc lớn: brainstorming ─► glossary-keeper ─► writing-plans ─► thi hành plan
việc nhỏ: vào thẳng code
   │
code ─► test-driven-development · ponytail · code-en-doc-vi · lỗi → systematic-debugging
   │
báo xong ─► verification-before-completion ─► review ─► finishing-a-development-branch
   │
sau phiên ─► /retro ─► bài học thành tệp
```

Khi các nguồn nói khác nhau: `CLAUDE.md` của dự án → skill project-local → `CLAUDE.md` base → skill base. Superpowers quyết quy trình, ponytail quyết viết bao nhiêu code. Luật của mình: ponytail chỉ được nới khối lượng code; test, validation, bảo mật và xử lý mất dữ liệu vẫn giữ nguyên.

## Project-local

| Thành phần | Làm gì |
|---|---|
| [`template/CLAUDE.template.md`](project-local/template/CLAUDE.template.md) | Khung `CLAUDE.md` của dự án: phần CORE (luật làm việc) giữ nguyên, 8 mục thông tin dự án (P1–P8) để điền |
| [`project-core`](project-local/skills/project-core/SKILL.md) | Khảo sát repo rồi viết `CLAUDE.md` của dự án từ template, điền P1–P8 bằng dữ kiện thật |
| [`change-control`](project-local/skills/change-control/SKILL.md) | Khi đổi code: truy caller và contract, kiểm regression, đồng bộ docs và changelog |

`GLOSSARY.md` và `docs/adr/` do `glossary-keeper` ghi vào repo khi cần. Thứ gì chỉ vài dự án dùng (cổng CI riêng, routine chạy đêm…) thì thêm vào project-local của đúng dự án đó.

## Mình setup thế nào

Cần Claude Code và `node` (hook của ponytail chạy bằng node). Các lệnh `cp` dưới đây chạy ở thư mục gốc của repo này.

Trước khi chép, xem chỗ đích đã có skill cùng tên chưa:
- là **symlink**: `cp` báo lỗi `cannot overwrite non-directory` và không chép gì, bản cũ vẫn chạy. Xoá symlink trước.
- là **thư mục thật**: `cp` ghi đè tệp trùng tên nhưng để lại tệp cũ thừa. Sao lưu rồi xoá thư mục cũ trước.

**Base, một lần trên mỗi máy.** Gõ trong Claude Code:

```text
/plugin install superpowers@claude-plugins-official
/plugin marketplace add DietrichGebert/ponytail
/plugin install ponytail@ponytail
```

Rồi chép skill và `CLAUDE.md` từ repo này:

```bash
mkdir -p ~/.claude/skills
cp -R base/skills/* ~/.claude/skills/
[ -e ~/.claude/CLAUDE.md ] || cp base/CLAUDE.md ~/.claude/CLAUDE.md   # đã có thì giữ, tự gộp tay
```

**Project-local, mỗi repo:**

```bash
mkdir -p <repo>/.claude/skills
cp -R project-local/skills/* <repo>/.claude/skills/
cp project-local/template/CLAUDE.template.md <repo>/.claude/
```

Template tên `CLAUDE.template.md` chứ không phải `CLAUDE.md`: Claude Code tự nạp mọi tệp tên đúng `CLAUDE.md` trong thư mục mà agent đọc tới, nên đặt tên đó thì khung trống sẽ bị nạp như luật thật.

Mở Claude Code trong repo đó và nhờ: *"Dùng skill project-core để viết CLAUDE.md cho repo này. Chỉ sửa CLAUDE.md, không sửa code."* Commit `CLAUDE.md`, `.claude/skills/` và `.claude/CLAUDE.template.md` cùng repo; thiếu template thì `project-core` sẽ dừng lại hỏi.

Sau khi chép, mở **phiên mới** rồi gõ `/skills` để chắc skill đã được nạp. Phiên đầu tiên có ponytail, hook của nó chép một script statusline vào `~/.claude/` và Claude sẽ đề nghị thêm `statusLine` vào `settings.json`; không cần thì từ chối.

## Nguồn

- **superpowers** — Jesse Vincent, MIT, <https://github.com/obra/superpowers>. Cài qua plugin, repo này không chép mã.
- **ponytail** — Dietrich Gebert, MIT, <https://github.com/DietrichGebert/ponytail>. Cài qua plugin, repo này không chép mã.
- **`glossary-keeper`, `retro`** — chuyển thể và dịch từ skill [`domain-modeling`](https://github.com/mattpocock/skills/tree/49dd158d1076134a641b33efb035946536778336/skills/engineering/domain-modeling) và [`retro`](https://github.com/mattpocock/skills/tree/49dd158d1076134a641b33efb035946536778336/skills/engineering/retro) của [mattpocock/skills](https://github.com/mattpocock/skills) (Copyright (c) 2026 Matt Pocock, [MIT](https://github.com/mattpocock/skills/blob/main/LICENSE)), bản đọc tại commit `49dd158`.
- **Ba luật "Đơn giản trước / Sửa phẫu thuật / Nói giả định" và ý "được phản biện" trong `base/CLAUDE.md`** — chuyển thể từ [Karpathy-Inspired Claude Code Guidelines](https://github.com/multica-ai/andrej-karpathy-skills) (trước là `forrestchang/andrej-karpathy-skills`), đúc từ nhận xét của Andrej Karpathy. Repo đó không ghi giấy phép. Ghi tại chỗ bằng `[Karpathy guidelines: …]`.
- **Các ý ghi `[Boris: …]` trong `base/CLAUDE.md`** — từ chia sẻ công khai của Boris Cherny (Claude Code) tại <https://howborisusesclaudecode.com/>.
- Phần còn lại mình tự viết.
