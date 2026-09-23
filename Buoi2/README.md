# Cách sử dụng file .md trên 
## Cách 1
### Bước 1 : Tải file trên hoặc sao chép toàn bộ đoạn mã 
### Bước 2 : Mở Visual Studio Code hoặc các phần mềm hỗ trợ đọc file .md
### Bước 3 : Trong Visual Studio Code ấn `Open as Preview`

## Cách 2 :
Truy cập vào link sau :
```
https://github.com/wew571/tmp/tree/main/Buoi2
```

# Chương 2 — Hệ thống máy tính

## Bài 2.1

Máy tính dùng bus địa chỉ 32 bit, đánh địa chỉ theo từng byte, bus dữ liệu rộng 64 bit.

**a) Không gian địa chỉ tối đa**

- Số địa chỉ có thể tạo ra: $2^{32}$
- Vì đánh địa chỉ theo từng byte nên không gian địa chỉ tối đa:

  $$
  \begin{aligned}
  2^{32}\ \text{byte}
    &= 4{,}294{,}967{,}296\ \text{byte} \\
    &= 4\ \text{GiB} \\
    &\approx 4\ \text{GB}
  \end{aligned}
  $$

**b) Mỗi lần truy cập bộ nhớ, máy trao đổi được bao nhiêu byte?**

- Bus dữ liệu rộng 64 bit.
- $64\ \text{bit} = 8\ \text{byte}$.
- Vậy mỗi lần truy cập bộ nhớ, máy có thể trao đổi tối đa **8 byte**.

---

## Bài 2.2

Máy tính dùng 32 bit địa chỉ, đánh địa chỉ bộ nhớ theo byte; bus dữ liệu nối với bộ nhớ chính rộng 32 bit.

**a) Số byte nhớ tối đa đánh được địa chỉ? Địa chỉ đầu và địa chỉ cuối ở hệ 16?**

- Số byte nhớ tối đa:

  $$
  \begin{aligned}
  2^{32}
    &= 4{,}294{,}967{,}296\ \text{byte} \\
    &= 4\ \text{GiB}
  \end{aligned}
  $$
- Địa chỉ đầu: `0x00000000`
- Địa chỉ cuối: `0xFFFFFFFF`

**b) Hai byte nhớ có địa chỉ `0x0FE12C3D` và `0x10ABCD06` nằm ở đường dữ liệu (byte lane) nào của bus?**

Bus dữ liệu rộng 32 bit nên có 4 byte lane, được chọn bởi 2 bit thấp của địa chỉ:

- Byte lane 0: offset `00`
- Byte lane 1: offset `01`
- Byte lane 2: offset `10`
- Byte lane 3: offset `11`

Xét địa chỉ:

- `0x0FE12C3D`: byte cuối là `0x3D = 0011 1101₂`, hai bit thấp là `01` → **byte lane 1**
- `0x10ABCD06`: byte cuối là `0x06 = 0000 0110₂`, hai bit thấp là `10` → **byte lane 2**

Vậy:

- Byte tại `0x0FE12C3D` nằm ở **byte lane 1**
- Byte tại `0x10ABCD06` nằm ở **byte lane 2**

---

## Bài 2.3

**a) Các bước của chu trình lệnh mà CPU lặp đi lặp lại khi thực hiện chương trình. Vai trò của PC và IR?**

Chu trình lệnh cơ bản gồm các bước:

1. **Nhận lệnh (Fetch)**
   - CPU đọc lệnh từ bộ nhớ tại địa chỉ do PC chỉ tới.
   - Lệnh được nạp vào thanh ghi IR.
   - PC được tăng để trỏ tới lệnh kế tiếp.

2. **Giải mã lệnh (Decode)**
   - CPU giải mã lệnh trong IR để xác định thao tác cần thực hiện và các toán hạng.

3. **Thực hiện lệnh (Execute)**
   - CPU thực hiện phép toán, truy cập bộ nhớ, đọc/ghi thanh ghi hoặc thiết bị I/O.
   - Ghi kết quả nếu có.

4. **Kiểm tra ngắt (Interrupt check)**
   - CPU kiểm tra xem có yêu cầu ngắt nào không trước khi sang lệnh kế tiếp.

Vai trò của các thanh ghi:

- **PC (Program Counter)**: giữ địa chỉ của lệnh tiếp theo cần nhận.
- **IR (Instruction Register)**: giữ lệnh hiện tại đang được giải mã và thực hiện.

**b) CPU kiểm tra tín hiệu ngắt ở thời điểm nào trong chu trình lệnh? Vì sao lại chọn thời điểm đó mà không kiểm tra giữa chừng một lệnh?**

CPU thường kiểm tra tín hiệu ngắt **ở cuối mỗi chu trình lệnh**, tức là sau khi đã thực hiện xong lệnh hiện tại và trước khi nhận lệnh kế tiếp.

Lý do:

- Đảm bảo mỗi lệnh được thực hiện trọn vẹn, giữ tính nguyên tử của lệnh.
- Trạng thái CPU, thanh ghi và bộ nhớ luôn nhất quán tại thời điểm ngắt.
- Dễ dàng lưu trạng thái và quay lại đúng điểm bị tạm dừng.
- Nếu kiểm tra giữa chừng một lệnh, CPU có thể đang thực hiện dở một thao tác, khó xác định đã hoàn thành bao nhiêu, gây sai lệch kết quả khi quay lại.

**c) Khi chấp nhận một ngắt từ thiết bị bên ngoài, CPU phải thực hiện những bước nào để sau đó quay lại đúng chỗ của chương trình bị tạm dừng?**

Khi chấp nhận ngắt, CPU thường thực hiện:

1. **Hoàn thành lệnh hiện tại** đang thực hiện.
2. **Lưu trạng thái hiện tại**:
   - Lưu PC (địa chỉ lệnh kế tiếp cần quay lại).
   - Lưu thanh ghi trạng thái/thanh ghi cờ (PSW/Flags).
   - Có thể lưu thêm các thanh ghi khác nếu kiến trúc yêu cầu.
3. **Xác định nguồn ngắt** và lấy địa chỉ của chương trình phục vụ ngắt (ISR) từ bảng vector ngắt.
4. **Nạp địa chỉ ISR vào PC** để bắt đầu thực hiện chương trình phục vụ ngắt.
5. **Tạm khóa ngắt** hoặc cập nhật mức ưu tiên ngắt để tránh ngắt lồng nhau ngoài ý muốn.
6. **Thực hiện ISR**.
7. **Kết thúc ISR**:
   - Khôi phục thanh ghi trạng thái/thanh ghi cờ.
   - Khôi phục PC từ nơi đã lưu.
   - Cho phép ngắt trở lại.
   - Tiếp tục thực hiện chương trình bị tạm dừng.
