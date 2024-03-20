# 1.LLM (Large Language Model)
- Large Language Model là một thứ được train, được nghe, được nói hàng này và sau này có thể đoán ra một số từ tiếp theo của một câu nói (Ví dụ như dạy vẹt, nói muốn ăn bánh, thịt, cơm. Sau này khi ta nói *muốn ăn* thì con vẹt có thể trả lời là *cơm* dựa trên xác xuất câu trả lời nhiều nhất). Về sau ở đây được train bởi dữ liệu lớn, có thể trả lời nhiều câu hỏi.
- Language Model là một model xác xuất mà có thể generate ra các từ ngữ dựa trên đã được train
- Large Language Model khác Language Model ở chỗ được có kiến trúc *deep learning* train bởi số lượng dữ liệu lớn hơn Language Model

# 2.Transformer architect (kiến trúc chuyển đổi)
- Là kiến trúc thay vì dịch từng từ một thì ném cả câu văn để dịch, mục đích để rút thời gian tính toán.
<img width="725" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/a273c48a-4387-4ae4-9529-98689d7ac002">

- Các tính năng gồm:
  - Positional Encoding: Đánh dấu thứ tự từ nào trước từ nào sau trong câu văn
  - Attendtion và Self Atendtion: Nhận biết, liên hệ được giữa các từ trong câu. Để biết cần chú trọng vào từ nào

# 3. Fine_turning
- Lấy một model đã được train, ta train nó thành của mình để ta sử dụng cho bản thân

<img width="880" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/8e0e96c5-a904-466e-9dc7-5d331faa5835">
