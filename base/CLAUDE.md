# CLAUDE.md — lõi vận hành (áp mọi dự án)

**MỤC TIÊU:** tin được kết quả với chi phí đọc-lại tối thiểu. Máy viết được code rồi ⇒ nút thắt là **TIN**, không phải **VIẾT**. Luật dưới không phủ ca nào → quyết theo mục tiêu này.

> **Thước đo mọi quy trình/đề xuất:** nó làm "tin-được-kết-quả" **RẺ đi hay ĐẮT lên**? Rẻ → làm. Đắt → bỏ.
> **Hiệu chỉnh:** thiên **CHẮC hơn NHANH**; việc vặt → dùng phán đoán, đừng biến thành nghi lễ.
> **Cổng:** chưa CHẶN được lần nào = chưa phải cổng → cố tình phá thử ≥1 lần để chứng minh.

## Ba kiểu hỏng — quy trình không chặn kiểu nào thì bỏ

| lỗi | dấu hiệu |
|---|---|
| **làm qua loa** | bỏ bước khó, báo "xong hết" |
| **tự chấm bài** | test đỏ → sửa TEST cho xanh, không sửa CODE |
| **đi lạc việc** | nhờ sửa 1 tệp, đổi chục tệp |

## Ba luật lõi — mỗi luật chặn một kiểu

1. **Người chấm ≠ người làm.** Khâu soát = phiên RIÊNG, không có quyền sửa. Sửa được → tự chữa rồi tự khen. [Boris: grader = author → self-preferential bias.] Review code → giao agent `reviewer`, truyền lệnh diff + đề bài; chụp vân tay cây làm việc trước và sau khi gọi, khác nhau thì bản soát vô hiệu: `{ git status --porcelain -uall; git diff HEAD; git ls-files -oz --exclude-standard | xargs -0r sha256sum; } | sha256sum`.
2. **Đòi LỆNH, không nhận LỜI KHAI.** "Test pass" là lời khai. Bằng chứng = lệnh tự chạy lại được + cách tái hiện + bảng chân trị. Báo cáo dài **dời** gánh nặng đọc, không **giảm** nó. `rc=0` = máy CÓ chạy, không = kết quả ĐÚNG.
3. **Sửa ở TẦNG CAO NHẤT.** Một lần → nói lại · lặp → luật/CLAUDE.md/skill · cả lớp → lint/CI/routine · routine sai → sửa routine. Sửa bằng chat là vá; viết thành luật là chữa. [Boris: fix the routine, not the PR.] Sau phiên khó, đề nghị người dùng gõ `/retro` để biến bài học thành tệp.

## Đo, đừng đoán

- Số đưa vào kết luận phải từ lệnh VỪA chạy. Chưa đo thì ghi "chưa đo". Số của agent/docs khác mà mình chưa tự chạy cũng là số chưa đo.
- `grep` ra 0 → chưa được kết luận "thiếu"; mở tệp ra đọc (sai mẫu tìm phổ biến hơn thiếu thật).
- Tách rạch ròi **Đã chứng minh** (có lệnh tái lập) và **Mới nghi** (kèm cách kiểm). Không đẩy nghi lên thành chứng minh cho báo cáo dày.
- Không tìm thấy gì vẫn báo: "soi 40 chỗ, 0 phát hiện" là kết quả hợp lệ.
- `bash -n` hay build OK ≠ chạy được. Cây làm việc mới thiếu tệp bị gitignore → số sai âm thầm → chạy một lệnh thật trước khi tin số.

## Tự hỏi TRƯỚC khi bị hỏi

Việc có quy mô hoặc kiến trúc (tải cao, dữ liệu lớn, nhiều thành phần) → tự đặt và tự trả lời trước khi bắt tay:
1. **Cái gì vỡ TRƯỚC?** Liệt kê từng tầng (app · hàng đợi · DB · cache · mạng · đĩa), đoán tầng nào là sàn, rồi **đo để bác bỏ chính mình**.
2. **Ca xấu nhất ra sao?** Một dòng nóng, một khoá nóng, một client chậm, một lần khởi động lại giữa chừng.
3. **Trần CỨNG ở đâu?** Thứ không nới được bằng code: số lõi, IOPS, dung lượng đĩa, giới hạn bên thứ ba. Đo trước.
4. **Cái gì hỏng ÂM THẦM?** Chỗ mất dữ liệu mà không ném lỗi. Không đếm được = không thấy = coi như đang hỏng.

## Sửa code cho sạch

- **Đơn giản trước.** Code tối thiểu giải ĐÚNG bài; không tính năng/abstraction/cấu hình/bắt lỗi ngoài yêu cầu.
- **Sửa phẫu thuật.** Chỉ chạm cái bắt buộc; không "cải thiện" code kế bên, khớp style sẵn có. Chỉ dọn thứ chính mình làm thừa; dead code có sẵn thì nhắc, không xoá.
- **Nói giả định, không đoán thầm.** Nhiều cách hiểu → nêu ra. Phân vân khi đang tương tác → hỏi trước khi code.

[Karpathy guidelines: ba luật trên và ý "được phản biện" ở mục dưới chuyển thể từ Karpathy-Inspired Claude Code Guidelines.]

## Giao việc và chạy song song

- Giao MỤC TIÊU, không giao từng bước. Plan là bản tóm tắt (brief), nhắm dưới 400 dòng, không chép code vào plan.
- **Được phản biện.** Giả định sai, có cách đơn giản hơn, plan sai → nói ra, đừng làm theo trong im lặng.
- Song song → đo trước: trần thật của máy, và số tệp giao nhau giữa các agent phải bằng 0.

## Hai tầng đi ngược chiều

- Commit: CHẺ NHỎ, một tính năng một commit, hoàn tác riêng được.
- MR: GỘP TO, để người soát đọc một lần rồi quyết.
- Tắc ở bước merge (thiếu quyền) không chặn phía trước: chạy tới bước mở MR rồi dừng đúng đó, báo lại.

## Test đỏ — đỏ loại gì

Ba loại: **môi trường** / **có sẵn từ trước** / **mới do mình**. Tách bằng ảnh chụp nhánh sạch, **đối chiếu theo TÊN test, không đếm số** (đếm vẫn xanh nếu ai đó lặng lẽ xoá một test).

## Bộ skill base và thứ bậc

Thứ tự khi mâu thuẫn: `CLAUDE.md` của dự án → skill project-local của dự án → tệp này → skill base.

| skill | quyết gì |
|---|---|
| superpowers | **quy trình**: làm rõ yêu cầu, plan, TDD, debug, verify, review |
| ponytail | **viết bao nhiêu code**: lời giải đơn giản nhất còn đúng. Chỉ nới khối lượng, không cắt test, validation ở ranh giới tin cậy, bảo mật hay xử lý mất dữ liệu |
| code-en-doc-vi | **ngôn ngữ**: identifier tiếng Anh, giải thích tiếng Việt |
| glossary-keeper | **thuật ngữ** dự án và quyết định khó đảo ngược |
| retro | gõ `/retro` sau phiên để đề xuất sửa môi trường |
| agent `reviewer` | **soát độc lập** một diff theo đề bài và chuẩn code của repo: ĐẠT / TRƯỢT / CHƯA ĐO |

Việc nhỏ (vài dòng, cấu hình): bỏ brainstorming và writing-plans; TDD vẫn giữ khi sửa logic.

## Đo SẢN LƯỢNG, không đo hoạt động

| ❌ | ✅ |
|---|---|
| "11/11 xong" · số token · thời gian | phát hiện mới/ngày · tỉ lệ được sửa · tuổi của phát hiện chưa xử lý |

Lượt chạy nhanh bất thường hoặc bị dừng vì hết giờ → đọc log trước khi báo; báo đúng là "hết giờ", không báo "xong".
