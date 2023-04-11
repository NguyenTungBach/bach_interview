# 1. Phone Recorder
## Nghiệp vụ ghi âm cuộc gọi
  - Khách hàng muốn ghi âm cuộc gọi thì phải vào app đăng ký
  - Sau khi đăng ký xong, trong quá trình muốn ghi âm lại cuộc gọi thì khách hàng chỉ cần thêm số điện thoại của app vào như vậy sẽ có 3 bên, 1 bên trung gian và 2 bên trao đổi
  - Sau khi kết thúc cuộc gọi, khách hàng chỉ cần vào xem record

# 2. Quản lý bài viết
## Tổng quan nghiệp vụ
  - Phóng viên sẽ là người đăng bài
  - Quản trị viên sẽ là người xét duyệt bài viết
  - Admin làm nhiệm vụ phân quyền

## Nghiệp vụ nhuận bút
  - Bài viết sau khi được xét duyệt sẽ được tính nhuận bút
  - Số tiền nhuận bút tính thêm sẽ dựa vào lượt xem, lượt tương tác, lượt thích. Lượt nào lớn nhất sẽ được thêm tiền tùy theo cấp độ
  - Sau khi Quản trị viên chốt nhuận bút trong tháng thì sẽ không tính chấm nhuận bút nữa, mọi lượt xem, lượt thích hay lượt tương tác của bài viết đó sẽ không được tính nữa

# 3. Web bán đèn
BackEnd gồm các chức năng trị như:
  - Admin quản lý sản phẩm, đơn hàng
  - Thống kê các doanh thu trong tháng

FrontEnd:
  - Người dùng sau khi chọn được những sản phẩm mà mình muốn sẽ vào giỏ hàng để xác nhận
  - Sau khi xác nhận xong đơn hàng sẽ chuyển sang tiến hành thanh toán
  - Sau khi thanh toán thành công thì đơn hàng sẽ chuyển trạng thái đang chờ để đơn vị vận chuyển sản phẩm
  - Sau khi vận chuyển đơn hàng thành công thì trạng thái đơn hàng sẽ chuyển thành hoàn thành

# 4. Quản lý chăm sóc khách hàng
- Khách hàng sau khi mua bộ cài và tải về máy để có thể đăng nhập vào sẽ cần một mã key để xác nhận.
- Sau khi key hết hạn hệ thống sẽ hiện những khách hàng hết hạn key.
- Đội nhân viên tư vấn sẽ báo về cho khách hàng gia hạn để reset key.


# 5. Quản lý hợp đồng
- Tạo ra một hệ thống quản lý và phân loại các file hợp đồng gồm file doc, excel
- Admin vào có thể vừa xem và vừa tải về

# 6. Đối soát thông tin
- SAP là một phần mềm ứng dụng hệ thống để quản lý doanh nghiệp
- SAP sẽ gửi thông tin về mua bán bên kinh doanh, nhập xuất bên sản xuất và tổng doanh thu
- Nhiệm vụ của mình là đối soát với các thông tin với kinh doanh và sản xuất với nhau
- Một đội lấy dữ liệu service kinh doanh
- Một đội lấy dữ liệu sản xuất
- Một đội lo cấu hình và đối soát thông qua dữ liệu bên kinh doanh và sản xuất
- Các service giao tiếp với nhau thông qua rabbitMQ
