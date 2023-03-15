# 1. biến static
- là biến cục bộ gọi đến mà không cần phải khởi tạo
- Cấp phát bộ nhớ chỉ xảy ra một lần nên tiết kiệm bộ nhớ

# 2 .hàm static
- Gọi được trực tiếp, không cần phải khởi tạo
- 1 phương thức static không gọi được this hay supper vì làm thế sẽ gọi đến instance của lớp
- 1 phương thức static không thể ghi đè vì nó là nó được gọi trực tiếp thông qua lớp chứ không phải qua đối tượng
- chỉ gọi đến biến static

# 3. class static
- cho phép truy cập các thành viên dữ liệu tĩnh của lớp ngoài
- VD:
```sh
class TestOuter1 {
    static int data = 30;
 
    static class Inner {
        void msg() {
            System.out.println("data is " + data);
        }
    }
 
    public static void main(String args[]) {
        TestOuter1.Inner obj = new TestOuter1.Inner();
        obj.msg();
    }
}
```

# 4. biến final
- Là biến không được thay đổi. Nếu thay đổi sẽ báo lỗi

# 5. hàm final
- là hàm sẽ không bị ghi đè. Giống phương thức với static

# 6. lớp final
- là lớp không thể kế thừa từ lớp này hoặc ghi đè các phương thức trong lớp
- VD:
```sh
public final class Circle {
    private final double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    public double getRadius() {
        return radius;
    }

    public double getArea() {
        return Math.PI * radius * radius;
    }
}
```
