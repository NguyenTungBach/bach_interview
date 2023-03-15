### 1 .Các câu hỏi phỏng vấn
- Em hãy mô tả bản thân, quá trình làm việc, kinh nghiệm của các dự án mà em đã từng trải qua
- Dự án nào mà em tâm đắc nhất
- Trong dự án, có những cách nào để tối ưu hóa hiệu năng trong lập trình
- Em có câu hỏi gì cho anh không?

### 2. Xử lý hệ thống bị chậm truy vấn lâu hay bị Timeout (Tracing)
- Sử dụng Tracing để tìm ra điểm nghẽn của nó. Tracing là kỹ thuật để theo dõi và ghi lại hoạt động xảy ra của chương trình. VD:
  ```sh
  public class Calculator {
    public static void main(String[] args) {
        int a = 10;
        int b = 5;
        int result = add(a, b);
        System.out.println("The sum of " + a + " and " + b + " is " + result);
    }

    public static int add(int a, int b) {
        // Tracing
        System.out.println("add method called with a=" + a + ", b=" + b);
        int result = a + b;
        System.out.println("add method returned " + result);

        return result;
    }
  }
  ```
Kỹ thuật tracing giúp chúng ta xác định được vị trí của các lỗi trong phương thức ***add*** và giải quyết chúng

- Để tracing thì ta cần phải biết nghiệp vụ của phần đó và ta sẽ check đường luồng từ đâu đến đâu. 
- Đặc điểm nhận biết giữa tracing và debug là tracing thì ta không biết code ở vị trí nào nên phải tìm luồng code. Còn debug thì biết rồi nên debug chỉ kiểm tra dữ liệu đầu ra bị lỗi ở đâu trong hàm

### 3 .TPS Counter
- TPS (Transactions Per Second) là một đơn vị đo lường tốc độ xử lý giao dịch của một hệ thống.
- TPS Counter (Transactions Per Second Counter) là một công cụ được sử dụng để giúp đo lường khả năng xử lý giao dịch của hệ thống và cung cấp thông tin về tình trạng hiện tại của hệ thống.
- Ta có thể sử dụng TPS Counter trong việc giới hạn request hệ thống. Giả sử trong 1s ta chỉ cho phép 1000 request, nếu request quá 1000 thì throw exception quá tải hệ thống

### 4 .Các thuật toán tìm kiếm cơ bản
- Thuật toán tuyến tính (Line Search): Duyệt qua từng phần tử, phần tử nào phù hợp thì trả ra
- Thuật toán tìm kiếm nhị phân (Binary Search): Thuật toán dựa vào thứ tự sắp xếp của tập hợp để chia nữa tập hợp, giảm số phần tử cần duyệt sau mỗi lần chia

![](https://blog.luyencode.net/wp-content/uploads/2018/07/thuat-toan-tim-kiem-nhi-phan-minh-hoa-code-su-dung-c-java.gif)
- Thuật toán tìm kiếm B-tree (hiện đang chưa rõ cách hoạt động thuật toán): Sắp xếp thàng dạng cây phân nhánh (bao gồm node gốc và các node con). Khi đứng ở 1 node phân nhánh sẽ luôn biết được node tiếp theo là gì

### 5 .Indexing
- Sigle Column Index: Index cho 1 cột duy nhất
- Index kiểu unique: Khóa chính của bảng không được trùng nhau, nhằm đảm bảo tính toàn vẹn dữ liệu
- Composite Index: Là chỉ mục kết hợp cho 2 hoặc nhiều cột trong bảng

### 6 .Các kiểu Index trong Database:
- Hash Index: Lưu index dưới dạng key value. Chỉ phù hợp với truy vấn chính xác. Trước khi truy vấn thì ở mỗi phần tử sẽ có một giá trị hash, khi truy vấn theo đối tượng nào thì chỉ hash giá trị đó và tìm giá trị hash trong Hash Index
- B - tree : mặc định khi tìm kiếm trong sql

### 7 .Các lưu ý khi đánh index
- Chỉ nên đánh index với những bảng có dữ liệu lớn (cỡ khoảng 100K trở lên) và thường xuyên phải truy vấn trên bảng đó.
- Chỉ đánh index cho các column thường xuyên theo mệnh đề Where hay Order by
- Không nên đánh index cho column có quá nhiều giá trị trùng lặp hoặc text dài
- Trường sử dụng nhiều column index thì cần chú ý thứ tự các column

### 8 .distinct 
- Loại bỏ tất cả các bản ghi trùng lặp và chỉ lấy các bản ghi duy nhất 

### 9 .UNION 
Là câu lệnh SQL dùng để gom kết quả từ 2 bảng với nhau.
Yêu cầu sử dụng:
  - Kết quả 2 bên trả về số cột phải giống nhau
  - Cùng kiểu dữ liệu

### 10 .Union với Union All
  - Giống nhau:
	  - Là sự kết hợp kết quả của 2 hoặc nhiều câu lệnh select trong sql
  - Khác nhau:
	  - Union: Chỉ trả về những kết quả không trùng lặp.
	  - Union All: Trả về tất cả các kết quả kể cả trùng lặp

### 11 .Kiến trúc database kiểu master slave
- Node master: chỉ phục vụ cho việc thêm sửa xóa
- Node slave: chỉ phục vụ cho việc search

### 12 .Cách tối ưu hóa truy vấn database
- Đánh index cho các cột sử dụng where, order by, group by
- Tránh sử dụng câu truy vấn like với '%' phía trước vì nó sẽ làm mất index cho cột được đánh index đó
- Chỉ lấy các trường cần thiết không lấy thừa.
- Sử dụng cache trong trường hợp truy vấn nhiều trong database
- Khi insert số lượng lớn, không insert lần lượt mà theo batch
- Đánh partition
- Dùng Distinct và Union khi cần

### 13 .Vì sao không nên đánh index cho nhiều bảng
- Khi thêm sửa xóa sẽ chậm vì có bảng sẽ phải sắp xếp lại
- Tăng bộ nhớ
- Chậm truy vấn vì hệ thống sẽ phải duyệt qua từng cột index theo điều kiện. Nếu where nhiều cột sẽ bị chậm

### 14 .Vì sao dùng index lại nhanh
- Vì index có thuật toán để tìm kiếm nhanh
