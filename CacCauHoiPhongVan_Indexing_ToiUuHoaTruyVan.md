### 1.Các câu hỏi phỏng vấn
- Em hãy mô tả bản thân, quá trình làm việc, kinh nghiệm của các dự án mà em đã từng trải qua
- Dự án nào mà em tâm đắc nhất
- Trong dự án, có những cách nào để tối ưu hóa hiệu năng trong lập trình
- Em có câu hỏi gì cho anh không?

### 2.Xử lý hệ thống bị chậm truy vấn lâu hay bị Timeout (Tracing)
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
