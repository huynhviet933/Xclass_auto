# Xclass_auto

# HƯỚNG DẪN SỬ DỤNG TOOL XCLASS AUTOMATION (V1.JS)

Tool hỗ trợ tự động hóa đăng nhập, làm nhiệm vụ (Quests) trên nền tảng XClass, tích hợp hệ thống xác thực bản quyền (License).

## 1. YÊU CẦU HỆ THỐNG
- Đã cài đặt Node.js (phiên bản 16 trở lên).
- Các thư viện cần thiết (Cài đặt bằng lệnh):
  npm install

## 2. CẤU TRÚC FILE ĐẦU VÀO (INPUT)
Trước khi chạy tool, bạn cần chuẩn bị các file sau trong cùng thư mục:

1. mail.txt: Danh sách tài khoản. Định dạng:
   email|password
   Ví dụ: abc@gmail.com|123456

2. proxy.txt: Danh sách Proxy (HTTP/Socks5). Định dạng:
   ip:port hoặc ip:port:user:pass
   (Nếu không có proxy tool sẽ chạy bằng IP máy).

3. code.txt: Chứa mã mời (Referral Code). Mỗi dòng 1 mã.
   Tool sẽ tự động lấy mã đầu tiên để ref, sau 20 acc sẽ đổi mã tiếp theo và tự thêm mã của acc vừa tạo vào cuối file.


## 3. CÁC FILE ĐẦU RA & TRẠNG THÁI (OUTPUT)
Tool sẽ tự tạo các file này trong quá trình chạy:

- license.txt: Lưu trữ Key bản quyền bạn đã nhập.
- index.txt: Lưu vị trí tài khoản cuối cùng đang chạy (để khi lỗi/dừng tool sẽ chạy tiếp từ đó).
- profiles.json: Lưu thông tin Token, UID, Proxy của từng tài khoản để tái sử dụng (giảm tỷ lệ login lại).

## 4. HƯỚNG DẪN KHỞI CHẠY
Bước 1: Mở Terminal/Command Prompt tại thư mục chứa tool.
Bước 2: Chạy lệnh: node v1.js
Bước 3: Xác thực License:
   - Nếu chạy lần đầu, Tool sẽ yêu cầu: "=> License Key : ".
   - Bạn nhập Key đã mua và nhấn Enter.
   - Nếu Key đúng và đúng HWID (máy tính), Tool sẽ hiện "Xác thực thành công" và bắt đầu chạy.

## 5. CƠ CHẾ HOẠT ĐỘNG
- Tool chạy đa luồng (MAX_THREADS = 15).
- Tự động kiểm tra Token cũ trong profiles.json, nếu hết hạn sẽ tự Refresh hoặc Login lại.
- Tự động làm tất cả Quest có sẵn.
- Tự động ẩn các log lỗi Proxy hoặc lỗi vặt để màn hình sạch sẽ, chỉ hiện log thành công và số Point nhận được.

## 6. LƯU Ý
- Key License: Mỗi Key thường chỉ gắn với 1 HWID (1 máy tính).
- Proxy: Nên dùng Proxy chất lượng để tránh bị lỗi kết nối đến Server XClass.
- Delay: Tool có chế độ nghỉ ngơi giữa các acc từ 3-7 giây để tránh bị quét.
