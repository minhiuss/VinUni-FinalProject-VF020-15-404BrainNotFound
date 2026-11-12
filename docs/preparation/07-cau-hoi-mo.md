# 07 — Câu hỏi mở

Những điểm chưa rõ. Trả lời xong thì ghi đáp án ngay dưới câu hỏi và ghi một dòng vào mục Quyết định của `PROJECT-LOG.md`.

## A. Hỏi mentor / ban tổ chức — chặn tiến độ

1. **Tiêu chí chấm final showdown** là gì và trọng số ra sao? Có giống thang 40 / 25 / 20 / 15 trong charter mẫu không?
2. **Có đối tác (stakeholder) thật không?** Mentor có nối được với một showroom hoặc đại lý xe cũ để lấy giá thẩm định thật cho ≥ 20 ca không? Nếu không, ban tổ chức có chấp nhận nhãn thay thế không (file 05, mục 3.1)?
3. **Mã đề "VF"** có nghĩa là xe mục tiêu phải là xe của một hãng cụ thể không? Nhóm được dùng bảng giá công khai của hãng đó chứ?
4. **Mục pin / trạm sạc / lộ trình** trong đề có bắt buộc không, hay chỉ cần các mục trong danh sách Cơ bản và Nâng cao?
5. **Lịch chính xác:** ngày bắt đầu W1, ngày Demo 1, ngày Demo 2, ngày nộp. Template của mentor là 6 tuần, nhóm đang tính 5 tuần.
6. **Thu thập dữ liệu từ các trang rao vặt** cho mục đích học tập có được chấp nhận không? Có nguồn dữ liệu nào ban tổ chức cấp sẵn không?
7. **Ngân sách:** có hỗ trợ API key hoặc server không (sheet "Đề xuất Hỗ Trợ Teams" trong file charter mẫu)?

## B. Nhóm tự chốt — trước W1

8. Ai là trưởng nhóm? Ai giữ vai trò chính nào (bảng trong file 01)?
9. Mỗi người cam kết bao nhiêu giờ mỗi tuần? Khung giờ nào cả nhóm cùng online?
10. Kênh liên lạc chính? Giờ gửi standup?
11. Trong nhóm ai đã từng dùng FastAPI, React, LangGraph, Docker, GitHub Actions? Chỗ nào không ai biết thì cần dành thời gian học ngay ở Bước 0.
12. File quản trị đặt trên Google Sheets (bản Drive) hay giữ Excel trong repo? Khuyến nghị: Google Sheets, vì 4 người sửa cùng lúc được.
13. Tên sản phẩm?

## C. Sản phẩm — trả lời bằng phỏng vấn ở Bước 0

14. Người muốn bán xe **thực sự làm gì** hôm nay để biết giá? Bước nào làm họ khó chịu nhất? (Phỏng vấn 3–5 người đã từng bán hoặc đổi xe.)
15. Họ có sẵn lòng chụp 4–6 ảnh xe không? Bao nhiêu ảnh là quá nhiều?
16. Thẩm định viên nhìn vào những gì khi định giá? Yếu tố nào làm giá thay đổi nhiều nhất? Họ có tin một con số do máy đưa ra không, và cần thấy gì thì mới tin?
17. Biên giữa giá rao, giá giao dịch và giá thu mua thường là bao nhiêu phần trăm?
18. Khoảng giá rộng bao nhiêu thì khách còn thấy có ích? (± 5%? ± 10%?)

## D. Thứ nhóm đang thiếu

| Thiếu | Vì sao cần | Cách bổ sung |
|---|---|---|
| Dữ liệu giá thật | Không có thì không có US-01 | T-005 trong Bước 0 |
| Người có nghề định giá xe | Hệ số biên, bảng trừ theo hư hỏng, nhãn eval | Qua mentor, hoặc người quen làm showroom / gara |
| Người dùng thật để thử | UAT với người ngoài nhóm từ W3 | Mỗi người mời 1–2 người quen có xe |
| Bảng quy tắc trừ giá theo hư hỏng | Phần tính sau bước vision | Phỏng vấn thợ; tham khảo báo giá sửa chữa |
| Bảng giá lăn bánh + lãi suất tham khảo | US-04, US-08 | Trang công khai của hãng và ngân hàng; ghi ngày lấy |
| Tài liệu chính sách trade-in | RAG | Trang công khai của hãng |
| Kinh nghiệm DevOps | CI/CD ngay từ đầu | Một người nhận vai phụ DevOps, dựng theo file 04 mục 4 |
| Văn bản đồng ý thu thập ảnh | Ràng buộc bảo mật | Một trang thông báo ngắn + ô tick |

## E. Ý tưởng để dành (không làm trong 5 tuần trừ khi dư thời gian)

- Tín hiệu thị trường: số ngày ước tính để bán, xu hướng giá theo tháng.
- Mô hình vision tự huấn luyện trên CarDD.
- Ước tính tiêu hao pin theo lộ trình, bản đồ trạm sạc.
- Xuất báo cáo định giá ra PDF cho khách mang tới showroom.
