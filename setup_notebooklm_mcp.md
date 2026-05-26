# Hướng Dẫn Chi Tiết: Tích Hợp `notebooklm-mcp-cli` với Antigravity

Tài liệu này hướng dẫn chi tiết cách cài đặt, cấu hình và tích hợp toàn diện máy chủ MCP `notebooklm-mcp-cli` vào **Antigravity**.

---

## 1. Cài Đặt `notebooklm-mcp-cli`

Sử dụng trình quản lý gói Python `uv` (khuyên dùng để cài đặt nhanh và sạch) hoặc `pip`/`pipx`.

```powershell
# Cách 1: Sử dụng uv (Khuyên dùng)
uv tool install notebooklm-mcp-cli --force

# Cách 2: Sử dụng pipx
pipx install notebooklm-mcp-cli

# Cách 3: Sử dụng pip thông thường
pip install --upgrade notebooklm-mcp-cli
```

*Lưu ý: Tham số `--force` đảm bảo ghi đè các symlink cũ nếu bạn đã cài đặt các bản cũ trước đó.*

Sau khi cài đặt thành công, bạn sẽ có 2 lệnh sẵn sàng trên terminal:
*   `nlm` — Command-line interface.
*   `notebooklm-mcp` — Lệnh chạy MCP Server.

---

## 2. Xác Thực Tài Khoản Google (Authentication)

Vì NotebookLM không cung cấp API công khai chính thức, công cụ này cần cookie trình duyệt để xác thực.

### Cách 1: Tự động qua Trình Duyệt (Khuyên dùng)
Chạy lệnh sau trên terminal của bạn:
```powershell
nlm login
```
Lệnh này sẽ tự động khởi chạy trình duyệt mặc định (Chrome, Edge, Brave, v.v.). Bạn chỉ cần đăng nhập tài khoản Google của mình, và `nlm` sẽ tự động trích xuất cookie và lưu cấu hình bảo mật.

*   Để kiểm tra trạng thái đăng nhập:
    ```powershell
    nlm login --check
    ```

---

## 3. Tích Hợp vào Antigravity

Antigravity hỗ trợ tích hợp trực tiếp `notebooklm-mcp-cli` thông qua cấu hình MCP Server và bộ tệp tin Kỹ Năng (Skill files).

### Bước A: Đăng ký MCP Server vào Antigravity
Cập nhật cấu hình MCP Server của Antigravity để nhận diện `notebooklm-mcp`.

1.  Tìm thư mục dữ liệu ứng dụng của Antigravity (App Data Directory):
    `C:\Users\<Tên-User>\.gemini\antigravity-ide`
2.  Mở hoặc tạo file cấu hình MCP (ví dụ: `mcp_config.json` hoặc file config chính của Antigravity).
3.  Thêm cấu hình máy chủ MCP dưới đây vào phần cấu hình `mcpServers`:

```json
{
  "mcpServers": {
    "notebooklm-mcp": {
      "command": "notebooklm-mcp",
      "args": []
    }
  }
}
```

> [!TIP]
> Nếu bạn không muốn cài đặt công cụ toàn cục trên hệ thống, bạn có thể cấu hình thông qua `uvx` để chạy on-the-fly:
> ```json
> {
>   "mcpServers": {
>     "notebooklm-mcp": {
>       "command": "uvx",
>       "args": [
>         "--from",
>         "notebooklm-mcp-cli",
>         "notebooklm-mcp"
>       ]
>     }
>   }
> }
> ```

### Bước B: Cài đặt Skills hỗ trợ Antigravity
Tải và cài đặt tệp tin Skill chuyên dụng giúp AI định hướng cách tương tác tối ưu nhất với NotebookLM:

```powershell
nlm skill install antigravity
```

Lệnh này sẽ cài đặt tệp tin chỉ dẫn trực tiếp vào thư mục skills của Antigravity, cho phép mô hình AI hiểu sâu hơn về 35 công cụ (tools) của NotebookLM.

---

## 4. Kiểm Tra & Vận Hành

1.  Khởi động lại Antigravity để tải lại danh sách MCP.
2.  Chạy công cụ `list_permissions` hoặc xem bảng danh sách tools trong Antigravity để xác nhận các tool có tiền tố `notebooklm-mcp/` đã hiển thị.
3.  Thực hiện tương tác bằng ngôn ngữ tự nhiên với Antigravity:
    *   *"Liệt kê các notebook của tôi trong NotebookLM"*
    *   *"Tạo một notebook mới tên là 'Nghiên cứu AI'"*
    *   *"Tóm tắt nội dung tài liệu trong notebook hiện tại"*
    *   *"Tạo file podcast audio cho notebook này"*
