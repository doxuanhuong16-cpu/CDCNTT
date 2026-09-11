# Tên đề tài: Xây dựng hệ thống phân tích xu hướng tuyển dụng ngành IT dựa trên dữ liệu tin đăng tuyển dụng

## 1.1 Đặt vấn đề

### a) Lý do chọn đề tài

Thị trường tuyển dụng ngành Công nghệ thông tin đang thay đổi rất nhanh, đặc biệt dưới tác động của làn sóng AI. Sinh viên, người đi làm thường gặp khó khăn khi trả lời các câu hỏi:

- Kỹ năng nào đang thực sự được nhà tuyển dụng cần?
- Những kỹ năng nào thường đi kèm với nhau trong một vị trí công việc?
- Mức lương có tương quan như thế nào với từng kỹ năng cụ thể?
- Xu hướng tuyển dụng đang thay đổi theo thời gian ra sao?

Thay vì dựa vào cảm tính, mạng xã hội hay lời đồn, đề tài này xây dựng một hệ thống tự động thu thập và phân tích dữ liệu tin tuyển dụng thật để trả lời các câu hỏi trên bằng dữ liệu định lượng.

### b) Tính mới và thực tiễn

Phần lớn đồ án sinh viên về khai phá dữ liệu sử dụng dataset có sẵn (Kaggle), thường là dữ liệu nước ngoài, không phản ánh đúng thị trường Việt Nam. Đề tài này tự thu thập dữ liệu thật, tiếng Việt, cập nhật theo thời gian thực tế thị trường trong nước. Kết quả có thể sử dụng thật để định hướng học tập, không chỉ là bài tập mang tính lý thuyết.

- Sử dụng dữ liệu tin tuyển dụng thực tế.
- Tập trung vào thị trường tuyển dụng IT Việt Nam.
- Kết hợp AI/LLM để trích xuất kỹ năng từ mô tả công việc.
- Kết hợp khai phá dữ liệu để tìm mối quan hệ giữa các kỹ năng.
- Trực quan hóa kết quả để người dùng dễ theo dõi.

## 1.2 Mục tiêu đề tài

- Thu thập dữ liệu tin tuyển dụng IT từ nguồn dữ liệu công khai (API hoặc crawl có kiểm soát)
- Dùng AI (LLM) để trích xuất và chuẩn hoá danh sách kỹ năng từ mô tả công việc dạng văn bản tự do
- Áp dụng kỹ thuật khai phá dữ liệu (luật kết hợp, phân cụm) để tìm ra pattern về kỹ năng và xu hướng tuyển dụng
- Xây dựng backend bằng Spring Boot cung cấp REST API phục vụ dữ liệu đã phân tích
- Xây dựng dashboard trực quan hoá kết quả cho người dùng cuối

## 1.3 Đối tượng nghiên cứu

- Dữ liệu tin đăng tuyển dụng ngành IT.
- Các vị trí tuyển dụng IT.
- Mô tả công việc.
- Yêu cầu kỹ năng.
- Mức lương.
- Công ty tuyển dụng.
- Thời gian đăng tuyển.
- Các kỹ thuật xử lý và khai phá dữ liệu.

## 1.4 Phạm vi thực hiện

Để đảm bảo hoàn thành trong thời gian một học kỳ, đề tài giới hạn phạm vi như sau:

- **Nguồn dữ liệu:** tập trung vào vị trí tuyển dụng ngành IT tại Việt Nam (ưu tiên dùng API tổng hợp hợp pháp, hoặc crawl một lần duy nhất từ một nguồn, không crawl real-time liên tục).
- **Quy mô dữ liệu:** khoảng 500 - 1000 tin tuyển dụng là đủ để có kết quả phân tích có ý nghĩa thống kê.
- **Không xử lý real-time streaming** — hệ thống xử lý theo dạng batch (theo lô), phù hợp với năng lực và thời gian của một đồ án sinh viên.

## 1.5 Công nghệ sử dụng

| Thành phần | Công nghệ đề xuất |
|---|---|
| Thu thập dữ liệu | Python, Requests, BeautifulSoup hoặc API |
| Backend | Java, Spring Boot |
| ORM | Spring Data JPA / Hibernate |
| Bảo mật | Spring Security |
| Database | PostgreSQL |
| AI | LLM API |
| Gọi API AI | WebClient |
| Khai phá dữ liệu | Apriori hoặc FP-Growth |
| Phân cụm | K-Means |
| Frontend/Dashboard | React + Chart.js hoặc Thymeleaf + Chart.js |
| Kiểm thử API | Postman |

## 1.6 Các bước triển khai chi tiết

### a) Chuẩn bị và thu thập dữ liệu

- Đăng ký thử JSearch API (RapidAPI) hoặc chuẩn bị script crawl từ một nguồn duy nhất (ví dụ ITviec).
- Thu thập dữ liệu một lần, lưu ra file JSON/CSV để có bộ dữ liệu ổn định dùng xuyên suốt đồ án.
- Thiết kế database schema (bảng JobPosting, Skill, SkillCombo, Company).

### b) Xây dựng Backend nền tảng

- Khởi tạo project Spring Boot, cấu hình kết nối database.
- Xây dựng entity, repository, service, controller CRUD cơ bản cho JobPosting.
- Viết API import dữ liệu từ file JSON/CSV đã thu thập vào database.

### c) Tích hợp AI trích xuất kỹ năng

- Thiết kế prompt cho LLM để trích xuất danh sách kỹ năng từ mô tả công việc.
- Xây dựng service gọi LLM API, xử lý và lưu kết quả chuẩn hoá vào database.
- Kiểm thử với một tập nhỏ dữ liệu trước khi chạy toàn bộ.

### d) Khai phá dữ liệu

- Cài đặt hoặc tích hợp thuật toán Apriori/FP-Growth để tìm luật kết hợp giữa các kỹ năng.
- Cài đặt K-Means để phân cụm các vị trí tuyển dụng theo nhóm nghề thực tế.
- Lưu kết quả phân tích vào database để phục vụ truy vấn nhanh.

### e) Xây dựng REST API và Dashboard

- Thiết kế và xây dựng các endpoint: `/api/trends/skills`, `/api/trends/skill-combos`, `/api/trends/salary-by-skill`.
- Xây dựng giao diện dashboard hiển thị biểu đồ xu hướng.

### f) Kiểm thử, hoàn thiện và viết báo cáo

- Kiểm thử toàn bộ luồng hệ thống end-to-end.
- Chuẩn bị dữ liệu demo, quay video dự phòng.
- Viết báo cáo, chuẩn bị slide thuyết trình.
