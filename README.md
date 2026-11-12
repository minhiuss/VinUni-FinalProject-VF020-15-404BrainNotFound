# VFO2O-15 — AI Agent hỗ trợ đổi xe cũ (Trade-in)

**Nhóm 404BrainNotFound** · VinUni AI20K — Final Project

Một web app đặt ra **một mức giá cơ sở chung** cho cả khách muốn đổi xe và thẩm định viên: khách khai thông tin và ảnh xe để nhận khoảng giá thu mua tạm tính có căn cứ, xem số tiền cần bù để lên đời xe điện, rồi đặt lịch; thẩm định viên dùng baseline đó để chốt giá chính thức.

> **Trạng thái:** Gate 1 — Chốt đề tài. Repo hiện chỉ có tài liệu, chưa có code.

## Bắt đầu từ đâu

| Bạn muốn | Đọc |
|---|---|
| Hiểu dự án trong 2 phút | [Brief](docs/01-brief.md) |
| Biết phải xây những gì | [PRD](docs/02-prd.md) |
| Xem các màn hình | [Wireframe / UI Flow](docs/03-wireframe-ui-flow.md) |
| Biết từng file trong repo dùng để làm gì, và mình phải làm gì | **[GUIDE.md](GUIDE.md)** |
| Biết cách tạo nhánh, commit, mở PR | [CONTRIBUTING.md](CONTRIBUTING.md) |
| Xem nhóm đang làm tới đâu | [PROJECT-LOG.md](PROJECT-LOG.md) |

## Các gate

| Gate | Nội dung | Deliverables | Trạng thái |
|---|---|---|---|
| **G1 — Chốt đề tài** | Chốt bài toán + thiết kế. Hạn 23:59 ngày 15/11/2026 | [Brief](docs/01-brief.md) · [PRD](docs/02-prd.md) · [Wireframe / UI Flow](docs/03-wireframe-ui-flow.md) · [AI Log](ai-logs/) | Bản nháp, chờ nhóm duyệt |
| **G2 — MVP** | Agent nhận input thật, tự xử lý, trả output giải quyết pain point cho ít nhất 1 luồng chính | Video demo 3 phút · sơ đồ kiến trúc · ≥ 10 PR đã merge · README cài đặt · ≥ 5 ca kiểm thử thủ công | Chưa mở |

## Cấu trúc repo

```
.
├── README.md                  Trang này
├── GUIDE.md                   Hướng dẫn từng file + việc cần làm theo từng gate
├── CONTRIBUTING.md            Quy tắc nhánh, commit, PR, review
├── PROJECT-LOG.md             Nhật ký chung: standup, quyết định, rủi ro
├── CHANGELOG.md               Mỗi lần release một dòng
├── .env.example               Danh sách biến môi trường (không chứa giá trị thật)
├── .github/
│   └── pull_request_template.md
├── ai-logs/                   Ghi lại việc dùng AI trong dự án
└── docs/
    ├── 01-brief.md            G1 — Brief 1 trang
    ├── 02-prd.md              G1 — PRD
    ├── 03-wireframe-ui-flow.md  G1 — Wireframe / UI Flow
    ├── management/
    │   └── project-management.xlsx   File quản trị: backlog, user story, eval, biểu đồ
    └── preparation/           Tài liệu nền (00–07): phạm vi, charter, user stories,
                               bài học Vucar, kiến trúc + CI/CD, eval, dữ liệu, câu hỏi mở
```

Khi bắt đầu code sẽ thêm `frontend/`, `backend/`, `data/`, `evals/`.

## Công nghệ dự kiến

| Lớp | Công nghệ |
|---|---|
| Frontend | Next.js (React), deploy Vercel |
| Backend | FastAPI (Python), deploy Render |
| Agent | LangGraph |
| CSDL | Postgres |
| Tính toán | Python thuần, có unit test — LLM không tính số tiền |

Chi tiết và lý do: [Kiến trúc, Prod & CI/CD](docs/preparation/04-kien-truc-prod-cicd.md).

## Cài đặt và chạy

Chưa có code. Phần này sẽ được viết cho Gate 2: yêu cầu hệ thống, các bước cài đặt, biến môi trường, câu hỏi mẫu.

## Nhóm

| Thành viên | GitHub | Vai trò |
|---|---|---|
| | | |
| | | |
| | | |
| | | |

## Ba nguyên tắc của sản phẩm

1. Giá ước tính luôn là **tạm tính**. Giá chính thức do thẩm định viên chốt.
2. Mọi con số tiền do **code** tính và có test. LLM chỉ hỏi, giải thích và điều phối.
3. Thiếu dữ liệu thì nói thẳng, **không bịa số**.
