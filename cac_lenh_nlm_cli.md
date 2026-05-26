# Tổng Hợp Lệnh CLI Cốt Lõi: `notebooklm-mcp-cli`

Tài liệu này tổng hợp các lệnh CLI (`nlm`) thường dùng khi làm việc với NotebookLM thông qua command line.

---

## 1. Xác Thực (Authentication)

*   **Đăng nhập tài khoản Google:**
    ```powershell
    nlm login
    ```
    *(Mở trình duyệt mặc định để lấy cookie xác thực)*

*   **Kiểm tra trạng thái đăng nhập:**
    ```powershell
    nlm login --check
    ```

*   **Quản lý Profile:**
    ```powershell
    nlm login profile list               # Danh sách profile đã lưu
    nlm login switch <tên-profile>       # Chuyển đổi tài khoản mặc định
    ```

---

## 2. Quản Lý Notebook

*   **Liệt kê tất cả Notebook:**
    ```powershell
    nlm notebook list
    nlm notebook list --title            # Hiển thị dạng ID: Tiêu đề
    ```

*   **Tạo Notebook mới:**
    ```powershell
    nlm notebook create "<Tiêu đề>"
    ```

*   **Truy vấn (Hỏi đáp) với Notebook:**
    ```powershell
    nlm notebook query <notebook-id> "<Câu hỏi của bạn>"
    ```

*   **Xóa Notebook:**
    ```powershell
    nlm notebook delete <notebook-id> --confirm
    ```

---

## 3. Quản Lý Nguồn Tài Liệu (Sources)

*   **Liệt kê các nguồn trong Notebook:**
    ```powershell
    nlm source list <notebook-id>
    ```

*   **Thêm nguồn từ Link Web hoặc YouTube:**
    ```powershell
    nlm source add <notebook-id> --url "<đường-dẫn-url>"
    ```

*   **Thêm nguồn bằng văn bản trực tiếp:**
    ```powershell
    nlm source add <notebook-id> --text "<Nội dung tài liệu>" --title "<Tên nguồn>"
    ```

*   **Xóa nguồn tài liệu:**
    ```powershell
    nlm source delete <source-id> --confirm
    ```

---

## 4. Tạo & Tải Nội Dung Học Tập (Generation)

*   **Tạo Podcast Audio Overview:**
    ```powershell
    nlm audio create <notebook-id> -y
    ```

*   **Tạo tài liệu học tập (Study Guide / Briefing Doc):**
    ```powershell
    nlm report create <notebook-id> --format "Study Guide" -y
    ```

*   **Tạo bộ câu hỏi trắc nghiệm (Quiz):**
    ```powershell
    nlm quiz create <notebook-id> --count 5 -y
    ```

*   **Tải các tài nguyên đã tạo về máy:**
    ```powershell
    nlm download audio <notebook-id> --output "C:\path\to\podcast.mp3"
    nlm download report <notebook-id> --output "C:\path\to\report.md"
    nlm download quiz <notebook-id> --output "C:\path\to\quiz.html" --format html
    ```

---

## 5. Đặt Biệt Danh (Alias) Rút Gọn ID

Vì ID của NotebookLM rất dài, sử dụng biệt danh giúp gõ lệnh nhanh hơn:

*   **Thiết lập Alias:**
    ```powershell
    nlm alias set <tên-rút-gọn> <ID-notebook-hoặc-source>
    ```

*   **Xem danh sách Alias đã đặt:**
    ```powershell
    nlm alias list
    ```

*   **Xóa Alias:**
    ```powershell
    nlm alias delete <tên-rút-gọn>
    ```
