# 00 — Đề bài & Phạm vi

**Mã đề:** VFO2O-15 · **Lĩnh vực:** Ô tô & Xe điện – Kinh doanh O2O · **Tên:** AI Agent hỗ trợ chương trình đổi xe cũ (Trade-in)

## 1. Đề bài tóm tắt

- **Thực trạng:** khách muốn đổi xe cũ lấy xe điện của hãng, nhưng định giá xe cũ chậm, thiếu minh bạch, mỗi nơi báo một giá → khách e ngại, giao dịch kéo dài.
- **Bài toán:** agent hướng dẫn khách khai thông tin xe (hãng, đời, km, tình trạng, ảnh) → ước tính giá thu mua sơ bộ → tính chênh lệch lên đời (gồm trả góp) → đặt lịch thẩm định → theo dõi tiến trình. Kết hợp mô-đun tính toán xác định (TCO 5 năm, trả góp, khấu hao, tiêu hao pin) với tư vấn của agent.
- **Ràng buộc:**
  1. Giá ước tính luôn kèm cảnh báo **tạm tính**; giá chính thức do **thẩm định viên** quyết (HITL bắt buộc).
  2. Dữ liệu định giá từ nguồn kiểm soát; minh bạch cơ sở định giá.
  3. Bảo mật thông tin xe và khách; ảnh lưu mã hóa.
  4. Kiểm soát chi phí xử lý ảnh / LLM.
  5. **Mọi phép tính** (giá lăn bánh, trả góp, TCO, pin) chạy bằng công thức code có kiểm chứng. **LLM không được tự tính số.**
- **Gợi ý công nghệ của đề:** LangGraph, LLM + vision, tool định giá (rule + dữ liệu thị trường), RAG bảng giá và chính sách, FastAPI + Postgres, React (wizard + tracker), Vercel + Render.

## 2. Checklist chấm điểm

Bản theo dõi trạng thái nằm ở sheet **Checklist đề bài** trong file quản trị.

**Cơ bản (bắt buộc đủ 9 mục)**

- [ ] Web deploy công khai
- [ ] 2 vai trò: khách / thẩm định viên
- [ ] Khai thông tin + ảnh xe cũ
- [ ] Ước tính giá thu mua
- [ ] Tính chênh lệch lên đời
- [ ] Đặt lịch thẩm định
- [ ] HITL: thẩm định viên chốt giá
- [ ] Cảnh báo giá tạm tính
- [ ] Xử lý thiếu thông tin

**Nâng cao**

- [ ] Đánh giá tình trạng qua ảnh
- [ ] Đề xuất mẫu xe hợp ngân sách sau trade-in
- [ ] Tracker tiến trình
- [ ] Eval sai lệch giá ước tính vs giá thẩm định ≥ 20 ca
- [ ] Dashboard tỷ lệ trade-in chuyển đổi
- [ ] Engine TCO / lộ trình năng lượng / định giá kết hợp agent tư vấn cá nhân hóa

## 3. Hướng đi của nhóm so với đề

| Ý của nhóm | Khớp với đề ở đâu | Lưu ý |
|---|---|---|
| Giai đoạn 1: phục vụ khách muốn bán / đổi xe | Vai trò "khách" | Khớp |
| Giai đoạn 2: baseline trung lập cho nhân viên báo giá | Vai trò "thẩm định viên" + HITL | Khớp, và là điểm khác biệt so với Vucar (họ chỉ phục vụ người bán) |
| MVP chính: hỗ trợ định giá từ thông tin + ảnh, đối chiếu database | "Ước tính giá thu mua", "khai thông tin + ảnh" | Khớp |
| Sub-MVP: computer vision xác định tình trạng | Nâng cao "đánh giá tình trạng qua ảnh" | Khớp |

**Khoảng trống cần lưu ý.** Ý tưởng hiện tại của nhóm xoay quanh *định giá*. Nhưng 4 mục **Cơ bản** của đề nằm ngoài định giá: tính chênh lệch lên đời, đặt lịch thẩm định, 2 vai trò, HITL chốt giá. Thiếu các mục này là thiếu điểm cơ bản. Kế hoạch 5 tuần trong file 02 đã xếp chúng vào W2–W3 ở mức mỏng nhưng chạy được.

## 4. Phạm vi đề xuất

| Làm (in-scope) | Không làm (out-of-scope) |
|---|---|
| Ô tô con cá nhân, khoảng 10 mẫu phổ biến, đời 2015 trở lại đây | Xe máy, xe tải, xe hiếm, xe nhập ít dữ liệu |
| Khoảng giá thu mua tạm tính + cơ sở tính | Giá chính thức tự động (trái ràng buộc HITL) |
| Tình trạng ngoại thất qua ảnh | Chẩn đoán máy, gầm, điện qua ảnh |
| Chênh lệch + trả góp + TCO 5 năm bằng công thức | Tích hợp ngân hàng, duyệt vay thật |
| Đặt lịch thẩm định trong hệ thống | Đồng bộ lịch showroom thật, thanh toán |
| Xe mục tiêu: các mẫu xe điện của một hãng (theo mã đề "VF") | So sánh nhiều hãng xe mới |
| Web chạy tốt trên điện thoại | App native |
| *Chờ hỏi mentor:* ước tính tiêu hao pin theo địa hình / thời tiết, trạm sạc theo lộ trình | — |

Mục pin / trạm sạc có trong đề nhưng xa pain point chính (định giá thiếu minh bạch). Đề xuất: chỉ làm nếu W4 còn dư thời gian, và hỏi mentor xem có bắt buộc không (xem file 07).
