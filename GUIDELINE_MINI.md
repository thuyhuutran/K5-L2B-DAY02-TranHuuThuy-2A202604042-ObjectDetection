# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp     | Định nghĩa của bạn                            | Ví dụ/điểm phân biệt                                                        |
| ------- | --------------------------------------------- | --------------------------------------------------------------------------- |
| `car`   | Xe con chở người, 4-7 chỗ, thân thấp.         | Sedan, hatchback, SUV nhỏ. Mui thấp hơn van, không có thùng hàng như truck. |
| `truck` | Xe tải chở hàng, cabin tách khỏi thùng hàng   | Xe tải thùng, xe ben, đầu kéo, bán tải.                                     |
| `bus`   | Xe khách/xe buýt dài, từ 16 chỗ trở lên.      | Xe buýt thành phố, xe khách đường dài. Dài hơn van nhiều                    |
| `van`   | Xe thân hộp cao, cỡ vừa, chở người hoặc hàng. | Hiace, Transit, xe 7-16 chỗ. Cao và vuông hơn car, ngắn hơn bus.            |

## Quy tắc chung

- **Box bám sát vật thể:** box ôm sát phần thân xe nhìn thấy, không chừa nền thừa. Hàng hóa chất trên xe tải tính là một phần của xe.
- **Vật thể bị che khuất:** vẫn gán nhãn nếu còn thấy khoảng 30% trở lên và xác định được loại xe. Chỉ vẽ box ôm phần nhìn thấy, không đoán phần bị che.
- **Vật thể bị cắt bởi rìa ảnh:** gán nhãn nếu còn nhận ra loại xe. Vẽ box sát mép ảnh, không vẽ ra ngoài khung.
- **Vật thể rất nhỏ/mơ hồ:** xe quá nhỏ, quá xa hoặc không phân biệt được loại thì bỏ qua. Nếu phân vân giữa `car` và `van` mà không có thêm thông tin thì chọn `car`. Áp dụng cùng một ngưỡng cho tất cả ảnh.
- **Không gán nhãn** cho người, xe máy, xe đạp.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| ----------- | --------------------------------------------------------------------------------------- | --- | ---------------------------------------------------------------------------------- |
| `drive_012` | Xe khách cỡ vừa màu kem giữa ảnh, khó phân biệt `bus` hay `van` | `bus` | Thân dài hơn hẳn `van`, nhiều cửa sổ hai bên, cỡ xe khách mini từ 16 chỗ trở lên, khớp định nghĩa `bus`. |
| `drive_027` | Cụm xe nhỏ dày đặc ở góc trên bên trái, xe nhỏ, xa và chồng lên nhau | `car`, box chỉ ôm phần xe nhìn thấy | Còn thấy từ 30% thân xe trở lên và nhận ra loại xe thì vẫn gán nhãn. |
| `drive_036` | Xe bạc lớn phía trước bị nhòe do chạy nhanh, thân khá cao, khó phân biệt `car` hay `van` | `car` | Mui không cao vuông như `van`, đầu xe có phần nhô ra rõ; ảnh nhòe nên theo quy tắc phân vân thì chọn `car`. |
