# AI Log — 2026-11-12 — zMerkurias

## Phiên 1 — Bước 0: tài liệu chuẩn bị

| | |
|---|---|
| Công cụ / model | Claude Code (ứng dụng desktop) |
| Việc liên quan | T-001, T-005 đến T-007 (lập kế hoạch) |

**Nhờ AI làm gì**

- Đọc đề VFO2O-15 và các tiêu chí của nhóm; đọc 3 tài liệu của mentor trên Drive (template quản trị, charter + mẫu báo cáo, slide QTDA).
- Khảo sát dinhgiaxe.vucar.vn như một người dùng bình thường và rút ra bài học.
- Dựng bộ tài liệu chuẩn bị, file quản trị chung và log tiến độ.

**AI tạo ra gì**

- `docs/preparation/00` đến `07`: đề bài và phạm vi, charter, user stories, bài học Vucar, kiến trúc và CI/CD, eval và test, kế hoạch dữ liệu, câu hỏi mở.
- `docs/management/project-management.xlsx`: 12 sheet, 39 việc, 3 biểu đồ (sinh bằng script Python).
- `PROJECT-LOG.md`.

**Giữ nguyên / sửa / bỏ**

- Giữ làm bản nháp. Cả nhóm cần đọc và chốt: mục tiêu số, phân vai, danh mục xe, thứ tự user story.

**Đã kiểm tra bằng cách nào**

- File Excel mở lại được bằng code. **Chưa** mở bằng Excel hoặc Google Sheets để kiểm tra công thức và biểu đồ.
- Giá dịch vụ hosting trong file 04 là ước lượng của AI, chưa đối chiếu trang giá.
- Hai tài liệu của mentor (pptx, docx) AI chưa đọc.

**Bài học**

- AI chỉ ra khoảng trống: ý tưởng ban đầu của nhóm xoay quanh định giá, trong khi đề còn 4 mục Cơ bản nằm ngoài định giá.
- AI chỉ ra dữ liệu rao vặt là giá rao, không phải giá thu mua mà đề yêu cầu.

## Phiên 2 — Bộ nộp Gate 1

| | |
|---|---|
| Công cụ / model | Claude Code (ứng dụng desktop) |
| Việc liên quan | Gate G1 — Chốt đề tài |

**Nhờ AI làm gì**

- Viết Brief 1 trang, PRD, Wireframe / UI Flow; sắp xếp thư mục thành cấu trúc repo; viết README và GUIDE; khởi tạo git và đẩy lên nhánh cá nhân.

**AI tạo ra gì**

- `docs/01-brief.md`, `docs/02-prd.md`, `docs/03-wireframe-ui-flow.md`
- `README.md`, `GUIDE.md`, `CONTRIBUTING.md`, `CHANGELOG.md`, `.gitignore`, `.env.example`, `.github/pull_request_template.md`
- `ai-logs/` (bản tạm)

**Giữ nguyên / sửa / bỏ**

- Bản nháp chờ nhóm duyệt trước khi nộp gate.

**Đã kiểm tra bằng cách nào**

- Chưa có ai trong nhóm duyệt nội dung.
- AI **không đọc được Technical Book** trên portal (cần đăng nhập GitHub), nên phần AI Log và cấu trúc repo chưa đối chiếu với template chính thức của chương trình.

**Bài học**

- Con số trong wireframe chỉ là minh họa bố cục, không phải kết quả tính thật.
