1. Phân tích lỗi
Lỗi 1: Truy cập giá phòng
Code sai:
javascript
const basePrice = bookingReservation.priceKey;
priceKey là biến có giá trị "roomPrice".
Khi dùng:
bookingReservation.priceKey
JavaScript tìm thuộc tính có tên chính xác là priceKey.
Object không có thuộc tính priceKey nên kết quả là:
undefined
Cách sửa:
const basePrice = bookingReservation[priceKey];
Kết quả:
1500000

Lỗi 2: Xóa mã voucher
Code sai:
bookingReservation.discountCode = undefined;
Cách này chỉ thay giá trị của discountCode thành undefined, nhưng key discountCode vẫn tồn tại trong object.
Cách sửa:
delete bookingReservation.discountCode;
Sau khi delete, kiểm tra:
"discountCode" in bookingReservation
Kết quả:
false
Lỗi 3: Duyệt object bằng for...in
Code sai:
for (const key in bookingReservation) {
    console.log(key + ": " + bookingReservation.key);
}
bookingReservation.key tìm thuộc tính có tên chính xác là key.
Cách đúng:
for (const key in bookingReservation) {
    console.log(key + ": " + bookingReservation[key]);
}
key là biến nên phải sử dụng Bracket Notation.

2. Test Cases
Trường hợp kiểm thử	Dữ liệu đầu vào	Kết quả sai thực tế	Kết quả đúng mong đợi
Tính giá phòng và phụ thu	priceKey = "roomPrice", roomPrice = 1500000, checkInHour = 9	basePrice = undefined, phụ thu = NaN, tổng tiền = NaN	basePrice = 1500000, phụ thu = 450000, tổng tiền = 1950000
Voucher không hợp lệ và hiển thị object	isVoucherValid = false, discountCode = "SUMMER10"	Key discountCode vẫn tồn tại; vòng lặp in giá trị undefined	discountCode bị xóa hoàn toàn, "discountCode" in bookingReservation trả về false, các thuộc tính hiển thị đúng giá trị

3. Kết quả kiểm tra
"discountCode" in bookingReservation
Kết quả:
false