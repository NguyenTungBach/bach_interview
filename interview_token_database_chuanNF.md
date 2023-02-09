# 1. Token là gì?
Token là đoạn mã được sinh ra từ phía server sử dụng để xác thực quyền truy cập tài nguyên mà không cần cung cấp tên và mật khẩu

# 2. Đánh Index là gì? 
- Đánh Index (đánh chỉ mục) giúp tăng tốc độ tìm kiếm
- Chỉ nên đánh khi bản ghi khoảng 100 nghìn

# 3. Cơ chế đánh Index? 
## 3.1 Hash index: 
- Có dạng key-value của column được đánh Index nên có thể tìm kiếm chính xác ROW tương ứng. 
- Mạnh mẽ khi truy vấn cới các toán tử chính xác = <> (IN, NOT IN) **=>Chỉ nên cân nhắc đánh Index này khi truy vấn với sự chính xác tuyệt đối **
- Vô dụng với > < LIKE vì chỉ tìm toán tử chính xác
- Vô dụng với ORDER BY vì Hash không thể tìm kiếm các phần tử tiếp theo trong Order **(Chỉ foreach được chứ không for i)**
## 3.2 B-tree index:
- Là mặc định khi đánh Index
- Sử dụng thuật toán nhị phân để tìm kiếm **(Chia giữa ra nhiều lần để tìm kiếm)**
- Có 2 trường hợp đánh B-tree index:
  - Đánh 1 trường
  - Đánh nhiều trường **(Tìm kiếm theo trường đầu tiên VD: (country, name, email) thì sẽ tìm kiếm theo country trước rồi name rồi mới email)**
## 3.3 Lưu ý đánh Index? 
- Chỉ nên đánh Index với dữ liệu lớn khoảng 100 nghìn vì việc tạo Index sẽ làm chậm add hoặc update vì nó sẽ phải tổ chức lại danh sách

# 4. Partition là gì? 
- Chỉa dữ liệu trong 1 bảng thành vùng

# 5. Chuẩn hóa trong Database
- 1NF: Cột không chứa giá trị trùng lặp, tính toán được từ cột khác, trong cột chỉ chưa 1 giá trị duy nhất chứ ko phải nhiều giá trị trong đó
- 2NF: Chỉ chứa các trường liên quan khóa chính
- 3NF: Các trường chỉ liên quan khóa chính (tách bỏ ra những trường liên quan đến khóa chính nhưng vẫn tách được)

# 6. UNION: 
- Là câu lệnh SQL dùng để gom kết quả từ 2 bảng với nhau.
- Yêu cầu sử dụng: 
  - Kết quả 2 bên trả về số cột phải giống nhau
  - Cùng kiểu dữ liệu
## 6.1 Union với Union All: 
  - Giống nhau:
	  - Là sự kết hợp kết quả của 2 hoặc nhiều câu lệnh select trong sql
  - Khác nhau:
	  - Union: Chỉ trả về những kết quả không trùng lặp.
	  - Union All: Trả về tất cả các kết quả kể cả trùng lặp
 
  
# 7. So sánh Sub query và Inner Join
Sub query truy vấn nhanh hơn join vì Inner join sẽ phải lấy 2 bảng để so sánh. Còn sub query sẽ chỉ lấy những cái nào mình cần so sánh

# 8. Constraint
Là những quy tắc được áp dụng trên các cột dữ liệu trên bảng
- Not Null: Đảm bảo dữ liệu của cột không nhận giá trị null
- Default: Gán giá trị mặc định cho cột trong trường hợp dữ liệu không được nhập vào hoặc không xác định
- Unique: Đảm bảo dữ liệu của cột là duy nhất, không trùng lặp
- Primary key: Thiết lập khóa chính cho bảng, không cho phép null hoặc duplicate
- Foreign key: Thiết lập khóa ngoại trên bảng tham chiếu tới một giá trị duy nhất trong bảng khác
- Check: Đảm bảo dữ liệu đầu vào thỏa mã điều kiện như Where **(VD CHECK age > 1)**

# 9. Trigger:
- Dùng để thực hiện thêm 1 tác vụ trong khi đang làm tác vụ này VD: như trong khi thêm bảng này ta có thể thêm sửa xóa bảng khác
>>![](https://images.viblo.asia/180efac6-8957-48a8-bc32-b2b468e20b79.jpg)

# 10. Toán tử Join:
- Inner Join(hoặc Join): Trả về tất cả các hàng khi có ít nhất 1 giá trị  ở cả 2 bảng.
- Left Join: Trả lại tất cả các bản ghi từ bản bên trái và các dòng tương ứng trong bảng bên phải.
- Right Join: Trả lại tất cả các bản ghi từ bảng bên phải, và các bản ghi tương ứng trong  bảng bên trái.
- Outer Join: Trả về tất cả các bản ghi được kết hợp từ các bảng.
