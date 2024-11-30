# laptrinhmang

Phần mềm phát video trong mạng LAN
1.Giới thiệu phầm mềm
Video để ở máy phát (chạy chương trình phát video, các máy join vào group này có thể xem video đó, việc phát này giống như đang livestream trên máy phát)
2.Chức năng
1. Đọc và chia nhỏ video
•	Sử dụng thư viện như JavaCV (dựa trên FFmpeg) để đọc video và trích xuất từng khung hình hoặc từng đoạn video nhỏ.
•	Cắt video thành các đoạn ngắn, hoặc thành từng khung hình (nếu cần) và lưu tạm vào bộ nhớ hoặc lưu tạm ra đĩa.
2. Chuyển đổi dữ liệu video thành dạng byte
•	Sau khi có các đoạn video nhỏ, bạn cần chuyển đổi chúng thành chuỗi byte (mảng byte) để có thể gửi qua UDP.
•	Dùng các lớp như ByteArrayOutputStream và DataOutputStream trong Java để hỗ trợ chuyển đổi.
3.Gửi dữ liệu qua UDP
•	Sử dụng DatagramSocket và DatagramPacket để gửi các đoạn byte qua UDP.
•	Đảm bảo thiết lập đúng kích thước gói tin để tránh vấn đề phân mảnh, thường là khoảng 1400-1500 byte mỗi gói để đảm bảo gói không bị chia nhỏ trong quá trình truyền.
•	Mỗi gói tin cần bao gồm thông tin về thứ tự gói để bên nhận có thể sắp xếp lại thành video ban đầu.
4. Bên nhận video
•	Thiết lập một DatagramSocket trên máy nhận để nhận các gói tin UDP.
•	Ghép các gói tin dựa trên thứ tự đã gửi để tạo lại video.
•	Sử dụng lại thư viện JavaCV để tạo lại video từ các đoạn nhỏ hoặc từ các khung hình.
•	Dùng 1 thư viện Player trên JavaFX để hiển thị video bên máy nhận.
2 Định nghĩa giao thức cho từng chức năng


![image](https://github.com/user-attachments/assets/d3d4133f-b856-47eb-b5c0-90edf50901c0)

Mô tả chi tiết từng chức năng:
Khởi tạo phiên chat:

Client gửi <SESSION_REQ>clientID</SESSION_REQ> để yêu cầu khởi tạo.
Server phản hồi với <SESSION_ACCEPTED>sessionID</SESSION_ACCEPTED> hoặc <SESSION_DENIED>.
Gửi và nhận tin nhắn:

Client gửi tin nhắn sử dụng <MESSAGE>.
Server xác nhận tin nhắn đã nhận bằng <MESSAGE_ACK>.
Thông báo trạng thái người dùng:

Khi có người tham gia hoặc rời khỏi session, server gửi <USER_JOIN> hoặc <USER_LEAVE>.
Heartbeat (Kiểm tra kết nối):

Duy trì kết nối giữa client và server qua <HEARTBEAT> và <HEARTBEAT_ACK>.
Kết thúc phiên chat:

Client gửi <SESSION_END> khi muốn đóng phiên làm việc.
Video minh họa






https://github.com/user-attachments/assets/a7caa68b-bf0e-473d-b6da-358e31bee165




