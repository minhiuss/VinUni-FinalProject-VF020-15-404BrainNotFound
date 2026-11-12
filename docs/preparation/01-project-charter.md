# 01 — Project Charter (nháp)

Theo mẫu `Template Project Charter + Mẫu báo cáo.xlsx`. Các ô `[...]` nhóm tự điền. Bản này cần cả nhóm chốt trước W1.

## 1. Thông tin

| | |
|---|---|
| Tên dự án | AI Agent hỗ trợ đổi xe cũ (Trade-in) — VFO2O-15 |
| Nhóm | [Tên nhóm] · 4 thành viên |
| Thời gian | 5 tuần · bắt đầu [DD/MM/YYYY] |
| Phiên bản | 0.1 (nháp) |

## 2. Vấn đề và mục tiêu

**Vấn đề.** Người muốn bán hoặc đổi xe không biết xe mình đáng bao nhiêu. Mỗi showroom báo một giá, không ai giải thích căn cứ. Phía nhân viên cũng thiếu một mức tham chiếu trung lập, nên báo giá phụ thuộc kinh nghiệm cá nhân và khó giải thích với khách.

**Giải pháp.** Một web app đặt ra **một mức giá cơ sở chung cho cả hai phía**:

- *Giai đoạn 1 — khách:* khai thông tin + ảnh → nhận khoảng giá thu mua tạm tính, có cơ sở tính, có cảnh báo → xem chênh lệch lên đời xe điện → đặt lịch thẩm định.
- *Giai đoạn 2 — thẩm định viên:* nhận hồ sơ kèm baseline và cơ sở tính → kiểm tra xe thật → chốt giá chính thức.

**Mục tiêu SMART (nháp, chờ nhóm chốt số):**

1. Khách hoàn tất định giá sơ bộ trong **dưới 3 phút** trên điện thoại.
2. Sai lệch trung bình giữa điểm giữa khoảng giá ước tính và giá thẩm định **≤ 15%** trên **≥ 20 ca**.
3. **≥ 70%** số ca có giá thẩm định nằm trong khoảng giá đã báo.
4. Đủ 9/9 mục Cơ bản và ≥ 4/6 mục Nâng cao chạy trên production trước Demo 2.
5. Release lên production **ít nhất 3 lần mỗi tuần**, mỗi lần có dòng trong Release log.

## 3. Khách hàng

| Nhóm | Pain point | Sản phẩm đưa cho họ |
|---|---|---|
| Người muốn bán / đổi xe (GĐ1) | Không biết giá hợp lý; sợ bị ép giá; quy trình chậm | Khoảng giá có căn cứ trong vài phút; bước tiếp theo rõ ràng |
| Nhân viên tư vấn / thẩm định viên (GĐ2) | Không có mức tham chiếu trung lập; khó giải thích giá với khách | Baseline + xe tương đồng + tình trạng từ ảnh, để chốt giá nhanh và nhất quán |

## 4. Vai trò (đề xuất, nhóm tự gán tên)

| Vai trò chính | Vai trò phụ | Chịu trách nhiệm |
|---|---|---|
| Trưởng nhóm / Product | QA + UAT | File quản trị, user story, demo, báo cáo |
| Backend + engine định giá | DevOps | FastAPI, Postgres, các công thức tính, CI/CD |
| Frontend | UX + thử đa thiết bị | Wizard, trang kết quả, màn thẩm định viên, tracker |
| AI + dữ liệu | Eval | Agent LangGraph, vision, thu và làm sạch dữ liệu, bộ eval |

Vai trò là để biết **ai chịu trách nhiệm cuối**, không phải ranh giới. User story là của cả nhóm: nó chỉ xong khi 4 người đều chạy qua UAT.

## 5. Cột mốc

| Mốc | Tuần | Kết quả |
|---|---|---|
| M0 | Trước W1 | Charter chốt, repo + CI/CD, trang rỗng chạy trên prod, mẫu dữ liệu 200 tin |
| M1 | W1 | Định giá sơ bộ dùng được trên prod |
| M2 | W2 | Ảnh → tình trạng → giá; chênh lệch + trả góp |
| M3 | W3 | **Demo 1** — luồng khách → thẩm định viên chốt giá (xong ~80%) |
| M4 | W4 | Sửa theo phản hồi; tracker, TCO, gợi ý xe |
| M5 | W5 | **Demo 2** — hoàn thiện, eval ≥ 20 ca, dashboard |

## 6. Nguồn lực

- Nhân sự: 4 người × [giờ/tuần].
- Công cụ miễn phí: GitHub, Vercel, Render, Supabase, Sentry, UptimeRobot, gói miễn phí của LLM.
- Chi phí có thể phát sinh: xem file 04 (ước tính 0–20 USD cho 2 tháng).

## 7. Rủi ro

| # | Rủi ro | Xác suất | Tác động | Cách xử lý |
|---|---|---|---|---|
| 1 | Không lấy được dữ liệu giá đủ sạch | Cao | Cao | Thu mẫu 200 tin ngay ở Bước 0; thu hẹp còn 10 mẫu xe; có phương án nhập tay |
| 2 | Giá rao ≠ giá giao dịch ≠ giá thu mua | Cao | Cao | Ghi rõ đang ước tính loại giá nào; trừ biên đại lý bằng hệ số có ghi nguồn |
| 3 | Không có thẩm định viên thật cho 20 ca eval | Trung bình | Cao | Hỏi mentor nối đối tác; phương án dự phòng trong file 05 |
| 4 | Vision đoán sai tình trạng | Cao | Trung bình | Ảnh chỉ điều chỉnh trong biên hẹp; luôn cho người dùng sửa; thẩm định viên quyết |
| 5 | Phình phạm vi (pin, trạm sạc, nhiều hãng) | Cao | Cao | Sprint đã chốt thì không thêm US; mục ngoài phạm vi ghi vào file 07 |
| 6 | Gói miễn phí ngủ / chậm lúc demo | Trung bình | Cao | Ping giữ thức; nâng gói trả phí trong tuần demo |
| 7 | Chi phí LLM / vision vượt | Thấp | Trung bình | Nén ảnh, giới hạn số ảnh, cache, đo chi phí mỗi yêu cầu |
| 8 | Thu thập dữ liệu vi phạm điều khoản trang nguồn | Trung bình | Trung bình | Chỉ lấy trường công khai, tần suất thấp, không lấy thông tin cá nhân người rao; hỏi mentor |

## 8. Tiêu chí thành công

Theo charter mẫu của mentor: sản phẩm chạy với dữ liệu thật 40% · mức hài lòng của đối tác 25% · chất lượng code và tài liệu 20% · làm việc nhóm 15%. **Cần xác nhận lại với mentor** xem final showdown có dùng đúng thang này không.

## 9. Quy chế làm việc (rút gọn)

- Standup hằng ngày bằng tin nhắn: hôm qua / hôm nay / kẹt gì. Ghi vào `PROJECT-LOG.md`.
- Mỗi việc 1 người chịu trách nhiệm, 1 hạn chót. Sắp trễ thì báo trước ít nhất 4 giờ.
- Mọi thay đổi code đi qua PR, có ít nhất 1 người review. PR dưới 400 dòng.
- Bất đồng kỹ thuật: người phụ trách mảng đó quyết. Bất đồng phạm vi: trưởng nhóm quyết.
- Nói thật về tiến độ. Chạy được quan trọng hơn hoàn hảo.
