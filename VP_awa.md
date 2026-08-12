# Phỏng vấn HR / quy trình — AWA (ôn ~10 phút)

Nói ngắn: mỗi câu **20–40 giây**. Học theo ý, không thuộc máy.

**Công thức nhớ nhanh (nếu hỏi sâu):**
- Cash In: `còn phải thu = dư đầu + doanh số + thuế 10% − đã thu (+ điều chỉnh)`
- Cash Out: `còn phải trả = dư đầu + phí associate + thuế 10% − đã chi (+ điều chỉnh)`

---

## Tổng hợp câu hỏi

1. Quy trình nhận task → thực thi thế nào?
2. Khó khăn khi phát triển và cách vượt qua?
3. Tính năng tâm đắc / nếu làm lại thì cải thiện gì?
4. Có dùng AI không? Dùng thế nào cho tốt? Check độ chính xác ra sao?
5. Có đo thời gian / hiệu suất dùng AI không?
6. Có dùng đa dạng AI / kiểm tra chéo không?
7. Có làm với team không? Vận hành hiệu quả thế nào?
8. Mốc thời gian, cách estimate task?
9. Có phải thêm giờ không?
10. Có bị mệt mỏi / thiếu ngủ không?
11. Nhận bug từ người khác — quy trình xử lý?
12. Dự án cần cải thiện gì?
13. Làm tính năng mới cần hỗ trợ — cần gì?
14. Mong muốn phát triển?
15. Có hỏi gì về công ty không?
16. Kỳ vọng mức lương?

---

## Trả lời từng câu — bản tối ưu (AI)

### 1. Quy trình nhận task → thực thi?

> Nhận task → đọc yêu cầu, nắm luồng nghiệp vụ → thiết kế / chạm DB nếu cần → nếu có FE thì theo mockup → tách việc cần làm → code → tự test → đẩy staging / nhờ PM hoặc khách phản hồi → chỉnh rồi mới production.

---

### 2. Khó khăn và cách vượt qua?

> Khó nhất là nghiệp vụ tiền dày — Cash In / Cash Out. Em nhớ **luồng**, không thuộc hết công thức. Ví dụ còn phải thu = dư đầu + doanh số + thuế − đã thu. Khi có bug hoặc bị hỏi sâu, em đối chiếu lại code và dữ liệu.  
> Ngoài ra lúc yêu cầu khách chưa rõ (validate, danh sách chọn, message tiếng Nhật), em hỏi lại cho rõ rồi mới làm — tránh đoán sai.

---

### 3. Tính năng tâm đắc / làm lại thì tốt hơn?

> Tâm đắc **Cash In Statistical** — phần lớn tính toán thu tiền của hệ thống tập trung ở đây.  
> Nếu làm lại: (1) list show thêm doanh số và có search — hiện phải xuất/xóa đơn mới cập nhật, khó kiểm tra; (2) thiết kế DB chắc hơn từ đầu — dự án sửa schema nhiều lần; ví dụ từng có edit shift rồi bỏ vì màn Course đã đủ.

---

### 4. Dùng AI? Dùng tốt / check chính xác?

> Có dùng. AI không thay hiểu nghiệp vụ: em mô tả rõ luồng rồi mới gen. Sau đó review code xem nó làm gì, rồi test đúng hành vi — đặc biệt chỗ tiền và API. AI xong chưa phải xong.

---

### 5. Có đo thời gian / hiệu suất AI không?

> Có quan sát thực tế, chưa đo lab formal. Ví dụ mockup màn History: tự nghĩ layout + data mẫu ước ~2–3 ngày; có AI thường **dưới 1 ngày**, độ đúng khoảng **70–80%** — phần còn lại phải chỉnh và test.

---

### 6. Đa dạng AI / kiểm tra chéo?

> Chủ yếu Cursor để gen code trong dự án. Đôi khi hỏi thêm ChatGPT hoặc Gemini khi cần giải thích đoạn khó — mỗi bên diễn đạt khác, dễ hiểu hơn. Không phải quy trình “hai AI chấm nhau” cố định, mà dùng đúng lúc cần.

---

### 7. Làm với team? Vận hành hiệu quả?

> Có. Cách hay nhất là **chia task rõ** để giảm conflict: ví dụ một người FE, một người BE; hoặc mỗi người một màn / một module. Sync sớm khi đụng chung API hay DB.

---

### 8. Mốc thời gian / estimate?

> Estimate xong thì **ưu tiên** task gấp / chặn người khác trước. Trong ngày em gom việc khoảng **8 tiếng**; việc còn lại xếp hôm sau. Task lớn tách nhỏ để dễ theo dõi tiến độ.

---

### 9. Có thêm giờ không?

> Thường đủ 8 tiếng. Việc **cần xong trong ngày** thì em vẫn thêm giờ để bàn giao đúng hạn.

---

### 10. Mệt mỏi / thiếu ngủ?

> Có lúc bị, nhất là deadline. Em quen dần: ưu tiên việc quan trọng, nghỉ đúng lúc để hôm sau còn làm được.

*(Tránh nói dài về mệt — kết bằng kiểm soát được.)*

---

### 11. Nhận bug từ người khác — xử lý?

> Ưu tiên **tái hiện** → tìm chỗ lỗi → nguyên nhân → sửa → tự kiểm lại. Bug số liệu: thường lấy data staging/server về máy để so. Xong thì báo lại cách tái hiện và đã sửa gì.

---

### 12. Dự án cần cải thiện gì?

> Đây là hệ thống nội bộ, phụ thuộc yêu cầu khách. Em từng góp ý: show thêm thông tin doanh số / course trên list Cash In cho dễ đối chiếu — giảm phụ thuộc xuất PDF mới thấy số.

---

### 13. Tính năng mới cần hỗ trợ người khác?

> Thường khi đụng **công nghệ / pattern mới**. Em hỏi có tài liệu hoặc chỗ tương tự trong repo không, người trước xử lý thế nào — rồi tự làm tiếp, hỏi thêm khi kẹt.

---

### 14. Mong muốn phát triển?

> Hiện em làm fullstack và dùng AI hỗ trợ code. Định hướng sâu hơn về **phát triển / ứng dụng AI** (không chỉ gọi API dịch vụ sẵn). Nếu team chưa có hướng đó, em vẫn làm tốt fullstack và học song song.

---

### 15. Hỏi lại công ty? (chọn 1–2 câu)

> 1. CI/CD và deploy hiện tự động hết chưa, hay còn bước thủ công?  
> 2. Team đang đau điểm nào — DB, refactor, hay nợ kỹ thuật?  
> 3. Team chia BE/FE rõ hay theo hướng fullstack?

---

### 16. Kỳ vọng lương?

> Ở công ty cũ lương gắn khối lượng/dự án. Với vai trò và yêu cầu ở đây, em kỳ vọng khoảng **15–18 triệu**. Em cũng sẵn sàng trao đổi theo khung và phúc lợi của công ty.

---

## Thứ tự nói nếu bị giới hạn thời gian (~10 phút)

Ưu tiên nói chắc: **1 → 2 → 3 → 4 → 7 → 11 → 14 → 16**.  
Còn lại trả lời ngắn khi được hỏi. Câu 9–10 giữ 1 câu, đừng lan man.

//////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////
## Bản gốc — bạn viết (giữ nguyên ý, chưa tối ưu)
//////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////

- Quy trình từ khi phát triển phần mềm từ lúc nhận và thực thi sẽ làm thế nào? (Nhận task em sẽ phân tích yêu cầu để nắm được luồng bài toán ví dụ như thiết kế database -> mockup (nếu có yêu cầu làm FE) -> liệt kê những tính năng cần có -> test để xem tính năng đó có vấn đề gì không -> đẩy lên cho khách hoặc PM quản lý phản ánh)

- Phát triển như thế thì có gặp khó khăn gì và vượt qua tính huống này thế nào? (việc nhớ công thức của dự án này vì thi thoảng phải xem lại khi có người báo bug hoặc hỏi lại về công thức tính toán. Logic thì đơn cử Số tiền phải thu tháng này = dư tháng trước + doanh số + thuế - tiền nhận. Hay của cash out statical là Tiền còn phải trả tháng này = tiền phải trả tháng trước + phí vận chuyển + thuế - đã trả  
Vì nghiệp vụ dày nên em chỉ nhớ luồng hơn thuộc công thức,  
ngoài ra đổi khi bản thân chưa nắm rõ mong muốn phía bên khách nên cũng phải hỏi lại để làm rõ ví dụ như validate, các danh sách được chọn, lỗi trả về tiếng nhật như nào?)

- Tính năng tích nhất và nếu được làm lại thì làm thế nào để nó tốt hơn (em nghĩ là phần cash in statical vì tất cả tính toán của cả dự án này đều tập trung vào nó. Nếu được làm lại thì em muốn cập nhật show thêm phần doanh số trong list và có search vì bài toán yêu cầu phải xuất xóa đơn mới được cập nhât. Còn nữa là nếu được thì em muốn làm lại database vì quá trình làm dự án database đã bị sửa đi lại rất nhiều, thường sẽ phải để sẵn thêm cột hay bảng mới ví dụ trước đây có edit shift nhưng sau bỏ đi vì khách thấy màn course đã đủ rồi)

- Quá trình làm có dùng AI không, làm thế nào để nó dùng tốt hơn, làm sao để check độ chính xác? (Em có dùng. Vì mình không phải gõ tay dòng code nữa nên mình phải hiểu rõ luồng để mô tả cho AI, ngoài ra sau khi nó tạo xong thì cũng phải test nó đã hoạt động đúng chưa và xem kỹ nhất là xem nó đang làm những gì trong dòng code)

- Có đo đếm thời gian, hiệu suất sử dụng AI không? ( Ví dụ yêu cầu tự mockup màn chức năng quản lý history để biết tài khoản nào đã làm gì. Phần phác thảo này sửa đi sửa lại rất nhiều và nếu ước tính làm ban đầu để nghĩ ra dữ liệu mẫu đẹp hay sửa lại giao diện sẽ mất nhiều thời gian. Thường thì em ước tính nó mất tầm 2-3 ngày để vừa làm vừa liệt kê ra nhưng phần cần show nhưng có AI thường chỉ mất chưa đến 1 ngày. Đúng thì tầm 70-80%)

- Có dùng đa dạng AI không, có dùng AI để kiểm tra chéo nhau không? (Câu này khó trả lời. Vì chủ yếu hiện tại chỉ dùng cursor để gen code nhưng đôi khi cũng có dùng chat gpt hay gemini để ngồi hỏi đoạn code vì mỗi con có thể sẽ có câu trả lời mình dễ hiểu hơn)

- Có làm với team không, làm sao để nó vận hành hiệu quả? (Em có, thường chúng em sẽ chú ý đến phần chia task để tránh conflict trong dự án ví dụ 1 người làm fe 1 người làm BE hay tính năng mỗi người xử lý 1 màn)

- Các mốc thời gian, cách estimate task (Câu này khó, vì việc giao task sau khi ước lượng thời gian xong thì phải xem task nào ưu tiên trước. Và thường em sẽ nhóm sao cho các task đủ 8 tiếng trong ngày, những task sau để mai làm)

- Có phải thêm giờ ko? (Thường thì em vẫn đi làm đủ 8 tiếng, nhưng nếu công việc cần gấp xong trong hôm nay thì em vẫn sẽ thêm giờ)

- Có bị mệt mỏi thiếu ngủ không? (Cái này thì em cũng bị nhiều rồi nhưng dần quen)

- Khi mình phải nhận bug từ người khác thì quy trình xử lý thế nào? (Em sẽ ưu tiên tái hiên bug, tìm vị trí, nguyên nhân và sửa lỗi. Ví dụ bug báo về dữ liệu không đúng thì em phải lấy dữ liệu từ server về máy)

- Dự án này cần cải thiện gì không? (câu khó, vì đây là dự án nội bộ phụ thuộc vào phía bên yêu cầu của khách. Em cũng từng có góp ý như nãy bảo show thêm các course trong doanh số để tiện nhìn)

- Nếu phát triển 1 tính năng mới cần sự hỗ trợ từ người khác thì cần hỗ trợ gì? (Thường vụ hỗ trợ này liên quan đến công nghệ mới. Em sẽ hỏi có tài liệu tham khảo không, hay trước đây người ta xử lý thế nào để em có thể tự làm)

- Mong muốn phát triển (Hiện em đang làm Fullstack và ứng dụng AI, nhưng định hướng sắp tới của em là học hỏi sâu hơn về phát triển AI thay vì chỉ dừng lại ở mức gọi API hay tích hợp dịch vụ có sẵn. Nếu hiện công ty chưa đáp ứng được thì vẫn theo fullstack)

- Có hỏi gì về phía công ty không? ( Quy trình CI/CD và Deployment (triển khai) của công ty hiện tại đã tự động hóa hoàn toàn chưa, hay team vẫn đang deploy thủ công? Đội ngũ hiện tại đang phải xử lý khó khăn gì ko, ví dụ tối ưu DB, hay refactor code? Hiện tại team có chia rõ Backend/Frontend hay Fullstack?

- Kỳ vọng mức lương (Mức lương ở công ty cũ được xây dựng dựa trên khối lượng công việc của dự án đó. Còn tại đây, với yêu cầu công việc mới, em kỳ vọng mức lương khoảng 15 - 18 triệu ạ)
