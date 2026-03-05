# Skill Pattern Tester & Reviewer (Automated QA Agent Skills)

Bộ kĩ năng AI Agent hỗ trợ quản lý Backlog và tự động hóa quy trình Kiểm thử (QA) dựa trên kỹ thuật **Decision Table Testing**, vận hành thông qua các bộ kỹ năng (Skills) chuyên biệt.

## 📂 Cấu trúc dự án
```text
.
├── .agent/skills/         # Tập hợp các prompt định nghĩa vai trò AI (Init, Tester, Reviewer)
├── backlogs/              # Không gian làm việc chứa spec, UI và test matrix đầu ra
│   └── {BACKLOG_NAME}/
│       ├── spec.md        # Đặc tả yêu cầu, nguồn sự thật duy nhất (Single Source of Truth)
│       ├── assets/        # Hình ảnh UI mockups, Flowchart cục bộ
│       └── patterns/      # Nơi lưu trữ các Ma trận kiểm thử (Test Matrix) được sinh ra
├── references/            # Thư mục mẫu (Template) để clone khi khởi tạo backlog mới
├── AGENTS.md              # Bộ quy tắc cốt lõi (Global Directives) điều hướng hành vi của AI
├── template.md            # Khung xương (Skeleton) thẻ <template-testcase> cho Test Matrix
└── README.md              # Tài liệu tổng quan dự án
```

## 🛠 Bộ kỹ năng của Agent (QA Experts)

Dự án cung cấp 3 vai trò (Persona) chính cho AI:

1. **Backlog Initializer**:
   - Clone cấu trúc chuẩn từ `references/` sang `backlogs/`.
   - Chuyển đổi Spec thô (CSV/Text) thành file `spec.md` một cách trung thực.
2. **Decision Table Tester (30 năm kinh nghiệm)**:
   - Phân tích `spec.md` và `assets` để tự động suy luận Test Matrix.
   - Trình bày dạng Unified Table (Gộp chung Input - Output).
   - Bao phủ 100% kịch bản: Edge cases, Security, Zenkaku/Hankaku, Validation.
3. **Decision Table Reviewer (50 năm kinh nghiệm)**:
   - Kiểm duyệt chéo (Cross-check) giữa Spec và các Pattern đã gen.
   - Phát hiện thiếu sót (missing cases), sai lệch logic, lỗi cấu trúc bảng và tự động sửa đổi.

## ⚖️ Nguyên tắc vận hành cốt lõi (Core Directives)
- **Không tự biên tự diễn (No Assumptions):** AI tuyệt đối không phán đoán hay sáng tạo cấu hình lệch khỏi spec. Nếu spec thiếu logic hoặc mâu thuẫn, AI phải hỏi người dùng để xác nhận.
- **Bảo toàn ngôn ngữ gốc:** Không dịch thuật hoặc tự ý thay đổi các Error messages (MSG_ERR, MSG_INF) hay mã code hệ thống.
- **Trung thành với Template:** Mọi bảng test được sinh ra đều phải trích xuất đúng cấu trúc định sẵn nằm trong thẻ `<template-testcase>` của file `template.md`.

## 🚀 Hướng dẫn kích hoạt Agent
Sử dụng các câu lệnh (prompts) đơn giản để gọi đúng kỹ năng:
- **Khởi tạo dữ liệu**: *"Tạo backlog LOGIN từ file spec.csv đính kèm"* (Khởi động `backlog-initializer`).
- **Viết kịch bản test**: *"Dựa vào spec hiện tại, hãy viết test matrix cho backlog LOGIN"* (Khởi động `decision-table-tester`).
- **Review và sửa lỗi**: *"Review lại kịch bản test của LOGIN, kiểm tra xem có thiếu case security/zenkaku nào không và fix lại giúp tôi"* (Khởi động `decision-table-reviewer`).

---
*Dự án được thiết lập để tối đa hóa tính chính xác, nhất quán và loại bỏ sự phán đoán chủ quan của AI trong quy trình QA.*
