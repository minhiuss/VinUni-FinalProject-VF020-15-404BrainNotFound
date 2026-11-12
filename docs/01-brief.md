# Brief — AI Agent hỗ trợ đổi xe cũ (Trade-in)

**Mã đề:** VFO2O-15 · **Nhóm:** 404BrainNotFound (4 thành viên) · **Phiên bản:** 1.0 — 12/11/2026

## Vấn đề

Người muốn đổi xe cũ lấy xe điện không biết xe mình đáng bao nhiêu. Mỗi showroom báo một giá và không ai giải thích căn cứ, nên khách e ngại và giao dịch kéo dài. Phía nhân viên cũng không có mức tham chiếu trung lập: giá phụ thuộc kinh nghiệm từng người và khó giải thích với khách.

## Người dùng

| Ai | Họ cần gì |
|---|---|
| **Khách** muốn bán / đổi xe | Một khoảng giá có căn cứ trong vài phút, và biết bước tiếp theo |
| **Thẩm định viên** / nhân viên tư vấn | Một baseline trung lập kèm bằng chứng, để chốt giá nhanh và nhất quán |

## Giải pháp

Một web app đặt ra **một mức giá cơ sở chung cho cả hai phía**:

1. Khách khai thông tin xe và chụp ảnh. Agent hỏi lại khi thiếu thông tin.
2. Hệ thống trả về **khoảng giá thu mua tạm tính**, kèm xe tương đồng, nguồn dữ liệu và từng dòng điều chỉnh theo tình trạng.
3. Khách xem **số tiền cần bù** để lên đời xe điện và lịch trả góp, rồi **đặt lịch thẩm định**.
4. Thẩm định viên mở hồ sơ, thấy baseline và cơ sở tính, kiểm tra xe thật rồi **chốt giá chính thức**.

## Điểm khác biệt

- **Ảnh và tình trạng xe đi vào giá.** Công cụ định giá hiện có trên thị trường chỉ hỏi hãng, đời, km, nên hai xe cùng đời ra cùng một giá.
- **Phục vụ cả nhân viên**, không chỉ người bán.
- **Giải thích được từng con số.** Mọi phép tính chạy bằng code có test; LLM chỉ hỏi, giải thích và điều phối.

## Nguyên tắc không thương lượng

- Giá ước tính luôn ghi rõ **tạm tính**. Giá chính thức chỉ có khi thẩm định viên bấm chốt.
- LLM không tự tính số tiền.
- Ảnh và thông tin khách được lưu riêng tư, mã hóa.
- Thiếu dữ liệu thì nói "chưa ước tính được", không bịa số.

## Phạm vi MVP (Gate 2)

Một luồng chạy thật từ đầu đến cuối: khách nhập thông tin xe → nhận khoảng giá có cơ sở và cảnh báo tạm tính → agent hỏi lại khi thiếu thông tin. Giới hạn khoảng 10 mẫu ô tô phổ biến.

**Không làm:** xe máy, xe tải, định giá chính thức tự động, tích hợp ngân hàng, app native.

## Đo thành công

| Chỉ số | Mục tiêu |
|---|---|
| Thời gian khách có khoảng giá | Dưới 3 phút trên điện thoại |
| Sai lệch trung bình so với giá thẩm định | ≤ 15% trên ≥ 20 ca |
| Giá thẩm định nằm trong khoảng đã báo | ≥ 70% số ca |
| Yêu cầu đề bài đạt trên production | 9/9 Cơ bản, ≥ 4/6 Nâng cao |

Các ngưỡng là bản nháp, chốt lại sau lần đo đầu tiên.

## Công nghệ

React (Next.js) trên Vercel · FastAPI trên Render · Postgres · LangGraph · model đa phương thức cho ảnh · engine định giá, trả góp, TCO viết bằng Python thuần.

## Rủi ro lớn nhất

Dữ liệu thu được là **giá rao**, trong khi đề yêu cầu **giá thu mua**, và nhóm chưa có nguồn giá thẩm định thật cho 20 ca eval. Cách xử lý: thu mẫu dữ liệu ngay trong tuần chuẩn bị, phỏng vấn người trong nghề để lấy hệ số quy đổi, và nhờ mentor kết nối đại lý.

---

Chi tiết: [PRD](02-prd.md) · [Wireframe / UI Flow](03-wireframe-ui-flow.md) · [Tài liệu chuẩn bị](preparation/)
