# Group Report — Day 02

## Thành viên nhóm

| STT | Họ và tên | Mã học viên | Vai trò trong nhóm |
| :--: | --- | :---: | --- |
| 1 | Nguyễn Phương Đông | 2A202601474 | Thành viên |
| 2 | Ngô Huy Hoàn | 2A202601925 | Thành viên |
| 3 | Nguyễn Thanh Hùng | 2A202601808 | Trưởng nhóm |
| 4 | Ngô Văn Kiệt | 2A202601524 | Thành viên |
| 5 | Ngô Minh Phước | 2A202601576 | Thành viên |
| 6 | Trần Thị Kiều Trang | 2A202601498 | Thành viên |

---

## 🃏 PROBLEM CARD 1 (PITCH ƯU TIÊN TOP 1)

> **Problem (1 câu):** Sinh viên chuyển cơ sở/đi thực tập gặp nhiều rủi ro và tốn thời gian khi tìm trọ ngắn hạn (3–6 tháng) do thị trường tràn ngập tin ảo, môi giới kê giá và giấu chi phí ẩn.
>
> **Actor:** Sinh viên đi thực tập, sinh viên chuyển cơ sở học tập (ngân sách hạn chế 2–3tr/tháng, cần ở ngắn hạn).

### Current Workflow (5 bước)

1. Lên các nhóm Facebook, Chợ Tốt lướt tìm bài đăng phòng trọ.
2. Nhắn tin/gọi điện cho người đăng để hỏi địa chỉ cụ thể và chi phí phụ (điện, nước, dịch vụ).
3. Mở Google Maps thủ công để đo khoảng cách từ phòng trọ tới chỗ làm thực tập/trường học.
4. Hẹn giờ và chạy xe máy đi xem phòng thực tế.
5. Đánh giá phòng, thương lượng hợp đồng ngắn hạn và chốt đặt cọc.

### Phân tích vấn đề

**Bottleneck:** Bước 1 & Bước 4 — Mất nhiều thời gian lọc tin rác/môi giới; đi xem thực tế không đúng như ảnh đăng; môi giới cố tình giấu chi phí ẩn hoặc ép ký hợp đồng dài hạn (1 năm).

**Impact:** Mất 7–14 ngày đi tìm; tốn chi phí đi lại; dễ bị hớ giá, cọc hớ hoặc thuê nhầm phòng không phù hợp với lịch thực tập.

**Success Metric:** Giảm thời gian tìm phòng trọ phù hợp từ 10 ngày xuống dưới 2 ngày; giảm tỷ lệ gặp tin ảo/môi giới kê giá xuống < 10%.

**Non-AI Alternative:** Nhờ người quen/cựu sinh viên tìm giúp, chấp nhận đăng ký KTX trường, hoặc trả phí dịch vụ cho môi giới uy tín.

**AI Hypothesis:** AI Agent tự động cào và tổng hợp dữ liệu từ các nền tảng, tự động phân tích hình ảnh/văn phong để lọc bỏ tin ảo/môi giới, tự động cộng tổng chi phí thực tế và đề xuất phòng tối ưu theo tuyến đường di chuyển.

**Quick Gut:** Agent (Phần lớn công việc cần thu thập dữ liệu đa nguồn, xác minh tin rác và tính toán đa tiêu chí).

### 📐 Draft Workflow (Before / After)

#### CURRENT STATE

```text
CURRENT STATE — 10 ngày (Tốn công sức, rủi ro tin ảo cao)
[Lướt Group FB/Chợ Tốt]
   ↳ [Nhắn tin hỏi chi tiết & mở Maps đo đường]
   ↳ [Đi xe máy xem phòng thực tế] <-- BOTTLENECK: Ảnh ảo, giá chênh, giấu phí
   ↳ [Thương lượng hợp đồng]
   ↳ [Chốt cọc]
```

#### FUTURE STATE

```text
FUTURE STATE — 1-2 ngày (Tối ưu hóa nhờ AI Agent)
[Nhập yêu cầu: Ngân sách + Vị trí thực tập + Thời gian ở]
   ↳ [AI Agent tự cào data & lọc bỏ tin ảo/môi giới]
   ↳ [AI đề xuất Top 3 phòng tối ưu + Bảng tổng chi phí thực tế]
   ↳ [Người dùng review phòng & chốt lịch xem] <-- HUMAN BOUNDARY: Kiểm tra thực tế & ký hợp đồng
   ↳ [Chốt cọc]
```

---

## 🃏 PROBLEM CARD 2

> **Problem (1 câu):** Sinh viên bị rối trí và tốn nhiều thời gian xếp lại thời khóa biểu khi cổng đăng ký tín chỉ của trường sập/lag và các lớp môn học dự định bị full slot liên tục.
>
> **Actor:** Sinh viên học theo hệ thống tín chỉ tại các trường đại học/cao đẳng.

### Current Workflow (5 bước)

1. Lên portal nhà trường xem danh sách môn mở và dùng Excel tự xếp thời khóa biểu (TKB) dự phòng.
2. Đến giờ G, đăng nhập cổng đăng ký tín chỉ và liên tục F5 web.
3. Chọn môn và bấm đăng ký.
4. Nếu môn chính bị full slot/báo lỗi, quay lại file Excel tìm môn/ca thay thế.
5. Thao tác chọn lại trên web và chốt TKB chính thức.

### Phân tích vấn đề

**Bottleneck:** Bước 2 & Bước 4 — Web trường bị sập/lag kéo dài; việc tự tính toán và vẽ lại TKB thủ công khi môn bị đầy gây rối trí, dễ dẫn đến đăng ký trùng ca hoặc học dồn lịch bất hợp lý.

**Impact:** Mất 1–3 tiếng căng thẳng canh web; ~50% sinh viên bị vỡ kế hoạch lịch học, phải đi xin mở lớp bổ sung hoặc học trái ca gây ảnh hưởng tiến độ ra trường.

**Success Metric:** Rút ngắn thời gian xử lý khi môn bị full slot từ 15 phút xuống < 30 giây; 0% trường hợp sinh viên bị đăng ký trùng ca.

**Non-AI Alternative:** Lập sẵn file Excel chứa 5–10 kịch bản TKB thủ công trước giờ G; nhờ bạn bè đăng ký hộ trên nhiều thiết bị.

**AI Hypothesis:** AI phân tích danh sách môn học, tự động sinh ra các kịch bản TKB tối ưu theo ưu tiên cá nhân (né ca sáng, nghỉ thứ 6...). Ngay khi môn A bị full slot, AI tức thì đề xuất kịch bản B thay thế không bị đụng ca.

**Quick Gut:** Rule + Workflow (Chủ yếu dựa trên thuật toán tối ưu hóa điều kiện ràng buộc - Constraint Satisfaction Problem, kết hợp AI gợi ý).

### 📐 Draft Workflow (Before / After)

#### CURRENT STATE

```text
CURRENT STATE — 2 tiếng (Căng thẳng, dễ đụng ca)
[Tự lập Excel TKB]
   ↳ [F5 web trường giờ G] <-- BOTTLENECK: Sập web, nghẽn mạng
   ↳ [Đăng ký môn A]
   ↳ [Môn A báo full slot] <-- BOTTLENECK: Rối trí, xoay xở tính lại TKB thủ công
   ↳ [Chọn môn B thay thế]
   ↳ [Chốt TKB]
```

#### FUTURE STATE

```text
FUTURE STATE — 10 phút (Chủ động kịch bản thay thế)
[Nhập ưu tiên lịch học]
   ↳ [AI tự động sinh 3-5 kịch bản TKB tối ưu]
   ↳ [Đăng ký giờ G]
   ↳ [Nếu Môn A full => AI tự đẩy Kịch bản B dự phòng] <-- HUMAN BOUNDARY: Sinh viên duyệt chốt kịch bản B
   ↳ [Chốt TKB]
```

---

## 🃏 PROBLEM CARD 3

> **Problem (1 câu):** Tân sinh viên và sinh viên học cơ sở mới tốn thời gian và dễ đi trễ học/thi do khó tìm phòng học hay tòa nhà cụ thể trong khuôn viên trường đại học rộng lớn.
>
> **Actor:** Tân sinh viên, sinh viên chuyển cơ sở, sinh viên đi học ca đầu/thi cử tại phòng lạ.

### Current Workflow (5 bước)

1. Mở app xem lịch học để lấy thông tin mã phòng (ví dụ: A2-401).
2. Di chuyển đến trường và gửi xe tại bãi.
3. Nhìn sơ đồ tổng quan của trường hoặc dùng Google Maps chỉ tới cổng/tòa nhà chung.
4. Đi bộ vào khuôn viên, tự mò mẫm tìm đúng tòa nhà, đúng cầu thang và tầng.
5. Nếu bị lạc, dừng lại hỏi đường bảo vệ hoặc sinh viên khác.

### Phân tích vấn đề

**Bottleneck:** Bước 3 & Bước 4 — Google Maps không hỗ trợ chỉ đường nội khu; sơ đồ trường thiếu chi tiết; biển chỉ dẫn mờ/cũ; quy ước đánh số phòng bất hợp lý gây nhầm lẫn giữa các đơn nguyên.

**Impact:** Mất 15–30 phút đi lòng vòng tìm phòng; trễ học/trễ thi 5–10 phút; gây căng thẳng mệt mỏi trước giờ vào lớp.

**Success Metric:** Giảm thời gian tìm phòng nội khu từ 20 phút xuống < 5 phút; giảm tỷ lệ đi trễ do lạc đường xuống 0%.

**Non-AI Alternative:** Đi học sớm 30 phút; chụp sẵn bản đồ sơ đồ trường lưu vào điện thoại; đi theo bạn bè đã quen đường.

**AI Hypothesis:** AI OCR quét mã phòng từ lịch học, kết hợp với dữ liệu bản đồ 3D/Sơ đồ nội khu trường để tự động tạo lộ trình di chuyển từng bước (Step-by-step navigation) từ bãi xe đến tận cửa phòng học.

**Quick Gut:** Workflow (Tích hợp Vision/OCR để đọc lịch học + Thuật toán định vị/chỉ đường indoor).

### 📐 Draft Workflow (Before / After)

#### CURRENT STATE

```text
CURRENT STATE — 25 phút (Lòng vòng, dễ đi trễ)
[Xem mã phòng trên lịch học]
   ↳ [Đến bãi gửi xe]
   ↳ [Xem sơ đồ trường / Google Maps] <-- BOTTLENECK: Chỉ dừng ở cổng trường
   ↳ [Mò mẫm tìm tòa nhà & cầu thang] <-- BOTTLENECK: Nhầm tầng, hỏi đường 3-4 lần
   ↳ [Tới phòng học]
```

#### FUTURE STATE

```text
FUTURE STATE — 5 phút (Lộ trình chi tiết từng bước)
[Quét ảnh lịch học]
   ↳ [AI nhận diện mã phòng & tạo lộ trình chỉ đường nội khu]
   ↳ [Đến bãi gửi xe]
   ↳ [Đi theo chỉ dẫn Step-by-Step của AI] (Ví dụ: Tòa A2 => Cầu thang sau => Tầng 4)
   ↳ [Tới phòng học] <-- HUMAN BOUNDARY: Sinh viên tự di chuyển theo chỉ dẫn
```

---

## 🎯 LỰA CHỌN PITCH & CÂU HỎI PHẢN BIỆN NHÓM

### 1. Card lựa chọn Pitch: PROBLEM CARD 1

*(Tìm phòng trọ ngắn hạn khi chuyển cơ sở / đi thực tập)*

#### Lý do chọn

- Đây là bài toán có nỗi đau rất thật (High Pain Point), tần suất lặp lại theo mỗi kỳ thực tập/chuyển cơ sở của sinh viên, và độ rộng thị trường lớn.
- Ranh giới Người – Máy rõ ràng: AI xử lý phần cực nhất là cào dữ liệu, phát hiện tin ảo và tính toán chi phí, còn Người giữ quyết định cuối cùng là đi xem thực tế và ký hợp đồng.

### 2. Câu hỏi nhờ nhóm phản biện (Feedback Questions)

**Về dữ liệu (Data Source):** AI có thể thu thập dữ liệu phòng trọ từ đâu để đảm bảo tính thời gian thực khi mà bài đăng trên các Group Facebook bị ẩn/xóa liên tục?

**Về khả năng chống tin ảo (Fraud Detection):** Môi giới hiện nay thường dùng tài khoản clone, đổi hình ảnh và thay số điện thoại liên tục. Bằng chứng/Logic nào đủ mạnh để AI tự tin gắn nhãn "Đây là tin ảo / môi giới kê giá" mà không bị nhầm lẫn?

**Về giá trị thực tế (Feasibility):** Liệu người dùng có sẵn sàng tin tưởng kết quả lọc của AI hay họ vẫn sẽ giữ thói quen tự lên Facebook lướt tìm vì sợ bỏ sót phòng tốt?