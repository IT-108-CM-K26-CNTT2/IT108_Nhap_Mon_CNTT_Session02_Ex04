# Bài 4: Chẩn đoán và "Phẫu thuật" Prompt Sơ sài thành Chuẩn CREATE

## Phần 1: Chẩn đoán lỗi

| Bộ phận | Thành phần bị thiếu | Hậu quả |
|---|---|---|
| CSKH | **Character** (không rõ vai trò), **Adjustment** (không có giọng văn, độ dài), **Type** (không rõ kênh, cấu trúc) | Tin nhắn sáo rỗng, thiếu đền bù và giờ giao mới |
| Bán hàng | **Extras** (thiếu ngân sách, nhu cầu), **Request** (không nói số mẫu, tiêu chí), **Examples** (không có mẫu trình bày) | Liệt kê 10 máy, không có điểm nhấn |
| Bảo hành | **Character** (không rõ vai trò), **Type** (không yêu cầu bảng giá), **Adjustment** (thiếu quy định bảo hành) | Trả lời chung chung "tùy model" |

## Phần 2: 3 Master Prompt

> Giá trị trong `[ ]` là ví dụ minh họa, cần thay bằng dữ liệu thật của TechShop.

### 1. CSKH

```text
[C] Bạn là nhân viên CSKH của TechShop, giọng chân thành, chuyên nghiệp.
[R] Viết tin nhắn xin lỗi khách vì giao hàng chậm: xin lỗi cụ thể, nguyên nhân ngắn gọn,
    giờ giao mới, phương án đền bù, kênh liên hệ.
[E] Mẫu mở đầu: "Chào anh Minh, TechShop chân thành xin lỗi vì đơn TS-00000 đến trễ hơn dự kiến..."
[A] Tối đa 100 từ, xưng "TechShop", gọi "anh/chị", không sáo rỗng, không hứa ngoài thông tin đã cho.
[T] Một tin nhắn Zalo, 3 đoạn (xin lỗi – giải pháp – liên hệ). Chỉ trả về nội dung tin nhắn.
[E] Khách: [Anh Minh] | Đơn: [TS-20451] | Hàng: [SSD Samsung 980 1TB] | Trễ: [2 ngày, kho quá tải]
    Giao mới: [trước 17h 12/10] | Đền bù: [freeship + voucher 5%, hạn 30 ngày] | Hotline: [1900 xxxx]
```

### 2. Bán hàng

```text
[C] Bạn là chuyên viên tư vấn laptop TechShop, trung thực, bám sát ngân sách, không ép mua.
[R] Đề xuất đúng 3 mẫu laptop gaming (tiết kiệm – cân bằng – hiệu năng cao),
    nêu điểm nhấn cấu hình, lý do phù hợp, rồi chọn 1 mẫu đáng mua nhất.
[E] Mẫu 1 gợi ý: "Mẫu A – [Tên] – [Giá]. RTX 4050, RAM 16GB → Valorant ~200 FPS. Hợp vì nằm trong ngân sách."
[A] Không quá 3 mẫu, không vượt tầm giá, giải thích bằng lợi ích, số FPS không chắc thì ghi "ước tính".
[T] Bảng (Tên máy | Giá | Cấu hình | Điểm nhấn) + 2–3 câu kết luận.
[E] Khách: sinh viên, chơi [Valorant, GTA V] | Ngân sách: [20–25 triệu] | Ưu tiên: [FPS ổn, pin 4–5 giờ, máy nhẹ]
    Chỉ chọn trong mẫu TechShop đang bán: [danh sách còn hàng]
```

### 3. Bảo hành

```text
[C] Bạn là kỹ thuật viên tư vấn bảo hành TechShop, báo giá minh bạch, nắm rõ chính sách.
[R] Báo giá thay màn hình laptop vỡ: chi phí linh kiện + công, thời gian sửa,
    bảo hành sau sửa, điều kiện loại trừ (vỡ do va đập không thuộc bảo hành hãng).
[E] Mẫu dòng: "Màn hình 15.6" FHD IPS: linh kiện 1.200.000đ + công 200.000đ = 1.400.000đ, bảo hành 3 tháng."
[A] Chỉ dùng giá trong bảng, không dùng "tùy model", thiếu thông tin thì ghi "cần kiểm tra máy thực tế".
[T] Bảng báo giá (Hạng mục | Đơn giá | Ghi chú) có dòng Tổng + 3 gạch đầu dòng (thời gian, bảo hành, lưu ý). Không chào hỏi.
[E] Khách: [chị Lan] | Máy: [Dell Inspiron 15 3520, vỡ do rơi]
    Bảng giá: [FHD IPS 1.200.000đ | IPS 120Hz 1.800.000đ | OLED 3.500.000đ] | Công: [200.000đ]
    Sửa: [1–2 ngày] | Bảo hành: [3 tháng] | Ưu đãi: [giảm 10% công cho thành viên]
```
