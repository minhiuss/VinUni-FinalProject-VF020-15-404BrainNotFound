# PROJECT LOG — VFO2O-15 Trade-in Agent

Nhật ký chung của cả nhóm. **Ai làm gì cũng ghi một dòng**, dù nhỏ. Dòng mới nhất nằm trên cùng của mỗi mục.

Cách ghi: `- DD/MM · Tên · việc đã làm · link (PR, file, ảnh)`

---

## 1. Trạng thái hiện tại

| | |
|---|---|
| Giai đoạn | **Bước 0 — Chuẩn bị** |
| Tình hình | Đúng tiến độ |
| Link prod | chưa có |
| Link repo | chưa có |
| File quản trị (Drive) | chưa tải lên |
| Đang chặn | Chưa có dữ liệu giá; chưa có lịch chính thức; chưa phân vai |

## 2. Bước 0 — Chuẩn bị (làm xong trước W1)

**Đọc và chốt**

- [ ] Cả nhóm đọc hết thư mục `docs/preparation/` và 3 tài liệu Gate 1 trong `docs/`
- [ ] Chốt Project Charter: mục tiêu, phạm vi, vai trò (file 01)
- [ ] Chốt 10 user story và thứ tự 5 tuần (file 02)
- [ ] Trả lời nhóm câu hỏi B trong file 07
- [ ] Gửi nhóm câu hỏi A cho mentor
- [ ] Một người đọc file pptx và docx của mentor, tóm tắt vào mục Nhật ký

**Quản trị**

- [ ] Tải `docs/management/project-management.xlsx` lên Drive chung, mở bằng Google Sheets, kiểm tra công thức và biểu đồ hiện đúng
- [ ] Điền ngày bắt đầu (ô vàng B6), tên thành viên, người phụ trách từng việc Sprint 0 và Sprint 1
- [ ] Tạo kênh chat + kênh standup

**Kỹ thuật**

- [ ] Tạo repo GitHub, bảo vệ nhánh `main`, mời đủ 4 người (T-002)
- [ ] Đăng ký tài khoản: Vercel, Render, Supabase / Neon, Sentry, UptimeRobot, LLM (theo hướng dẫn của mentor)
- [ ] Walking skeleton lên prod: trang chủ gọi được backend, backend đọc được CSDL (T-003)
- [ ] CI chạy trên PR; merge `main` tự deploy; smoke test (T-004)
- [ ] Mỗi người chạy được dự án trên máy mình theo README

**Dữ liệu và người dùng**

- [ ] Thu tay 200 tin rao mẫu, ghi nhận chất lượng từng nguồn (T-005)
- [ ] Chốt danh mục khoảng 10 mẫu xe (T-007)
- [ ] Phỏng vấn 3–5 người từng bán / đổi xe và 1 người trong nghề (T-006)
- [ ] Tính tay khoảng giá cho 3 xe từ dữ liệu mẫu

## 3. Outline 5 tuần (tạm, theo yêu cầu đề bài)

| Tuần | User story | Mục đề bài hoàn thành | Mốc |
|---|---|---|---|
| W1 | US-01 Định giá sơ bộ có cơ sở · US-02 Hỏi lại khi thiếu thông tin | Ước tính giá · cảnh báo tạm tính · xử lý thiếu thông tin · web deploy | M1 |
| W2 | US-03 Ảnh làm giá chính xác hơn · US-04 Chênh lệch + trả góp | Khai ảnh · đánh giá qua ảnh · chênh lệch lên đời | M2 |
| W3 | US-05 Đặt lịch · US-06 Baseline cho thẩm định viên | Đặt lịch · 2 vai trò · HITL chốt giá | M3 · **Demo 1** |
| W4 | US-07 Tracker · US-08 Gợi ý xe + TCO | Tracker · đề xuất mẫu xe · engine TCO + agent tư vấn | M4 |
| W5 | US-09 Đo sai lệch giá · US-10 Dashboard chuyển đổi | Eval ≥ 20 ca · dashboard | M5 · **Demo 2** |

Chi tiết từng việc: sheet Backlog. Chi tiết nghiệm thu: file 02.

Nhịp mỗi tuần: Thứ Hai chốt story và spec → Thứ Ba đến Thứ Sáu code, merge và deploy hằng ngày → Thứ Bảy UAT 4 người trên prod, cập nhật file quản trị, viết báo cáo tuần.

## 4. Nhật ký hằng ngày

### Tuần chuẩn bị

- 12/11 · zMerkurias · Bộ nộp Gate 1 (bản nháp): Brief, PRD, Wireframe / UI Flow trong `docs/`; sắp xếp lại thư mục thành cấu trúc repo; thêm README, GUIDE, CONTRIBUTING, CHANGELOG, mẫu PR, `ai-logs/`. Đẩy lên nhánh `zMerkurias`. **Chưa xong:** phần AI Log chưa đối chiếu Technical Book (portal cần đăng nhập). Hạn G1: 23:59 ngày 15/11.

- 12/11 · (khởi tạo) · Tạo thư mục dự án, bộ tài liệu Bước 0 (file 00–07), file quản trị Excel và log này. Đã đọc 3 tài liệu mentor (template quản trị, charter + mẫu báo cáo, slide QTDA) và khảo sát dinhgiaxe.vucar.vn.

<!-- Mẫu standup, copy mỗi ngày:
- DD/MM · Tên
  - Hôm qua:
  - Hôm nay:
  - Kẹt:
-->

## 5. Release log

Mỗi lần deploy lên prod một dòng. Bản đầy đủ nằm ở sheet **Release log**.

| Ngày | Phiên bản | Thay đổi | US / Bug | PR | Người deploy |
|---|---|---|---|---|---|
| | | | | | |

## 6. Quyết định

Ghi lại mỗi quyết định ảnh hưởng tới cả nhóm, kèm lý do, để sau này không cãi lại.

| Ngày | Quyết định | Lý do | Người chốt |
|---|---|---|---|
| 12/11 | (đề xuất, chờ nhóm duyệt) Sản phẩm trả về khoảng giá, không trả một con số | Thể hiện đúng độ không chắc chắn; khớp ràng buộc "tạm tính" | |
| 12/11 | (đề xuất) LLM không tính số; mọi con số đi ra từ engine có test | Ràng buộc của đề | |
| 12/11 | (đề xuất) Giới hạn khoảng 10 mẫu xe phổ biến | Dữ liệu đủ dày quan trọng hơn phủ rộng | |
| 12/11 | (đề xuất) Vercel + Render + Postgres miễn phí; nâng gói Render trong tuần demo | Đề gợi ý; chi phí 0–20 USD cho 2 tháng | |

## 7. Rủi ro và vướng mắc đang mở

| Ngày | Vấn đề | Ai xử lý | Trạng thái |
|---|---|---|---|
| 12/11 | Chưa có nguồn giá thẩm định thật cho ≥ 20 ca eval | | Mở |
| 12/11 | Dữ liệu chợ xe là giá rao, cần hệ số quy đổi sang giá thu mua | | Mở |
| 12/11 | Template mentor 6 tuần, nhóm tính 5 tuần — cần xác nhận lịch | | Mở |

## 8. Báo cáo tuần

Theo mẫu của mentor: tiến độ · số liệu · vướng mắc · kế hoạch tuần sau · bằng chứng (ảnh chụp, link).

<!-- ### Tuần W1 (DD/MM – DD/MM)
**Tiến độ:**
**Số liệu:** story xong x/y · lỗi mở n · số lần release n · trạng thái deploy
**Vướng mắc:**
**Tuần sau:**
**Bằng chứng:**
-->
