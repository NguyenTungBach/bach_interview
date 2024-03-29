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

# 3. Fine turning (Tinh chỉnh)
- Lấy một model đã được train, ta train nó thành của mình để ta sử dụng cho bản thân

<img width="880" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/8e0e96c5-a904-466e-9dc7-5d331faa5835">

- Có 3 cách Fine turning
  -  Self-supervised: Kiểm một model tự học và một dữ liệu text của chúng ta, ném vào cho model tự học. Sau một thời gian tự học sẽ sinh ra câu văn theo dữ liệu của chúng ta
  -  Supervised: Kiếm một input và output để train cho nó thành một model question answear
  -  Reinforcing (gia cố): ???

<img width="864" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/7bd22548-15b1-4872-b212-c0d58913136b">

# 4. Hugging Face
- Là một nơi thư viện chứa nhiều api để hỗ trợ train AI, fine tune

# 5. Google Colab
- Giải quyết vấn đề train model vì máy yếu nên train lâu

# 6. LangChain
- Chanin là một chuỗi mắt xích kèm block được thục hiện lần lượt. Ví dụ mắt xích 1 có in out, thì mắt xích 2 sẽ lấy out mắt xích 1 để xử lý ra out
- Là một framework giúp hỗ trợ phát triển Large Language Model. Cấu trúc tổng quan gồm
  - Model I/O
    - Model: Large Language Model, sử dụng để load vào LangTrain, hiểu ý định người dùng và sinh ra các từ ngữ đoán
    - Prompt: Dấu nhắc để đưa vào trong Model, giúp model hiểu ý muốn
  - Retrieval
    - Retriever: Cơ sở dữ liệu lưu dạng vector
    - Document Loader: Load toàn bộ văn bản cần xử lý, query nhanh chóng thay vì ta phải viết hàm đọc file PDF thủ công
    - Vector Store: DB lưu vector đặc trưng từng văn bản
    - Text Spliter: Thay vì lưu cả văn bản dài thì sẽ chia văn bản thành từng đoạn nhỏ
    - Embedding Model: Chuyển văn bản thành một vector đặc trưng. Giúp tìm ra văn bản phù hợp với query để LLM trả ra cho người dùng

# 7. Vector DB
- Vì LLM không thể nào nhìn được toàn bộ văn bản, chỉ nhìn được một đoạn. Nên ta sẽ chia nhỏ văn bản ra thành nhiều đoạn, mỗi đoạn sẽ được đi qua model embedding để sinh ra vector đặc trưng và vector này sẽ được đưa vào DB nên được gọi là vector DB

<img width="825" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/703d5d5b-ce55-4b34-baf6-8468745af019">

<img width="770" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/5b3e71b1-3af6-40bb-a3b7-276305ddbd81">

- Khi dùng nhập vào một văn bản, nó sẽ được embedding thành vector. Vector này sẽ được đưa vào Vector DB so sánh để lấy ra những đoạn văn bản mà liên quan nhất đến câu query đấy. Những văn bản được lấy ra sẽ được đưa cho LLM để sinh ra trả lời cho người dùng

- Luồng model để query chat hỏi đáp nội dung văn bản:
  - Chuẩn bị dữ liệu câu trả lời, văn bản để chia nhỏ và embedding vào vector DB lưu trữ. Ở đây ta sử dụng Text Spliter và Model Embedding
  - B1: Khi người dùng nhập câu hỏi. Prompt sẽ đưa vào Model LLM để biết cần query gì?
  - B2: LLM sẽ xử lý embedding nội dụng câu hỏi và gọi vào Vector DB để lấy các câu trả lời
  - B3: Sau khi nhận câu trả lời từ Vector DB, LLM sẽ chọn generate câu trả lời cho người dùng 

<img width="885" alt="image" src="https://github.com/NguyenTungBach/bach_interview/assets/78024702/cdbb194a-5a70-46c4-b0ab-19af01e72ace">
