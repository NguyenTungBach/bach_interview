### 1 .Các câu hỏi phỏng vấn
- Em hãy mô tả bản thân, quá trình làm việc, kinh nghiệm của các dự án mà em đã từng trải qua
- Dự án nào mà em tâm đắc nhất
- Trong dự án, có những cách nào để tối ưu hóa hiệu năng trong lập trình
- Em có câu hỏi gì cho anh không?

### 2. Xử lý hệ thống bị chậm truy vấn lâu hay bị Timeout (Tracing)
- Sử dụng Tracing. Tracing là kỹ thuật để theo dõi và ghi lại hoạt động xảy ra của chương trình. VD:
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

### 3 .TPS Counter
- TPS (Transactions Per Second) là một đơn vị đo lường tốc độ xử lý giao dịch của một hệ thống.
- TPS Counter (Transactions Per Second Counter) là một công cụ được sử dụng để giúp đo lường khả năng xử lý giao dịch của hệ thống và cung cấp thông tin về tình trạng hiện tại của hệ thống.
- Ta có thể sử dụng TPS Counter trong việc giới hạn request hệ thống. Giả sử trong 1s ta chỉ cho phép 1000 request, nếu request quá 1000 thì throw exception
