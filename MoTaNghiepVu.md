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

# 7. Quản lý giao hàng
- Một công ty đang gặp muốn quản lý các địa điểm đầu cuối giao hàng cho các lái xe. Bằng cách import file thông tin chuyến giao hàng vào và có thể chuyển hướng chuyến hàng vào nhóm chuyến đi khác (cụ thể một chuyến giao hàng không giao đi từng chuyến mà thành một nhóm để giao) (trên web), các lái xe sẽ biết được thông tin về các địa điểm giao hàng và đăng ký chuyến giao hàng phù hợp với mình (trên mobie)
- Một công ty có các mối quan hệ sau, từng thằng lần lượt là cha của các thằng còn lại **(VD: Branch store có thể gọi đến Base và Delivery Company nhưng không gọi được đến Arata Branch office)**
  - Arata
  - Branch office
  - Branch store
  - Base
  - Delivery Company 
  
- Nghiệp vụ đối soát thông tin chuyến giao hàng: 
  - B1 ***(các bảng liên quan: delivery_datas, delivery_data_files)***: Thông tin giao hàng sẽ được import vào hệ thống
  - B2 ***(các bảng liên quan: delivery_datas, delivery_data_errors)***: Kiểm tra ngày xem có phù hợp không, nếu không sẽ xóa dữ liệu đó khỏi database VD bị quá hạn
  - B3 ***(các bảng liên quan: delivery_datas, delivery_data_direction_errors, delivery_data_between_centers, delivery_data_store_directs)***: Thông tin kiểm tra sẽ được lưu vào database, dựa theo cột code
    -  cột delivery_route nào kiểm tra bị lỗi sẽ được đưa vào bảng delivery_data_direction_errors để add lại vào về sau
    -  cột delivery_route thỏa mãn sẽ lưu vào bảng chuyến đi store_direct
  - B4 ***(các bảng liên quan: delivery_datas, delivery_data_between_centers, delivery_data_store_directs)***: Check quyền tài khoản này xem sẽ được xem department nào (nghiệp vụ 5 Department phía trên: Arata, Branch office, Branch store, Base, Delivery Company)
  - B5 ***(các bảng liên quan: delivery_datas, delivery_data_between_centers, delivery_data_store_directs, delivery_data_destination_errors)***: Kiểm tra và cập nhật các địa điểm giao hàng từ bảng delivery_destination **(bảng delivery_data_destination_errors)** vào bảng delivery_data_store_directs hoặc delivery_data_between_centers
  - B6 ***(các bảng liên quan: delivery_data_between_centers, delivery_data_store_directs, delivery_between_center_aggregations)***: Tổng hợp và cập nhật lại nhóm lại các địa điểm giao hàng trùng lại với nhau 
  
- Admin
  - Công ty
  - Chi nhánh
  
  1) Chọn được nhiều chi nhánh (cửa hàng hoặc cơ sở) thuộc đơn vị vận chuyển được xác định từ trước
  2) Một công ty vận chuyển kết nối với chi nhánh

- Chi nhánh 
    - Chọn nhiều
    - Chọn một

- Cơ sở
  - Chọn nhiều
  - Chọn một
  - Một công ty vận chuyển kết nối với chi nhánh sẽ được phái đi

- Quá trình vận chuyển 
  - Tất cả quá trình vận chuyển phải được xác nhận bởi lái xe

- Một số tính năng trong quản lý như
  - Quản lý các cơ sở
  - Quản lý công ty
  - Quản lý các loại xe
  - Quản lý xe
  - Quản lý tài khoản
  - Quản lý lái xe
  - Quản lý quá trình vận chuyển đến địa điểm
  - Quản lý địa điểm
  - Thời gian hoạt động trong ngày

- Một số tính năng trong báo cáo như:
  - Đặt giá
  - Quá trình hoạt đông vận chuyển
  - Bảng tóm tắt hàng ngày 
  - Bảng tóm tắt hàng tuần
  - Bảng tóm tắt hàng tháng
  - Ghi lại quá trình giao hàng
  - Thông tin giao hàng
  - Bảng phí giao hàng hàng ngày
  - Doanh số bán hàng theo xe
  - Báo cáo vận chuyển hằng ngày
  - Bảng lương
  - Hóa đơn cửa hàng
  - Hóa đơn (trung tâm vận chuyển)

# 8. Quản lý giao hàng và thu chi giao hàng:
#### Hệ thống quản lý phân công tạo ra các chuyến giao hàng cho trong tháng, trong tuần cho lái xe giao hàng hoặc các công ty vận chuyển. Các tính toán về chi phí đều đã được tính từ trước

### Thống kê giao hàng theo từng ngày trong tháng (Mỗi một ô sẽ tương ứng một mã, click vào sẽ ra thông tin chi tiết):
 - Bảng lịch trình
   - Ca làm (ngày lễ, ngày nghỉ yêu cầu)
   - Tên nhân viên hoặc công ty vận chuyển liên kết
   - Tên công ty khách
   - Chi tiết thời gian vận chuyển khi nhấn vào mã (Khi click vào sẽ show ra lịch trình địa điểm, thời gian đi và đến, thời gian giải lao)
 - Bảng chi phí ở các trạm thu phí (show ra từng ngày ngày trong tháng):
   - Mã giao hàng
   - Tên nhân viên
   - Số tiền cho các trạm thu phí mỗi ngày
 - Bảng doanh thu (show ra từng ngày ngày trong tháng):
   - Mã giao hàng
   - Tên nhân viên và công ty vận chuyển
   - Số tiền nhận mỗi ngày
 - Bảng số tiền thanh toán cho bên công ty vận chuyển liên kết (show ra từng ngày ngày trong tháng):
   - Số tiền phải trả theo ngày
   - Mã vận chuyển
   - Tên công ty vận chuyển

### Danh sách khu vực giao hàng:
 - Tên khách
 - Tên cửa hàng
 - Nơi đi và đến
 - Giá vận chuyển

### Trong chuyến giao hàng gồm có:
- Tên tài xế
- Giá vận chuyển hàng
- Số tiền thanh toán cho công ty hợp tác(Nếu có)
- Tiền cho các trạm thu phí (Đã được tính)
- Ngày bắt đầu
- Thời gian bắt đầu kết thúc
- Giờ nghỉ trưa
- Tiền trợ cấp ăn
- Khu vực vận chuyển (Điểm đến và đi)

### Quản lý chi phí giao hàng lái xe trong tháng:
- Số tiền doanh thu khách trả tháng này (tiền nhận)
- Số tiền khách còn nợ (tiền chưa nhận)
- Số tổng tiền nhận được giao hàng trong tháng (tổng tiền sẽ được nhận)
- Số tài khoản
- Tên tài xế

### Quản lý chi phí giao hàng công ty vận chuyển trong tháng:
 - Số tổng doanh thu tiền nhận được giao hàng trong tháng từ công ty vận chuyển (tổng tiền được nhận)
 - Số tiền đã trả công ty vận chuyển nhận tháng này (tiền đã trả bên)
 - Số tiền còn nợ công ty vận chuyển (tiền còn phải trả cho công ty vận chuyển)
 - Số tiền còn lại sau khi thanh toán (tiền còn dư ra sau khi thanh toán cho bên công ty vận chuyển liên kết)
 - Số tài khoản
 - Tên tài xế
- Quản lý chi phí giao hàng công ty liên kết vận chuyển:
### Các quản lý nhỏ như (Data manager): Lái xe, tài khoản admin, khách hàng(tên công ty)
