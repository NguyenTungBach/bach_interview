### 0. Array
- Là một mảng cố định với các phần tử cùng iểu cố định

### 1. List?
- Các phần tử được sắp xếp có thứ tự và có thể có giá trị giống nhau
    - ### 1.1) ArrayList: 
         - Là mảng động
         - Chứa được các phần tử trùng lặp
         - Sử dụng một mảng (array) để lưu trữ các phần tử
         - Truy vấn bằng index
         - Lý do thường dùng ArrayList bởi khi lấy dữ liệu từ database nhỏ và tốc độ sửa xóa không chênh quá nhiều
    - ### 1.2) Vector:
         - Giống ArrayList nhưng các phương thức của vector theo hướng thread đồng bộ. Khi chạy luồng sẽ đảm bảo các phần tử thêm vào theo trình tự
    - ### 1.3) LinkedList: 
        - Lưu dưới dạng danh sách liên kết để lưu nên việc thêm hoặc xóa nhanh đối với phần tử đầu và cuối
        - Tốc độ truy cập các phần tử tương đối chậm hơn ArrayList và Vector do phải duyệt qua từng phần tử

### 2. Set?
- Các phần tử là duy nhất, không chứa các phần tử chùng lặp
    - HashSet: 
        - Không chứa các phần tử trùng lắp, vị trí các phần tử lưu dưới dạng mã băm thông qua HashCode
    - TreeSet: 
        - Lưu trữ các phần tử theo thứ tự tăng dần hoặc giảm dần và không cho phép phần tử trùng lặp
    - LinkedHashSet: 
        - Lưu trữ các phần tử theo thứ tự chèn và không cho phép phần tử trùng lặp
    
    
### 3. Map?
- Lưu trữ các cặp key/value, key của các phần tử này là duy nhất
    - HashMap: 
        - key của các phần tử này là duy nhất, vị trí các phần tử lưu dưới dạng mã băm thông qua HashCode

### 4. Queue?
- Các phần tử được sắp xếp và xử lý theo FIFO (first in first out: vào trước ra trước)
- Lấy hay gọi ra là mất phần tử đó

### 5. Deque?
- Các phần tử được sắp xếp và xử lý theo FIFO và LIFO (last in first out: vào cuối ra trước).

### 6. Phân biệt list và array ?
- Array: 
    - cố định kích thước
    - Chứa được cả 2 dữ liệu đối tượng và nguyên thủy
- List: 
    - có thể mở rộng kích thước
    - Chỉ chứa được các kiểu dữ liệu đối tượng, không chứa được kiểu dữ liệu nguyên thủy
