### 1. Pojo là gì?
- Là lớp được triển khai các đặc điểm cơ bản nhất trong java như  như các thuộc tính, getter/setter, constructor và các phương thức equals(), hashCode(), toString().

### 2. IOC và DI?
- IOC dựa trên nguyên tắc ***(nguyên tắc là yêu cầu)*** solid. Trong nguyên tắc có nguyên lý ***(lý thuyết)*** DIP.
- Nguyên lý DIP chỉ ra các class không giao tiếp với nhau thông qua lớp triển khai (lớp implement gì gì đó) mà thống qua lớp trừu tượng (các interface, abtract)
- Dựa trên nguyên lý đó IOC tạo ra IOC Container để quản lý sự phụ thuộc.
- Còn DI và IOC về bản chất nó giống nhau là để giảm sự phụ thuộc. DI là một trong những triển khai của IOC
