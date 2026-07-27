# Bản nộp — Tìm trọ trước và sau AI

> Bài nộp này mô tả quá trình đi từ problem scan → chọn vấn đề ưu tiên → phân tích workflow hiện tại → xác định bottleneck → đề xuất Rule / Workflow / Agent → thiết kế quy trình trước và sau AI → đưa ra quyết định cuối.

Case lựa chọn: **Hỗ trợ sinh viên và người mới đi làm tìm, lọc và so sánh phòng trọ phù hợp**

Nhân vật chính: **Nam**, sinh viên tham gia chương trình VinAI-20K, cần tìm phòng trọ tại Hà Nội. Nam muốn phòng nằm trong khoảng di chuyển hợp lý tới nơi học, địa điểm học offline và nơi làm thêm; đồng thời phải phù hợp ngân sách, có tiện ích cơ bản, khu vực an toàn và thuận tiện ăn uống.

---

## Vì sao đây là một problem đáng ưu tiên?

- Có actor cụ thể: sinh viên và người mới đi làm đang cần thuê trọ.
- Workflow hiện tại gồm nhiều bước thủ công, lặp lại và phân tán trên nhiều nền tảng.
- Người thuê phải cân bằng nhiều tiêu chí xung đột, không chỉ tìm phòng “gần nhất” hoặc “rẻ nhất”.
- Bottleneck rõ: thu thập, chuẩn hóa, xác minh và so sánh thông tin giữa các tin đăng.
- Hậu quả có thể đo được bằng thời gian tìm kiếm, số chuyến đi xem phòng và rủi ro mất cọc.
- AI có thể hỗ trợ tìm kiếm đa tiêu chí, tóm tắt, so sánh và phát hiện dấu hiệu rủi ro.
- Vẫn có ranh giới con người rõ ràng: người thuê phải trực tiếp xác minh, xem phòng, đọc hợp đồng và quyết định đặt cọc.

---

# 01 — Individual Problem Scan

## Scan rộng

Từ trải nghiệm của sinh viên VinAI-20K, có thể quan sát các pain point sau:

| # | Lăng kính | Problem quan sát được | Ai chịu ảnh hưởng? | Dấu hiệu thật |
|---|---|---|---|---|
| 1 | Lặp lại | Mỗi ngày phải đọc Slack, Discord, Notion và GitHub để biết task mới và deadline | Sinh viên VinAI-20K | Mất khoảng 20–40 phút/ngày, dễ bỏ sót thông báo |
| 2 | Lặp lại | Viết daily hoặc weekly report từ commit, task và tin nhắn nhóm | Sinh viên, Team Lead | Mất khoảng 30–60 phút/lần, nội dung thường lặp lại |
| 3 | Tốn thời gian | Đọc paper, slide và documentation dài nhưng khó tìm đúng phần cần dùng | Sinh viên AI | Có thể mất 1–3 giờ/tài liệu và phải tìm lại nhiều lần |
| 4 | Tốn thời gian | Cài đặt Python, dependency, CUDA, Docker và sửa lỗi môi trường | Sinh viên AI, Developer | Một lỗi có thể làm mất vài giờ hoặc cả ngày |
| 5 | AI có thể tốt hơn | Phân tích log lỗi và xác định nguyên nhân gốc còn phụ thuộc nhiều vào việc hỏi thủ công | Sinh viên AI | Copy log qua nhiều công cụ, thử nhiều cách nhưng không biết cách nào đáng tin |
| 6 | AI có thể tốt hơn | Kiến thức nằm rải rác trong PDF, ghi chú, video, hội thoại AI và repository | Sinh viên AI | Khó tìm lại nguồn, mất thời gian ôn tập và kết nối kiến thức |
| 7 | Pain từ người khác | Tin phòng trọ nằm rải rác trên Facebook, Chợ Tốt và website; thông tin thiếu hoặc đã cũ | Sinh viên, người mới đi làm | Mất nhiều giờ hoặc nhiều ngày để lọc và liên hệ |
| 8 | Pain từ người khác | Khó tìm teammate có kỹ năng phù hợp hoặc nắm rõ ai đang phụ trách phần nào | Sinh viên VinAI-20K | Phân công chồng chéo, thiếu người ở một số task, chậm tiến độ |
| 9 | Ra quyết định đa tiêu chí | Người thuê muốn gần nhiều địa điểm nhưng đồng thời cần giá thấp, phòng đẹp và khu vực tiện lợi | Sinh viên, người mới đi làm | Khó biết nên đánh đổi tiêu chí nào, thường thay đổi quyết định sau khi đi xem |
| 10 | Rủi ro thông tin | Tin đăng có thể dùng ảnh cũ, giá mồi, thiếu phí dịch vụ hoặc yêu cầu cọc trước | Người thuê trọ | Tốn chi phí đi lại, thuê nhầm phòng hoặc có nguy cơ mất tiền cọc |

### Vì sao phần scan này mạnh?

- Scan rộng trước khi chọn giải pháp.
- Bao phủ nhiều lăng kính: lặp lại, tốn thời gian, AI có thể làm tốt hơn, pain từ người khác, ra quyết định và rủi ro.
- Mỗi vấn đề đều có actor và dấu hiệu quan sát được.
- Không bắt đầu từ ý tưởng “làm chatbot tìm trọ”, mà bắt đầu từ workflow thực tế của người thuê.
- Cho thấy tìm trọ không chỉ là bài toán tìm kiếm, mà còn là bài toán so sánh, đánh đổi và xác minh.

---

## Top 3 problems

| Rank | Problem | Vì sao chọn | Điều còn chưa chắc |
|---|---|---|---|
| 1 | Tìm, lọc và so sánh phòng trọ | Pain rõ, nhiều người gặp, workflow dài, có rủi ro tài chính và có thể đo thời gian | Khả năng truy cập dữ liệu và xác minh tin đăng theo thời gian thực |
| 2 | AI Debug Assistant | Phù hợp năng lực kỹ thuật của nhóm, tần suất sử dụng cao | Thị trường đã có nhiều công cụ mạnh, khó tạo khác biệt |
| 3 | Trợ lý quản lý kiến thức học tập | Dữ liệu dễ kiểm soát, phù hợp RAG | Giá trị mới có thể chưa đủ mạnh so với các công cụ ghi chú hiện có |

---

# 02 — Problem Card #1: Tìm trọ đa tiêu chí

## Problem 1 câu

Sinh viên và người mới đi làm mất nhiều giờ hoặc nhiều ngày để tìm được phòng trọ phù hợp vì tin đăng phân tán, thông tin không đồng nhất, khó so sánh theo nhiều tiêu chí và khó xác minh độ tin cậy.

## Actor

### Actor chính

Sinh viên hoặc người mới đi làm đang chuyển đến một khu vực mới và cần thuê phòng trong thời gian ngắn.

### Actor phụ

- Người thân hỗ trợ tìm phòng.
- Bạn bè cùng thuê.
- Chủ nhà và người quản lý phòng.
- Môi giới hoặc nhân viên sale.
- Người thuê cũ có kinh nghiệm về khu trọ.

## Thời điểm / bối cảnh

- Trước kỳ học mới hoặc trước ngày bắt đầu công việc.
- Khi chuyển địa điểm học, thực tập hoặc làm việc.
- Khi hợp đồng hiện tại sắp hết hạn.
- Khi giá thuê tăng hoặc điều kiện phòng hiện tại không còn phù hợp.
- Khi người thuê chỉ có khoảng vài ngày đến hai tuần để ra quyết định.

---

## Thực trạng quan sát được

Người thuê thường có nhiều yêu cầu cùng lúc:

- Muốn gần địa điểm A để đi học.
- Muốn không quá xa địa điểm B để làm việc hoặc tham gia chương trình.
- Muốn thuận tiện tới địa điểm C như trường, văn phòng, bến xe hoặc nhà người thân.
- Muốn giá thuê nằm trong ngân sách.
- Muốn phòng sạch, đẹp, có điều hòa, nóng lạnh, chỗ để xe và an ninh.
- Muốn khu vực có đồ ăn hợp túi tiền, chợ, cửa hàng tiện lợi và dịch vụ thiết yếu.
- Muốn ít phí phát sinh.
- Muốn hợp đồng rõ ràng và không gặp lừa đảo.

Đây không nên được xem đơn giản là “tiêu chuẩn kép”. Bản chất là một **bài toán ra quyết định đa tiêu chí**, trong đó người thuê phải đánh đổi giữa:

```text
Khoảng cách ↔ Giá thuê
Chất lượng phòng ↔ Ngân sách
Vị trí trung tâm ↔ Diện tích
Tiện ích ↔ Phí dịch vụ
Giá rẻ ↔ Độ tin cậy
Quyết định nhanh ↔ Mức độ xác minh
```

---

## Current workflow

```text
1. Xác định ngân sách và khu vực mong muốn
2. Tìm bài đăng trên nhiều Facebook Group
3. Tìm thêm trên Chợ Tốt và các website phòng trọ
4. Lưu link hoặc chụp màn hình các phòng có vẻ phù hợp
5. Đọc từng bài để lấy giá, địa chỉ, diện tích và tiện ích
6. Nhắn tin hoặc gọi cho chủ trọ / sale
7. Hỏi lại giá thực tế, tiền cọc và các khoản phí
8. Kiểm tra phòng còn hay đã được thuê
9. Mở bản đồ để ước lượng khoảng cách đến các địa điểm quan trọng
10. Tự so sánh các phòng bằng ghi chú, Excel hoặc trí nhớ
11. Sắp xếp lịch đi xem nhiều phòng
12. Đến xem và phát hiện một số phòng không giống mô tả
13. Kiểm tra hợp đồng, người cho thuê và điều kiện đặt cọc
14. Chọn phòng hoặc quay lại tìm từ đầu
```

---

## Các dữ liệu người thuê phải tự thu thập

| Nhóm thông tin | Dữ liệu cần biết | Vấn đề thường gặp |
|---|---|---|
| Giá | Giá phòng, tiền cọc, phí môi giới | Giá hiển thị có thể chỉ là giá mồi |
| Phí hằng tháng | Điện, nước, Internet, vệ sinh, thang máy, gửi xe | Nhiều bài không ghi hoặc ghi thiếu |
| Vị trí | Địa chỉ chính xác, ngõ, khoảng cách tới nơi học/làm | Chỉ ghi tên phường hoặc khu vực chung |
| Phòng | Diện tích, nội thất, cửa sổ, nhà vệ sinh, số người ở | Ảnh có thể cũ hoặc không đúng phòng |
| Tiện ích | Điều hòa, nóng lạnh, máy giặt, bếp, chỗ để xe | Cách mô tả không đồng nhất |
| Môi trường | An ninh, tiếng ồn, ngập, giờ giấc, hàng xóm | Khó xác minh nếu chỉ đọc tin đăng |
| Di chuyển | Thời gian tới nhiều địa điểm vào giờ cao điểm | Khoảng cách đường thẳng không phản ánh thời gian thực |
| Người đăng | Chủ nhà, môi giới hay người thuê cũ | Danh tính và quyền cho thuê khó kiểm chứng |
| Hợp đồng | Thời hạn, phạt cọc, tăng giá, hoàn cọc | Chỉ biết khi đã đi xem hoặc chuẩn bị cọc |

---

## Bottleneck

### Bottleneck chính

**Chuẩn hóa và so sánh thông tin của nhiều phòng theo cùng một bộ tiêu chí.**

Mỗi nền tảng và người đăng sử dụng một cách mô tả khác nhau. Người thuê phải tự đọc, suy luận và chuyển thông tin về cùng một dạng trước khi có thể so sánh.

Ví dụ:

```text
Tin A: “Phòng full đồ, giá sinh viên, gần trường”
Tin B: “3,2 triệu, 22 m², điện 4.000 đồng/kWh, cách trường 2,5 km”
Tin C: “Giá từ 2,x triệu, ib để biết phòng”
```

Ba tin trên không thể so sánh trực tiếp nếu chưa:

- Xác định giá thực tế.
- Tính tổng chi phí hằng tháng.
- Chuẩn hóa khoảng cách.
- Kiểm tra tiện ích.
- Xác định thông tin nào còn thiếu.
- Ước lượng độ tin cậy của bài đăng.

### Bottleneck phụ

1. **Thông tin phân tán:** Người thuê phải chuyển qua lại giữa nhiều nền tảng.
2. **Thông tin thiếu minh bạch:** Giá, phí và địa chỉ có thể không đầy đủ.
3. **Tin đăng nhanh lỗi thời:** Phòng đã thuê nhưng bài vẫn còn.
4. **Khó tối ưu nhiều vị trí:** Phòng gần trường có thể xa chỗ làm hoặc ngược lại.
5. **Khó xác minh:** Ảnh, người đăng, hợp đồng và yêu cầu đặt cọc có thể có rủi ro.
6. **Quá tải lựa chọn:** Có quá nhiều tin nhưng ít tin thật sự phù hợp.
7. **Thiếu tiêu chí đánh đổi:** Người thuê biết mình muốn nhiều thứ nhưng chưa xác định thứ tự ưu tiên.

---

## Impact

### Đối với người thuê

- Mất nhiều giờ mỗi ngày để tìm và đọc tin.
- Quá trình có thể kéo dài nhiều ngày hoặc nhiều tuần.
- Tốn chi phí đi lại khi xem các phòng không phù hợp.
- Dễ bỏ sót lựa chọn tốt do không theo dõi được tất cả tin.
- Dễ chọn phòng theo cảm tính vì quá tải thông tin.
- Có thể thuê phòng xa, đắt hoặc thiếu tiện ích so với nhu cầu thực tế.
- Có nguy cơ gặp tin giả, giá mồi hoặc lừa đảo đặt cọc.
- Áp lực thời gian khiến người thuê phải quyết định khi chưa đủ thông tin.

### Đối với nhóm cùng thuê

- Mỗi người có ưu tiên khác nhau.
- Khó thống nhất tiêu chí và trọng số.
- Phải gửi nhiều link qua lại rồi thảo luận thủ công.
- Dễ xảy ra tranh luận vì không có bảng so sánh chung.

### Đối với thị trường

- Tin đăng thiếu chuẩn hóa làm giảm khả năng tìm được người thuê phù hợp.
- Chủ nhà uy tín khó nổi bật giữa lượng lớn bài đăng.
- Môi giới và sale phải trả lời lặp lại các câu hỏi giống nhau.

---

## Dấu hiệu thật cần thu thập

Các con số dưới đây là **giả thuyết ban đầu**, cần được kiểm chứng bằng phỏng vấn và thử nghiệm:

| Dấu hiệu | Câu hỏi cần kiểm chứng |
|---|---|
| Thời gian tìm kiếm | Người thuê dành bao nhiêu phút mỗi ngày để xem tin? |
| Thời gian toàn hành trình | Từ lúc bắt đầu tìm đến lúc chốt phòng mất bao nhiêu ngày? |
| Số nguồn sử dụng | Một người thường tìm trên bao nhiêu group hoặc website? |
| Số tin đã xem | Có bao nhiêu tin được đọc trước khi chọn được shortlist? |
| Số lượt liên hệ | Phải nhắn hoặc gọi cho bao nhiêu người đăng? |
| Tin không còn hiệu lực | Bao nhiêu phần trăm phòng đã hết khi liên hệ? |
| Tin thiếu phí | Bao nhiêu bài không ghi đầy đủ điện, nước và phí dịch vụ? |
| Số lần đi xem | Người thuê đi xem bao nhiêu phòng trước khi chốt? |
| Chi phí đi xem | Tổng chi phí xăng xe, xe buýt hoặc gọi xe là bao nhiêu? |
| Sai lệch mô tả | Bao nhiêu phòng không giống ảnh hoặc thông tin đã đăng? |
| Rủi ro cọc | Người thuê từng gặp yêu cầu chuyển tiền trước khi xem phòng chưa? |

---

## Success metric

### North Star Metric

**Giảm thời gian từ lúc nhập nhu cầu đến khi tạo được shortlist 3–5 phòng phù hợp và có đủ thông tin để liên hệ.**

### Metrics đề xuất

| Nhóm | Metric hiện tại cần đo | Mục tiêu MVP |
|---|---|---|
| Thời gian | Thời gian tạo shortlist | Giảm ít nhất 50% |
| Hiệu quả lọc | Số tin phải đọc thủ công | Giảm ít nhất 60% |
| Chất lượng shortlist | Tỷ lệ phòng trong shortlist được người dùng đánh giá là phù hợp | Từ 70% trở lên |
| Minh bạch | Tỷ lệ listing được hiển thị đủ giá và phí | Từ 80% trở lên với dữ liệu đã xử lý |
| Liên hệ | Tỷ lệ phòng còn trống khi người dùng liên hệ | Cải thiện so với workflow hiện tại |
| Đi xem | Số phòng không phù hợp sau khi tới xem | Giảm ít nhất 30% |
| Độ tin cậy | Tỷ lệ cảnh báo rủi ro được người dùng đánh giá là hữu ích | Từ 70% trở lên |
| Trải nghiệm | Điểm hài lòng sau khi tạo shortlist | Từ 4/5 trở lên |

### Metric không nên dùng một mình

- Tổng số tin đăng thu thập được.
- Tổng số lượt chat với AI.
- Tổng số tiêu chí hệ thống hỗ trợ.
- Số lượng người dùng đăng ký.

Các metric trên không chứng minh rằng người dùng tìm phòng nhanh hơn hoặc an toàn hơn.

---

## Non-AI alternatives

Trước khi chọn AI, cần xem các giải pháp đơn giản hơn có thể xử lý được bao nhiêu phần của vấn đề.

### Alternative 1 — Form nhu cầu + bảng Excel

```text
Người dùng nhập:
- Ngân sách
- Các địa điểm quan trọng
- Khoảng cách tối đa
- Tiện ích bắt buộc
- Tiện ích ưu tiên

Sau đó copy từng tin vào một bảng chung để so sánh.
```

**Ưu điểm:**

- Dễ làm.
- Chi phí thấp.
- Minh bạch cách chấm điểm.
- Không cần LLM.

**Hạn chế:**

- Người dùng vẫn phải nhập dữ liệu thủ công.
- Không đọc được mô tả tự do.
- Không phát hiện tốt thông tin thiếu hoặc mâu thuẫn.
- Không hỗ trợ giải thích trade-off tự nhiên.

### Alternative 2 — Template tin đăng chuẩn

Yêu cầu người đăng điền đầy đủ:

- Giá.
- Phí.
- Địa chỉ.
- Diện tích.
- Tiện ích.
- Ảnh.
- Chính sách cọc.
- Trạng thái còn phòng.

**Ưu điểm:**

- Giải quyết gốc vấn đề chuẩn hóa.
- Dễ lọc và so sánh.

**Hạn chế:**

- Không kiểm soát được các nguồn bên ngoài.
- Cần mạng lưới chủ trọ hoặc nền tảng riêng.
- Khó áp dụng cho bài đăng Facebook cũ.

### Alternative 3 — Bộ lọc và scoring cố định

Mỗi phòng được chấm theo công thức:

```text
Điểm tổng =
30% vị trí
+ 25% tổng chi phí
+ 20% tiện ích
+ 15% chất lượng phòng
+ 10% độ tin cậy
```

**Ưu điểm:**

- Dễ giải thích.
- Kết quả ổn định.
- Phù hợp MVP.

**Hạn chế:**

- Khó hiểu các mô tả không có cấu trúc.
- Trọng số cố định không phản ánh từng người.
- Không xử lý tốt câu như: “chấp nhận xa hơn nếu phòng rộng và không mất phí gửi xe”.

---

## AI hypothesis

AI có thể giảm đáng kể thời gian tìm trọ bằng cách:

1. Đọc mô tả tin đăng không có cấu trúc.
2. Trích xuất giá, phí, vị trí, diện tích, tiện ích và thông tin liên hệ.
3. Chuẩn hóa các tin về cùng một schema.
4. Nhận biết thông tin còn thiếu hoặc mâu thuẫn.
5. So sánh phòng theo nhiều địa điểm và tiêu chí.
6. Giải thích trade-off giữa các lựa chọn.
7. Tạo câu hỏi cần hỏi chủ trọ trước khi đi xem.
8. Cảnh báo dấu hiệu rủi ro nhưng không khẳng định chắc chắn là lừa đảo.
9. Cập nhật shortlist khi người dùng thay đổi ưu tiên.
10. Hỗ trợ lập lịch đi xem phòng theo tuyến đường hợp lý.

### AI không nên tự làm

- Khẳng định một tin đăng chắc chắn là thật hoặc giả.
- Tự chuyển tiền cọc.
- Tự ký hợp đồng.
- Tự quyết định phòng thay người dùng.
- Công khai dữ liệu cá nhân của chủ nhà hoặc người thuê.
- Thu thập dữ liệu trái điều khoản của nền tảng.
- Dùng ảnh để kết luận chắc chắn về chất lượng thực tế của phòng.

---

## Quick gut

**Workflow có AI hỗ trợ**, chưa cần một Agent tự trị hoàn toàn.

Lý do:

- Phần lớn quy trình có thể mô hình hóa thành các bước rõ ràng.
- Cần kết quả ổn định, có thể kiểm tra và giải thích.
- Các hành động có rủi ro cao như liên hệ, đi xem và đặt cọc phải do con người quyết định.
- Agent chỉ thực sự cần thiết khi hệ thống phải chủ động tìm thêm thông tin, hỏi lại người dùng hoặc cập nhật shortlist qua nhiều vòng.

---

# 03 — Draft current workflow

```text
CURRENT STATE — ước tính cần kiểm chứng

[1 Xác định nhu cầu: 20']
→ [2 Tìm trên Facebook: 60–120']
→ [3 Tìm trên website khác: 30–60']
→ [4 Lưu và đọc lại tin: 30–60']
→ [5 Nhắn/gọi xác minh: 30–90']
→ [6 Tự so sánh: 30–60']  <-- bottleneck
→ [7 Lập lịch đi xem: 15–30']
→ [8 Đi xem phòng: nhiều giờ]
→ [9 Kiểm tra hợp đồng/cọc]
→ [10 Chốt hoặc tìm lại từ đầu]

Tổng thời gian online:
Khoảng 3–7 giờ cho một vòng tìm kiếm.

Tổng hành trình:
Có thể kéo dài nhiều ngày hoặc nhiều tuần.
```

## Điểm gãy trong current workflow

```text
Nhiều nguồn
    ↓
Dữ liệu không đồng nhất
    ↓
Thiếu giá/phí/địa chỉ
    ↓
Không so sánh trực tiếp được
    ↓
Phải liên hệ thủ công
    ↓
Phòng đã hết hoặc không giống mô tả
    ↓
Quay lại bước tìm kiếm
```

---

# 04 — Draft future workflow

```text
FUTURE STATE — MVP có AI hỗ trợ

[1 Người dùng nhập nhu cầu và các địa điểm: 3–5']
→ [2 Hệ thống chuẩn hóa yêu cầu: <1']
→ [3 Nhập link / nội dung các tin đăng]
→ [4 AI trích xuất dữ liệu từng phòng: <1']
→ [5 Rule engine tính chi phí và khoảng cách]
→ [6 Hệ thống phát hiện dữ liệu thiếu / mâu thuẫn]
→ [7 AI tạo shortlist và giải thích trade-off: <1']
→ [8 Người dùng điều chỉnh trọng số: 2–5']
→ [9 Hệ thống tạo câu hỏi xác minh cho từng phòng]
→ [10 Người dùng tự liên hệ và cập nhật trạng thái]
→ [11 Hệ thống lập bảng so sánh cuối]
→ [12 Người dùng đi xem, đọc hợp đồng và quyết định]  <-- human boundary
```

### Mục tiêu thời gian của future workflow

```text
Từ lúc có danh sách tin đăng
đến shortlist 3–5 phòng:

Hiện tại: 2–4 giờ lọc và so sánh
Mục tiêu MVP: dưới 30 phút
```

### Fallback

```text
AI trích xuất sai
→ Người dùng sửa trực tiếp trường dữ liệu.

Không lấy được vị trí chính xác
→ Yêu cầu người dùng hoặc người đăng bổ sung địa chỉ.

Điểm phù hợp không hợp lý
→ Hiển thị toàn bộ tiêu chí và cho phép đổi trọng số.

Không đủ dữ liệu để cảnh báo
→ Hiển thị “Chưa đủ thông tin”, không suy đoán chắc chắn.
```

---

# 05 — Before / After comparison

| Bước | Trước AI | Sau AI | Vai trò con người |
|---|---|---|---|
| Nhập nhu cầu | Nghĩ trong đầu hoặc ghi chú rời rạc | Form có hướng dẫn, AI chuẩn hóa tiêu chí | Xác nhận nhu cầu và mức ưu tiên |
| Thu thập tin | Tự tìm và lưu link | Người dùng nhập link; có thể bổ sung nguồn phù hợp pháp lý | Chọn nguồn và tin muốn phân tích |
| Đọc tin | Đọc từng bài | AI trích xuất thành schema | Sửa dữ liệu nếu AI đọc sai |
| Tính chi phí | Tự cộng giá và phí | Rule engine tính tổng chi phí dự kiến | Kiểm tra giả định sử dụng |
| So sánh vị trí | Mở bản đồ từng phòng | Hệ thống tính khoảng cách tới nhiều điểm | Chọn thời gian di chuyển chấp nhận được |
| So sánh phòng | Dùng trí nhớ hoặc Excel | Bảng chuẩn hóa + scoring | Điều chỉnh trọng số |
| Xác minh | Tự nghĩ câu hỏi | AI tạo checklist câu hỏi | Trực tiếp gọi hoặc nhắn |
| Đánh giá rủi ro | Dựa vào kinh nghiệm cá nhân | Hệ thống chỉ ra dấu hiệu bất thường | Tự xác minh và quyết định |
| Đi xem | Có thể đi xem nhiều phòng không phù hợp | Chỉ đi xem shortlist tốt hơn | Xem thực tế |
| Đặt cọc | Có thể quyết định dưới áp lực | Checklist hợp đồng và cọc | Chịu trách nhiệm quyết định cuối |

---

# 06 — Rule vs Workflow vs Agent

## Option A — Rule-based system

### Cách hoạt động

```text
Input nhu cầu
→ Lọc theo điều kiện cứng
→ Tính điểm bằng công thức
→ Xếp hạng phòng
```

### Ví dụ rule

```text
Nếu tổng chi phí > ngân sách tối đa
→ Loại.

Nếu thiếu địa chỉ chính xác
→ Gắn cờ “cần xác minh”.

Nếu yêu cầu chuyển cọc trước khi xem
→ Gắn cảnh báo rủi ro cao.

Nếu thời gian di chuyển tới một địa điểm bắt buộc vượt giới hạn
→ Loại hoặc giảm điểm.
```

### Phù hợp với

- Lọc tiêu chí rõ ràng.
- Tính tổng chi phí.
- Chấm điểm minh bạch.
- Cảnh báo theo checklist.

### Không phù hợp với

- Đọc bài đăng viết tự do.
- Hiểu nhu cầu có điều kiện.
- Giải thích trade-off bằng ngôn ngữ tự nhiên.

---

## Option B — AI Workflow

### Cách hoạt động

```text
Người dùng nhập nhu cầu
→ AI chuyển nhu cầu thành cấu trúc
→ AI trích xuất dữ liệu từ tin đăng
→ Rule engine tính toán và lọc
→ AI giải thích kết quả
→ Người dùng review
```

### Phù hợp với

- MVP 6 tuần.
- Có thể kiểm thử từng bước.
- Dễ đặt human-in-the-loop.
- Kết hợp được tính linh hoạt của LLM với độ ổn định của rule.
- Chi phí và độ phức tạp thấp hơn agent tự trị.

### Rủi ro

- LLM có thể trích xuất sai.
- Chất lượng phụ thuộc nội dung tin đăng.
- Cần schema và validation chặt chẽ.

---

## Option C — AI Agent

### Cách hoạt động

```text
Nhận mục tiêu tìm trọ
→ Tự lập kế hoạch
→ Tìm hoặc đọc nhiều nguồn
→ Phát hiện thiếu dữ liệu
→ Hỏi lại người dùng
→ Cập nhật truy vấn
→ So sánh
→ Theo dõi trạng thái phòng
→ Đề xuất hành động tiếp theo
```

### Giá trị tiềm năng

- Cá nhân hóa tốt.
- Có thể xử lý hành trình nhiều vòng.
- Có thể tự quyết định cần dùng công cụ nào tiếp theo.
- Có thể cập nhật shortlist khi điều kiện thay đổi.

### Rủi ro

- Dễ vượt scope 6 tuần.
- Khó kiểm soát hành vi khi truy cập nhiều nguồn.
- Dữ liệu online thay đổi nhanh.
- Có rủi ro vi phạm điều khoản nền tảng nếu crawl tự động.
- Kết quả sai có thể ảnh hưởng tài chính và an toàn của người dùng.
- Chi phí vận hành và kiểm thử cao hơn.

---

## Bảng so sánh

| Tiêu chí | Rule | AI Workflow | AI Agent |
|---|---:|---:|---:|
| Dễ triển khai trong 6 tuần | Cao | Cao | Thấp |
| Hiểu mô tả tự do | Thấp | Cao | Cao |
| Tính ổn định | Cao | Trung bình–cao | Trung bình |
| Dễ giải thích | Cao | Cao nếu kết hợp rule | Thấp hơn |
| Cá nhân hóa | Trung bình | Cao | Rất cao |
| Chi phí phát triển | Thấp | Trung bình | Cao |
| Rủi ro dữ liệu | Thấp | Trung bình | Cao |
| Phù hợp MVP | Có, nhưng giá trị hạn chế | **Phù hợp nhất** | Chỉ nên làm phạm vi nhỏ |

---

# 07 — Quyết định cuối

## Hướng chọn

**Xây dựng AI-assisted workflow, kết hợp LLM + rule engine + human-in-the-loop.**

Không xây một chatbot hỏi đáp chung về phòng trọ.  
Không xây agent tự động đặt cọc hoặc liên hệ thay người dùng.  
Không cố thu thập toàn bộ tin đăng trên Internet trong MVP.

## Lý do

1. Bottleneck chính là chuẩn hóa và so sánh dữ liệu, không phải thiếu một giao diện chat.
2. LLM phù hợp để đọc bài đăng và hiểu nhu cầu tự nhiên.
3. Rule engine phù hợp để tính toán giá, khoảng cách và điều kiện cứng.
4. Người dùng cần thấy lý do một phòng được xếp hạng cao hoặc thấp.
5. Các bước rủi ro cao phải giữ con người trong vòng kiểm soát.
6. Scope đủ nhỏ để nhóm sinh viên có thể demo trong 6 tuần.

---

# 08 — Problem Statement hoàn chỉnh

## Phiên bản ngắn

> Sinh viên và người mới đi làm mất nhiều giờ hoặc nhiều ngày để tìm phòng trọ phù hợp vì tin đăng phân tán, thông tin không đồng nhất và khó so sánh theo nhiều tiêu chí. Chúng tôi muốn giúp họ chuyển một tập tin đăng rời rạc thành shortlist 3–5 phòng có giải thích rõ ràng trong dưới 30 phút, trong khi người dùng vẫn trực tiếp xác minh, xem phòng và quyết định đặt cọc.

## Phiên bản theo actor – need – insight

> Sinh viên và người mới đi làm cần một cách nhanh, minh bạch để so sánh các phòng trọ theo tổng chi phí, khoảng cách tới nhiều địa điểm, tiện ích và mức độ rủi ro, bởi vì workflow hiện tại buộc họ phải đọc và xác minh thủ công hàng chục tin đăng có cấu trúc không đồng nhất.

## How Might We

> Làm thế nào chúng ta có thể giúp sinh viên tạo được shortlist phòng trọ phù hợp theo nhiều tiêu chí trong dưới 30 phút mà không khiến họ phụ thuộc mù quáng vào AI hoặc bỏ qua bước xác minh thực tế?

---

# 09 — MVP đề xuất trong 6 tuần

## User flow chính

```text
1. Người dùng nhập ngân sách
2. Nhập 2–3 địa điểm quan trọng
3. Chọn tiện ích bắt buộc và ưu tiên
4. Dán nội dung hoặc link tin đăng
5. AI trích xuất dữ liệu
6. Người dùng kiểm tra và sửa
7. Hệ thống tính tổng chi phí
8. Hệ thống xếp hạng theo trọng số
9. AI giải thích ưu/nhược điểm
10. Hệ thống tạo checklist xác minh
11. Người dùng lưu shortlist
```

## Tính năng bắt buộc

- Form thu thập nhu cầu.
- Schema chuẩn cho phòng trọ.
- Trích xuất dữ liệu từ nội dung tin đăng.
- Cho phép người dùng sửa dữ liệu.
- Tính tổng chi phí dự kiến.
- So sánh nhiều địa điểm.
- Bộ lọc điều kiện cứng.
- Scoring có trọng số.
- Bảng so sánh 3–5 phòng.
- Giải thích trade-off.
- Checklist câu hỏi cần hỏi người đăng.
- Cảnh báo rủi ro theo rule rõ ràng.

## Tính năng nên hoãn

- Crawl toàn bộ Facebook.
- Tự nhắn tin cho chủ trọ.
- Tự thương lượng giá.
- Tự đặt lịch xem phòng với nhiều bên.
- Phân tích pháp lý hợp đồng chuyên sâu.
- Nhận diện lừa đảo với cam kết chính xác tuyệt đối.
- Computer vision đánh giá chất lượng phòng từ ảnh.
- Theo dõi real-time toàn bộ thị trường.
- Tích hợp thanh toán hoặc đặt cọc.

---

# 10 — Dữ liệu đầu vào và đầu ra

## Input

### Nhu cầu người dùng

```json
{
  "monthly_budget_max": 4000000,
  "deposit_max_months": 1,
  "important_locations": [
    {
      "name": "Địa điểm học",
      "priority": "required",
      "max_travel_minutes": 25
    },
    {
      "name": "Nơi làm thêm",
      "priority": "preferred",
      "max_travel_minutes": 35
    }
  ],
  "required_amenities": [
    "điều hòa",
    "nóng lạnh",
    "chỗ để xe"
  ],
  "preferred_amenities": [
    "máy giặt",
    "cửa sổ",
    "không chung chủ"
  ]
}
```

### Tin đăng

- Văn bản người dùng copy.
- URL công khai mà hệ thống được phép truy cập.
- Dữ liệu người dùng nhập thủ công.
- Ảnh chỉ dùng như dữ liệu tham khảo trong giai đoạn sau.

## Schema phòng trọ

```json
{
  "title": "",
  "source": "",
  "posted_at": "",
  "address_raw": "",
  "address_normalized": "",
  "monthly_rent": null,
  "deposit": null,
  "electricity_fee": null,
  "water_fee": null,
  "service_fee": null,
  "parking_fee": null,
  "estimated_monthly_total": null,
  "area_m2": null,
  "amenities": [],
  "rules": [],
  "contact_type": "unknown",
  "availability_status": "unverified",
  "missing_fields": [],
  "risk_flags": [],
  "evidence": {}
}
```

## Output

- Danh sách phòng đã chuẩn hóa.
- Tổng chi phí ước tính.
- Khoảng cách hoặc thời gian di chuyển tới từng địa điểm.
- Điểm phù hợp tổng.
- Lý do xếp hạng.
- Dữ liệu còn thiếu.
- Các câu hỏi cần xác minh.
- Cảnh báo rủi ro có dẫn chứng.
- Shortlist 3–5 phòng.

---

# 11 — Human boundary và safety

## AI được phép

- Tóm tắt thông tin.
- Trích xuất dữ liệu.
- Tính toán dựa trên công thức.
- Chỉ ra thông tin thiếu.
- Đề xuất câu hỏi.
- So sánh và giải thích.
- Gắn cờ dấu hiệu bất thường.

## Người dùng phải thực hiện

- Xác nhận địa chỉ.
- Liên hệ người đăng.
- Đi xem phòng.
- Kiểm tra giấy tờ và quyền cho thuê.
- Đọc hợp đồng.
- Xác minh tài khoản nhận cọc.
- Quyết định chuyển tiền.
- Quyết định ký hợp đồng.

## Nguyên tắc cảnh báo

Không hiển thị:

> “Đây chắc chắn là lừa đảo.”

Nên hiển thị:

> “Tin đăng có 3 dấu hiệu cần xác minh: yêu cầu cọc trước khi xem, giá thấp bất thường so với các tin cùng khu vực và không cung cấp địa chỉ cụ thể.”

---

# 12 — Kế hoạch research nhanh

## Giả thuyết cần kiểm chứng

1. Người thuê mất nhiều thời gian nhất ở bước đọc và so sánh tin.
2. Phí không minh bạch là nguyên nhân phổ biến khiến phòng bị loại.
3. Người thuê sẵn sàng dán link hoặc nội dung tin vào một công cụ trung gian.
4. Người dùng muốn hệ thống giải thích trade-off thay vì chỉ đưa một điểm số.
5. Checklist xác minh có thể giảm số chuyến đi xem không cần thiết.
6. Người dùng tin kết quả hơn khi có evidence từ chính nội dung tin đăng.

## Đối tượng phỏng vấn

- 5–7 sinh viên đang tìm hoặc vừa tìm trọ.
- 3–5 người mới đi làm.
- 2–3 người từng ở ghép.
- 2 chủ trọ hoặc quản lý nhà trọ.
- 1–2 môi giới để hiểu workflow cung cấp thông tin.

## Câu hỏi phỏng vấn

1. Lần gần nhất bạn tìm trọ là khi nào?
2. Bạn đã dùng những nguồn nào?
3. Bạn mất bao lâu để tạo được danh sách phòng tiềm năng?
4. Tiêu chí nào khiến bạn loại một phòng ngay lập tức?
5. Thông tin nào thường bị thiếu?
6. Bạn phải liên hệ bao nhiêu người trước khi đi xem?
7. Có phòng nào khác xa mô tả không?
8. Bạn từng gặp yêu cầu đặt cọc đáng ngờ chưa?
9. Bạn so sánh các phòng bằng cách nào?
10. Công đoạn nào khiến bạn mệt nhất?
11. Bạn có sẵn sàng dán nội dung tin vào một công cụ để hệ thống phân tích không?
12. Điều gì khiến bạn không tin một đề xuất do AI tạo ra?

---

# 13 — Kịch bản demo

## Tình huống

Nam có ngân sách tối đa **4.000.000 đồng/tháng** và cần tìm phòng:

- Không quá 25 phút tới địa điểm học.
- Không quá 35 phút tới nơi làm thêm.
- Bắt buộc có điều hòa, nóng lạnh và chỗ để xe.
- Ưu tiên phòng có cửa sổ, máy giặt và không chung chủ.

Nam nhập 10 tin đăng được lấy từ các nguồn khác nhau.

## Hệ thống thực hiện

```text
10 tin đăng
→ 2 tin thiếu giá thực tế
→ 3 tin vượt ngân sách sau khi cộng phí
→ 1 tin thiếu địa chỉ chính xác
→ 1 tin yêu cầu cọc trước khi xem
→ 3 tin đủ điều kiện để vào shortlist
```

## Output mẫu

| Rank | Phòng | Tổng chi phí ước tính | Vị trí | Điểm phù hợp | Lưu ý |
|---|---|---:|---|---:|---|
| 1 | Phòng A | 3.750.000 đồng/tháng | Cân bằng tốt giữa hai địa điểm | 88/100 | Cần hỏi phí Internet |
| 2 | Phòng B | 3.500.000 đồng/tháng | Gần nơi học, xa nơi làm hơn | 82/100 | Không có máy giặt riêng |
| 3 | Phòng C | 3.950.000 đồng/tháng | Gần nơi làm, phòng rộng | 79/100 | Cần xác minh tiền cọc |

### Giải thích của hệ thống

> Phòng A đứng đầu vì đáp ứng toàn bộ tiện ích bắt buộc, tổng chi phí vẫn nằm trong ngân sách và thời gian di chuyển cân bằng giữa hai địa điểm. Phòng B rẻ hơn nhưng mất thêm thời gian tới nơi làm. Phòng C rộng nhất nhưng gần chạm mức ngân sách tối đa và chưa có thông tin rõ về điều kiện hoàn cọc.

### Checklist trước khi đi xem

- Phòng hiện còn trống không?
- Giá trên bài có phải giá cuối cùng không?
- Điện, nước, Internet và gửi xe tính thế nào?
- Có khoản phí quản lý hoặc phí dịch vụ khác không?
- Tiền cọc bao nhiêu và điều kiện hoàn cọc là gì?
- Người cho thuê có phải chủ nhà hoặc được ủy quyền không?
- Có thể xem hợp đồng mẫu trước không?
- Phòng trong ảnh có đúng là phòng sẽ thuê không?
- Khu vực có ngập, ồn hoặc giới hạn giờ giấc không?

---

# 14 — Problem Cards #2 và #3 — Tóm tắt

| Card | Actor | Bottleneck | Metric | Quick gut | Vì sao chưa chọn làm #1 |
|---|---|---|---|---|---|
| AI Debug Assistant | Sinh viên AI | Đọc log, tìm nguyên nhân và thử nhiều cách sửa | 1–3 giờ/lỗi → dưới 30 phút | Workflow / Agent | Nhiều công cụ cạnh tranh, khó tạo khác biệt rõ |
| Study Knowledge Assistant | Sinh viên AI | Tìm lại kiến thức trong PDF, note và hội thoại | 15 phút/lần tìm → dưới 2 phút | Workflow | Dễ làm nhưng impact tài chính và urgency thấp hơn tìm trọ |

---

# 15 — Kết luận

Vấn đề ưu tiên không phải là “thiếu một ứng dụng đăng tin phòng trọ”, mà là:

> Người thuê không có một quy trình đáng tin cậy để biến hàng loạt tin đăng phân tán và thiếu chuẩn hóa thành một quyết định đa tiêu chí có thể giải thích.

Giải pháp MVP phù hợp nhất là một **AI-assisted rental comparison workflow**:

```text
LLM:
Đọc nhu cầu + trích xuất tin + giải thích trade-off

Rule engine:
Tính chi phí + điều kiện cứng + scoring + cảnh báo

Map service:
Khoảng cách và thời gian di chuyển

Human:
Xác minh + xem phòng + đọc hợp đồng + đặt cọc
```

Thành công của sản phẩm không được đo bằng số tin mà hệ thống thu thập, mà bằng việc:

- Người dùng tạo shortlist nhanh hơn.
- Shortlist phù hợp hơn.
- Ít phải đi xem phòng không đạt yêu cầu.
- Nhận biết sớm thông tin thiếu và dấu hiệu rủi ro.
- Hiểu rõ mình đang đánh đổi điều gì trước khi quyết định.