# 項目定義

| No. | 項目名（日本語） | 項目名（英語） | 項目タイプ | 必須 | 文字種 | 文字数 (最小数) | 文字数 (最大数) | 数値 (最小値) | 数値 (最大値) | 初期値 | イベントコード | 備考(プレースホルダ、リストの内容 等) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | Logo hệ thống | | ラベル | | | － | － | － | － | － | － | |
| 2 | テナントID | | ラベル | | | － | － | － | － | － | － | |
| 3 | テナントID | | テキスト | | 〇 | － | － | － | － | 空欄 | － | Place Holder：　テナントIDを入力 |
| 4 | ユーザーID | | ラベル | | | － | － | － | － | － | － | |
| 5 | ユーザーID | | テキスト | | 〇 | － | － | － | － | 空欄 | － | Place Holder：　ユーザーIDを入力 |
| 6 | パスワード  | | ラベル | | | － | － | － | － | － | － | |
| 7 | パスワード  | | テキスト | | 〇 | － | － | － | 100 | 空欄 | － | ・Place Holder：　パスワードを入力<br>・Mặc định, mật khẩu đã nhập sẽ được hiển thị dưới dạng 「•••••••• 」.<br>・Có thể nhập tùy ý, khi focus out thì không chuyển đổi sang định dạng half-size |
| 8 | パスワード表示/非表示 | | ボタン | | | － | － | － | － | 有効 | EV01 | Ẩn/Hiện mật mã |
| 9 | ログイン  | | ボタン | | | － | － | － | － | 有効 | EV02 | |
| 10 | Googleでログイン | | ボタン | | | － | － | － | － | 有効 | EV03 | |
| 11 | パスワードを忘れた方はコチラ | | リンク | | | － | － | － | － | 有効 | EV04 | |
| 12 | 言語選択 | | コンボボックス | | | － | － | － | － | 先頭項目 | － | Cho phép chọn ngôn ngữ được sử dụng trong hệ thống<br>Default: 日本語 |
| 13 | COPYRIGHT LOREM COMMUNICATIONS Inc. ALL RIGHTS RESERVED. | | ラベル | | | － | － | － | － | － | － | |

# イベント

| イベントコード | イベント名称 | 処理内容 |
|---|---|---|
| EV01 | Click vào biểu tượng hiển thị/ẩn mật khẩu. | 1. Trường hợp mật khẩu đang bị ẩn, hiển thị mật khẩu (•••••••• → 123456)<br>2.Trường hợp mật khẩu đang hiển thị, ẩn mật khẩu (123456 → ••••••••) |
| EV02 | Click button「ログイン」 | 1. Trường hợp để trống Tenant ID: Hiển thị thông báo lỗi tương ứng.<br>2. Trường hợp để trống ID người dùng: Hiển thị thông báo lỗi tương ứng.<br>3. Trường hợp để trống Mật khẩu: Hiển thị thông báo lỗi tương ứng.<br>4. Trường hợp dữ liệu hợp lệ<br>    Thực hiện việc xác thực login đến hệ thống<br>            Kiểm tra テナントID có tồn tại hay không<br>            Kiểm tra ユーザID có tồn tại trong テナントID tương ứng hay không<br>            Kiểm tra パスワード có khớp với ユーザID tương ứng hay không<br>            Kiểm tra ユーザID còn hiệu lực hay không<br>     4.2 Trường hợp tìm thấy dữ liệu trong cơ sở dữ liệu<br>           4.1.1 Trường hợp có tùy chọn xác thực 2FA<br>                   Hệ thống tạo mã xác thực tài khoản (OTP)<br>                   Gửi mã xác thực đến メールアドレス đã đăng ký<br>                   Chuyển sang màn hình xác thực tài khoản (Tham khảo sheet 2FA認証画面)<br>           4.1.2 Trường hợp không có tùy chọn xác thực 2FA<br>                   Tạo session đăng nhập<br>                   Di chuyển đến màn hình TOP (Tham khảo file 【「i-lorem」リニューアル】基本設計_I_LOR002_001_トップ画面_v0.1)<br>     4.3 Trường hợp không tìm thấy dữ liệu trong cơ sở dữ liệu<br>           Hiển thị thông báo: MSG_INF_019「認証に失敗しました。」 |
| EV03 | Click button「Googleでログイン」 | 1. Chuyển hướng sang màn hình xác thực Google (OAuth 2.0)<br>2. Người dùng chọn hoặc đăng nhập tài khoản Google<br>3. Google xác thực quyền truy cập và trả về thông tin người dùng (email, Google ID)<br>4. Hệ thống nhận thông tin từ Google<br>    Lấy メールアドレス từ tài khoản Google<br>          Kiểm tra email tồn tại trong hệ thống không<br>          Kiểm tra tài khoản người dùng đang ở trạng thái 無効 không<br>    4.1 Trường hợp email tồn tại trong hệ thống và người dùng ở trạng thái 有効<br>          4.1.1 Nếu tài khoản Google đã được liên kết với user trong hệ thống<br>                  Tạo session đăng nhập<br>                  Di chuyển đến màn hình TOP (Tham khảo file 【「i-lorem」リニューアル】基本設計_I_LOR002_001_トップ画面_v0.1)<br>          4.1.2 Nếu tài khoản Google chưa được liên kết<br>                  Hiển thị thông báo lỗi: MSG_INF_020「このGoogleアカウントは登録されていません。」<br>     4.2 Trường hợp email không tồn tại trong hệ thống hoặc người sử dụng ở trạng thái 無効<br>           Hiển thị thông báo: MSG_INF_019「認証に失敗しました。」 |
| EV04 | Click link「パスワードを忘れた方はコチラ」 | ・Di chuyển đến màn hình Quên Mật Khẩu (Tham khảo 【「i-lorem」リニューアル】基本設計_I_LOR001_003_パスワード再発行画面_v0.1) |

# バリデーションチェック

| No. | イベントコード | 画面項目名 | 操作 | チェック仕様（エラーとなる条件） | 種別 | メッセージＩＤ | 備考 |
|---|---|---|---|---|---|---|---|
| 1 | EV02 | テナントID | ・Focus out ra khỏi ô nhập「テナントID」<br>・Click button「ログイン」 | 空欄 | エラー | MSG_ERR_001 | 内容：「テナントIDを入力してください。」 |
| 2 | | ユーザーID | ・Focus out ra khỏi ô nhập「ユーザーID」<br>・Click button「ログイン」 | 空欄 | エラー | MSG_ERR_001 | 内容：「ユーザーIDを入力してください。」 |
| 3 | | パスワード | ・Focus out ra khỏi ô nhập「パスワード」<br>・Click button「ログイン」 | 空欄 | エラー | MSG_ERR_001 | 内容：「パスワードを入力してください。」 |
| 4 | | ログイン | ・Click button「ログイン」 | ・Nhập thông tin Tenant ID, ID người dùng hoặc mật khẩu không tồn tại trong hệ thống. | 情報 | MSG_INF_019 | 内容：「認証に失敗しました。」 |

# 補足事項
(Không có nội dung)
