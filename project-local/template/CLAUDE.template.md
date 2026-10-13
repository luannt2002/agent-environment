# CLAUDE.md — Thông tin dự án và quy tắc làm việc

> Phần quy tắc chung hướng dẫn cách làm việc; phần thông tin dự án được điền theo mã nguồn và tài liệu của từng dự án.

## CORE — Quy tắc làm việc

- Giải đúng bài bằng cách đơn giản đủ dùng; giữ yêu cầu và quyết định sản phẩm đã chốt.
- Theo luật hệ thống/môi trường và quyền chủ dự án cấp. P2 khai thứ tự áp dụng: hướng dẫn repo theo phạm vi → skill repo → base được phép → mặc định template, trừ khi nguồn cấp trên quy định khác.
- Base chỉ đọc khi làm task dự án. Skill chuyên biệt ở trong repo, kiểm đích thực trước ghi; tạo/cập nhật trong scope đã giao, phần ngoài scope thì đề xuất. Nguồn bắt buộc thiếu thì báo; phần độc lập vẫn làm.
- Làm rõ mục tiêu, scope và tiêu chí xong; khai giả định, phân biệt dữ kiện/mục tiêu/đề xuất. Dùng nguồn thật, không bịa kết quả, path hoặc cổng đã hoạt động.
- Trước task đọc nguồn phù hợp trong P7. Khi đổi hành vi, kiểm caller/contract/test/docs/comment; kiểm regression và đồng bộ phần bị lệch.
- Identifier EN, mô tả/docs/comment VI, giữ keyword kỹ thuật. Theo convention repo, giữ thay đổi của người khác; ưu tiên reuse/stdlib/platform.
- Chọn Haiku cho việc cơ học rõ, Sonnet cho việc thường ngày, Opus cho suy luận khó; verify/edge case dùng high theo gợi ý đã khai ở P2. Môi trường quyết cấu hình thực tế; effort không thay spec, quyền hay bằng chứng.
- Chạy kiểm tra theo rủi ro và cổng repo; bộ lọc kiểm cả cho qua và từ chối. Không nới cổng/test để che lỗi hoặc ghi secret vào tài liệu.
- Review, commit/MR/merge/deploy theo scope và cổng hiện hành. Bàn giao thay đổi, lệnh/kết quả, giới hạn và việc chưa kiểm chứng; không coi tự review là soát độc lập.

## PROJECT — Quy ước điền

- Giữ P1–P8 đúng thứ tự. Thay hướng dẫn điền bằng dữ kiện có nguồn; không để placeholder.
- P4/P5/P7 dùng bảng. P1/P2/P3/P6 dùng list ngắn hoặc bảng. P8 dùng bảng khi có điểm chưa rõ; nếu không, ghi phạm vi đã kiểm.
- “Đủ khi” là checklist lúc tạo, bỏ các dòng này trong CLAUDE.md cuối nếu không giúp vận hành. Repo nhỏ giữ tám mục với mỗi mục 1–3 dòng; mục không áp dụng ghi lý do. Nhắm dưới 200 dòng, dẫn nguồn cho chi tiết dài thay vì chép đầy đủ.
- Dữ kiện: **ĐÃ XÁC MINH / CHƯA XÁC MINH**. Lệnh: **ĐÃ CHẠY / CHƯA CHẠY**. Tiêu chí: **ĐẠT / TRƯỢT / CHƯA KIỂM CHỨNG**. Ghi nguồn, kết quả hoặc cách kiểm tương ứng; không cần gắn trạng thái vào mọi câu.
- Phân biệt **HIỆN TRẠNG / MỤC TIÊU / ĐỀ XUẤT**. Mục tiêu chưa triển khai không được ghi là hành vi đã có; thiếu dữ kiện không được bịa để điền đủ.

### P1. Mục tiêu sản phẩm và quyền thực hiện

- Điền: bài toán; người dùng; giai đoạn; mục tiêu; tiêu chí thành công; ngoài phạm vi; quyền agent.
- Mặc định THỰC HIỆN; REVIEW khi được giao review. Chế độ không thay đổi các cổng phê duyệt hoặc quyền công cụ.
- Đủ khi: xác định được task có phục vụ sản phẩm và agent được làm phần nào; thiếu quyết định ảnh hưởng quyền thì hỏi.

### P2. Nguồn luật và quyết định

- Điền: hướng dẫn theo phạm vi; nguồn luật; thứ tự ưu tiên; vị trí skill repo/base; lựa chọn model/effort thực tế hoặc chưa xác minh; đặc tả/decision record; quyết định và mâu thuẫn. Base mặc định: Superpowers, Ponytail, code-en-doc-vi, glossary-keeper, retro, agent reviewer; bổ sung theo luật môi trường.
- Dẫn đường dẫn thật, portable trong repo khi có; nguồn cá nhân chỉ ghi khi môi trường sử dụng và đã kiểm. Không coi tải skill từ internet là điều kiện để dùng CORE.
- Ghi file changelog hiện có, đơn vị ghi và trigger bắt buộc. Nếu chưa có hoặc thiếu quy tắc, ghi rõ và đề xuất khi cần; không tự tạo chỉ để điền mục này.
- Đủ khi: nguồn quan trọng truy được hoặc được đánh dấu thiếu; quy tắc cũ có nơi chuyển tới, không bị âm thầm bỏ. Quy tắc cũ trái mục tiêu dự án được nêu để chủ dự án quyết định thay thế.

### P3. Kiến trúc và bản đồ repo

- Điền: stack có nguồn; entry point; module; dữ liệu/tích hợp; thư mục code/test/config/migration khi có; hướng phụ thuộc và invariant chính.
- Dẫn file/symbol mẫu và convention hiện hành; không áp cấu trúc của dự án khác. Không có một thành phần thì ghi không áp dụng.
- Đủ khi: biết bắt đầu đọc/sửa ở đâu, luồng phụ thuộc chính và ranh giới cần giữ.

### P4. Luồng nghiệp vụ chính

| Luồng và loại thông tin | Trigger/entry point | Xử lý → đọc/ghi → kết quả | Lỗi/quyền quan trọng | Nguồn file/symbol |
|---|---|---|---|---|

- Điền luồng đại diện, thường 3–5 luồng với repo lớn; đây là ngân sách trình bày, không phải giới hạn an toàn. Repo nhỏ có thể một luồng.
- Luồng về quyền/tiền/dữ liệu phải được mô tả hoặc có tham chiếu rõ. Dẫn bản đồ đầy đủ nếu có; không tạo đường dẫn chưa tồn tại.
- Đủ khi: theo được đầu vào tới kết quả, biết nhánh quan trọng và phần chưa triển khai; chi tiết dài ở nguồn riêng.

### P5. Lệnh và môi trường kiểm tra

| Mục đích | Working directory và phụ thuộc | Lệnh có nguồn | Thực thi | Kết quả/giới hạn |
|---|---|---|---|---|

- Điền lệnh local/lint/build/test có thật; ghi ĐÃ CHẠY/CHƯA CHẠY và kết quả. Lệnh có trong manifest chưa chứng minh chạy được.
- Ghi cấu hình mẫu, dịch vụ cần và giới hạn tài nguyên khi liên quan. Không chạy migration/deploy/dữ liệu thật chỉ để điền bảng.
- Đủ khi: người khác biết điều kiện chạy lại và điều đã/chưa kiểm; không có script giả hoặc secret trong hướng dẫn.

### P6. Cổng, phát hành và vận hành

- Điền: hook/CI, branch protection, review/phê duyệt, điều kiện commit/MR/merge/deploy, môi trường mục tiêu, smoke test và rollback nếu có.
- Nêu cách nhận biết lỗi sau phát hành, nguồn log/metric/runbook và người hoặc vai chịu trách nhiệm khi đã xác định; không bịa cấu hình vận hành.
- Tách yêu cầu trên giấy, cấu hình đã xác minh và hoạt động đã kiểm bằng phép thử; chưa biết thì ghi rõ.
- Chỉ mục môi trường dùng format: environment ID | nguồn config/runbook chung | ghi chú LOCAL nếu có | cách chọn/đọc | trạng thái xác minh. Chỉ áp ghi chú đúng môi trường task, không mặc định production.
- Ghi chú server ở file riêng trong repo theo convention hiện có; LOCAL không vào CORE/bản server khác, không tự import mọi môi trường. Config chung có thể version control; ghi chú local riêng cần loại khỏi version control khi được giao thiết lập. Không tự tạo file/sửa `.gitignore` chỉ để điền P6.
- Chỉ ghi tên biến/alias hoặc tham chiếu secret được phép, không ghi giá trị; path/địa chỉ nhạy cảm không vào tài liệu chung. Có file ghi chú không chứng minh nó được tự nạp; chỉ rõ cách đọc.
- Đủ khi: biết cổng/quyền thực tế, cách kiểm phát hành và xử lý lỗi hoặc những điểm đang chặn phát hành; tài liệu không thay bằng chứng cổng đã chạy.

### P7. Định tuyến docs, skill và mã mẫu

- Điền path/symbol thật: luật chỉ định trước → skill repo phù hợp → base bổ sung. Ghi REPO/BASE CHỈ ĐỌC; thứ tự xung đột theo P2.
- Thuật ngữ và quyết định khó đảo ngược: trỏ tới `GLOSSARY.md` và `docs/adr/` nếu có (glossary-keeper ghi); không chép nội dung glossary vào CLAUDE.md.
- Trước task, chọn và đọc nguồn tương ứng trong P7; chỉ nạp phần liên quan, không nạp tất cả skill. Kiểm nội dung còn phù hợp. Thiếu skill: ghi “Chưa có skill chuyên biệt”, báo thiếu; tạo/cập nhật trong repo nếu thuộc phạm vi đã giao, ngoài phạm vi thì đề xuất; kiểm symlink trước ghi.
- Dẫn luồng/contract/test/docs và changelog khi liên quan; chỉ đọc phần cần. Ví dụ dưới đây là format minh họa, thay bằng nguồn thật hoặc bỏ khi áp dụng:

| Loại task | Tài liệu/hợp đồng chuẩn | Skill ưu tiên | Phạm vi/nguồn skill | Mã mẫu/convention | Khi đọc / khi không cần |
|---|---|---|---|---|---|
| Đổi API | Contract và docs có thật | Skill API nếu có | REPO | Handler/test tương ứng | Khi đổi contract; bỏ qua khi sửa chữ |

- Đủ khi: từ loại task tìm được nguồn cần đọc, phạm vi lưu/sửa và mã mẫu còn đúng; không nạp skill riêng của dự án khác hoặc làm thay đổi kho base.

### P8. Điểm chưa xác minh

| Điểm chưa biết | Tác động | Cách kiểm | Task/bước bị chặn |
|---|---|---|---|

- Nếu không còn điểm nào, ghi phạm vi đã kiểm; không tuyên bố mọi hệ thống đều đã được kiểm.
- Đủ khi: mỗi điểm chưa rõ có cách xử lý và ảnh hưởng cụ thể; phần độc lập được phép vẫn tiếp tục.

## Bảo trì

- Cập nhật PROJECT khi hành vi/lệnh/ràng buộc đổi; đồng bộ caller và docs/comment liên quan trong phạm vi được giao.
- Chỉ cập nhật mục bị lệch: kiến trúc/đường vào → P3; luồng → P4; lệnh/phụ thuộc chạy → P5; môi trường/vận hành → P6; nguồn luật/changelog → P2; docs/skill/mã mẫu → P7. Sửa nội bộ không đổi các thông tin này thì giữ CLAUDE.md.
- Giữ CORE theo bản nguồn đã áp dụng, chỉ đổi khi chủ dự án yêu cầu. Dẫn nguồn thay chép dài; không dùng CLAUDE.md làm backlog hoặc nhật ký.
