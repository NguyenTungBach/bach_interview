# 1. biến static
- là biến cục bộ gọi đến mà không cần phải khởi tạo
- Cấp phát bộ nhớ chỉ xảy ra một lần nên tiết kiệm bộ nhớ

# 2 .hàm static
- Gọi được trực tiếp, không cần phải khởi tạo
- 1 phương thức static không gọi được this hay supper vì làm thế sẽ gọi đến instance của lớp
- 1 phương thức static không thể ghi đè vì nó là nó được gọi trực tiếp thông qua lớp chứ không phải qua đối tượng ***(Tức là nó tồn tại trong phạm vi của lớp chứ không phải trong phạm vi đối tượng cụ thể của lớp đ)***
- chỉ gọi đến biến static
- hàm thường có thể gọi đến hàm static
- hàm static có thể gọi đến hàm thường

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

# 4. Khối static
- Được sử dụng để khởi tạo thành viên dữ liệu static,nó được thực thi trước lúc hàm main đc chạy
- VD:
```sh
public class Example {
    static {
        System.out.println("Khối static được thực thi!");
    }

    public static void main(String[] args) {
        System.out.println("Phương thức main được thực thi!");
    }
}
```

# 5. biến final
- Là biến không được thay đổi. Nếu thay đổi sẽ báo lỗi

# 6. hàm final
- là hàm sẽ không bị ghi đè ***(Giống phương thức với static)***. Điều này là để đảm bảo nó sẽ không bị thay đổi và giữ nguyên chức năng

# 7. lớp final
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

# 8. list final: 
- thay đổi đc nhưng khi new 1 collection mới có lỗi
