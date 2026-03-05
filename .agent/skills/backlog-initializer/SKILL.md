---
name: backlog-initializer
description: Initialize a new backlog directory explicitly and safely converting provided specification documents (like CSV) into `spec.md`. Trigger this skill when the user asks to "tạo thư mục backlog mới", "khởi tạo cấu trúc dự án backlog", "chuyển đổi spec", or "tạo spec mới".
---

# Backlog Initializer

Ngữ cảnh: Khi người dùng muốn tạo một tính năng / backlog mới trong dự án, họ sẽ cung cấp cho bạn một cái tên backlog (ví dụ: `LOR001_001`, `LOGIN_FEATURE`, v.v.) và cung cấp nội dung đặc tả (Spec) đính kèm (có thể là file `.csv`, đoạn text, hay một định dạng chưa được chuẩn hóa markdown).

Nhiệm vụ của bạn là:
1. Khởi tạo cấu trúc thư mục chuẩn.
2. Chuyển đổi định dạng spec sang `spec.md` MỘT CÁCH TRUNG THỰC NHẤT.

BẠN BẮT BUỘC PHẢI TUÂN THỦ CÁC QUY TẮC SAU:

## 1. Khởi tạo Cấu trúc (Structure Initialization)
- Khuôn mẫu gốc của dự án được đặt trong thư mục: `references/{BACKLOG_NAME}/`.
- Khi nhận yêu cầu tạo backlog tên là `[TÊN_BACKLOG]`, bạn phải **sao chép (copy) toàn bộ thư mục và nội dung bên trong** từ `references/{BACKLOG_NAME}/` sang `backlogs/[TÊN_BACKLOG]/`.
- Tuyệt đối không tự ý đẻ ra file hoặc thư mục khác ngoài những thứ có sẵn trong thư mục reference (ngoại trừ việc bạn phải tạo file ảnh trong thư mục `assets` nếu người dùng upload ảnh).

## 2. Quy Tắc Chuyển Đổi Định Dạng Đặc Tả (Strict Spec Conversion Rule)
- Người dùng có thể cung cấp nội dung đặc tả (spec) dưới dạng file `.csv`, dạng bảng text hoặc file bất kỳ không phải markdown.
- Nhiệm vụ của bạn là convert spec đó thành định dạng Markdown (table, list) và lưu vào file `backlogs/[TÊN_BACKLOG]/spec.md`.

**[QUY TẮC CẤM]:**
- **KHÔNG ĐƯỢC PHÉP CHỈNH SỬA, THÊM BỚT HOẶC SÁNG TẠO NỘI DUNG.** Bạn chỉ là "Máy chuyển đổi định dạng", không phải người phác thảo ý tưởng.
- **GIỮ NGUYÊN TỪ VỰNG GỐC (NO TRANSLATION).** Các keyword, thuật ngữ chuyên ngành, tên biến, thông báo lỗi (MSG_ERR, MSG_INF), mã chức năng... bằng tiếng Nhật, tiếng Anh hay bất kỳ ngôn ngữ nào của bản gốc **TUYỆT ĐỐI KHÔNG ĐƯỢC CHUYỂN NGỮ/DỊCH**. Bạn phải bê y xì đúc text gốc đưa vào markdown.
- **KHÔNG LÀM SAI LỆCH LOGIC.** Nếu file CSV có bao nhiêu dòng, bao nhiêu cột điều kiện, file markdown của bạn sinh ra phải thể hiện đủ và đúng y như thế.

## 3. Quy Trình Vận Hành (Workflow To Execute)
Mỗi khi bắt đầu một yêu cầu tạo backlog:
1. Xác định tên Backlog mục tiêu (hỏi người dùng nếu họ chưa cung cấp).
2. Sao chép Cấu trúc: Nhân bản `references/{BACKLOG_NAME}` sang `backlogs/[TÊN_BACKLOG]`.
3. Đọc dữ liệu đầu vào: Yêu cầu người dùng upload file spec gốc (.csv, hình ảnh UI...) nếu họ chưa cung cấp.
4. **Phân tích dạng bảng / text của đầu vào và viết Markdown**: Soạn thảo kết quả vào `backlogs/[TÊN_BACKLOG]/spec.md`.
5. Đảm bảo bạn đã giữ nguyên văn bản gốc 100%. Xác nhận lại với user: "Spec đã được sao chép nguyên trạng và convert sang định dạng markdown".
