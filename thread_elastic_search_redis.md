# 1. In-memory Database (IMDB) là gì?
- Là một loại cơ sở dữ liệu, sử dụng bộ nhớ của máy tính để lưu trữ

# 2. Redis là gì?
- Là In-memory Database và cụ thể hơn là 1 no sql database **(Không có những khái niệm như bảng, table)**. Tất cả dữ liệu đều được lưu dưới dạng key value pair **(cặp khóa có giá trị)** **(giống như JSON cũng có 1 key value thì ta có thể nhìn Redis như là 1 JSON to)**
- Khác với các database lưu trên disk thì REDIS lưu trên RAM. **Mặc dù xử lý nhanh nhưng Điều này dẫn đến 1 vấn đề đó là khi ta khởi động máy tính thì tất cả bộ nhớ trên RAM cũng mất luôn. Nếu đang sử dụng server mà đùng cái mất điện thì xác định mất toàn bộ dữ liệu Redis nếu không Back Up**
- Tóm lại redis là 1 In-memory Database database (sử dụng bộ nhớ máy tính lưu trên Ram)
- Chính vì nhưng điều này mà Redis không dùng để lưu dữ liệu. Mà nó dùng để lưu những dữ liệu dùng đi dùng lại (tài khoản, user id), dùng cho web (VD thông tin người dùng), bộ nhớ đệm để sau có thể sử dụng sau này. Đó là lý do Redis Cache thường được dùng
- Caching là một kỹ thuật tăng độ truy xuất dữ liệu và giảm tải cho hệ thống. Lưu ý phải update cache
- Cache server
- Rabitt MQ là 1 message queue
- Thường để lưu dữ liệu dụng JSON
- Enqueue (Ghi) và Dequeue (Đọc)

# 2. Redis các ứng dụng
- Caching
- Counting (đếm lượt view)
- Pubsub (Hiện thông báo, lấy thông tin chung)
- Message broker (modul trung gian trung chuyển message từ người gửi đến người nhận)

# 3. Caching
- Là một kỹ thuật giúp hệ thống tăng tốc độ truy vấn dữ liệu và giảm tải truy vấn. Bằng cách lưu trữ và dùng lại các dữ liệu đã được truy vấn từ trước, giúp cho hệ thống không phải truy vấn lại.

# 3. Ưu và nhược điểm của redis
- Cùng nằm trong Spring Framework

|  | Ưu | Nhược |
|---|---|---|
| Lưu trữ | Lưu trên RAM nên truy vấn nhanh | Lưu trên RAM khi khởi động lại máy, hay sever thì dữ liệu sẽ mất hết nếu không Back up |
| Single Thread | Sử dụng IO mutilplexing | ??? |
| Tính nhất quán dữ liệu | ??? | vấn đề xảy ra khi cả hay cùng update dữ liệu |

# 4. Đồng bộ và bất đồng bộ
- Đa luồng giúp giải quyết nhiều công việc cùng 1 lúc
- Bất đồng bộ (bài toán nấu cơm, trong lúc nấu cơm có thể làm nhiều việc). Trong lúc chờ công việc này có thể làm nhiều việc khác.( trong lúc chạy vì biết xử lý dòng 5 mất thời gian, thay vì đợi thì làm việc khác giúp tránh mất thời gian)

- Đồng bộ là chạy theo từng dòng. Dòng trên chưa xong thì dòng dưới nó ko đc chạy tiếp. (asyn, synchronization).

- Khác nhau giữa đa luồng và bất đồng bộ là số người làm công việc. 
- Bất đồng bộ là 1 mình tôi làm nhưng nhiều công việc

- Đa luồng là nhiều người làm nhiều công việc. Vấn đề là về xung đột tài nguyên như thằng rửa rau và rang thịt đều cần dùng chung cái bếp.

# 4. Chu kỳ sống của thread trong java được kiểm soát bởi JVM
- New: tạo lớp Thread
- Runnable: sau khi gọi đến phương thức start(). Chuẩn bị chạy chương trình
- Running: Chạy chương trình
- Non-Runnable (Blocked): Trong quá trình Running. Thread bị sleep hoặc chặn vì phải đợi Thread khác chạy xong 
- Terminated: Kết thúc Thread	

# 4. Thread cách khởi tạo:
- Cách 1: extend từ Thread 
```sh
package com.gpcoder.flow;
 
public class ThreadDemo extends Thread {
    private Thread t;
    private String threadName;
 
    ThreadDemo(String name) {
        threadName = name;
        System.out.println("Creating " + threadName);
    }
 
    @Override
    public void run() {
        System.out.println("Running " + threadName);
        try {
            for (int i = 4; i > 0; i--) {
                System.out.println("Thread: " + threadName + ", " + i);
                // Let the thread sleep for a while.
                Thread.sleep(50);
            }
        } catch (InterruptedException e) {
            System.out.println("Thread " + threadName + " interrupted.");
        }
        System.out.println("Thread " + threadName + " exiting.");
    }
 
    public void start() {
        System.out.println("Starting " + threadName);
        if (t == null) {
            t = new Thread(this, threadName);
            t.start();
        }
    }
 
}
```

```sh
package com.gpcoder.flow;
 
public class ThreadDemoTest {
    public static void main(String args[]) {
        System.out.println("Main thread running... ");
 
        ThreadDemo T1 = new ThreadDemo("Thread-1-HR-Database");
        T1.start();
 
        ThreadDemo T2 = new ThreadDemo("Thread-2-Send-Email");
        T2.start();
 
        System.out.println("==&gt; Main thread stopped!!! ");
    }
}
```

```sh
Main thread running...
Creating Thread-1-HR-Database
Starting Thread-1-HR-Database
Creating Thread-2-Send-Email
Starting Thread-2-Send-Email
==&amp;amp;gt; Main thread stopped!!!
Running Thread-1-HR-Database
Running Thread-2-Send-Email
Thread: Thread-2-Send-Email, 4
Thread: Thread-1-HR-Database, 4
Thread: Thread-1-HR-Database, 3
Thread: Thread-2-Send-Email, 3
Thread: Thread-2-Send-Email, 2
Thread: Thread-1-HR-Database, 2
Thread: Thread-2-Send-Email, 1
Thread: Thread-1-HR-Database, 1
Thread Thread-2-Send-Email exiting.
Thread Thread-1-HR-Database exiting.
```
- Cách 2: impliment từ Runable
```sh
package com.gpcoder.flow;
 
class RunnableDemo implements Runnable {
    private Thread t;
    private String threadName;
 
    RunnableDemo(String name) {
        threadName = name;
        System.out.println("Creating " + threadName);
    }
 
    @Override
    public void run() {
        System.out.println("Running " + threadName);
        try {
            for (int i = 4; i > 0; i--) {
                System.out.println("Thread: " + threadName + ", " + i);
                // Let the thread sleep for a while.
                Thread.sleep(50);
            }
        } catch (InterruptedException e) {
            System.out.println("Thread " + threadName + " interrupted.");
        }
        System.out.println("Thread " + threadName + " exiting.");
    }
 
    public void start() {
        System.out.println("Starting " + threadName);
        if (t == null) {
            t = new Thread(this, threadName);
            t.start();
        }
    }
 
}
```

```sh
package com.gpcoder.flow;
 
public class RunnableDemoTest {
    public static void main(String args[]) {
        System.out.println("Main thread running... ");
 
        RunnableDemo R1 = new RunnableDemo("Thread-1-HR-Database");
        R1.start();
 
        RunnableDemo R2 = new RunnableDemo("Thread-2-Send-Email");
        R2.start();
 
        System.out.println("==&gt; Main thread stopped!!! ");
    }
}
```

```sh
Main thread running...
Creating Thread-1-HR-Database
Starting Thread-1-HR-Database
Creating Thread-2-Send-Email
Starting Thread-2-Send-Email
==&amp;amp;gt; Main thread stopped!!!
Running Thread-1-HR-Database
Running Thread-2-Send-Email
Thread: Thread-1-HR-Database, 4
Thread: Thread-2-Send-Email, 4
Thread: Thread-1-HR-Database, 3
Thread: Thread-2-Send-Email, 3
Thread: Thread-1-HR-Database, 2
Thread: Thread-2-Send-Email, 2
Thread: Thread-1-HR-Database, 1
Thread: Thread-2-Send-Email, 1
Thread Thread-1-HR-Database exiting.
Thread Thread-2-Send-Email exiting.
```

- Cách 3: tải thư viện

# 5. Thread và Process
- Thread là 1 đơn vị xử lý nhỏ nhất của máy tính, hoạt động của cpu
- Process là 1 app dựng lên

# 6. Khi nào dùng thread


# 7. @Cache able và Redis Template

# 8. Elastic search
- thường lưu log (VD: log xem quảng cáo, thời gian xem của người dùng)
- Là search engine
- lưu dưới dạng bảng

# 9. Biết đang dùng index
- 
