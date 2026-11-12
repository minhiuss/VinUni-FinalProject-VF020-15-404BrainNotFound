# 06 — Kế hoạch dữ liệu

Dữ liệu giá là rủi ro lớn nhất của dự án. Phải có mẫu thật **trước W1**, nếu không US-01 không làm được.

## 1. Ba loại giá — đừng nhầm

| Loại giá | Là gì | Lấy được ở đâu |
|---|---|---|
| Giá rao | Giá người bán đăng trên chợ xe | Các trang rao vặt, công khai |
| Giá giao dịch | Giá hai bên thực sự chốt | Hầu như không công khai |
| **Giá thu mua** | Giá đại lý / hãng trả cho khách khi trade-in | Không công khai; thấp hơn giá rao vì đại lý còn chi phí tân trang và lợi nhuận |

Đề yêu cầu ước tính **giá thu mua**. Thứ nhóm thu được là **giá rao**. Vì vậy engine cần hai bước rõ ràng:

```
giá rao trung vị của xe tương đồng
   → trừ biên thương lượng (giá rao → giá giao dịch)
   → trừ biên đại lý (giá giao dịch → giá thu mua)
   → trừ điều chỉnh tình trạng
= khoảng giá thu mua tạm tính
```

Hai hệ số biên phải có nguồn (phỏng vấn người trong nghề, hoặc suy ra từ các ca thẩm định thật) và hiển thị cho người dùng. Đây là câu hỏi cần đem đi phỏng vấn ở Bước 0.

## 2. Đánh giá các nguồn nhóm đã nghĩ tới

| Nguồn | Có gì | Khả thi | Ghi chú |
|---|---|---|---|
| Chợ xe cũ trực tuyến (Bonbanh, Chợ Tốt Xe, Oto.com.vn, Carmudi…) | Hãng, dòng, đời, phiên bản, km, giá rao, khu vực, mô tả | **Cao** — nguồn chính | Đọc điều khoản sử dụng và `robots.txt` của từng trang; lấy tần suất thấp; chỉ lấy thông tin xe, **không** lấy tên và số điện thoại người rao |
| Trung tâm đăng kiểm | Thông số kỹ thuật, lịch sử kiểm định | **Thấp** | Không có dữ liệu giá, và dữ liệu theo từng xe không mở cho công chúng. Chỉ dùng được nếu có đối tác cấp |
| Forum, nhóm Facebook | Kinh nghiệm, giá tham khảo, lỗi thường gặp theo dòng xe | Trung bình | Lộn xộn, khó chuẩn hóa. Hợp để làm tài liệu cho RAG hơn là bảng giá |
| Bảng giá xe mới của hãng | Giá niêm yết, phiên bản | **Cao** | Cần cho chênh lệch lên đời và làm mốc khấu hao |
| Đại lý / showroom (qua mentor) | Giá thu mua thật, giá thẩm định | Phụ thuộc quan hệ | Giá trị nhất; chỉ cần 20–50 ca là đủ cho eval và hiệu chỉnh hệ số biên |
| Bộ dữ liệu công khai (CarDD…) | Ảnh hư hỏng xe đã gán nhãn | **Cao** | Cho phần vision; xe trong ảnh không phải xe Việt Nam nhưng loại hư hỏng thì giống |
| Bộ "Used Car Valuation" nước ngoài | Giá xe cũ thị trường khác | Thấp | Không dùng được cho giá Việt Nam; chỉ tham khảo cách dựng mô hình |

## 3. Cần bao nhiêu

Không cần nhiều; cần **đủ dày cho từng mẫu xe**.

| Hạng mục | Mục tiêu | Lý do |
|---|---|---|
| Số mẫu xe hỗ trợ | Khoảng 10 mẫu phổ biến | Mẫu phổ biến có nhiều tin rao; khách đổi xe cũng chủ yếu đi các mẫu này |
| Tin rao mỗi mẫu | 150–300, trải nhiều đời và mức km | Sau khi lọc theo đời ± 1 và phiên bản vẫn còn 15–30 xe tương đồng |
| Tổng tin rao sạch | 2.000–3.000 | Đủ cho MVP |
| Ca có giá thẩm định thật | ≥ 20 (đề yêu cầu), nhắm 30–50 | Eval + hiệu chỉnh hệ số biên |
| Ảnh gán nhãn cho eval vision | 40–60 | Mục 3.2 file 05 |
| Bảng xe mới mục tiêu | Toàn bộ mẫu và phiên bản của hãng mục tiêu | Chênh lệch, trả góp, TCO |
| Tài liệu chính sách trade-in | 5–15 tài liệu | RAG |

Nếu một mẫu xe không đủ 50 tin sạch thì loại khỏi danh mục hỗ trợ, thay vì cố ước tính.

## 4. Lược đồ tối thiểu cho một tin rao

`source`, `source_url`, `collected_at`, `brand`, `model`, `year`, `variant`, `mileage_km`, `asking_price_vnd`, `province`, `transmission`, `fuel`, `color`, `posted_at`

Không lưu tên, số điện thoại, địa chỉ của người rao.

## 5. Quy trình làm sạch

1. **Chuẩn hóa tên:** một bảng danh mục chuẩn (hãng → dòng → đời → phiên bản). Mọi tin rao phải khớp vào bảng này; không khớp thì loại. Wizard của khách dùng chính bảng này, nên đầu vào của khách luôn khớp được với database.
2. **Lọc trùng:** cùng xe đăng nhiều nơi hoặc đăng lại nhiều lần.
3. **Lọc ngoại lai:** giá gõ nhầm đơn vị, tin "giá liên hệ", km bằng 0 ở xe đời cũ, giá lệch quá xa trung vị của nhóm.
4. **Ghi phiên bản dữ liệu:** mỗi lần cập nhật là một phiên bản có ngày. Trang kết quả hiện ngày này cho khách.
5. **Báo cáo chất lượng:** mỗi mẫu xe còn bao nhiêu tin sau lọc, loại vì lý do gì.

## 6. Việc ở Bước 0 (T-005, T-007)

- [ ] Mỗi người lấy tay 50 tin của 2–3 mẫu xe từ một nguồn khác nhau → gộp thành 200 tin mẫu.
- [ ] Ghi nhận cho từng nguồn: trường nào có, trường nào thiếu, tên xe viết lộn xộn đến mức nào, điều khoản có cho phép thu thập không.
- [ ] Chốt danh mục khoảng 10 mẫu xe dựa trên số tin tìm được.
- [ ] Thử tính tay khoảng giá cho 3 xe từ 200 tin đó — nếu tính tay không ra số hợp lý thì code cũng không ra.
- [ ] Đem câu hỏi "biên đại lý bao nhiêu phần trăm" đi phỏng vấn (T-006).
