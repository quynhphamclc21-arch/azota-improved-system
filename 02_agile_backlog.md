# BƯỚC 2: CHUYỂN ĐỔI SANG ARTEFACTS SCRUM (AGILE BACKLOG)

> **Căn cứ kế thừa từ Bước 1:** [specs/01_requirements_ingestion.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/01_requirements_ingestion.md) (`RAW-001` đến `RAW-053`)  
> **Tài liệu quy trình:** [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md) & [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md)  
> **Quy chuẩn thực hiện:** Tuân thủ chuẩn **INVEST** cho User Stories, định dạng **Given - When - Then (GWT)** cho Acceptance Criteria, và thiết lập **Ma trận truy vết (Traceability Matrix)** khép kín từ `RAW-xxx`.

---

## 1. Cấu trúc Phân rã Agile (Epic ➔ Feature ➔ User Story)

Toàn bộ hệ thống AZOTA cải tiến mở rộng được phân rã thành **8 Epics lớn**, **33 Features** và **52 User Stories**:

```text
EPIC-01: Xác thực, Đăng ký & Phân quyền 4 Vai trò (Authentication, Registration & RBAC)
  ├── FEAT-1.1: Form Đăng nhập Tối giản & 4 Tabs Chuyển đổi Vai trò (4-Role Switcher Form)
  ├── FEAT-1.2: Định tuyến & Cách ly Giao diện theo Quyền (Strict RBAC Navigation)
  └── FEAT-1.3: Đăng ký Tài khoản & Cam kết Điều khoản Dịch vụ (User Registration & Terms)

EPIC-02: Không gian Thi, Học Tập & Tương Tác Học Sinh (Student Testing, Learning & Classroom Suite)
  ├── FEAT-2.1: Quản lý & Cảnh báo Đề thi tại Trang chủ (Exam Portal & Urgent Alerts)
  ├── FEAT-2.2: Phòng chờ Trước giờ thi & Cam kết Quy định (Pre-check Lobby & Rules Acceptance)
  ├── FEAT-2.3: Trực quan hóa Giao diện Làm bài thi Toán (Math Graphic Exam Workspace)
  ├── FEAT-2.4: Chỉ báo Lưu tự động Ngầm (Silent Auto-save Indicator)
  ├── FEAT-2.5: Phân hệ Tự Luyện tập theo Chủ đề (Topic-based Practice Portal)
  ├── FEAT-2.6: Xem lại Chi tiết Bài thi & Lời giải (Detailed Exam Review & Explanations)
  ├── FEAT-2.7: Phúc khảo & Giải trình Vi phạm (Dispute & Appeal Submission)
  ├── FEAT-2.8: Giao & Nộp Bài tập Tự luận Kèm Ảnh Chụp Vở & Đối soát AI (Homework Submission & AI Similarity)
  ├── FEAT-2.9: Tham Gia Lớp Học Bằng Mã Mời & Quản Lý Lớp Đang Học (Student Class Enrollment - Bảng 1.8)
  └── FEAT-2.10: Kênh Tương Tác & Thảo Luận Q&A Với Giáo Viên & Bạn Học (Student Class Q&A & Peer Discussions - Bảng 1.14)

EPIC-03: Mô phỏng Giám sát, Chống Gian lận & Phục hồi Sự cố (Anti-Cheat & Session Recovery)
  ├── FEAT-3.1: Bắt Sự kiện Chuyển Tab & Khóa Màn hình (Tab-Switch Detection & Freeze Modal)
  ├── FEAT-3.2: Cơ chế Cấp đổi Mã đề Thay thế Tương đương (Dynamic Paper Substitution)
  ├── FEAT-3.3: Mô phỏng Mất Mạng & Khôi phục Phiên thi (Network Drop & Session Recovery)
  └── FEAT-3.4: Cơ Chế Cưỡng Ép Nộp Bài Khi Vi Phạm Vượt Ngưỡng (Threshold-based Forced Submission)

EPIC-04: Cơ chế Khảo thí Thông minh Nâng cao (Smart Exam Engineering)
  ├── FEAT-4.1: Câu hỏi Toán học Biến đổi Tham số Ngẫu nhiên (Parametric Question Engine)
  ├── FEAT-4.2: Đếm ngược Từng câu & Khóa Câu hỏi Đã Hết Giờ (Per-Question Timer & Locking)
  └── FEAT-4.3: Chế Độ Thi Tuyến Tính Một Chiều & Khóa Câu Hết Giờ 30s (Strict Linear Exam & Lock)

EPIC-05: Quản lý Đề, Giám sát Phòng thi, Xử lý Phúc khảo & Tiện ích GV (Teacher Suite)
  ├── FEAT-5.1: Ngân hàng Câu hỏi & Bộ lọc Đa tiêu chí (Question Bank & Tag Filter)
  ├── FEAT-5.2: Thiết lập Ma trận Đề & Cấu hình Chống Gian lận (Exam Matrix & Duplicate Slider)
  ├── FEAT-5.3: Bảng Giám sát Phòng thi Trực tiếp (Live Proctoring & Event Timeline Drawer)
  ├── FEAT-5.4: Trực quan hóa Báo cáo, Nhật ký & Xử lý Phúc khảo (Analytics, Logs & Appeal Review)
  ├── FEAT-5.5: Công cụ Thi Offline - Chấm Phiếu tô Trắc nghiệm (Offline Bubble Sheet Scanner)
  ├── FEAT-5.6: Mô phỏng Phòng thi Tương tác Trực tiếp AZOTA Live (Virtual Exam Classroom)
  ├── FEAT-5.7: Quản lý Lớp học & Mã mời Tham gia (Classroom Management & Invite Code)
  ├── FEAT-5.8: Kho Học liệu & Bài giảng Số của Lớp học (Digital Class Materials & Slides)
  ├── FEAT-5.9: Gửi Thông Báo & Nhắc Hạn Nộp Cá Nhân Hóa (Custom Announcements & Reminders)
  └── FEAT-5.10: Kênh Tương Tác & Thảo Luận Q&A Lớp Học (Class Discussion & Q&A Forum)

EPIC-06: Cổng Tương tác Dành cho Phụ huynh (Parent Portal & Communication)
  ├── FEAT-6.1: Liên kết Hồ sơ Học sinh (Student Account Linking)
  ├── FEAT-6.2: Bảng Điều khiển Theo dõi Tiến độ & Lời phê (Student Progress Dashboard)
  └── FEAT-6.3: Kênh Trao đổi Trực tiếp với Giáo viên (Direct Teacher Chat Widget)

EPIC-07: Quản trị Cấp trường & Phân quyền Đội nhóm (Admin School Management & Centralized Exams)
  ├── FEAT-7.1: Dashboard Quản trị Tổng thể & KPIs Nhà trường (Admin School KPIs Dashboard)
  ├── FEAT-7.2: Quản lý Người dùng & Đội nhóm Phân quyền RBAC (User & Group Access Control)
  ├── FEAT-7.3: Quản lý Cấu trúc Trường, Khối lớp & Import Học sinh (School Structure & Excel Import)
  ├── FEAT-7.4: Tổ chức & Giám sát Kỳ thi Chung Toàn trường/Khối (Centralized School Exams)
  ├── FEAT-7.5: Thống kê & Báo cáo Chuyên sâu Cấp trường (School-wide Analytics & Comparison)
  ├── FEAT-7.6: An toàn Hệ thống, Audit Logs & Giám sát Tài nguyên (Security Audit & Server Health)
  ├── FEAT-7.7: Trung tâm Thông báo Toàn trường & Hỗ trợ Kỹ thuật (Notifications & Ticket Support)
  └── FEAT-7.8: Quản Lý Học Liệu & Dung Lượng Lưu Trữ Hệ Thống (Storage & Digital Asset Management)

EPIC-08: Chuẩn hóa Giao diện & Tối ưu hóa Chế độ Điện thoại (AZOTA Design System & Mobile Refinement)
  ├── FEAT-8.1: Nhận diện Thương hiệu AZOTA & Client Mock Store (Azota Tokens & Local State)
  ├── FEAT-8.2: Khung Mô phỏng Thiết bị Điện thoại Di động (Mobile App Viewport Chassis)
  └── FEAT-8.3: Tinh chỉnh Bố cục & Trải nghiệm Chế độ Điện thoại (Container-Scoped Mobile Layout)
```

---

## 2. Danh mục Chi tiết 50 User Stories & Tiêu chí Chấp nhận (GWT)

### EPIC-01: Xác thực, Đăng ký & Phân quyền 4 Vai trò

#### `US-001`: Đăng nhập với 4 Tabs chuyển đổi vai trò
- **Định dạng:** Là một người dùng (Học sinh / Giáo viên / Phụ huynh / Quản trị viên), tôi muốn chọn vai trò ngay trên Form đăng nhập thông qua các Tab lớn, để form tự đổi màu sắc nhận diện tương ứng.
- **Traceability:** `RAW-001`, `RAW-024`
- **Acceptance Criteria (AC-001):**
  - **Kịch bản 1: Đổi sắc thái nhận diện theo 4 tab**
    - *Given:* Người dùng đang ở màn hình Đăng nhập.
    - *When:* Nhấn lần lượt các tab `[Học sinh]`, `[Giáo viên]`, `[Phụ huynh]`, `[Quản trị viên]`.
    - *Then:* Tab được chọn hiển thị Active nổi bật; form và nút Đăng nhập chuyển sang màu tương ứng (Xanh dương $\rightarrow$ Tím $\rightarrow$ Xanh ngọc $\rightarrow$ Xanh đen/Chàm).

#### `US-002`: Tiện ích Hiện/Ẩn mật khẩu và Ghi nhớ đăng nhập
- **Định dạng:** Là người dùng, tôi muốn bấm icon con mắt để kiểm tra mật khẩu và có ô ghi nhớ đăng nhập, để thao tác nhập liệu chính xác và tiện lợi.
- **Traceability:** `RAW-002`
- **Acceptance Criteria (AC-002):**
  - **Kịch bản 1: Toggle mật khẩu:** Nhấn icon con mắt chuyển đổi mật khẩu giữa dạng `••••••` và chữ rõ ràng.
  - **Kịch bản 2: Ghi nhớ:** Checkbox "Ghi nhớ đăng nhập" lưu cờ phiên làm việc giả lập vào localStorage.

#### `US-003`: Điều hướng tức thì & Cách ly nghiêm ngặt giao diện theo vai trò (RBAC)
- **Định dạng:** Là một người dùng đăng nhập hợp lệ, tôi muốn được chuyển thẳng vào không gian làm việc của đúng vai trò đó và chỉ thấy các menu thuộc thẩm quyền của mình.
- **Traceability:** `RAW-003`, `NFR-07`
- **Acceptance Criteria (AC-003):**
  - **Kịch bản 1: Cách ly vai trò:** Đăng nhập vai trò nào (HS, GV, PH, Admin) chỉ nhìn thấy đúng Header và các trang của vai trò đó, tuyệt đối không xuất hiện menu vai trò khác.

#### `US-042`: Form Đăng ký tài khoản mới tích hợp điều khoản và chính sách dịch vụ
- **Định dạng:** Là người dùng mới, tôi muốn chuyển sang tab Đăng ký để điền thông tin và tích chọn đồng ý điều khoản, chính sách của AZOTA để tạo tài khoản hợp lệ.
- **Traceability:** `RAW-044`
- **Acceptance Criteria (AC-042):**
  - **Kịch bản 1: Đăng ký thành công:** Điền đầy đủ thông tin, tích chọn "Tôi đồng ý với các điều khoản và chính sách" $\rightarrow$ Hiển thị thông báo đăng ký thành công và tự động chuyển sang form Đăng nhập.
  - **Kịch bản 2: Chưa tích điều khoản:** Nếu bỏ trống checkbox cam kết $\rightarrow$ Hiển thị cảnh báo màu đỏ yêu cầu chấp thuận điều khoản trước khi tạo tài khoản.

---

### EPIC-02: Không gian Thi & Khảo thí Học sinh

#### `US-004`: Grid danh sách đề thi & Ô tìm kiếm/nhập mã đề
- **Định dạng:** Là một học sinh, tôi muốn xem các đề thi dạng Grid Card với huy hiệu màu trạng thái và ô nhập mã đề thi, để dễ dàng quản lý và tham gia thi.
- **Traceability:** `RAW-004`
- **Acceptance Criteria (AC-004):**
  - Thẻ đề thi hiển thị rõ: Tên môn, Hạn nộp, Badge màu (🟢 Đã nộp, 🟡 Đang mở, 🔴 Quá hạn). Ô input tìm kiếm hoặc dán liên kết hoạt động nhanh chóng.

#### `US-005`: Widget cảnh báo bài thi sắp đến hạn kèm Countdown
- **Định dạng:** Là một học sinh, tôi muốn có widget cảnh báo khẩn cấp màu đỏ/cam kèm đồng hồ đếm lùi thời gian thực, để không bị trễ hạn bài thi quan trọng nhất.
- **Traceability:** `RAW-005`
- **Acceptance Criteria (AC-005):**
  - Hiển thị đồng hồ đếm lùi nhảy từng giây (`02:14:58`) và thanh tiến trình thời gian đã trôi qua.

#### `US-039`: Phòng chờ Trước giờ thi (Pre-check Lobby) với kiểm tra thiết bị & cam kết quy định
- **Định dạng:** Là thí sinh trước khi nhận đề, tôi muốn được kiểm tra tình trạng kết nối mạng, đọc quy định phòng thi và tích cam kết, để chuẩn bị tâm lý và thiết bị tốt nhất.
- **Traceability:** `RAW-041`
- **Acceptance Criteria (AC-039):**
  - **Kịch bản 1: Kiểm tra thiết bị & Quy định thi:**
    - *Given:* Thí sinh nhấn "Vào thi ngay" từ Trang chủ.
    - *Then:* Hiển thị màn hình Sảnh chờ (Pre-check Lobby) với 2 thẻ trạng thái xanh: "Thiết bị: Sẵn sàng", "Mạng: Ổn định (Ping 18ms)".
    - *And:* Bảng thông báo quy định: Cảnh báo chuyển tab, đếm lùi từng câu, khóa câu khi hết giờ.
    - *When:* Thí sinh tích chọn "Tôi đã đọc và đồng ý quy định phòng thi" và bấm "Bắt đầu làm bài".
    - *Then:* Hệ thống mới chính thức cấp mã đề ban đầu và mở màn hình thi.

#### `US-006`: Khu vực câu hỏi toán học với đồ thị Parabol và 4 đáp án Radio
- **Định dạng:** Là thí sinh, tôi muốn câu hỏi trắc nghiệm Toán có đồ thị parabol vector SVG sắc nét ở giữa và 4 nút Radio A, B, C, D to rõ ràng.
- **Traceability:** `RAW-006`
- **Acceptance Criteria (AC-006):**
  - Đồ thị parabol $y = x^2 - 4x + 3$ hiển thị chuẩn xác đỉnh $I(2; -1)$, cắt các trục tọa độ; click chọn đáp án đổi màu xanh thương hiệu ngay tức thì.

#### `US-007`: Sidebar đồng hồ đếm lùi lớn và Lưới trạng thái câu hỏi
- **Định dạng:** Là thí sinh, tôi muốn có đồng hồ đếm lùi lớn (chuyển đỏ khi sắp hết giờ) và lưới ô vuông câu hỏi đổi màu theo 4 trạng thái tiến độ làm bài.
- **Traceability:** `RAW-007`
- **Acceptance Criteria (AC-007):**
  - Đồng hồ chuyển đỏ khi thời gian còn dưới 5 phút; lưới câu hỏi hiển thị Trắng/Xám (chưa làm), Xanh lá (đã làm), Xanh dương (đang chọn), Xám mờ có ổ khóa 🔒 (đã bị khóa).

#### `US-008`: Thanh điều hướng và Nút nộp bài
- **Định dạng:** Là thí sinh, tôi muốn có nút "Câu trước", "Câu sau", "Lưu lựa chọn" và "Nộp bài" ở footer để dễ dàng di chuyển và kết thúc bài thi.
- **Traceability:** `RAW-008`
- **Acceptance Criteria (AC-008):**
  - Nhấn Trước/Sau chuyển mượt mà giữa các câu hỏi; nhấn Nộp bài hiển thị modal xác nhận số câu đã làm và điểm số/kết quả.

#### `US-009`: Chỉ báo tự động lưu ngầm (Auto-save Indicator)
- **Định dạng:** Là thí sinh, tôi muốn thấy thông báo lưu ngầm kèm timestamp mỗi khi chọn đáp án, để hoàn toàn an tâm không mất bài.
- **Traceability:** `RAW-009`
- **Acceptance Criteria (AC-009):**
  - Mỗi khi click chọn đáp án, text đổi thành *"✓ Đã lưu câu trả lời lúc [HH:mm:ss]"* đi kèm dấu tick và hiệu ứng chớp sáng nhẹ.

#### `US-025`: Phân hệ Tự Luyện tập theo Chủ đề môn học
- **Định dạng:** Là một học sinh, tôi muốn chọn các chủ đề (Hàm số, Hình học, Tổ hợp) để làm đề luyện tập tự do và xem ngay đáp án giải thích.
- **Traceability:** `RAW-038`
- **Acceptance Criteria (AC-025):**
  - Màn hình Luyện tập cho phép chọn chủ đề, tạo bài luyện tập tức thì, có chấm điểm ngay sau khi làm xong từng câu.

#### `US-026`: Màn hình Xem lại Chi tiết Bài thi & Lời phê giáo viên
- **Định dạng:** Là học sinh, tôi muốn xem lại chi tiết bài kiểm tra đã nộp với bảng đối chiếu đáp án đúng/sai, lời giải chi tiết và nhận xét của thầy cô.
- **Traceability:** `RAW-039`
- **Acceptance Criteria (AC-026):**
  - Hiển thị danh sách câu hỏi của bài thi đã nộp: Đánh dấu rõ câu học sinh chọn đúng (xanh) hoặc sai (đỏ), hiển thị đáp án đúng kèm lời giải chi tiết và lời phê của giáo viên.

#### `US-041`: Quy trình Gửi và Xử lý Phúc khảo / Giải trình vi phạm
- **Định dạng:** Là học sinh có thắc mắc về điểm hoặc bị ghi nhận nhầm vi phạm, tôi muốn có nút gửi yêu cầu phúc khảo kèm lý do giải trình; và là giáo viên, tôi muốn xem xét và chỉnh sửa điểm trực tiếp.
- **Traceability:** `RAW-043`
- **Acceptance Criteria (AC-041):**
  - **Kịch bản 1: Học sinh gửi phúc khảo:** Tại màn hình kết quả bài thi, học sinh bấm nút "Phúc khảo / Giải trình vi phạm", nhập lý do (VD: *"Em bấm nhầm phím Windows làm nhảy tab 1s, mong cô xem xét lại câu 4"*), bấm "Gửi yêu cầu" $\rightarrow$ Trạng thái chuyển thành "Đã gửi phúc khảo (Chờ duyệt)".
  - **Kịch bản 2: Giáo viên xem xét & Chỉnh sửa điểm:** Giáo viên mở bảng Chi tiết vi phạm, đọc lý do giải trình của học sinh $\rightarrow$ Bấm nút "Chỉnh sửa điểm" (+0.5 điểm), nhập ghi chú $\rightarrow$ Điểm số của học sinh cập nhật từ 9.0 lên 9.5 kèm nhãn "Đã xử lý phúc khảo".

#### `US-045`: Giao & Nộp Bài tập Tự luận Kèm Ảnh Chụp Vở & Đối soát Trùng lặp AI
- **Định dạng:** Là học sinh, tôi muốn xem danh sách bài tập về nhà môn học, tải ảnh chụp vở bài làm (hỗ trợ nhiều trang JPG/PNG hoặc PDF) kèm lời nhắn gửi giáo viên; và là giáo viên, tôi muốn xem ma trận đối soát AI để phát hiện tự động bài làm có tỷ lệ trùng lặp cao bất thường theo Bảng 1.11, 1.48, 1.55, 1.71 của BT4-Nhóm 7.
- **Traceability:** `RAW-047`, `NFR-01`, `NFR-03`, `NFR-05`
- **Acceptance Criteria (AC-045):**
  - **Kịch bản 1: Học sinh nộp ảnh chụp bài tập về nhà:**
    - *Given:* Học sinh ở tab "Lớp học" -> sub-tab "Bài Tập Về Nhà".
    - *When:* Bấm nút "Nộp Bài" trên thẻ bài tập tự luận Toán hình không gian.
    - *Then:* Modal nộp bài mở ra với khu vực kéo thả ảnh/tài liệu (`#modal-submit-homework`), cho phép chọn file ảnh trang vở bài làm và nhập ghi chú.
    - *When:* Bấm "Xác Nhận Nộp Bài" -> Hiển thị thông báo Toast thành công, trạng thái bài tập chuyển thành `🟢 Đã nộp (Đúng hạn)` kèm 2 ảnh đính kèm.
  - **Kịch bản 2: Giáo viên kiểm tra Ma trận Đối soát AI (AI Similarity Matrix):**
    - *Given:* Giáo viên xem danh sách nộp bài ở tab Ma trận Chống gian lận.
    - *Then:* Hiển thị Banner cảnh báo màu đỏ: *"Phát hiện 02 bài nộp có mức tương đồng 95.4% (Trần Thị Bích & Lê Hoàng Nam)"*.
    - *When:* Giáo viên bấm "So Sánh Bài Làm (AI)" -> Modal đối soát mở ra hiển thị song song 2 bài nộp với các dòng công thức bị phát hiện trùng khớp màu đỏ.
    - *Then:* Giáo viên có thể bấm "Ghi Nhận Vi phạm" hoặc "Chấp nhận giải trình".

#### `US-051`: Tham Gia Lớp Học Bằng Mã Mời & Quản Lý Lớp Đang Học (Bảng 1.8 BT4-Nhóm 7)
- **Định dạng:** Là học sinh, tôi muốn sử dụng mã lớp học hoặc liên kết mời do giáo viên cung cấp để tham gia vào lớp học mới, xác nhận tham gia và xem danh sách các lớp học mình đang theo học, để được cấp quyền truy cập tài liệu, bài tập và lịch thi của lớp.
- **Traceability:** `RAW-052`, `NFR-02`, `NFR-03`
- **Acceptance Criteria (AC-051):**
  - **Kịch bản 1 (Nhập mã tham gia lớp):** Given học sinh ở tab "Lớp Học (Tham Gia Lớp)" (`#subtab-classroom-content`), When nhập mã lớp hợp lệ (ví dụ: `10A1-TOAN`, `10A2-TOAN`) và bấm "Xác Nhận Tham Gia Lớp", Then lớp học được thêm vào danh sách lớp đã liên kết, tăng biến đếm số lớp đang học và hiển thị thông báo Toast thành công.
  - **Kịch bản 2 (Quản lý danh sách lớp học):** Given học sinh xem danh sách lớp học, Then hiển thị đầy đủ thông tin: Tên lớp, Môn học, GVCN/Giảng viên phụ trách, Sĩ số, Mã mời, Lịch học trực tiếp, kèm các nút tắt chuyển nhanh sang Học liệu, Thảo luận Q&A và Bài tập về nhà của lớp đó.

#### `US-052`: Kênh Tương Tác & Thảo Luận Q&A Lớp Học Với Giáo Viên & Bạn Học (Bảng 1.14 ứng Bảng 1.7)
- **Định dạng:** Là học sinh, tôi muốn có diễn đàn thảo luận theo lớp/môn học để đặt câu hỏi thắc mắc bài học, trao đổi với các bạn cùng lớp và nhận lời giải chuẩn mực được ghim từ giáo viên theo Bảng 1.14 và tương ứng hai chiều với Bảng 1.7 của BT4-Nhóm 7.
- **Traceability:** `RAW-053`, `NFR-02`
- **Acceptance Criteria (AC-052):**
  - **Kịch bản 1 (Học sinh đặt câu hỏi thắc mắc mới):** Given học sinh ở tab "Thảo Luận Q&A Lớp Học" (`#subtab-discussions-content`), When mở form đặt câu hỏi, nhập tiêu đề, chọn chuyên đề và nội dung thắc mắc rồi bấm "Gửi Câu Hỏi Lên Diễn Đàn Lớp", Then câu hỏi xuất hiện trên diễn đàn của lớp và đồng thời xuất hiện trên bảng Thảo Luận của Giáo viên (Bảng 1.7) ở trạng thái chờ giải đáp.
  - **Kịch bản 2 (Xem lời giải chuẩn mực ghim của giáo viên & Trao đổi bạn học):** Given học sinh xem chủ đề thảo luận (ví dụ: Giao điểm Parabol khi delta < 0), Then hiển thị câu hỏi của học sinh, hộp phản hồi ghim nổi bật "Lời Giải Chuẩn Của Giáo Viên" từ Thầy Hoàng Nam, các trao đổi của bạn cùng lớp, và học sinh có thể gửi thêm phản hồi thảo luận trực tiếp.

---

### EPIC-03: Mô phỏng Giám sát, Chống Gian lận & Phục hồi Sự cố

#### `US-010`: Phát hiện chuyển tab và Khóa bài thi bằng Modal đỏ
- **Định dạng:** Là hệ thống giám sát, tôi muốn bắt sự kiện thí sinh chuyển tab hoặc thu nhỏ cửa sổ để lập tức khóa màn hình bằng Modal đỏ cảnh báo.
- **Traceability:** `RAW-010`, `NFR-04`
- **Acceptance Criteria (AC-010):**
  - Khi phát hiện `visibilitychange` hoặc `blur`, Modal đỏ cảnh báo lập tức phủ kín màn hình với thông điệp: *"CẢNH BÁO: RỜI KHỎI BÀI THI!"*.

#### `US-011`: Animation cấp đổi mã đề thay thế 01 ➔ 04 trên Modal
- **Định dạng:** Là thí sinh vi phạm, tôi muốn nhìn thấy hiệu ứng thị giác mũi tên chuyển đổi mã đề rõ ràng để hiểu cơ chế xử lý của hệ thống.
- **Traceability:** `RAW-011`
- **Acceptance Criteria (AC-011):**
  - Trên Modal đỏ xuất hiện animation mũi tên chuyển đổi: $\text{Mã đề cũ 01} \longrightarrow \text{Mã đề mới 04}$.

#### `US-012`: Khôi phục phòng thi với mã đề mới, bảo lưu giờ và câu đã làm
- **Định dạng:** Là thí sinh sau khi bị đổi đề, tôi muốn tiếp tục làm bài với mã đề mới mà thời gian còn lại và các câu đã làm trước đó vẫn được bảo lưu 100%.
- **Traceability:** `RAW-012`
- **Acceptance Criteria (AC-012):**
  - Đóng Modal, thí sinh tiếp tục làm Đề 04; đồng hồ đếm lùi giữ nguyên mốc thời gian; các câu đã trả lời trước đó được giữ nguyên trong bộ nhớ bài làm.

#### `US-040`: Mô phỏng Mất kết nối mạng & Khôi phục trạng thái bài thi
- **Định dạng:** Là thí sinh, tôi muốn hệ thống tự động nhận diện và khôi phục bài làm đã lưu khi mạng bị rớt hoặc tải lại trang, để tôi an tâm hoàn thành bài thi.
- **Traceability:** `RAW-042`
- **Acceptance Criteria (AC-040):**
  - **Kịch bản 1: Mất mạng & Khôi phục:** Khi nhấn nút "Mô phỏng Mất mạng / Tải lại", hệ thống hiển thị banner màu hổ phách: *"Đang gián đoạn kết nối... Đang kiểm tra dữ liệu đệm!"*. Sau 1 giây, thanh thông báo chuyển xanh: *"✓ Đã khôi phục thành công phiên thi từ dữ liệu đệm!"* và học sinh tiếp tục làm bài mà không mất bất kỳ đáp án nào.

#### `US-050`: Cơ Chế Cưỡng Ép Nộp Bài Khi Vi Phạm Gian Lận Vượt Ngưỡng (3/3 Lần)
- **Định dạng:** Là Hệ thống Giám sát thi, tôi muốn tự động cưỡng ép thu bài thi tức thì khi học sinh cố tình vi phạm chuyển tab quá 3 lần, để bảo đảm tính liêm chính và công bằng trong khảo thí.
- **Traceability:** `RAW-051`, `NFR-04`
- **Acceptance Criteria (AC-050):**
  - **Kịch bản 1 (Cảnh báo & Đổi mã đề):** Given học sinh vi phạm chuyển tab lần 1 và 2, Then hệ thống hiển thị modal cảnh báo và hoán vị đề thay thế (Mã đề 04).
  - **Kịch bản 2 (Cưỡng ép thu bài tức thì):** When học sinh vi phạm lần 3, Then hệ thống kích hoạt lệnh CƯỠNG ÉP THU BÀI ngay lập tức, đồng hồ dừng lại, bài thi bị khóa vĩnh viễn, tính điểm các câu đã làm, hiển thị modal đỏ khẩn cấp, cập nhật trạng thái "Bị đình chỉ thi" trên bảng Live Proctoring của giáo viên và ghi Audit Log của Admin.

---

### EPIC-04: Cơ chế Khảo thí Thông minh Nâng cao

#### `US-027`: Câu hỏi Toán học Biến đổi Tham số Ngẫu nhiên
- **Định dạng:** Là giáo viên và thí sinh, tôi muốn các câu hỏi toán học được tự động sinh tham số ngẫu nhiên $(X, Y)$ khác nhau cho từng thí sinh, để dù ngồi cạnh hay trao đổi cũng không thể chép kết quả của nhau.
- **Traceability:** `RAW-034`
- **Acceptance Criteria (AC-027):**
  - Cùng mẫu câu hỏi, hệ thống sinh cho Thí sinh 1 tham số $X_1, Y_1$ và Thí sinh 2 tham số $X_2, Y_2$; đáp án đúng và các đáp án nhiễu tự động tính theo công thức tương ứng.

#### `US-028`: Giới hạn Thời gian Từng câu & Khóa Câu hỏi Đã Hết Giờ
- **Định dạng:** Là giáo viên, tôi muốn cấu hình thời gian riêng cho từng câu hỏi; khi hết giờ câu nào, hệ thống tự động chuyển câu tiếp theo và khóa vĩnh viễn câu cũ, để học sinh không thể dồn giờ tra cứu tài liệu bên ngoài.
- **Traceability:** `RAW-035`
- **Acceptance Criteria (AC-028):**
  - Chế độ "Countdown từng câu" kích hoạt đồng hồ đếm lùi riêng (ví dụ 45s). Hết 45s, câu đó bị gắn nhãn [ĐÃ KHÓA 🔒], không thể chọn lại đáp án và tự động chuyển sang câu tiếp theo.

#### `US-049`: Chế Độ Thi Bảo Mật Cao: Tuyến Tính Một Chiều & Khóa Câu Hết Giờ 30s
- **Định dạng:** Là Hệ thống Khảo thí, tôi muốn áp dụng chế độ thi tuyến tính một chiều và khóa cứng câu hỏi khi hết thời gian 30s, để ngăn chặn học sinh quay lại sửa đáp án hoặc trao đổi câu cũ.
- **Traceability:** `RAW-035`, `RAW-051`
- **Acceptance Criteria (AC-049):**
  - **Kịch bản 1 (Khóa câu hết giờ 30s):** Given học sinh đang làm bài thi, When đồng hồ câu đếm lùi về 0s, Then câu hỏi bị khóa cứng, đáp án bị vô hiệu hóa và thí sinh không thể làm lại câu đó.
  - **Kịch bản 2 (Thi tuyến tính một chiều):** Given học sinh bấm chuyển sang câu tiếp theo, Then câu cũ được đánh dấu hoàn thành và khóa lại, nút "Câu trước" bị vô hiệu hóa (🔒), và thí sinh không được phép bấm quay lại câu trước trên danh sách câu hỏi.

---

### EPIC-05: Quản lý Đề, Giám sát Phòng thi, Xử lý Phúc khảo & Tiện ích GV

#### `US-013`: Bộ lọc ngân hàng câu hỏi 3 cấp độ kèm tags màu sắc
- **Định dạng:** Là giáo viên, tôi muốn lọc câu hỏi theo Môn, Chủ đề, Mức độ khó với các thẻ tag màu, để tìm kiếm câu hỏi nhanh chóng.
- **Traceability:** `RAW-013`
- **Acceptance Criteria (AC-013):**
  - Lọc theo Dropdown: Toán học $\rightarrow$ Hàm số $\rightarrow$ Vận dụng; bảng hiển thị danh sách câu hỏi kèm tag màu độ khó rõ rệt.

#### `US-014`: Đính kèm học liệu Kéo thả và Xem thử Video
- **Định dạng:** Là giáo viên, tôi muốn kéo thả ảnh đề thi và xem video học liệu trực tiếp với nút Play.
- **Traceability:** `RAW-014`
- **Acceptance Criteria (AC-014):**
  - Khung Drag & Drop ảnh đề thi hiển thị preview tức thì; thẻ video có nút Play mở video mẫu mượt mà.

#### `US-015`: Cấu hình Ma trận đề và Slider tỷ lệ trùng lặp
- **Định dạng:** Là giáo viên, tôi muốn nhập số câu theo 3 mức độ và kéo thanh trượt tỷ lệ trùng lặp tối đa giữa các đề (ví dụ 30%).
- **Traceability:** `RAW-015`, `RAW-016`
- **Acceptance Criteria (AC-015):**
  - Bảng ma trận tự tính tổng số câu; thanh trượt Slider cập nhật giá trị % hiển thị ngay khi kéo.

#### `US-016`: Toggles cấu hình chống gian lận thông minh
- **Định dạng:** Là giáo viên, tôi muốn bật/tắt các tùy chọn: Trộn câu hỏi, Trộn đáp án, Cảnh báo chuyển tab bằng công tắc gạt toggle.
- **Traceability:** `RAW-017`
- **Acceptance Criteria (AC-016):**
  - 3 Toggle Switches chuyển đổi trạng thái On (Xanh) / Off (Xám) mượt mà và lưu cấu hình vào bài thi.

#### `US-017`: Bảng Live Proctoring nhấp nháy Badge đỏ khi có vi phạm
- **Định dạng:** Là giáo viên giám thị, tôi muốn thấy danh sách thí sinh trong phòng thi trực tuyến; khi có thí sinh vi phạm chuyển tab, badge đỏ lập tức nhấp nháy.
- **Traceability:** `RAW-018`
- **Acceptance Criteria (AC-017):**
  - Bảng danh sách thí sinh cập nhật theo thời gian thực; khi có tín hiệu chuyển tab, dòng thí sinh tương ứng xuất hiện Badge đỏ nhấp nháy pulse: `! Chuyển tab (1 lần)`.

#### `US-018`: Bảng trượt Timeline xem chi tiết nhật ký sự kiện của thí sinh
- **Định dạng:** Là giáo viên, tôi muốn click vào thí sinh để mở ngăn trượt Timeline từ bên phải, xem lại lịch sử từng giây về thời điểm rời trang và đổi mã đề.
- **Traceability:** `RAW-019`
- **Acceptance Criteria (AC-018):**
  - Click vào học sinh mở Slide-over Drawer từ cạnh phải màn hình; hiển thị chuỗi sự kiện chi tiết: Bắt đầu thi $\rightarrow$ Rời trang $\rightarrow$ Đổi mã đề 04 $\rightarrow$ Tiếp tục làm bài.

#### `US-019`: Trực quan hóa Báo cáo kết quả bằng Biểu đồ cột và Donut
- **Định dạng:** Là giáo viên, tôi muốn xem biểu đồ cột phổ điểm lớp và biểu đồ tròn tỷ lệ hoàn thành để đánh giá chất lượng học tập.
- **Traceability:** `RAW-020`
- **Acceptance Criteria (AC-019):**
  - Hiển thị biểu đồ phổ điểm lớp (Giỏi, Khá, Trung bình, Yếu) và biểu đồ tròn tỷ lệ nộp bài đúng hạn / quá hạn / chưa nộp.

#### `US-029`: Thi Offline - Xuất Phiếu tô và Mô phỏng Camera Quét Chấm Điểm
- **Định dạng:** Là giáo viên, tôi muốn xuất phiếu trả lời trắc nghiệm (phiếu tô 20/50 câu) và mô phỏng giao diện camera quét chấm phiếu tô tự động.
- **Traceability:** `RAW-036`
- **Acceptance Criteria (AC-029):**
  - Tab "Thi Offline" có nút xuất xem trước mẫu phiếu tô PDF; khung mô phỏng camera quét phiếu tô hiển thị khung nhận diện quang học và trả về kết quả số câu đúng/sai tức thì.

#### `US-030`: Mô phỏng Phòng thi Tương tác Trực tiếp AZOTA Live
- **Định dạng:** Là giáo viên, tôi muốn mở phòng thi trực tuyến AZOTA Live với danh sách camera thí sinh thu nhỏ, tính năng điểm danh và giám sát trực tiếp.
- **Traceability:** `RAW-037`
- **Acceptance Criteria (AC-030):**
  - Giao diện AZOTA Live hiển thị lưới ô camera giả lập của thí sinh, nút điểm danh tự động và bảng chat trao đổi nhanh trong phòng thi.

#### `US-043`: Tạo & Quản lý Lớp học, Danh sách Học sinh và Mã mời tham gia của Giáo viên
- **Định dạng:** Là giáo viên bộ môn và chủ nhiệm, tôi muốn tạo lớp học mới, cấu hình khối/môn, quản lý danh sách học sinh thuộc lớp, phân nhóm học tập, cấp mã mời tham gia và xuất sổ điểm lớp ra Excel, để tổ chức và điều hành hoạt động dạy học theo Bảng 1.1, 1.31, 1.75 của BT4-Nhóm 7.
- **Traceability:** `RAW-045`, `NFR-02`, `NFR-03`, `NFR-07`
- **Acceptance Criteria (AC-043):**
  - **Kịch bản 1 (Tạo lớp học mới):** Khi giáo viên ở Cổng giáo viên chọn tab "Lớp Học Của Tôi" và bấm "Tạo Lớp Mới", hệ thống hiển thị modal nhập Tên lớp, Khối, Môn học, Năm học và tự động sinh Mã mời lớp học (Invite Code: `AZT-10A1-MATH`). Bấm xác nhận sẽ tạo lớp thành công.
  - **Kịch bản 2 (Quản lý học sinh & Phân nhóm):** Khi chọn một lớp học trong danh sách (10A1, 10A2, 11A3), bảng học sinh hiển thị đầy đủ: STT, Mã HS, Họ và tên, SĐT phụ huynh, Phân nhóm học tập (Nâng cao / Chuẩn / Phụ đạo), Điểm TB tích lũy và Trạng thái. Có thanh tìm kiếm và bộ lọc nhóm học tập.
  - **Kịch bản 3 (Thêm học sinh & Thích ứng Mobile):** Giáo viên có thể bấm "Thêm Học Sinh" để bổ sung học sinh mới vào lớp, hoặc bấm "Xuất Sổ Điểm Excel". Khi xem trên Mobile Simulator, bảng tự động chuyển đổi thành card dọc không bị tràn viền.

#### `US-044`: Kho Học liệu, Bài giảng & Đề cương Lớp học
- **Định dạng:** Là giáo viên bộ môn, tôi muốn tải lên tài liệu học tập, bài giảng điện tử (Slide, PDF, Video minh họa) gắn với lớp học; và là học sinh, tôi muốn dễ dàng tra cứu, xem trước và tải về học liệu bổ trợ để tự học theo Bảng 1.2, 1.10, 1.47, 1.54 của BT4-Nhóm 7.
- **Traceability:** `RAW-046`, `NFR-01`, `NFR-02`, `NFR-03`
- **Acceptance Criteria (AC-044):**
  - **Kịch bản 1: Giáo viên quản lý kho học liệu lớp học:**
    - *Given:* Giáo viên chọn tab "Học Liệu & Bài Giảng" (`#tab-btn-materials`).
    - *Then:* Hiển thị danh mục tài liệu theo từng lớp (10A1, 10A2, 11A3) với đầy đủ thông tin: Tên tài liệu, Định dạng (PDF, PPTX, MP4), Dung lượng, Ngày tải lên và Số lượt xem/tải.
    - *When:* Bấm nút "Tải Lên Học Liệu Mới" -> Modal tải lên cho phép nhập Tên học liệu, chọn Chuyên đề, đính kèm file và phân quyền "Chỉ xem" hoặc "Cho phép tải về". Bấm lưu -> Tài liệu lập tức xuất hiện trong danh sách.
  - **Kịch bản 2: Học sinh tra cứu và tải tài liệu học tập:**
    - *Given:* Học sinh vào mục "Lớp học" -> sub-tab "Kho Học Liệu & Bài Giảng" (`#subtab-materials-content`).
    - *Then:* Hiển thị lưới card học liệu với icon định dạng trực quan (PDF đỏ, PPTX cam, Video xanh).
    - *When:* Học sinh bấm nút "Tải về" hoặc "Xem trực tuyến" -> Hệ thống kích hoạt xem trước hoặc tải file thành công và tăng biến đếm lượt tải.

#### `US-046`: Gửi Thông Báo & Nhắc Hạn Nộp Cá Nhân Hóa (Bảng 1.6 BT4-Nhóm 7)
- **Định dạng:** Là Giáo viên, tôi muốn soạn và phát thông báo bài học/bài thi, tích hợp cơ chế nhắc hạn nộp cá nhân hóa đến từng lớp hoặc nhóm học sinh, để tăng tỷ lệ hoàn thành bài tập đúng hạn.
- **Traceability:** `RAW-048`, `NFR-02`
- **Acceptance Criteria (AC-046):**
  - **Kịch bản 1 (Soạn thông báo cá nhân hóa):** Given giáo viên ở màn hình Thông báo (Bảng 1.6), When mở form soạn thông báo, Then có thể chọn đối tượng (Cả lớp, Nhóm cần phụ đạo, Nhóm nâng cao), loại thông báo (Nhắc hạn, Lịch thi, Khẩn cấp) và hẹn giờ tự động nhắc trước deadline 2 tiếng.
  - **Kịch bản 2 (Phát thông báo & Đồng bộ đa cổng):** Given giáo viên bấm "Phát Thông Báo Ngay", Then thông báo được lưu vào nhật ký, hiển thị tỷ lệ học sinh đã xem và đồng thời đồng bộ sang Cổng Học sinh và Cổng Phụ huynh.

#### `US-047`: Kênh Tương Tác & Diễn Đàn Thảo Luận Q&A Lớp Học (Bảng 1.7 BT4-Nhóm 7)
- **Định dạng:** Là Giáo viên và Học sinh, tôi muốn có diễn đàn thảo luận hỏi đáp trực tuyến theo môn học/lớp, để giáo viên giải đáp thắc mắc, ghim lời giải chuẩn mực và học sinh trao đổi chuyên đề.
- **Traceability:** `RAW-049`, `NFR-02`
- **Acceptance Criteria (AC-047):**
  - **Kịch bản 1 (Mở chủ đề thảo luận):** Given giáo viên hoặc học sinh ở tab Thảo luận, When mở chủ đề mới, Then chủ đề được hiển thị trong feed thảo luận của lớp với các thẻ phân loại chủ đề (Parabol, Tham số m).
  - **Kịch bản 2 (Trả lời & Ghim lời giải chuẩn):** Given giáo viên trả lời câu hỏi của học sinh, When bấm "Trả lời & Ghim", Then câu trả lời được gắn nhãn "Lời Giải Chuẩn Của Giáo Viên" nổi bật ở đầu chủ đề và đánh dấu Đã giải đáp.

---

### EPIC-06: Cổng Tương tác Dành cho Phụ huynh

#### `US-020`: Liên kết hồ sơ con qua Mã định danh học sinh
- **Định dạng:** Là phụ huynh, tôi muốn nhập mã định danh con để kết nối tài khoản phụ huynh với hồ sơ học sinh.
- **Traceability:** `RAW-021`
- **Acceptance Criteria (AC-020):**
  - Nhập mã học sinh `HS-2026-07`, bấm liên kết $\rightarrow$ Mở khóa Dashboard theo dõi của con.

#### `US-021`: Dashboard theo dõi bài tập, Mini-chart điểm số và Lời phê
- **Định dạng:** Là phụ huynh, tôi muốn xem các widget bài nợ/sắp hạn, biểu đồ tiến bộ điểm số và danh sách nhận xét của giáo viên.
- **Traceability:** `RAW-022`
- **Acceptance Criteria (AC-021):**
  - Hiển thị 3 widget nổi bật (Tiến độ, Bài chưa nộp đỏ, Bài sắp hạn cam), Mini-chart điểm qua các bài thi và Notification Feed nhận xét của giáo viên.

#### `US-022`: Bong bóng Chat nổi trao đổi trực tiếp với giáo viên
- **Định dạng:** Là phụ huynh, tôi muốn có Bong bóng Chat nổi ở góc phải dưới để mở khung trò chuyện trực tiếp với giáo viên phụ trách.
- **Traceability:** `RAW-023`
- **Acceptance Criteria (AC-022):**
  - Click icon bong bóng chat ở góc phải dưới mở khung chat mini trao đổi cùng giáo viên; click lại để thu nhỏ.

---

### EPIC-07: Quản trị Cấp trường & Phân quyền Đội nhóm (Admin Portal)

#### `US-031`: Dashboard Quản trị Tổng thể & Chỉ số KPIs Nhà trường
- **Định dạng:** Là Quản trị viên nhà trường, tôi muốn xem bảng điều khiển tổng quan với các chỉ số KPIs (tổng số học sinh, giáo viên, lớp học, kỳ thi chung và trạng thái máy chủ).
- **Traceability:** `RAW-027`
- **Acceptance Criteria (AC-031):**
  - Dashboard Quản trị hiển thị các thẻ KPIs: 1.250 Học sinh, 68 Giáo viên, 32 Lớp học, 3 Kỳ thi chung đang diễn ra, Tải máy chủ CPU 28% / RAM 42%.

#### `US-032`: Quản lý Người dùng & Đội nhóm Phân quyền RBAC
- **Định dạng:** Là Quản trị viên, tôi muốn quản lý danh sách tài khoản toàn trường, phân quyền theo nhóm (Ban Giám Hiệu, Tổ trưởng, Giáo viên, Học sinh, Phụ huynh) và thực hiện khóa/mở tài khoản.
- **Traceability:** `RAW-028`
- **Acceptance Criteria (AC-032):**
  - Bảng danh sách người dùng có bộ lọc theo vai trò; nút Thêm tài khoản mới, nút Gán nhóm quyền và nút Khóa/Mở tài khoản với thông báo xác nhận.

#### `US-033`: Quản lý Cấu trúc Nhà trường, Khối lớp & Nhập học sinh từ Excel
- **Định dạng:** Là Quản trị viên, tôi muốn quản lý danh sách khối 10, 11, 12, phân công giáo viên chủ nhiệm và xem trước tính năng nhập danh sách học sinh từ file Excel.
- **Traceability:** `RAW-029`
- **Acceptance Criteria (AC-033):**
  - Danh sách cây cấu trúc lớp theo Khối; nút "Nhập từ Excel" mở modal kéo thả file Excel mẫu và hiển thị bảng xem trước 5 học sinh mẫu chuẩn bị nạp vào lớp.

#### `US-034`: Thiết lập & Tổ chức Kỳ thi Chung Toàn trường/Toàn khối
- **Định dạng:** Là Quản trị viên, tôi muốn tạo kỳ thi chung (ví dụ Khảo sát chất lượng Giữa kỳ), phân bổ đề thi chung và theo dõi danh sách các phòng thi ảo tập trung.
- **Traceability:** `RAW-030`
- **Acceptance Criteria (AC-034):**
  - Giao diện Kỳ thi chung cho phép tạo đợt thi mới, chọn khối tham gia (Khối 12), gán đề thi chung môn Toán và xem danh sách các phòng thi ảo đang hoạt động.

#### `US-035`: Thống kê & Báo cáo Chuyên sâu Cấp trường
- **Định dạng:** Là Quản trị viên, tôi muốn xem biểu đồ so sánh phổ điểm giữa các lớp trong khối và xếp hạng môn học để đánh giá chất lượng dạy học toàn trường.
- **Traceability:** `RAW-031`
- **Acceptance Criteria (AC-035):**
  - Biểu đồ so sánh điểm trung bình giữa các lớp 12A1, 12A2, 12A3 và tỷ lệ đạt loại Giỏi/Khá toàn khối; có nút xuất báo cáo Excel/PDF.

#### `US-036`: Giám sát An toàn, Audit Logs & Trạng thái Hệ thống
- **Định dạng:** Là Quản trị viên, tôi muốn theo dõi nhật ký hoạt động hệ thống (Audit Logs) để truy vết các thao tác quan trọng và kiểm soát an toàn bảo mật.
- **Traceability:** `RAW-032`
- **Acceptance Criteria (AC-036):**
  - Bảng Audit Logs liệt kê lịch sử chi tiết: Thời gian, Người thực hiện, Hành động (Đăng nhập, Thay đổi đề thi, Cấp mã đề mới, Cập nhật điểm), Địa chỉ IP giả lập và trạng thái an toàn.

#### `US-037`: Trung tâm Quản lý Thông báo Toàn trường & Xử lý Yêu cầu Hỗ trợ
- **Định dạng:** Là Quản trị viên, tôi muốn gửi thông báo tức thì đến toàn trường và quản lý danh sách các yêu cầu hỗ trợ sự cố từ giáo viên/học sinh.
- **Traceability:** `RAW-033`
- **Acceptance Criteria (AC-037):**
  - Form tạo thông báo toàn trường (chọn người nhận: Tất cả, Giáo viên, Học sinh); bảng tiếp nhận ticket sự cố có nút đánh dấu "Đã xử lý".

#### `US-048`: Quản Lý Học Liệu, Giám Sát Lưu Trữ & Dữ Liệu Hệ Thống (Bảng 1.25 BT4-Nhóm 7)
- **Định dạng:** Là Quản trị viên, tôi muốn theo dõi dung lượng lưu trữ đám mây, kiểm duyệt danh mục tệp học liệu, bài tập, đề thi toàn trường và bảo trì dọn dẹp hệ thống.
- **Traceability:** `RAW-050`, `NFR-07`
- **Acceptance Criteria (AC-048):**
  - **Kịch bản 1 (Giám sát tài nguyên đám mây):** Given quản trị viên ở tab Quản lý học liệu (Bảng 1.25), Then hiển thị các chỉ số dung lượng đám mây (412.5 GB / 1 TB, 1.240 bài giảng, 2.850 đề thi, tỷ lệ khả dụng 100%).
  - **Kịch bản 2 (Kiểm duyệt, dọn cache & Sao lưu):** Given quản trị viên xem sổ quản lý tệp, Then có thể kiểm duyệt, tải về bản sao lưu, dọn dẹp cache rác và kích hoạt lệnh sao lưu đám mây tức thì.

---

### EPIC-08: Chuẩn hóa Giao diện & Tối ưu hóa Chế độ Điện thoại

#### `US-023`: Đồng bộ Design System AZOTA và Client Mock Store
- **Định dạng:** Là người xem demo, tôi muốn giao diện tuân thủ bảng màu chuẩn AZOTA, font chữ, card layout và tự lưu trạng thái mượt mà không cần backend.
- **Traceability:** `RAW-024`, `RAW-025`, `NFR-01`, `NFR-05`
- **Acceptance Criteria (AC-023):**
  - 100% components tuân thủ design tokens AZOTA; dữ liệu bài thi, lịch sử vi phạm, thông tin người dùng được quản lý nhất quán trong Local Store.

#### `US-024`: Chuyển đổi Linh hoạt Giữa Giao diện Máy tính và Khung Điện thoại
- **Định dạng:** Là người thuyết trình, tôi muốn có nút chuyển đổi tức thì giữa chế độ Desktop Web và Khung điện thoại iPhone 16 Pro có Dynamic Island và Status Bar.
- **Traceability:** `RAW-026`, `NFR-08`
- **Acceptance Criteria (AC-024):**
  - Nút `[💻 Máy tính]` $\leftrightarrow$ `[📱 Điện thoại]` trên thanh Demo Toolbar chuyển đổi ngay lập tức khung viền iPhone sắc nét kèm thanh trạng thái.

#### `US-038`: Tinh chỉnh Bố cục & Trải nghiệm Chế độ Điện thoại (Mobile App Simulator Refinement)
- **Định dạng:** Là người dùng trải nghiệm trên chế độ Điện thoại, tôi muốn bố cục, nút bấm, bảng biểu và modal được thiết kế chuẩn mobile vừa khít khung viền smartphone mô phỏng mà không bị vỡ giao diện hay tràn màn hình.
- **Traceability:** `RAW-040`, `NFR-03`
- **Acceptance Criteria (AC-038):**
  - **Kịch bản 1: Container-Scoped Layout & Bottom Navigation Bar:**
    - *Given:* Ứng dụng đang ở chế độ Điện thoại (`max-w-[430px]`).
    - *Then:* Bố cục tự động chuyển sang layout mobile chuyên dụng (container-scoped); Header thu gọn thành App Header và đáy xuất hiện thanh **Bottom Navigation Bar** 4-5 tabs ứng dụng chạm nhạy.
  - **Kịch bản 2: Phòng thi toán và đồ thị Parabol chuẩn cảm ứng:**
    - *Given:* Đang làm bài thi trong chế độ điện thoại.
    - *Then:* Đồ thị Parabol co giãn vừa khít 100% chiều ngang màn hình điện thoại; các phương án Radio A, B, C, D to bản dễ chạm bằng một ngón tay; lưới câu hỏi chuyển thành dải pill vuốt ngang (Horizontal Swipe) tiện lợi.
  - **Kịch bản 3: Tự động chuyển Bảng biểu sang Thẻ Card dọc (Card-view):**
    - *Given:* Đang xem các bảng dữ liệu (Giám sát thí sinh, Danh sách học sinh, Audit Logs, Đề thi).
    - *Then:* Bảng tự động xếp lại thành các thẻ Card dọc gọn gàng, hỗ trợ thao tác cuộn mượt mà mà tuyệt đối không xuất hiện thanh cuộn ngang gây vỡ viền.
  - **Kịch bản 4: Modal cảnh báo chống gian lận nằm trọn trong khung điện thoại:**
    - *Given:* Học sinh chuyển tab khi đang trong chế độ điện thoại.
    - *Then:* Modal đỏ cảnh báo và animation đổi mã đề tự động co lại và neo trọn vẹn bên trong màn hình điện thoại, mô phỏng chính xác trải nghiệm cảnh báo trên ứng dụng AZOTA Mobile thật.

---

## 3. Ma trận Truy vết Yêu cầu Khép kín (Traceability Matrix)

| RAW ID | Tên Yêu cầu Khách hàng | Epic ID | Feature ID | User Story ID | Acceptance Criteria (GWT) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAW-001** | Form đăng nhập 4 tabs đổi màu nhận diện | EPIC-01 | FEAT-1.1 | `US-001` | `AC-001` (Kịch bản 1) |
| **RAW-002** | Ẩn/hiện mật khẩu & ghi nhớ đăng nhập | EPIC-01 | FEAT-1.1 | `US-002` | `AC-002` (Kịch bản 1, 2) |
| **RAW-003** | Điều hướng tức thì & cách ly RBAC 4 vai trò | EPIC-01 | FEAT-1.2 | `US-003` | `AC-003` (Kịch bản 1) |
| **RAW-004** | Grid đề thi học sinh & input mã/link | EPIC-02 | FEAT-2.1 | `US-004` | `AC-004` (Kịch bản 1) |
| **RAW-005** | Widget sắp đến hạn & countdown thời gian thực | EPIC-02 | FEAT-2.1 | `US-005` | `AC-005` (Kịch bản 1) |
| **RAW-006** | Câu hỏi Toán đồ thị parabol & 4 nút Radio | EPIC-02 | FEAT-2.3 | `US-006` | `AC-006` (Kịch bản 1) |
| **RAW-007** | Sidebar countdown lớn & lưới câu hỏi đổi màu | EPIC-02 | FEAT-2.3 | `US-007` | `AC-007` (Kịch bản 1) |
| **RAW-008** | Footer điều hướng & nút nộp bài | EPIC-02 | FEAT-2.3 | `US-008` | `AC-008` (Kịch bản 1) |
| **RAW-009** | Chỉ báo Auto-save ngầm kèm timestamp | EPIC-02 | FEAT-2.4 | `US-009` | `AC-009` (Kịch bản 1) |
| **RAW-010** | Modal đỏ cảnh báo khi chuyển tab | EPIC-03 | FEAT-3.1 | `US-010` | `AC-010` (Kịch bản 1) |
| **RAW-011** | Animation đổi mã đề 01 ➔ 04 trên modal | EPIC-03 | FEAT-3.2 | `US-011` | `AC-011` (Kịch bản 1) |
| **RAW-012** | Đổi đề tương đương, bảo lưu giờ và câu đã làm | EPIC-03 | FEAT-3.2 | `US-012` | `AC-012` (Kịch bản 1) |
| **RAW-013** | Bộ lọc ngân hàng câu hỏi 3 cấp độ kèm tags | EPIC-05 | FEAT-5.1 | `US-013` | `AC-013` (Kịch bản 1) |
| **RAW-014** | Kéo thả ảnh đề thi & xem thử video học liệu | EPIC-05 | FEAT-5.2 | `US-014` | `AC-014` (Kịch bản 1) |
| **RAW-015** | Bảng thiết lập ma trận đề 3 mức độ | EPIC-05 | FEAT-5.2 | `US-015` | `AC-015` (Kịch bản 1) |
| **RAW-016** | Slider tỷ lệ trùng lặp câu hỏi tối đa | EPIC-05 | FEAT-5.2 | `US-015` | `AC-015` (Kịch bản 1) |
| **RAW-017** | Toggles cấu hình chống gian lận | EPIC-05 | FEAT-5.2 | `US-016` | `AC-016` (Kịch bản 1) |
| **RAW-018** | Bảng Live Proctoring nhấp nháy badge đỏ | EPIC-05 | FEAT-5.3 | `US-017` | `AC-017` (Kịch bản 1) |
| **RAW-019** | Drawer Timeline nhật ký sự kiện chi tiết | EPIC-05 | FEAT-5.3 | `US-018` | `AC-018` (Kịch bản 1) |
| **RAW-020** | Biểu đồ cột điểm TB & biểu đồ tròn hoàn thành | EPIC-05 | FEAT-5.4 | `US-019` | `AC-019` (Kịch bản 1) |
| **RAW-021** | Form liên kết mã học sinh cho phụ huynh | EPIC-06 | FEAT-6.1 | `US-020` | `AC-020` (Kịch bản 1) |
| **RAW-022** | Dashboard phụ huynh: widget, mini-chart, feed | EPIC-06 | FEAT-6.2 | `US-021` | `AC-021` (Kịch bản 1) |
| **RAW-023** | Bong bóng Chat nổi trao đổi với giáo viên | EPIC-06 | FEAT-6.3 | `US-022` | `AC-022` (Kịch bản 1) |
| **RAW-024** | Chuẩn hóa nhận diện Design System AZOTA | EPIC-08 | FEAT-8.1 | `US-023` | `AC-023` (Kịch bản 1) |
| **RAW-025** | Mockup Frontend độc lập, giả lập Local State | EPIC-08 | FEAT-8.1 | `US-023` | `AC-023` (Kịch bản 1) |
| **RAW-026** | Khung mô phỏng Điện thoại di động (iPhone chassis) | EPIC-08 | FEAT-8.2 | `US-024` | `AC-024` (Kịch bản 1) |
| **RAW-027** | Dashboard Quản trị cấp trường & KPIs vận hành | EPIC-07 | FEAT-7.1 | `US-031` | `AC-031` (Kịch bản 1) |
| **RAW-028** | Quản lý người dùng & Đội nhóm phân quyền RBAC | EPIC-07 | FEAT-7.2 | `US-032` | `AC-032` (Kịch bản 1) |
| **RAW-029** | Cấu trúc nhà trường, khối lớp & Import Excel | EPIC-07 | FEAT-7.3 | `US-033` | `AC-033` (Kịch bản 1) |
| **RAW-030** | Thiết lập & Tổ chức kỳ thi chung toàn trường | EPIC-07 | FEAT-7.4 | `US-034` | `AC-034` (Kịch bản 1) |
| **RAW-031** | Thống kê & Báo cáo chuyên sâu cấp trường | EPIC-07 | FEAT-7.5 | `US-035` | `AC-035` (Kịch bản 1) |
| **RAW-032** | Giám sát an toàn, Audit Logs & Máy chủ | EPIC-07 | FEAT-7.6 | `US-036` | `AC-036` (Kịch bản 1) |
| **RAW-033** | Quản lý thông báo toàn trường & Hỗ trợ kỹ thuật | EPIC-07 | FEAT-7.7 | `US-037` | `AC-037` (Kịch bản 1) |
| **RAW-034** | Thi thông minh: Câu hỏi biến đổi tham số | EPIC-04 | FEAT-4.1 | `US-027` | `AC-027` (Kịch bản 1) |
| **RAW-035** | Thi thông minh: Countdown từng câu & Khóa câu | EPIC-04 | FEAT-4.2 | `US-028` | `AC-028` (Kịch bản 1) |
| **RAW-036** | Giáo viên: Chấm phiếu tô trắc nghiệm offline | EPIC-05 | FEAT-5.5 | `US-029` | `AC-029` (Kịch bản 1) |
| **RAW-037** | Giáo viên: AZOTA Live phòng thi trực tuyến | EPIC-05 | FEAT-5.6 | `US-030` | `AC-030` (Kịch bản 1) |
| **RAW-038** | Học sinh: Phân hệ Tự luyện tập theo chủ đề | EPIC-02 | FEAT-2.5 | `US-025` | `AC-025` (Kịch bản 1) |
| **RAW-039** | Học sinh: Xem lại bài thi chi tiết & Lời phê | EPIC-02 | FEAT-2.6 | `US-026` | `AC-026` (Kịch bản 1) |
| **RAW-040** | Tinh chỉnh Bố cục & Trải nghiệm Chế độ Điện thoại | EPIC-08 | FEAT-8.3 | `US-038` | `AC-038` (Kịch bản 1, 2, 3, 4) |
| **RAW-041** | Phòng chờ trước giờ thi kiểm tra mạng & cam kết | EPIC-02 | FEAT-2.2 | `US-039` | `AC-039` (Kịch bản 1) |
| **RAW-042** | Mô phỏng Mất mạng & Khôi phục phiên thi | EPIC-03 | FEAT-3.3 | `US-040` | `AC-040` (Kịch bản 1) |
| **RAW-043** | Quy trình Phúc khảo & Chỉnh sửa Điểm số | EPIC-02 / EPIC-05 | FEAT-2.7 / FEAT-5.4 | `US-041` | `AC-041` (Kịch bản 1, 2) |
| **RAW-044** | Biểu mẫu Đăng ký & Điều khoản Chính sách | EPIC-01 | FEAT-1.3 | `US-042` | `AC-042` (Kịch bản 1, 2) |
| **RAW-045** | Quản lý Lớp học của Giáo viên | EPIC-05 | FEAT-5.7 | `US-043` | `AC-043` (Kịch bản 1, 2, 3) |
| **RAW-046** | Kho Học liệu, Bài giảng & Đề cương Lớp học | EPIC-05 | FEAT-5.8 | `US-044` | `AC-044` (Kịch bản 1, 2) |
| **RAW-047** | Giao & Nộp Bài tập Tự luận Kèm Ảnh & Đối soát AI | EPIC-02 / EPIC-05 | FEAT-2.8 / FEAT-5.2 | `US-045` | `AC-045` (Kịch bản 1, 2) |
| **RAW-048** | Gửi thông báo & nhắc hạn nộp cá nhân hóa | EPIC-05 | FEAT-5.9 | `US-046` | `AC-046` (Kịch bản 1, 2) |
| **RAW-049** | Kênh tương tác & diễn đàn thảo luận Q&A lớp học | EPIC-05 | FEAT-5.10 | `US-047` | `AC-047` (Kịch bản 1, 2) |
| **RAW-050** | Quản lý học liệu & dữ liệu hệ thống cho Admin | EPIC-07 | FEAT-7.8 | `US-048` | `AC-048` (Kịch bản 1, 2) |
| **RAW-051** | Chế độ thi bảo mật cao & Cưỡng ép nộp bài | EPIC-04 / EPIC-03 | FEAT-4.3 / FEAT-3.4 | `US-049`, `US-050` | `AC-049`, `AC-050` |
| **RAW-052** | Học sinh tham gia lớp học bằng mã mời | EPIC-02 | FEAT-2.9 | `US-051` | `AC-051` (Kịch bản 1, 2) |
| **RAW-053** | Học sinh thảo luận với giáo viên & bạn học | EPIC-02 | FEAT-2.10 | `US-052` | `AC-052` (Kịch bản 1, 2) |

---

## 4. Kết luận Bước 2 & Sẵn sàng cho Bước 3
- Toàn bộ **53/53 yêu cầu thô** (`RAW-001` đến `RAW-053`) đã được bao phủ khép kín 100% trong **8 Epics**, **33 Features**, và **52 User Stories (`US-001` đến `US-052`)**.
- Tích hợp trọn vẹn quy trình 7 giai đoạn từ [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md) và toàn bộ 86 Bảng biểu chức năng theo [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md):
  - **Quản lý Lớp học Giáo viên (`US-043`)** & **Kho Học liệu & Bài giảng số (`US-044`)**
  - **Học sinh tham gia lớp học bằng mã mời (`US-051` / Bảng 1.8)** & **Học sinh thảo luận Q&A với giáo viên và bạn học (`US-052` / Bảng 1.14)**
  - **Gửi thông báo & Nhắc hạn nộp cá nhân hóa (`US-046` / Bảng 1.6)** & **Diễn đàn hỏi đáp Q&A lớp học của giáo viên (`US-047` / Bảng 1.7)**
  - **Quản lý học liệu & Dung lượng lưu trữ đám mây Admin (`US-048` / Bảng 1.25)**
  - **Giao & Nộp Bài tập Tự luận Kèm Ảnh Chụp Vở & Đối soát Trùng lặp AI (`US-045`)**
  - **Phòng chờ Pre-check Lobby (`US-039`)** & **Khôi phục bài thi khi mất mạng (`US-040`)**
  - **Quy trình Phúc khảo & Chỉnh sửa điểm (`US-041`)** & **Đăng ký tài khoản có điều khoản (`US-042`)**
  - **Chế độ thi tuyến tính một chiều & Khóa câu hết giờ 30s (`US-049`)**
  - **Cơ chế Cưỡng ép nộp bài khi vi phạm 3/3 lần (`US-050`)**
- Sẵn sàng chuyển sang **Bước 3: Cập nhật MoSCoW, Story Points & Sprint Roadmap**.
