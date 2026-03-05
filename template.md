# Quy Tắc Tạo Ma Trận Kiểm Thử (Decision Table Testing)

Tài liệu này định nghĩa cấu trúc ma trận kiểm thử dưới dạng **Decision Table Testing**, dựa trên cách xây dựng test case chuyên nghiệp.

## Khái Niệm Cơ Bản
- **Decision Table Testing**: Kỹ thuật kiểm thử sử dụng bảng quyết định nhằm kết hợp các điều kiện đầu vào với kết quả đầu ra.
- **Hàng (Row)**: Mỗi dòng đại diện cho một yếu tố kiểm tra (Item) bao gồm **Input** (Đầu vào/Điều kiện) hoặc **Output** (Đầu ra/Kết quả).
- **Cột P{Number} (P1, P2, P3...)**: Đại diện cho mỗi một **Pattern Test Case** (Kịch bản kiểm thử).
- **Ký hiệu `〇`**: Điểm giao cắt (map) giữa điều kiện đầu vào và kết quả đầu ra tương ứng trên cùng một Pattern.

Dưới đây là mẫu cấu trúc nằm trong tag `<template-testcase></template-testcase>`.

<template-testcase>
## ■ Quan điểm 1: [Tên Quan Điểm Kiểm Thử]
**Mục đích**: [Mô tả mục đích kiểm tra]

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | [Tên nhóm 1] | [Hành động/Dữ liệu nhập 1] | 〇 | | 〇 | |
| | | [Hành động/Dữ liệu nhập 2] | | 〇 | | |
| | [Tên nhóm 2] | [Hành động/Dữ liệu nhập 3] | | | | 〇 |
| **Output (Đầu ra)** | [Kết quả kỳ vọng] | [Mô tả kết quả mong đợi 1] | 〇 | | | |
| | | [Mô tả kết quả mong đợi 2] | | 〇 | | 〇 |
| | | [Mô tả kết quả mong đợi 3] | | | 〇 | |

## ■ Quan điểm 2-1: Kiểm tra hiển thị các loại ký tự nhập vào
**Mục đích**: Xác nhận việc hiển thị các loại ký tự khác nhau.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Tất cả đầu vào | | | | | | |
| | Ký tự đặc biệt hệ thống | (㌔〠,〠㌔) | 〇 | 〇 | 〇 | 〇 | 〇 |
| | Các loại ký tự cho phép | Kanji (漢字) | 〇 | 〇 | 〇 | 〇 | 〇 |
| | | Hiragana (こんにちは) | 〇 | 〇 | 〇 | 〇 | 〇 |
| **Output (Đầu ra)** | Kết quả kỳ vọng | Các ký tự đã nhập được hiển thị chính xác | 〇 | 〇 | 〇 | 〇 | 〇 |
| | Xác nhận theo mục | Năm (Bắt đầu dự án) | 〇 | | | | |
| | | Tháng (Bắt đầu dự án) | | 〇 | | | |

## ■ Quan điểm 2-2: Khoảng trắng đầu và cuối chuỗi (Trim Space)
**Mục đích**: Đảm bảo hệ thống trim bỏ khoảng trắng thừa.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Tất cả đầu vào | Nhập chuỗi có khoảng trắng ở đầu | 〇 | | | | |
| | | Nhập chuỗi có khoảng trắng ở cuối | | 〇 | | | |
| | | Nhập khoảng trắng ở cả đầu và cuối | | | 〇 | | |
| | | Chỉ nhập toàn khoảng trắng | | | | 〇 | |
| | | Nhập chuỗi không có khoảng trắng | | | | | 〇 |
| **Output (Đầu ra)** | Kết quả kỳ vọng | Trim khoảng trắng ở đầu chuỗi | 〇 | | | | |
| | | Trim khoảng trắng ở cuối chuỗi | | 〇 | | | |
| | | Trim khoảng trắng 2 đầu chuỗi | | | 〇 | | |
| | | Hiển thị thông báo "Vui lòng nhập" | | | | 〇 | |
| | | Dữ liệu nhập được hiển thị đúng | | | | | 〇 |
</template-testcase>
