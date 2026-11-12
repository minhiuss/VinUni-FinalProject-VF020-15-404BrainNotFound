# Quy tắc làm việc với repo

## Nhánh

| Nhánh | Dùng cho |
|---|---|
| `main` | Bản đang chạy trên production. Chỉ nhận code qua PR đã review |
| `feature/us-01-wizard` | Tính năng mới, gắn mã user story |
| `fix/bug-012-upload` | Sửa lỗi, gắn mã bug |
| `docs/...`, `chore/...` | Tài liệu, cấu hình |

Tạo nhánh mới từ `main` mới nhất:

```bash
git checkout main
```

```bash
git pull
```

```bash
git checkout -b feature/us-01-wizard
```

## Commit

- Nhỏ và thường xuyên. Sửa một chút cũng commit.
- Viết bằng tiếng Anh, bắt đầu bằng động từ: `add valuation range endpoint`, `fix mileage validation`, `update PRD scope`.
- Một commit làm một việc.

## Pull Request

1. Dưới 400 dòng thay đổi. Lớn hơn thì chia nhỏ.
2. Tiêu đề có mã: `[US-01] Add vehicle info wizard`, `[F-06] Return price range`, `[BUG-012] Fix upload on Safari`.
3. Điền đủ khung mô tả: đổi gì, vì sao, test thế nào.
4. Nếu có dùng AI: thêm hoặc cập nhật file trong `ai-logs/` ngay trong PR đó.
5. Ít nhất **1 người khác** review. Người review phản hồi trong 4 giờ làm việc.
6. CI phải xanh mới được merge. Merge xong thì xóa nhánh.

Tính năng làm dở vẫn merge được nếu ẩn sau cờ bật/tắt. Nhờ vậy nhóm deploy được nhiều lần mỗi ngày mà không làm hỏng production.

## Review

- Đọc code, kéo về chạy thử nếu là thay đổi lớn.
- Góp ý cụ thể vào từng dòng.
- Phần tính tiền (định giá, trả góp, TCO): kiểm tra có unit test và hệ số có ghi nguồn.

## Sau khi merge

- Kiểm tra bản production còn chạy.
- Thêm một dòng vào `CHANGELOG.md` và sheet Release log.
- Cập nhật trạng thái việc trong Backlog.

## Không đưa lên git

`.env`, API key, mật khẩu, ảnh xe của khách, dữ liệu có thông tin cá nhân, thư mục `node_modules`, `.venv`, file build.
