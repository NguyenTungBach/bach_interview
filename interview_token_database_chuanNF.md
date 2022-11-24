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

# 5.Chuẩn hóa trong Database
- 1NF: Cột không chứa giá trị trùng lặp, tính toán được từ cột khác, trong cột chỉ chưa 1 giá trị duy nhất chứ ko phải nhiều giá trị trong đó
- 2NF: Chỉ chứa các trường liên quan khóa chính
- 3NF: Các trường chỉ liên quan khóa chính (tách bỏ ra những trường liên quan đến khóa chính nhưng vẫn tách được)

# 6. UNION: 
- Là câu lệnh SQL dùng để gom kết quả từ 2 bảng với nhau.
- Yêu cầu sử dụng: 
  - kết quả 2 bên trả về số cột phải giống nhau
  - Cùng kiểu dữ liệu
