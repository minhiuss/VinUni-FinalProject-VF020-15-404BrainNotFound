# 03 — Bài học từ dinhgiaxe.vucar.vn

Khảo sát ngày 12/11/2026 bằng cách dùng trang như một khách bình thường (trang chủ, wizard, trang kết quả, FAQ). Mục đích là học cách họ giải bài toán, **không sao chép** giao diện, nội dung hay dữ liệu.

## 1. Họ làm gì

**Luồng chính:** nút "Định giá ngay" → wizard 7 bước → trang kết quả.

| Bước | Trường |
|---|---|
| 1–4 | Hãng → Dòng → Đời → Phiên bản (chọn lần lượt, bước sau lọc theo bước trước) |
| 5 | Màu xe |
| 6 | Công tơ mét |
| 7 | Nhu cầu định giá (để bán, để mua, hay chỉ xem) |

**Trang kết quả** (ví dụ Toyota Vios 1.5G 2015, 157.000 km):

- Một **khoảng giá** hẹp (225–235 triệu), ghi "ước tính dựa trên AI và dữ liệu thị trường".
- Ước tính **số ngày để bán** ở mức giá đó, và **số người mua đang tìm** mẫu này.
- Ghi rõ nguồn dữ liệu: Bonbanh, Chợ Tốt, Oto.com.vn, TikTok, Facebook Marketplace và các nhóm mua bán.
- Danh sách **xe tương đồng** đang rao (giá, màu, ngày đăng, link tới tin gốc).
- **Trượt giá** theo năm và giá trị dự phóng sau 5 năm.
- Các nút chuyển đổi: "Bán xe ngay", "Khám xe 0 đồng" (đặt lịch kiểm định tận nơi), "Nhận báo cáo giá thị trường".

**Trang chủ ngoài wizard:** xe vừa được định giá, xe được định giá nhiều nhất, bảng biến động giá 1/3/6 tháng, top xe trượt giá nhanh, cùng các công cụ phụ để kéo người dùng (định giá biển số, tra phạt nguội, từ điển lỗi xe).

**FAQ đáng chú ý:**

- Phân biệt **giá mua** (giá showroom bán ra) và **giá bán** (giá đại lý thu vào); chênh lệch do chi phí tân trang.
- Tự công bố độ chính xác "lên tới 90%" và thừa nhận có ca lệch so với giao dịch thật.
- Có câu "Tại sao xe của tôi không định giá được?" — tức là họ chấp nhận có xe không ra kết quả.

**Kỹ thuật quan sát được:** Next.js (App Router); trang kết quả mang toàn bộ đầu vào trên URL (`/ket-qua?brand=...&model=...&mileage=...`) nên chia sẻ được; gắn Google Analytics, Microsoft Clarity, Facebook Pixel, TikTok Pixel.

## 2. Những gì nhóm học được

| # | Bài học | Áp dụng cho dự án |
|---|---|---|
| 1 | Trả về **khoảng giá**, không trả một con số | US-01. Khoảng giá thể hiện đúng độ không chắc chắn và khớp ràng buộc "tạm tính" |
| 2 | **Chọn lần lượt** hãng → dòng → đời → phiên bản, không cho gõ tự do | Dữ liệu vào sạch, khớp được với database. Cần một bảng danh mục xe chuẩn hóa ngay từ đầu |
| 3 | **Chỉ ra nguồn** và cho xem **xe tương đồng** kèm link | Đây chính là "minh bạch cơ sở định giá" của đề. Bằng chứng thuyết phục hơn lời khẳng định |
| 4 | Phân biệt **giá rao / giá bán / giá thu mua** | Đề yêu cầu *giá thu mua*. Dữ liệu chợ xe là *giá rao*. Phải có bước quy đổi rõ ràng, có ghi hệ số (xem file 06) |
| 5 | Định giá miễn phí là **mồi**; đích đến là đặt lịch kiểm định | Giống luồng của đề: ước tính → đặt lịch thẩm định. Đặt nút đặt lịch ngay cạnh kết quả |
| 6 | Hỏi **nhu cầu** của người dùng ở bước cuối | Biết khách muốn bán thẳng hay đổi xe để rẽ sang luồng chênh lệch lên đời |
| 7 | Chấp nhận **"không định giá được"** | US-01 tiêu chí 5: thiếu dữ liệu thì nói thẳng, không bịa |
| 8 | Kết quả **chia sẻ được** bằng link | Hữu ích cho khách gửi người nhà. Nhóm nên dùng mã hồ sơ thay vì nhét dữ liệu vào URL, vì hồ sơ của nhóm có ảnh và số điện thoại |
| 9 | Gắn **đo lường hành vi** từ đầu | Cần cho dashboard chuyển đổi (US-10). Clarity miễn phí, xem lại được phiên người dùng |
| 10 | Thêm tín hiệu **thị trường** (số ngày bán, số người tìm, trượt giá) | Ý hay cho W4–W5 nếu dư thời gian; không phải lõi |
| 11 | Tự công bố **độ chính xác** | Nhóm nên công bố số đo thật từ bộ eval ≥ 20 ca thay vì một con số quảng cáo |

## 3. Chỗ họ để trống — cơ hội của nhóm

1. **Không hỏi tình trạng xe, không nhận ảnh.** Hai xe cùng đời cùng km ra cùng một giá. Đây là đúng chỗ MVP chính và sub-MVP của nhóm nhắm vào.
2. **Chỉ phục vụ người bán.** Không có màn hình cho nhân viên / thẩm định viên. Giai đoạn 2 của nhóm là phần mới.
3. **Không có bài toán lên đời.** Không tính chênh lệch, trả góp hay TCO.
4. **Giải thích còn mỏng.** Có xe tương đồng nhưng không cho thấy từng yếu tố (km, màu, tình trạng) cộng trừ bao nhiêu.
5. **Số liệu có chỗ không nhất quán.** Ở ca Vios ở trên, trang báo trượt giá −9%/năm nhưng giá trị "sau 5 năm" (khoảng 252 triệu) lại cao hơn giá hiện tại (225–235 triệu). Xe tương đồng rẻ nhất đang rao 255 triệu, cao hơn cả đầu trên của khoảng giá, mà trang không giải thích khoảng cách này. Bài học: mọi con số hiển thị phải đi ra từ cùng một engine có test, và phải giải thích được quan hệ giữa chúng.

## 4. Điều không nên bắt chước

- Các công cụ phụ kéo traffic (biển số, phạt nguội, "định mệnh xe"): ngoài phạm vi.
- Tín hiệu thúc ép kiểu "đang có N người mua" khi không có dữ liệu thật đứng sau.
- Lấy nội dung, hình ảnh hoặc dữ liệu của họ.
