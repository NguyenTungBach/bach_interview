# 1. Đồng bộ và bất đồng bộ
- Đa luồng giúp giải quyết nhiều công việc cùng 1 lúc
- Bất đồng bộ (bài toán nấu cơm, trong lúc nấu cơm có thể làm nhiều việc). Trong lúc chờ công việc này có thể làm nhiều việc khác.( trong lúc chạy vì biết xử lý dòng 5 mất thời gian, thay vì đợi thì làm việc khác giúp tránh mất thời gian)

- Đồng bộ là chạy theo từng dòng. Dòng trên chưa xong thì dòng dưới nó ko đc chạy tiếp. (asyn, synchronization).

- Khác nhau giữa đồng bộ và bất đồng bộ là số người làm công việc. 
- Bất đồng bộ là 1 mình tôi làm nhưng nhiều công việc

- Đa luồng là nhiều người làm nhiều công việc. Vấn đề là về xung đột tài nguyên như thằng xào rau và rang thịt đều cần dùng chung cái chảo.

////////////// Kết luận chung
- Đồng bộ là các tác vụ theo 1 trình tự cụ thể, tiến trình tác vụ hiện tại xong thì mới đến tác vụ tiếp theo
- Bất đồng bộ là các tác vụ chạy đồng thời tiến trình chạy song song giữa các tác vụ. Khi nói đến Bất đồng bộ, ta nói đến đa luồng
- Đa luồng là một kỹ thuật lập trình cho phép các luồng chạy đồng thời cùng lúc.

# 2. Chu kỳ sống của thread trong java được kiểm soát bởi JVM
- New: tạo lớp Thread
- Runnable: sau khi gọi đến phương thức start(). Chuẩn bị chạy chương trình
- Running: Chạy chương trình
- Non-Runnable (Blocked): Trong quá trình Running. Thread bị sleep hoặc chặn vì phải đợi Thread khác chạy xong 
- Terminated: Kết thúc Thread	

# 3. Thread cách khởi tạo:
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

# 4. Thread và Process
- Thread là 1 đơn vị xử lý nhỏ nhất của việc thực thi một chương trình. Hiểu là 1 tiến trình con
- Tiến tình là một chương trình đang được chạy trên hệ thống. 1 tiến trình sẽ có nhiều luồng
- Mỗi tiến trình có một không gian địa chỉ riêng, một bộ đếm chương trình, một bộ đếm ngăn xếp, các tài nguyên hệ thống riêng và có thể có nhiều luồng ***(Không nên tìm hiểu quá sâu)***
  - Không gian địa chỉ riêng: là nơi tiến trình lưu trữ dữ liệu và đảm bảo an toàn dữ liệu của tiến trình. (Tức là nó được thanh RAM cấp không gian để chạy)
  - Bộ đếm chương trình: là con số dùng để xác định lệnh nào đang được thực thi trong chương trình. (Nằm trong CPU)
  - Bộ đếm ngăn xếp: là con số dùng để xác định vị trí hiện tại trên ngăn xếp của tiến trình.(Nằm trong CPU)
  - Các tài nguyên hệ thống riêng: bao gồm các tài nguyên mà tiến trình được cấp phát để sử dụng như bộ nhớ, bộ xử lý, các thiết bị I/O và các tài nguyên khác của hệ   thống.

# 5. Callable, Future, Executors là gì?
- Thay vì tạo thread bằng việc Extend Thread hoặc implement Runable và tự quản lý số lượng thread. Thì ta có một hướng tiếp cận khác đó là sử dụng Callable và Future. 
***(Cho phép hủy các thread, kiểm tra thread đã hoàn thành chưa, quản lý số thread chạy cùng lúc …)***
- Callablelà một interface trong java, nó định nghĩa một công việc và trả về một kết quả trong tương lai và có thể throw Exception
- Future là kết quả trả về của Callable, nó thể hiện kết quả của một phép tính không đồng bộ, cho phép kiểm tra trạng thái của phép tính 
(đã thực hiện xong chưa, kết quả trả về là gì…)
- 


