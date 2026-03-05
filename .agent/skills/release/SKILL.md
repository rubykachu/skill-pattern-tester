---
name: release
description: Kỹ năng quản lý phiên bản và tự động tạo Git Release qua Github CLI (`gh`). Kích hoạt khi người dùng yêu cầu "tạo release", "phát hành bản mới" hoặc "bump version". Tự chủ động phân tích log để quyết định nâng loại phiên bản tương ứng (Major, Minor, Patch) nếu cần.
---

# Release Manager Skill

Bất cứ khi nào người dùng yêu cầu tạo release (phát hành tính năng/sửa lỗi mới), bạn đang đóng vai trò là một **Release Manager**. Trách nhiệm của bạn là tự động hóa quá trình sinh version mới, cập nhật file `VERSION.md`, tổng hợp release notes (changelog) và sử dụng lệnh `gh` (Github CLI) để công bố release lên repository.

## Quy trình thực thi (Workflow)

Bạn BẮT BUỘC phải thực thi tuần tự các bước sau:

### Bước 1: Thu thập thông tin phiên bản
1. Đọc nội dung file `VERSION.md` lấy phiên bản hiện tại (ví dụ: `1.0.0`).
2. Chạy lệnh `git tag --sort=-v:refname | head -n 1` (hoặc `gh release list --limit 1`) để lấy tag mới nhất thực tế trên Git. Lấy phiên bản mới nhất từ Git để soi chiếu. (Nếu chưa từng release, coi như chưa có).

### Bước 2: Phân tích lịch sử thay đổi (Git Log)
1. Xác định số lượng và nội dung các commit từ phiên bản cấu hình trước tới HEAD.
   Sử dụng lệnh: `git log <latest_tag>..HEAD --oneline` (Nếu chưa có tag nào thì `git log --oneline`).
2. Dừng quá trình nếu không có commit mới nào (Thông báo: "Không có thay đổi nào cần thiết để release").

### Bước 3: Đánh giá và Quyết định Phiên bản (Semantic Versioning)
Bạn được trao quyền tự quyết định nâng thông số phiên bản (Major, Minor, Patch) dựa vào việc phân loại các commit ở Bước 2.
- **Major (X.y.z)**: Nếu git log có "BREAKING CHANGE", hoặc commit thể hiện việc đập bỏ luồng logic, thay đổi cấu trúc lớn của `skill` hay `template`.
- **Minor (x.Y.z)**: Nếu git log chủ yếu là thêm tính năng (`feat:`), thêm file mới, tạo thêm `pattern` mới cho một backlog.
- **Patch (x.y.Z)**: Nếu git log chủ yếu là sửa lỗi (`fix:`), refactor, cập nhật tài liệu (`docs:`), chỉnh sửa giao diện nhỏ gọn (`chore:`).

*Quy tắc cập nhật `VERSION.md`:*
Đối chiếu kiểm tra xem version lưu trong `VERSION.md` đã được người dung update (so với `latest_tag` ở bước 1) hay chưa.
- **Nếu `VERSION.md` ĐÃ LỚN HƠN** bản release thực tế cũ và phù hợp với mức thay đổi bạn dự tính: GIỮ NGUYÊN nội dung file `VERSION.md` và lấy version đó để làm tag.
- **Nếu `VERSION.md` CHƯA ĐƯỢC CẬP NHẬT** (Bằng với `latest_tag` hoặc lạc hậu): Bạn phải **TỰ TÍNH TOÁN VÀ GHI ĐÈ (overwrite)** file `VERSION.md` thành phiên bản mới tương ứng với quyết định ở trên.

### Bước 4: Soạn thảo Release Notes
Tự động tổng hợp và nhóm các commit thành một chuỗi văn bản Markdown chất lượng cao (Release Notes).
Ví dụ Format đầu ra:
```markdown
## What's Changed
### 🚀 Features / Enhancements
- Tích hợp thêm tính năng abc (#id)
- Cập nhật agent skills
### 🐛 Bug Fixes
- Sửa lỗi scroll trong XYZ (#id)
### 🛠 Chores & Refactoring
- Refactor cấu trúc thư mục
```

### Bước 5: Commit `VERSION.md` (Nếu có cập nhật)
Nếu file `VERSION.md` được thay đổi ở Bước 3, bạn phải tạo 1 commit tự động:
- `git add VERSION.md`
- `git commit -m "chore(release): bump version to <NEW_VERSION>"`
- Chú ý: Sử dụng lệnh command bash cẩn thận để đẩy lên local ref. Trước khi push nhớ check upstream. Có thể `git push` để đẩy commit.

### Bước 6: Tạo Release bằng `gh`
Thực thi lệnh CLI của Github để tạo bản phát hành:
`gh release create v<NEW_VERSION> --title "Release v<NEW_VERSION>" --notes "<Nội dung Markdown Release Notes>"`

*(Lưu ý: Nếu format cũ không sử dụng tiền tố 'v', hãy tuân thủ format cũ. Đặc định default thì hãy dùng prefix 'v').*

## Nguyên Tắc Cốt Lõi (Core Directives)
- **Tự quyết và Độc lập**: Quyết định logic nâng version là do bạn, không hỏi xin phép người dùng xem nên Major hay Patch.
- **Quan hệ phiên bản**: Phải cực kỳ thận trọng khi đánh giá xem file `VERSION.md` ở thời điểm hiện tại đã là version sẵn sàng cho release hay chỉ là một thông số quên update.
- **Lỗi thao tác CLI**: Nếu `gh` chưa đăng nhập hoặc gặp lỗi permission, phải dừng lại và thông báo cách giải quyết cho người dùng (`gh auth login`).
