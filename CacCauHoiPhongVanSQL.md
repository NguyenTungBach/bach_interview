# 1. Các loại Join
- Outter Join: Lấy hết cả 2 bảng chính và phụ thỏa mãn điều kiện phù hợp (cụ thể là khóa phụ và khóa chính)
- Left Join: Lấy tất cả bảng chính và lấy những phần tử bảng phụ mãn điều kiện
- Right Join: Lấy tất cả bảng phụ và lấy những phần tử bảng chính mãn điều kiện
- Full Join: Lấy tất cả kể cả không thỏa mãn điều kiện (bao gồm Null)

# 2. Vấn đề trong Join
- Nếu dùng Left Join và Right Join thì phải chú ý cẩn thận với các phần tử NULL
- Giả sử Left Join bảng có chính có 1 phần tử nào đó NULL mà tìm điều kiện với 1000 phần tử bảng phụ. Điều này sẽ dẫn đến 1 phần tử NULL sẽ phải so sánh với 1000 phần tử

# 3. Distinct
- Loại bỏ tất cả các bản ghi trùng lặp và chỉ lấy các bản ghi duy nhất
VD:

| id | name | class | score |
| ------ | ------ | ------ | ------ |
| 1 | John | A | 90 |
| 2 | Jane | A | 85 |
| 3 | Bob | B | 92 |
| 4 | Alice | C | 87 |
| 5 | Charlie | B | 85 |
| 6 | David | A | 90 |

```sh
SELECT DISTINCT department
FROM employees;
```
