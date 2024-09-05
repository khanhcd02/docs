Cấu trúc microservice: 
- Module người dùng:
+ Đăng ký/Đăng nhập: Xác thực qua email, Google OAuth.
+ Hồ sơ cá nhân: Cập nhật thông tin cá nhân, lịch sử học tập, quản lý khóa học đã mua.
+ Nạp tiền.
+ Quản lý tài khoản học viên: Hiển thị khóa học đang học, tiến độ khóa học, lịch sử giao dịch.

- Module khóa học
+ Danh sách khóa học.
+ Chi tiết khóa học: bài giảng, bài tập, quiz.
+ Tương tác: đánh giá khóa học, bình luận.
+ Bài kiểm tra cuối khóa.

- Module quản lý giáo viên
+ Tạo khóa học mới.
+ Theo dõi tiến độ học tập của học viên.
+ Thống kê: Số học viên, thu nhập từ khóa học.

- Module quản trị viên
+ Quản lý người dùng: Tạo, sửa, xóa tài khoản, kiểm tra lịch sử giao dịch.
+ Quản lý khóa học: Phê duyệt khóa học mới.
+ Báo cáo & thống kê: Doanh thu, số lượng học viên, đánh giá khóa học.

- yếu tố chống copy: sử dụng css,javascript để vô hiệu hóa chuột phải, 1 số phím tắt và select văn bản 


Note chống copy:
- css,script chặn nút s,u,p,c,...,chặn chuột phải,f12,...
- không được tắt "javascript" khi mở bài giảng
