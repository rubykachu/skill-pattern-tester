<template-testcase>
## ■ Quan điểm 1: Kiểm tra Validate các trường nhập liệu (テナントID, ユーザーID, パスワード)
**Mục đích**: Đảm bảo hệ thống hiển thị thông báo lỗi chính xác khi các trường bắt buộc bị bỏ trống.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 | P6 | P7 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Hành động thao tác | Focus out ra khỏi ô nhập「テナントID」 | 〇 | | | | | | |
| | | Focus out ra khỏi ô nhập「ユーザーID」 | | 〇 | | | | | |
| | | Focus out ra khỏi ô nhập「パスワード」 | | | 〇 | | | | |
| | | Click button「ログイン」 | | | | 〇 | 〇 | 〇 | 〇 |
| | Trạng thái dữ liệu | Để trống ô「テナントID」 | 〇 | | | 〇 | | | 〇 |
| | | Để trống ô「ユーザーID」 | | 〇 | | | 〇 | | 〇 |
| | | Để trống ô「パスワード」 | | | 〇 | | | 〇 | 〇 |
| **Output (Đầu ra)** | Kết quả hệ thống | Hiển thị lỗi MSG_ERR_001:「テナントIDを入力してください。」 | 〇 | | | 〇 | | | 〇 |
| | | Hiển thị lỗi MSG_ERR_001:「ユーザーIDを入力してください。」 | | 〇 | | | 〇 | | 〇 |
| | | Hiển thị lỗi MSG_ERR_001:「パスワードを入力してください。」 | | | 〇 | | | 〇 | 〇 |

## ■ Quan điểm 2: Kiểm tra chức năng Ẩn/Hiện mật khẩu (EV01)
**Mục đích**: Xác nhận người dùng có thể chuyển đổi trạng thái hiển thị của mật khẩu.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 |
| :--- | :--- | :--- | :---: | :---: |
| **Input (Đầu vào)** | Trạng thái ban đầu | Mật khẩu đang bị ẩn (••••••••) | 〇 | |
| | | Mật khẩu đang hiển thị (123456) | | 〇 |
| | Hành động thao tác | Click vào biểu tượng hiển thị/ẩn mật khẩu | 〇 | 〇 |
| **Output (Đầu ra)** | Kết quả hiển thị | Hiển thị mật khẩu dưới dạng text rõ (123456) | 〇 | |
| | | Đổi mật khẩu thành dạng ẩn (••••••••) | | 〇 |

## ■ Quan điểm 3: Kiểm tra chức năng Đăng nhập hệ thống (EV02)
**Mục đích**: Xác nhận việc xác thực login vào hệ thống dựa trên thông tin đã nhập.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 | P6 | P7 | P8 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Điều kiện chung | Đã nhập đầy đủ các trường yêu cầu | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 |
| | Hành động thao tác | Click button「ログイン」1 lần | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 | 〇 | |
| | | Double click / Nhấp liên tục button「ログイン」 | | | | | | | | 〇 |
| | Xác thực dữ liệu cơ sở | テナントID không tồn tại | 〇 | | | | | | | |
| | | ユーザID không tồn tại trong テナントID | | 〇 | | | | | | |
| | | パスワード không khớp với ユーザID | | | 〇 | | | | | |
| | | ユーザID đang ở trạng thái vô hiệu hóa (無効) | | | | 〇 | | | | |
| | | Dữ liệu hợp lệ, tìm thấy trong CSDL | | | | | 〇 | 〇 | 〇 | 〇 |
| | Cấu hình 2FA | Hệ thống có cấu hình 2FA | | | | | 〇 | | | |
| | | Hệ thống KHÔNG cấu hình 2FA | | | | | | 〇 | 〇 | 〇 |
| **Output (Đầu ra)** | Xử lý & Thông báo | Hiển thị: MSG_INF_019「認証に失敗しました。」 | 〇 | 〇 | 〇 | 〇 | | | | |
| | | Nút "Login" bị disable ngay sau click đầu tiên để chặn gọi API nhiều lần | | | | | | | | 〇 |
| | | Tạo mã xác thực OTP và gửi đến email đã đăng ký | | | | | 〇 | | | |
| | | Chuyển sang màn hình xác thực tài khoản (2FA認証画面) | | | | | 〇 | | | |
| | | Tạo session đăng nhập | | | | | | 〇 | 〇 | 〇 |
| | | Chuyển đến màn hình TOP (LOR002_001_トップ画面) | | | | | | 〇 | 〇 | 〇 |

## ■ Quan điểm 4: Kiểm tra chức năng Đăng nhập bằng Google (EV03)
**Mục đích**: Xác nhận việc người dùng sử dụng tuỳ chọn OAuth 2.0 để đăng nhập.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Hành động thao tác | Click button「Googleでログイン」 1 lần | 〇 | 〇 | 〇 | 〇 | |
| | | Double click / Nhấp liên tục button「Googleでログイン」 | | | | | 〇 |
| | Trạng thái Google | Chọn hoặc đăng nhập tài khoản Google thành công | 〇 | 〇 | 〇 | 〇 | |
| | Xác thực hệ thống (Email) | Email KHÔNG tồn tại trong hệ thống | 〇 | | | | |
| | | Email CÓ tồn tại, nhưng người dùng trạng thái 無効 | | 〇 | | | |
| | | Email CÓ tồn tại, người dùng trạng thái 有効 | | | 〇 | 〇 | |
| | Liên kết Google | Tài khoản Google CHƯA được liên kết với user hệ thống | | | 〇 | | |
| | | Tài khoản Google ĐÃ được liên kết với user hệ thống | | | | 〇 | |
| **Output (Đầu ra)** | Xử lý trung gian | Chuyển hướng sang màn hình xác thực Google (OAuth 2.0) | 〇 | 〇 | 〇 | 〇 | |
| | | Nút "Googleでログイン" bị disable ngay sau click đầu tiên | | | | | 〇 |
| | | Nhận thông tin từ Google (email, Google ID) | 〇 | 〇 | 〇 | 〇 | |
| | Xử lý & Thông báo | Hiển thị MSG_INF_019「認証に失敗しました。」 | 〇 | 〇 | | | |
| | | Hiển thị lỗi MSG_INF_020「このGoogleアカウントは登録されていません。」 | | | 〇 | | |
| | | Tạo session đăng nhập và di chuyển đến màn hình TOP | | | | 〇 | |

## ■ Quan điểm 5: Kiểm tra các luồng phụ trợ và Giới hạn ký tự
**Mục đích**: Xác nhận chức năng quên mật khẩu, đổi ngôn ngữ, ranh giới, định dạng ký tự và paste dữ liệu.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 | P6 | P7 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Hành động thao tác | Click link「パスワードを忘れた方はコチラ」 | 〇 | | | | | | |
| | | Thay đổi lựa chọn「言語選択」 | | 〇 | | | | | |
| | Ranh giới dữ liệu | Nhậpパスワード có độ dài đúng 100 ký tự | | | 〇 | | | | |
| | | Nhậpパスワード có độ dài 101 ký tự | | | | 〇 | | | |
| | | Copy text >100 ký tự và Paste vào ô「パスワード」 | | | | | 〇 | | |
| | Định dạng dữ liệu (Half/Full-width) | Nhập ký tự Full-width (Zenkaku) / Tiếng Nhật vào ô「パスワード」 và Focus out | | | | | | 〇 | |
| | | Nhập ký tự Half-width (Hankaku) vào ô「パスワード」 và Focus out | | | | | | | 〇 |
| **Output (Đầu ra)** | Kết quả thực thi | Di chuyển đến màn hình Quên Mật Khẩu (LOR001_003_パスワード再発行画面) | 〇 | | | | | | |
| | | Giao diện tự động thay đổi ngôn ngữ tương ứng | | 〇 | | | | | |
| | | Cho phép nhập bình thường | | | 〇 | | | | |
| | | Không cho phép nhập thêm ký tự thứ 101 | | | | 〇 | | | |
| | | Hệ thống tự động cắt bớt (truncate) text chỉ giữ lại 100 ký tự đầu | | | | | 〇 | | |
| | | Đoạn text ĐƯỢC GIỮ NGUYÊN trạng thái Full-width (Zenkaku), KHÔNG TỰ ĐỘNG CONVERT sang Half-width | | | | | | 〇 | |
| | | Đoạn text được giữ nguyên trạng thái Half-width (Hankaku) | | | | | | | 〇 |

## ■ Quan điểm 6-1: Kiểm tra phần chung hiển thị các loại ký tự nhập vào
**Mục đích**: Xác nhận việc hiển thị các loại ký tự khác nhau ở các ô nhập liệu テキスト.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 |
| :--- | :--- | :--- | :---: | :---: | :---: |
| **Input (Đầu vào)** | Tất cả đầu vào text | | | | |
| | Ký tự đặc biệt hệ thống | (㌔〠,〠㌔) | 〇 | | |
| | Các loại ký tự cho phép | Kanji (漢字) | | 〇 | |
| | | Hiragana (こんにちは) | | | 〇 |
| **Output (Đầu ra)** | Kết quả kỳ vọng | Các ký tự đã nhập được hiển thị chính xác | 〇 | 〇 | 〇 |

## ■ Quan điểm 6-2: Khoảng trắng đầu và cuối chuỗi (Trim Space)
**Mục đích**: Đảm bảo hệ thống trim bỏ khoảng trắng thừa đối với ô nhập liệu thông thường.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | Tất cả ô nhập liệu text | Nhập chuỗi có khoảng trắng ở đầu | 〇 | | | | |
| | | Nhập chuỗi có khoảng trắng ở cuối | | 〇 | | | |
| | | Nhập khoảng trắng ở cả đầu và cuối | | | 〇 | | |
| | | Chỉ nhập toàn khoảng trắng | | | | 〇 | |
| | | Nhập chuỗi không có khoảng trắng | | | | | 〇 |
| **Output (Đầu ra)** | Kết quả kỳ vọng | Trim khoảng trắng ở đầu chuỗi (xử lý ở BE) | 〇 | | | | |
| | | Trim khoảng trắng ở cuối chuỗi | | 〇 | | | |
| | | Trim khoảng trắng 2 đầu chuỗi | | | 〇 | | |
| | | Áp dụng rule "Focus/Click Login trống" (vì chuỗi rỗng) | | | | 〇 | |
| | | Dữ liệu nhập được xử lý bình thường | | | | | 〇 |

## ■ Quan điểm 7: Kiểm tra Bảo mật (Security & Vulnerability)
**Mục đích**: Xác nhận hệ thống chống lại các cuộc tấn công phổ biến như SQL Injection và XSS tại các trường nhập liệu.

| Khối lượng (Input/Output) | Nhóm điều kiện | Mục kiểm tra / Nội dung thực thi | P1 | P2 | P3 | P4 | P5 | P6 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Input (Đầu vào)** | SQL Injection | Nhập `' OR 1=1--` vào ô「テナントID」 | 〇 | | | | | |
| | | Nhập `' OR 1=1--` vào ô「ユーザーID」 | | 〇 | | | | |
| | | Nhập `' OR 1=1--` vào ô「パスワード」 | | | 〇 | | | |
| | Cross-Site Scripting (XSS) | Nhập `<script>alert(1)</script>` vào ô「テナントID」 | | | | 〇 | | |
| | | Nhập `<script>alert(1)</script>` vào ô「ユーザーID」 | | | | | 〇 | |
| | | Nhập `<script>alert(1)</script>` vào ô「パスワード」 | | | | | | 〇 |
| **Output (Đầu ra)** | Kết quả thực thi an toàn | Hệ thống xử lý chuỗi như text bình thường, KHÔNG thực thi SQL (trả báo lỗi xác thực MSG_INF_019「認証に失敗しました。」) | 〇 | 〇 | 〇 | | | |
| | | Hệ thống bảo vệ XSS, KHÔNG run alert(), chỉ xử lý như văn bản text thông thường (trả báo lỗi xác thực MSG_INF_019「認証に失敗しました。」) | | | | 〇 | 〇 | 〇 |
</template-testcase>
