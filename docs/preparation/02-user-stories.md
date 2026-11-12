# 02 — User Stories

Khuôn: **Với vai trò [ai], tôi muốn [tính năng], để [lợi ích].**

Quy tắc của nhóm:

- Mỗi tuần 2–3 story, trong đó 1–2 story **sâu**. Story đã chốt cho sprint thì không thêm, không bớt.
- Một story ≈ 2–3 ngày dev. Lớn hơn thì cắt.
- **Xong** nghĩa là: đã deploy lên prod, cả 4 người chạy qua UAT trên thiết bị của mình, có dòng trong Release log.
- Story sâu phải có spec (Động lực → Thiết kế → Kế hoạch) trước khi code.

## Bản đồ 5 tuần

| Tuần | Story | Sâu | Mục đề bài được đáp ứng |
|---|---|---|---|
| W1 | US-01, US-02 | US-01 | Ước tính giá, cảnh báo tạm tính, xử lý thiếu thông tin |
| W2 | US-03, US-04 | US-03 | Ảnh xe, đánh giá tình trạng qua ảnh, chênh lệch lên đời |
| W3 | US-05, US-06 | US-06 | Đặt lịch, 2 vai trò, HITL chốt giá → **Demo 1** |
| W4 | US-07, US-08 | US-08 | Tracker, gợi ý xe theo ngân sách, TCO |
| W5 | US-09, US-10 | — | Eval ≥ 20 ca, dashboard chuyển đổi → **Demo 2** |

---

## US-01 — Định giá sơ bộ có cơ sở · W1 · SÂU

> Với vai trò **người muốn bán / đổi xe**, tôi muốn **nhập thông tin xe và nhận một khoảng giá thu mua kèm cơ sở tính**, để **biết xe mình đáng bao nhiêu trước khi ra showroom và không bị mỗi nơi báo một giá**.

**Pain point:** khách không có mốc tham chiếu nên không biết giá nào là hợp lý.

**Tiêu chí nghiệm thu (UAT)**

1. *Cho* xe thuộc danh mục hỗ trợ, *khi* nhập đủ hãng, dòng, đời, phiên bản, km, *thì* thấy một **khoảng giá** (thấp – cao), không phải một con số.
2. Trang kết quả hiện: số xe tương đồng đã dùng, nguồn dữ liệu, ngày cập nhật dữ liệu, và ít nhất 3 xe tương đồng.
3. Cảnh báo **"Giá tạm tính — giá chính thức do thẩm định viên quyết định"** nằm ngay cạnh con số, không cần cuộn.
4. Cùng một đầu vào cho ra cùng một kết quả (tính bằng code, không qua LLM).
5. *Cho* xe ngoài danh mục hoặc quá ít dữ liệu, *thì* báo rõ "chưa đủ dữ liệu để ước tính" và mời đặt lịch thẩm định. Không được bịa số.
6. Từ lúc mở trang đến lúc thấy giá dưới 3 phút trên điện thoại, mạng 4G.

**Không làm trong story này:** ảnh, đăng nhập, trả góp.

## US-02 — Hỏi lại khi thiếu thông tin · W1

> Với vai trò **người muốn bán / đổi xe**, tôi muốn **được hỏi lại đúng thông tin còn thiếu thay vì bị báo lỗi**, để **hoàn tất định giá dù không rành thông số xe**.

**UAT**

1. Bỏ trống phiên bản → hệ thống đưa danh sách phiên bản của đúng dòng và đời đó để chọn, có lựa chọn "Tôi không rõ".
2. Chọn "Tôi không rõ" → vẫn có kết quả, nhưng khoảng giá rộng hơn và có ghi chú lý do.
3. Nhập mâu thuẫn (ví dụ xe đời 2023 đi 400.000 km) → hệ thống hỏi xác nhận lại, không tự sửa.
4. Agent chỉ **hỏi và giải thích**; mọi con số trong câu trả lời lấy từ kết quả của engine.

## US-03 — Ảnh làm giá chính xác hơn · W2 · SÂU

> Với vai trò **người muốn bán / đổi xe**, tôi muốn **chụp ảnh xe để hệ thống ghi nhận tình trạng và điều chỉnh giá**, để **giá ước tính sát với xe thật của tôi, không phải giá chung của cả dòng xe**.

**Pain point:** hai xe cùng đời cùng km có thể lệch hàng chục triệu vì tình trạng; khách cảm thấy giá "chung chung" là vô dụng.

**UAT**

1. Có hướng dẫn các góc cần chụp (trước, sau, hai bên, nội thất, đồng hồ km). Chụp thẳng từ camera điện thoại được.
2. Sau khi tải ảnh, thấy danh sách phát hiện: vị trí, loại hư hỏng, mức độ.
3. Người dùng **sửa hoặc bỏ** được từng phát hiện trước khi áp vào giá.
4. Khoảng giá thay đổi kèm giải thích từng dòng (ví dụ "Móp cản sau, mức vừa: −X triệu"). Mức trừ lấy từ bảng quy tắc trong code.
5. Ảnh mờ, tối, hoặc không phải ô tô → yêu cầu chụp lại, không đoán.
6. Ảnh được nén trước khi gửi; mỗi hồ sơ tối đa N ảnh; ảnh lưu mã hóa và chỉ chủ hồ sơ cùng thẩm định viên xem được.
7. Không tải ảnh vẫn dùng được US-01.

## US-04 — Chênh lệch lên đời + trả góp · W2

> Với vai trò **người muốn đổi sang xe điện**, tôi muốn **thấy số tiền cần bù và lịch trả góp phần còn lại**, để **quyết định được mình có đủ tài chính để đổi xe hay không**.

**UAT**

1. Chọn một mẫu xe mục tiêu → thấy giá lăn bánh, giá thu mua tạm tính, **số tiền cần bù** (hiện cả hai đầu của khoảng).
2. Nhập số tiền trả trước, kỳ hạn, lãi suất → thấy khoản trả hằng tháng và tổng lãi.
3. Kết quả khớp với bảng tính tay của nhóm ở ít nhất 5 ca kiểm thử (unit test).
4. Có ghi chú: lãi suất và giá lăn bánh là giả định minh họa, có ngày cập nhật.

## US-05 — Đặt lịch thẩm định · W3

> Với vai trò **người muốn bán / đổi xe**, tôi muốn **đặt lịch thẩm định thực tế ngay sau khi xem giá**, để **chốt được giá chính thức mà không phải gọi điện nhiều nơi**.

**UAT**

1. Từ trang kết quả, đặt lịch trong không quá 3 bước: chọn ngày giờ, địa điểm, số điện thoại.
2. Không đặt được vào khung giờ đã kín hoặc đã qua.
3. Sau khi đặt, thấy mã hồ sơ và trạng thái "Chờ thẩm định".
4. Thẩm định viên thấy lịch mới trong danh sách của mình.

## US-06 — Baseline trung lập cho thẩm định viên · W3 · SÂU

> Với vai trò **thẩm định viên / nhân viên tư vấn**, tôi muốn **xem hồ sơ xe, ảnh, giá baseline và cơ sở tính, rồi chốt giá chính thức**, để **báo giá nhanh, nhất quán và có căn cứ giải thích với khách**.

**Pain point:** nhân viên định giá theo kinh nghiệm riêng, mỗi người một giá, khó thuyết phục khách.

**UAT**

1. Đăng nhập vai trò thẩm định viên → thấy danh sách hồ sơ chờ. Tài khoản khách không vào được trang này.
2. Mở một hồ sơ → thấy thông tin xe, ảnh, phát hiện từ ảnh, khoảng giá baseline, xe tương đồng, các dòng điều chỉnh.
3. Nhập giá chính thức. Nếu nằm ngoài khoảng baseline → bắt buộc chọn lý do.
4. **Chỉ sau khi thẩm định viên chốt**, khách mới thấy "Giá chính thức". Trước đó khách chỉ thấy "tạm tính".
5. Mỗi lần chốt được lưu lại (ai, lúc nào, giá bao nhiêu, lý do) và tự thành một dòng dữ liệu eval.

## US-07 — Theo dõi tiến trình · W4

> Với vai trò **người đã gửi hồ sơ**, tôi muốn **xem hồ sơ trade-in của tôi đang ở bước nào**, để **không phải gọi hỏi và biết bước tiếp theo là gì**.

**UAT:** mở bằng mã hồ sơ → thấy các bước (Đã định giá sơ bộ → Đã đặt lịch → Đang thẩm định → Đã có giá chính thức → Hoàn tất / Hủy), bước hiện tại, thời điểm của từng bước, và việc khách cần làm tiếp.

## US-08 — Gợi ý xe hợp ngân sách + TCO · W4 · SÂU

> Với vai trò **người muốn đổi sang xe điện**, tôi muốn **được gợi ý mẫu xe vừa ngân sách sau trade-in kèm chi phí sở hữu 5 năm**, để **chọn xe theo tổng chi phí thật chứ không chỉ theo giá niêm yết**.

**UAT**

1. Nhập ngân sách hằng tháng và số km đi mỗi tháng → nhận tối đa 3 mẫu xe phù hợp, xếp theo khoản trả hằng tháng.
2. Mỗi mẫu có bảng TCO 5 năm so với việc giữ xe cũ: năng lượng, bảo dưỡng, khấu hao, lãi vay.
3. Hỏi agent một câu phản đối (ví dụ "xe điện mất giá nhanh lắm") → câu trả lời có dẫn số từ engine hoặc trích từ tài liệu chính sách, có ghi nguồn.
4. Mọi con số TCO có unit test.

## US-09 — Đo sai lệch giá · W5

> Với vai trò **quản lý chương trình trade-in**, tôi muốn **xem sai lệch giữa giá ước tính và giá thẩm định trên ≥ 20 ca**, để **biết baseline đáng tin đến đâu và cần sửa ở đâu**.

**UAT:** trang hiện số ca, sai lệch trung bình (%), tỷ lệ ca nằm trong khoảng, và danh sách các ca lệch nhiều nhất kèm lý do thẩm định viên đã chọn.

## US-10 — Dashboard chuyển đổi · W5

> Với vai trò **quản lý chương trình trade-in**, tôi muốn **xem tỷ lệ hồ sơ đi từ định giá → đặt lịch → chốt giá**, để **biết khách rơi rụng ở bước nào**.

**UAT:** phễu 3 bước với số lượng và tỷ lệ, lọc theo tuần.

---

## Mẫu spec cho story sâu

Copy khối này vào PR hoặc file riêng trước khi code US-01, 03, 06, 08:

```
# Spec US-xx — <tên>
## 1. Động lực
Vấn đề · Người dùng · Kết quả mong đợi + chỉ số · Phương án đã cân nhắc
## 2. Thiết kế
Luồng màn hình · API (endpoint, request, response, lỗi) · Bảng dữ liệu
Phần AI (prompt, đầu ra có cấu trúc) · Phần tính toán (công thức, nguồn hệ số)
Trường hợp biên · Bảo mật
## 3. Kế hoạch
Việc con (mã T-xxx) · Phụ thuộc · Cách test · Tiêu chí xong
```
