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

1. Bước 1: Khởi tạo khóa học (Draft - Bản nháp)
Mục tiêu: Người dạy có thể tạo khung cơ bản của khóa học mà không cần phải hoàn thành mọi nội dung ngay lập tức.
Thông tin cần cung cấp:
Tên khóa học: Tiêu đề khóa học.
Mô tả: Mô tả sơ lược về nội dung và mục tiêu của khóa học.
Giá cả: Đặt giá cho khóa học (có thể cập nhật sau).
Thể loại: Chọn danh mục khóa học thuộc lĩnh vực nào (ví dụ: Toán, Khoa học, Kỹ năng mềm,...).
Trạng thái: Khóa học bắt đầu ở trạng thái Draft (Bản nháp), có nghĩa là chỉ người dạy mới có thể thấy và chỉnh sửa.
Cập nhật vào cơ sở dữ liệu: Lưu thông tin khóa học vào bảng Courses với trường is_active ở trạng thái Draft và thêm dấu thời gian vào trường created_at.
Tiếp tục chỉnh sửa: Người dạy có thể quay lại khóa học ở trạng thái nháp để chỉnh sửa, thêm mới bài giảng, bài kiểm tra.
2. Bước 2: Thêm bài giảng và bài kiểm tra (Bổ sung nội dung)
Thêm bài giảng:
Người dạy có thể thêm các bài giảng dần dần vào khóa học.
Các bài giảng bao gồm nội dung dạng văn bản, video, tài liệu hoặc bài tập.
Mỗi bài giảng sẽ được thêm vào bảng Lessons và liên kết với khóa học đang tạo.
Thêm bài kiểm tra:
Người dạy có thể thêm bài kiểm tra (Test) vào khóa học, bao gồm các câu hỏi trắc nghiệm hoặc tự luận.
Mỗi câu hỏi được thêm vào bảng Questions và các câu trả lời được lưu trong bảng Answers.
3. Bước 3: Xem trước khóa học (Preview)
Mục tiêu: Người dạy có thể xem trước khóa học ở chế độ không công khai để kiểm tra các nội dung đã tạo.
Chức năng: Người dạy có thể xem cấu trúc của khóa học (danh sách các bài giảng, bài kiểm tra), nhưng không thể đưa khóa học này ra công khai cho học viên.
4. Bước 4: Gửi khóa học để duyệt (Submitted for Approval)
Mục tiêu: Khi người dạy đã hoàn thành đủ nội dung hoặc cảm thấy khóa học sẵn sàng, họ có thể gửi khóa học để quản trị viên duyệt.
Thao tác:
Chuyển trạng thái của khóa học từ Draft sang Pending (Chờ duyệt).
Gửi yêu cầu duyệt lên hệ thống quản trị.
Cập nhật trường updated_at trong bảng Courses để lưu lại thời điểm khóa học được gửi duyệt.
Dữ liệu cập nhật:
Trạng thái của khóa học sẽ chuyển thành Pending trong bảng Courses (is_active = false và pending_review = true), cho phép quản trị viên thấy rằng có một khóa học mới chờ xét duyệt.
5. Bước 5: Quản trị viên xét duyệt khóa học
Mục tiêu: Quản trị viên sẽ kiểm tra và đánh giá nội dung khóa học.
6. xử lý vấn đề cập nhật chỉnh sửa khóa học:
   - chỉ có thể sửa khi đang ở chế độ draft, 1 khi đã được duyệt thì không được phép sửa nữa.
   - có thể bật chế độ chỉnh sửa(server cho sửa trong thời gian tạm thời và sẽ tự động lưu hoặc giáo viên chủ động lưu)
   - có thể tạo ra 1 bảng mới để lưu tạm thời những chỉnh sửa đó và update vào bảng khóa học chính ngay khi có yêu cầu xác nhận cập nhật
   - có thể ẩn khóa học để không đăng ký mới được và đưa vào danh sách chờ trên n8n, khi các học sinh đang trong khóa học đã hoàn thành hết, n8n tự đưa về dạng draft.
Quá trình duyệt:

Quản trị viên xem nội dung bài giảng, kiểm tra tài liệu có phù hợp không.
Nếu khóa học đáp ứng các tiêu chuẩn về nội dung và chất lượng, quản trị viên sẽ duyệt và chuyển khóa học sang trạng thái Active (Hoạt động).
Nếu không đạt yêu cầu, quản trị viên có thể trả lại khóa học cho người dạy để chỉnh sửa và bổ sung thêm.
Dữ liệu cập nhật:

Nếu khóa học được duyệt: Trạng thái của khóa học trong bảng Courses sẽ chuyển thành Active (is_active = true) và cập nhật thời gian duyệt vào trường updated_at.
Nếu khóa học bị từ chối: Khóa học sẽ quay lại trạng thái Draft hoặc Rejected, và người dạy có thể chỉnh sửa nội dung dựa trên nhận xét của quản trị viên.

- dùng CSP thêm vào header chống XSS
chống copy:
- vô hiệu hóa nút và menu
- chèn 1 thẻ div lên trên video để người dùng phải tương tác trên thẻ div => hạn chế thao tác trực tiếp trên video
- sử dụng Device Fingerprint: chỉ số Browser Plugins xem Các plugin trình duyệt đã cài đặt. viết 1 list các extendsion chống an-ti copy để check kết quả với Browser Plugins

- nếu không thể xử lý được video thủ công, có thể tách riêng bài viết và video thành 2 cột để video ở phía dưới bài viết, sẽ dễ xử lý hơn
