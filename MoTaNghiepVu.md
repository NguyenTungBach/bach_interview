# 1. Phone Recorder
## Nghiệp vụ ghi âm cuộc gọi
  - Khách hàng muốn ghi âm cuộc gọi thì phải vào app đăng ký
  - Sau khi đăng ký xong, trong quá trình muốn ghi âm lại cuộc gọi thì khách hàng chỉ cần thêm số điện thoại của app vào như vậy sẽ có 3 bên, 1 bên trung gian và 2 bên trao đổi
  - Sau khi kết thúc cuộc gọi, khách hàng chỉ cần vào xem record

# 2. Quản lý bài viết
## Tổng quan nghiệp vụ
  - Phóng viên sẽ là người đăng bài
  - Biên tập viên sẽ là người xét duyệt bài viết
  - Admin làm nhiệm vụ phân quyền

## Nghiệp vụ nhuận bút
  - Bài viết sau khi được xét duyệt sẽ được tính nhuận bút
  - Số tiền nhuận bút tính thêm sẽ dựa vào lượt xem, lượt tương tác, lượt thích. Lượt nào lớn nhất sẽ được thêm tiền tùy theo cấp độ
  - Sau khi Quản trị viên chốt nhuận bút trong tháng thì sẽ không tính chấm nhuận bút nữa, mọi lượt xem, lượt thích hay lượt tương tác của bài viết đó sẽ không được tính nữa

## Một số nghiệp vụ quản lý: quản lý video, audio, ảnh, silde, danh mục,...

## Tổng bài viết, số bài viết trong 7 ngày gần đây, tổng số bài viết chưa được duyệt, tổng số bài viết được xuất bản, tổng số bài viết đã bị từ chối

## Các trạng thái bài viết
  - Đang soạn thảo
  - Chờ duyệt
  - Chờ xuất bản
  - Từ chối phê duyệt
  - Đã xuất bản

## Đếm số lượng người xem trong quản lý bài viết
- Mỗi khi một người dùng xem một bài viết, ta tăng giá trị của của bài viết đó lên một
- Để đảm bảo rằng một người dùng chỉ được tính là một lượt xem duy nhất. Bài viết chỉ đếm khi người dùng đã đăng ký và đăng nhập. Dữ liệu sẽ được lưu trong database theo id người dùng và id bài viết. Nếu chưa có thì đếm và tạo trong bảng views của database

## Truy vấn nhuận bút
***Tìm bài viết đã được chấm nhuận bút nối theo tác giả, tên thành viên, user admin(về phần thành viên và user admin thì sẽ chung 1 id vì vấn đề trong quá trình tìm hiểu nghiệp vụ chưa rõ ràng. Đến khi hiểu thì mới thấy bảng member là dành cho phía máy khách, còn bảng user là dành cho phía quản lý)***
```sh
select posts.*, users.email as u_email, users.fullname as u_fullname, members.email as m_email, royalties.status as royalties_status, royalties.interactive_royalties_notes, royalties.interactive_royalties, posts.id as total_like, posts.id as total_comment, posts.id as total_views, members.name as m_fullname 
from posts left join users on users.id = posts.user_id 
left join members on members.id = posts.author_id 
left join royalties on royalties.post_id = posts.id 
where posts.status = ? 
and (DATE_FORMAT(published_time, "%Y-%m-%d %H:%i:%s") <= NOW()) and year(posts.published_time) = ? and month(posts.published_time) = ? 
group by posts.id 
order by posts.published_time desc
```

## Truy vấn thống kê danh sách bài viết của tác giả theo danh mục, có sắp xếp
```sh
SELECT t.TenTacGia, d.TenDanhMuc, COUNT(b.Id) as SoBaiViet
FROM TacGia t
INNER JOIN BaiViet b ON t.Id = b.IdTacGia
INNER JOIN DanhMuc d ON b.IdDanhMuc = d.Id
GROUP BY t.TenTacGia, d.TenDanhMuc
ORDER BY t.TenTacGia, d.TenDanhMuc
```


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
- Quản lý chi tiết các vấn đề khách gặp phải
- Khách hàng sau khi mua bộ cài và tải về máy để có thể đăng nhập vào sẽ cần một mã key để xác nhận.
- Sau khi key hết hạn hệ thống sẽ hiện những khách hàng hết hạn key.
- Đội nhân viên tư vấn sẽ báo về cho khách hàng gia hạn để reset key.


# 5. Quản lý hợp đồng
- Tạo ra một hệ thống quản lý và phân loại các file hợp đồng gồm file doc, excel
- Admin vào có thể vừa xem và vừa tải về
- Trong quản lý hợp đồng sẽ có 
  - Thông tin hợp đồng: Tên, loại hợp đồng, Chuyên viên soạn thảo (người viết hợp đồng), Công chứng viên, nơi công chứng, tình trạng, giá trị hợp đồng, số hợp đồng, số tờ, số bản công chứng
  - Thông tin đương sự: CMT/Hộ chiếu,Ngày cấp CMT
  - Thông tin ngân hàng: Tên, Cán bộ tín dụng (cho vay và huy động), tình trạng, chiết khấu
  - Loại tài sản: nhà đất, xe 

# 6. Đối soát thông tin
- SAP là một phần mềm ứng dụng hệ thống để quản lý doanh nghiệp
- SAP sẽ gửi thông tin về mua bán bên kinh doanh, nhập xuất bên sản xuất và tổng doanh thu
- Nhiệm vụ của mình là đối soát với các thông tin với kinh doanh và sản xuất với nhau
- Một đội lấy dữ liệu service kinh doanh
- Một đội lấy dữ liệu sản xuất
- Một đội lo cấu hình và đối soát thông qua dữ liệu bên kinh doanh và sản xuất
- Các service giao tiếp với nhau thông qua rabbitMQ
