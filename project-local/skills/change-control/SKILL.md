---
name: change-control
description: Kiểm caller/contract và regression khi đổi code, đồng bộ test/docs/comment và changelog theo repo; dùng cho sửa hoặc review, không audit toàn repo cho sửa chữ.
---

# Change control — kiểm tác động khi đổi code

### Trước sửa

- Đọc luật và diff hiện có; xác định hành vi trước/sau, input/output/error/side effect, invariant cần giữ.
- Dùng find references/language server nếu có và `rg` để tìm symbol, alias/import/interface/route/event/config key; đọc ngữ cảnh match.
- Truy caller tới đường vào hoặc side effect quan trọng; xét callback, registry, DI, reflection và consumer ngoài repo khi liên quan.
- Tìm README, spec/contract/OpenAPI, ví dụ, runbook, comment/docstring và TODO/FIXME/NOTE. Tìm cả tên nghiệp vụ; docs có thể không chứa tên hàm.
- Search có thể bỏ hidden/ignored file: tìm có mục tiêu, tránh quét dependency/build output. Không có match không chứng minh không ai dùng.
- Việc nhỏ không đổi contract: module, caller trực tiếp, test và mô tả gần nhất; ghi vài dòng là đủ. Mở rộng khi có ảnh hưởng lan truyền.

Với thay đổi có nhiều phụ thuộc, dùng bảng: nơi phụ thuộc | hành vi đang dựa vào | điều cần giữ/đổi | hành động và cách kiểm.

Ví dụ đổi `findUser` từ trả `null` sang ném lỗi: handler phải vẫn trả HTTP 401; job phải tiếp tục batch; docs/docstring phải khớp contract mới nếu đã chốt; client ngoài repo chưa truy cập được ghi CHƯA KIỂM CHỨNG. Đây là minh họa, không phải dữ kiện repo.

### Sửa và kiểm

- Triển khai trong scope/quyền; áp dụng TDD theo quy trình repo. Bugfix có ca tái hiện và regression test, ưu tiên chỗ consumer quan sát hành vi.
- Đổi contract kiểm integration/serialization/compatibility phù hợp; đổi đồng thời kiểm race/thứ tự theo stack. Một lần xanh không chứng minh hết race.
- Chạy kiểm tra hẹp trước, mở rộng tới vùng bị ảnh hưởng và cổng bắt buộc, theo tài nguyên môi trường.
- Test đỏ phân biệt lỗi mới/lỗi cũ/môi trường bằng bằng chứng; không đổi assertion hoặc bỏ test để che lỗi.
- Bộ lọc/quyền kiểm cho qua lẫn từ chối; cổng quan trọng thử lỗi đại diện trong môi trường cô lập.

### Nguồn nào cần cập nhật

Kiểm nguồn liên quan là bắt buộc; sửa khi mô tả bị sai, hợp đồng đổi hoặc chính sách repo yêu cầu. Không sửa hàng loạt cho đủ nghi thức.

| Đổi gì | Phải kiểm khi liên quan | Cập nhật CLAUDE.md khi |
|---|---|---|
| Logic/hành vi hàm | Caller, test, comment/docstring, docs nghiệp vụ | Luồng tóm tắt thay đổi → P4 |
| API/event/contract | CONTRACT/OpenAPI/schema, consumer, ví dụ, contract test | Luồng/định tuyến hợp đồng đổi → P4/P7 |
| Schema/dữ liệu | Migration, query/model, fixture, rollback | Bản đồ dữ liệu/vận hành đổi → P3/P6 |
| Config/default/flag | Config mẫu, validation, deployment docs, runbook | Điều kiện chạy/môi trường đổi → P5/P6 |
| Module/dependency/entry point | Manifest/lockfile, kiến trúc, docs | Bản đồ/nguồn mã mẫu đổi → P3/P7 |
| Lệnh build/test/chạy | Script, CI, README | Lệnh/điều kiện chạy đổi → P5 |
| Deploy/quan sát/rollback | Runbook, log/metric/config mục tiêu | Hướng dẫn vận hành đổi → P6 |
| Nguồn luật/skill/changelog | Link và định tuyến | Nguồn/chính sách đổi → P2/P7 |

- Nội bộ không đổi các thông tin trên: giữ CLAUDE.md, sửa test/docs/comment gần nhất khi cần.
- Giữ ADR/incident lịch sử; cập nhật trạng thái thay vì viết lại quá khứ. Không sửa spec để hợp thức hóa bug, không sửa tay generated output, không sửa migration đã áp dụng để che lịch sử.
- Docs ngoài repo hoặc vượt quyền cần đổi: báo phần còn thiếu, không tự sửa dịch vụ ngoài phạm vi.
- Changelog theo file/trigger/đơn vị ghi đã chọn của repo. Ghi tác động người dùng/vận hành và breaking change khi bắt buộc; không bịa version/ngày release, không ghi mọi commit/format/refactor.
- Chưa có changelog/chính sách: báo và đề xuất nếu cần; chỉ tạo khi được giao.

### Bàn giao

Soát diff cuối và tìm claim/tên cũ khi có rename; kiểm lại nếu có thay đổi sau lượt test. Báo caller/docs đã kiểm hoặc sửa, lệnh/output, giới hạn chưa kiểm chứng. Không kết luận “không còn bug ngầm”.
