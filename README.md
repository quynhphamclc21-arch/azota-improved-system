# AZOTA CẢI TIẾN (AZOTA ENHANCED) - TỔNG QUAN DỰ ÁN

Hệ thống Khảo thí & Đào tạo Trực tuyến Toàn diện – Phiên bản Prototype Mockup Tương tác cao (Interactive Single Page Application).  
Dự án được phân tích, thiết kế kỹ thuật và hoàn thiện theo đúng **Quy chuẩn 5 bước phát triển** dựa trên bộ tài liệu đầu vào tại thư mục [Init/](file:///Users/phamkhanh/Documents/Project/Miu/Init/).

---

## 📑 Mục Lục
1. [Nguồn Căn Cứ & Tài Liệu Đầu Vào (`Init/`)](#1-nguồn-căn-cứ--tài-liệu-đầu-vào-init)
2. [Khung Quy Chuẩn 5 Bước Phát Triển (`specs/`)](#2-khung-quy-chuẩn-5-bước-phát-triển-specs)
3. [Hệ Sinh Thái 4 Cổng Phân Quyền (RBAC)](#3-hệ-sinh-thái-4-cổng-phân-quyền-rbac)
4. [Các Giải Pháp Kỹ Thuật Đột Phá & Chống Gian Lận Đa Tầng](#4-các-giải-pháp-kỹ-thuật-đột-phá--chống-gian-lận-đa-tầng)
5. [Kiến Trúc Bộ Giả Lập Di Động (Container-Scoped Mobile Engine)](#5-kiến-trúc-bộ-giả-lập-di-động-container-scoped-mobile-engine)
6. [Kết Quả Kiểm Thử Chấp Nhận Tự Động (E2E Test Suite)](#6-kết-quả-kiểm-thử-chấp-nhận-tự-động-e2e-test-suite)
7. [Cấu Trúc Thư Mục Dự Án](#7-cấu-trúc-thư-mục-dự-án)
8. [Hướng Dẫn Vận Hành & Trải Nghiệm Nhanh](#8-hướng-dẫn-vận-hành--trải-nghiệm-nhanh)

---

## 1. Nguồn Căn Cứ & Tài Liệu Đầu Vào (`Init/`)

Toàn bộ giải pháp được đối soát và phát triển bám sát 4 tài nguyên khởi tạo cốt lõi:
* [client_request.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/client_request.md): Yêu cầu trực quan ban đầu của khách hàng (mockup thuần Frontend, thiết kế chuẩn AZOTA, đồ thị Parabol, pop-up chuyển tab đổi đề 01 ➔ 04, ma trận đề, mobile chassis).
* [Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md): Đặc tả chi tiết 5 cụm giao diện, bảng màu Design System AZOTA (`#2563EB`, `#F3F4F6`, 5 badge trạng thái) và quy trình vận hành khép kín qua **7 giai đoạn**.
* [Frame.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Frame.md): Khung phương pháp luận chuẩn 5 bước chuyển hóa từ tài liệu thô đến sản phẩm mã nguồn hoàn thiện và vòng lặp Code Review 3 lăng kính.
* [BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md): Báo cáo nghiệp vụ AZOTA cải tiến chi tiết (Chương 1 đến Chương 3), đáp ứng đầy đủ **86 bảng biểu nghiệp vụ**.

---

## 2. Khung Quy Chuẩn 5 Bước Phát Triển (`specs/`)

```text
[Init/ Đầu vào] ➔ [Bước 1: Ingestion] ➔ [Bước 2: Agile Backlog] ➔ [Bước 3: Roadmap] ➔ [Bước 4: Tech Design] ➔ [Bước 5: Code & Tests]
```

1. **Bước 1: Trích Xuất & Chuẩn Hóa Yêu Cầu ([01_requirements_ingestion.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/01_requirements_ingestion.md)):**
   - Phân tích và trích xuất **53 yêu cầu thô** nguyên văn (`RAW-001` ➔ `RAW-053`).
   - Xây dựng **8 kịch bản nghiệp vụ As-Is / To-Be** cho toàn bộ các quy trình trong hệ thống.
   - Xác lập **8 tiêu chuẩn phi chức năng (NFR-01 ➔ NFR-08)**: UI/UX chuẩn Azota, zero backend dependency, RBAC nghiêm ngặt, container-scoped mobile, Page Visibility API event capture.
2. **Bước 2: Agile Backlog Scrum ([02_agile_backlog.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/02_agile_backlog.md)):**
   - Phân rã thành **8 Epics lớn**, **33 Features**, và **52 User Stories** (`US-001` ➔ `US-052`) đạt 100% chuẩn **INVEST**.
   - Thiết lập bộ tiêu chí nghiệm thu **Given - When - Then (GWT)** chi tiết cho từng User Story.
   - Xây dựng **Ma trận truy vết (Traceability Matrix)** khép kín từ `RAW-xxx` đến User Story và AC.
3. **Bước 3: Định Lượng MoSCoW & Lộ Trình Phát Hành ([03_product_roadmap.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/03_product_roadmap.md)):**
   - Phân loại MoSCoW: **34 Must-have** (149 SP), **15 Should-have** (49 SP), **3 Could-have** (9 SP).
   - Ước lượng độ phức tạp theo dãy số Fibonacci: Tổng cộng **207 Story Points (SP)**.
   - Lộ trình chia thành **6 Sprints phát triển** (5 Sprints nền tảng + Sprint 6 hoàn thiện nghiệp vụ chuyên sâu).
4. **Bước 4: Thiết Kế Kỹ Thuật & Kiến Trúc Mockup ([04_technical_design.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/04_technical_design.md)):**
   - Kiến trúc Single Page Application (SPA) với Reactive Local Store và Multi-channel Event Bus.
   - Dual Viewport Engine: Khung iPhone 16 Pro mockup chassis với Dynamic Island, Status Bar và Bottom Navigation Bar.
   - CSS Keyframes Transition Engine (`fadeInView`, `tabSlideFade`, `roleMorphing`).
   - Đặc tả 7 Mock RESTful API contracts phục vụ giả lập tương tác mạng.
5. **Bước 5: Mã Nguồn, Review Loops & Kiểm Thử ([05_code_and_tests/](file:///Users/phamkhanh/Documents/Project/Miu/specs/05_code_and_tests/)):**
   - Ứng dụng Mockup SPA hoàn chỉnh tích hợp trong [index.html](file:///Users/phamkhanh/Documents/Project/Miu/output/index.html).
   - Bộ Test Suite tự động DOM Runner [test_suite.html](file:///Users/phamkhanh/Documents/Project/Miu/output/test_suite.html) (52/52 Acceptance Tests PASSED).
   - Nhật ký 9 vòng Code Review & Refactor chuyên sâu [REVIEW_LOG.md](file:///Users/phamkhanh/Documents/Project/Miu/REVIEW_LOG.md) (`REV-SPRINT-01` ➔ `REV-SPRINT-09`).

---

## 3. Hệ Sinh Thái 4 Cổng Phân Quyền (RBAC)

Ứng dụng cách ly giao diện 100% theo vai trò, không để lẫn menu giữa các phân hệ:

### 🎓 3.1. Cổng Học Sinh (Student Workspace)
* **Tham gia lớp học (`US-051` / Bảng 1.8):** Đặt ở vị trí ưu tiên đầu thanh chức năng; nhập mã mời lớp học (`10A1-TOAN`, `10A2-TOAN`, `11A3-TOAN`) hoặc nhấp liên kết mời để ghi danh; hiển thị thẻ lớp học trực quan với thông tin giáo viên phụ trách, sĩ số và bài tập đang giao.
* **Đề thi của tôi & Trang chủ:** Lưới đề thi thẻ Card trực quan, badge trạng thái 3 màu (Đã nộp, Đang mở, Quá hạn), Widget cảnh báo "Sắp đến hạn!" kèm đồng hồ đếm lùi và thanh tiến trình.
* **Phòng chờ Pre-check Lobby (`US-039`):** Kiểm tra thiết bị & kết nối mạng xanh ổn định, bảng quy định phòng thi và checkbox cam kết trước khi mở đề.
* **Không gian làm bài thi Toán (`US-006` - `US-009`):** Đồ thị Parabol giải tích SVG chuẩn tọa độ $Oxy$, 4 phương án Radio to bản chuẩn cảm ứng, sidebar đồng hồ đếm lùi cỡ lớn, lưới 20 ô vuông chuyển màu thông minh, chỉ báo auto-save ngầm kèm timestamp `[HH:mm:ss]`.
* **Tự luyện tập theo chủ đề (`US-025`):** Ôn tập không giới hạn theo các chuyên đề (Hàm số, Hình học, Tổ hợp).
* **Xem lại bài thi & Phúc khảo (`US-026`, `US-041`):** Đối chiếu câu đúng/sai, xem giải thích chi tiết, lời phê giáo viên và gửi đơn giải trình vi phạm / phúc khảo điểm (`DISP-001`).
* **Nộp bài tập tự luận chụp ảnh vở (`US-045`):** Đính kèm nhiều trang ảnh vở bài làm, ghi chú gửi thầy cô.
* **Thảo luận & Hỏi đáp Q&A Lớp học (`US-052` / Bảng 1.14):** Đặt câu hỏi thắc mắc theo bài tập/chủ đề, tương tác trao đổi đa chiều với giáo viên và các bạn cùng lớp; tiếp nhận và xem lời giải đáp chuẩn mực được ghim từ giáo viên (đồng bộ hai chiều với Bảng 1.7 bên Cổng Giáo viên).

### 👨‍🏫 3.2. Cổng Giáo Viên (Teacher Suite)
* **Quản lý lớp học (`US-043` / Bảng 1.1):** Đặt ở vị trí ưu tiên đầu thanh chức năng; tạo lớp, cấu hình khối/môn, quản lý danh sách học sinh, phân nhóm học tập (Nâng cao / Chuẩn / Phụ đạo), cấp mã mời vào lớp.
* **Kho học liệu & Bài giảng số (`US-044` / Bảng 1.2):** Tải lên bài giảng PDF, PPTX, Video bài học theo chuyên đề, phân quyền xem/tải trực tuyến.
* **Gửi thông báo & Nhắc hạn nộp cá nhân hóa (`US-046` / Bảng 1.6):** Soạn thông báo bài học/bài thi theo lớp hoặc nhóm đối tượng, kích hoạt nhắc hạn tự động trước 2 tiếng, đồng bộ tức thì sang Cổng Học sinh và Phụ huynh.
* **Kênh tương tác Q&A lớp học (`US-047` / Bảng 1.7):** Diễn đàn hỏi đáp môn học, ghim lời giải chuẩn mực của giáo viên và đánh dấu đã giải đáp.
* **Ngân hàng câu hỏi & Tạo đề ma trận (`US-013` - `US-016`):** Bộ lọc 3 tiêu chí kèm tag màu, kéo thả học liệu, thiết lập ma trận đề (Nhận biết, Thông hiểu, Vận dụng), slider điều chỉnh tỷ lệ trùng câu tối đa (%).
* **Giám sát trực tiếp Live Proctoring (`US-017`, `US-018`):** Bảng trạng thái thí sinh thời gian thực, nhấp nháy badge đỏ khi có vi phạm, Drawer Timeline trượt ra hiển thị lịch sử từng giây.
* **Báo cáo & Thống kê (`US-019`):** Phổ điểm lớp dạng cột và biểu đồ tỷ lệ hoàn thành dạng tròn Donut.
* **Xử lý phúc khảo (`US-041`):** Duyệt giải trình vi phạm và chỉnh sửa điểm trực tiếp (+0.5đ lên 9.0/10) kèm đồng bộ hai chiều.
* **Thi Offline phiếu tô trắc nghiệm (`US-029`):** Xuất phiếu tô PDF và mô phỏng camera quét chấm điểm OMR AI.
* **Phòng thi tương tác AZOTA Live (`US-030`):** Lưới camera thí sinh trực tuyến, điểm danh và giơ tay phát biểu.

### 👪 3.3. Cổng Phụ Huynh (Parent Portal)
* **Liên kết hồ sơ (`US-020`):** Nhập mã học sinh (`HS-2026-07`) để liên kết và đồng bộ hồ sơ con em.
* **Dashboard theo dõi tiện ích (`US-021`):** Các thẻ Widget thông minh ("Tiến độ học tập", "Bài chưa nộp", "Bài sắp đến hạn"), Mini-chart xu hướng điểm số, Notification Feed cập nhật lời phê của thầy cô.
* **Bong bóng Chat nổi (`US-022`):** Floating chat widget cố định góc phải dưới màn hình trao đổi trực tiếp với giáo viên chủ nhiệm.

### 🏛️ 3.4. Cổng Quản Trị Viên (Admin School Management)
* **Dashboard tổng quan cấp trường (`US-031`):** Chỉ số KPIs toàn trường (học sinh, giáo viên, phòng thi, tài nguyên máy chủ).
* **Quản lý người dùng & RBAC (`US-032`):** Danh sách tài khoản, phân nhóm quyền, cấp mới, khóa/mở khóa tài khoản.
* **Cấu trúc trường & Khối lớp (`US-033`):** Quản lý khối 10, 11, 12, phân công chuyên môn, hỗ trợ xem trước danh sách học sinh từ file Excel mẫu.
* **Tổ chức kỳ thi chung (`US-034`):** Thiết lập kỳ thi tập trung toàn khối, phân phòng thi ảo, theo dõi tiến độ thi chung.
* **Thống kê chuyên sâu (`US-035`):** So sánh chất lượng giáo dục giữa các lớp và xếp hạng môn học.
* **Giám sát an toàn & Audit Logs (`US-036`):** Nhật ký hệ thống ghi vết bảo mật toàn bộ hành vi quản trị (đăng nhập, đổi đề, sửa điểm).
* **Quản lý học liệu & Dung lượng đám mây (`US-048` / Bảng 1.25):** Giám sát 412.5 GB / 1 TB lưu trữ AWS S3, kiểm duyệt tệp bài giảng, dọn dẹp cache rác và kích hoạt bản sao lưu.
* **Trung tâm thông báo & Tiếp nhận Ticket (`US-037`):** Phát thông báo khẩn cấp toàn trường và quản lý xử lý sự cố.

---

## 4. Các Giải Pháp Kỹ Thuật Đột Phá & Chống Gian Lận Đa Tầng

1. **Chế Độ Thi Tuyến Tính Một Chiều & Khóa Câu Hết Giờ 30s (`US-049`):**
   - Mỗi câu hỏi có đồng hồ đếm lùi riêng **30 giây**. Khi hết giờ, câu hỏi lập tức bị khóa cứng vĩnh viễn (icon 🔒), đáp án bị vô hiệu hóa, không thể xem lại hay làm lại.
   - Khi thí sinh chọn nộp câu để chuyển sang câu kế tiếp, câu cũ được chốt kết quả và khóa lại ngay lập tức; nút **"Câu trước" bị vô hiệu hóa (disabled)** và danh sách câu hỏi chặn hoàn toàn thao tác click quay lại câu cũ.
2. **Bắt Chuyển Tab & Hoán Vị Mã Đề Thay Thế Tương Đương (`US-010` - `US-012`):**
   - Tích hợp sự kiện trình duyệt `Page Visibility API` (`document.visibilitychange` / `window.onblur`).
   - Khi thí sinh rời màn hình làm bài, một **Modal màu đỏ cảnh báo vi phạm** che kín giao diện thi.
   - Kích hoạt hiệu ứng chuyển đổi mã đề: $\text{Mã đề cũ 01} \longrightarrow \text{Mã đề mới 04}$.
   - Khi trở lại làm bài, hệ thống cấp bộ câu hỏi mới cùng cấu trúc ma trận nhưng **bảo lưu toàn bộ thời gian còn lại và các câu đã làm trước đó**, triệt tiêu triệt để lợi ích của hành vi tra cứu bên ngoài.
3. **Cơ Chế Cưỡng Ép Nộp Bài Khi Vi Phạm Vượt Ngưỡng 3/3 Lần (`US-050`):**
   - Hệ thống đếm số lần vi phạm (Strikes). Khi học sinh chuyển tab lần thứ 3:
     - Kích hoạt lệnh **CƯỠNG ÉP THU BÀI** ngay lập tức, đình chỉ phiên làm bài.
     - Đồng hồ dừng lại, bài thi bị khóa vĩnh viễn, tự động tính điểm các câu đã hoàn thành.
     - Bật modal đỏ cảnh báo đình chỉ thi, nhấp nháy badge đỏ trên bảng Live Proctoring của giáo viên và ghi Audit Log của Quản trị viên.
4. **Mô Phỏng Rớt Mạng & Khôi Phục Bài Làm Client State (`US-040`):**
   - Cho phép mô phỏng sự cố mất mạng: Hệ thống hiển thị thanh cảnh báo mất kết nối màu hổ phách.
   - Khi kết nối phục hồi hoặc tải lại trang, hệ thống tự động nhận diện phiên thi đang diễn ra, khôi phục 100% dữ liệu đã chọn từ local storage và đưa học sinh tiếp tục làm bài mà không mất dữ liệu.
5. **Câu Hỏi Toán Biến Đổi Tham Số Ngẫu Nhiên (`US-027`):**
   - Tự động sinh ngẫu nhiên bộ tham số $(X, Y)$ khác nhau cho từng thí sinh trên cùng cấu trúc đề bài, tự tính toán đáp án đúng và đáp án gây nhiễu, ngăn chặn việc đọc chép đáp án giữa các thí sinh.
6. **Ma Trận AI Đối Soát Trùng Lặp Bài Tập Tự Luận (`US-045`):**
   - Công cụ AI phân tích độ tương đồng chữ viết, cấu trúc bài làm và công thức toán học giữa các bài tập nộp gần giờ nhau, tự động gắn cờ cảnh báo nghi vấn trùng lặp (ví dụ: phát hiện 95.4% tương đồng giữa hai học sinh).

---

## 5. Kiến Trúc Bộ Giả Lập Di Động (Container-Scoped Mobile Engine)

Ứng dụng trang bị bộ điều hối giao diện kép hỗ trợ chuyển đổi tức thì giữa **Máy tính (Desktop)** và **Mô phỏng Điện thoại di động (iPhone 16 Pro Chassis)**:
* **Khung viền thiết bị chân thực (`US-024`):** Khung viền Bezel đen bóng bo góc `rounded-[48px]`, Dynamic Island, Status Bar (giờ 09:41, pin đầy, sóng 5G) và Home Indicator đáy.
* **Container-Scoped Layout (`US-038`):** Bố cục thích ứng hoàn toàn theo chiều rộng khung chứa (~390px - 430px), không bị phụ thuộc vào breakpoint của màn hình máy tính ngoài.
* **Thanh điều hướng đáy (Bottom Navigation Bar):** Tự động kích hoạt khi ở chế độ điện thoại với 4-5 tab ứng dụng chạm nhạy.
* **Touch-Friendly Controls:** Đồ thị Parabol co giãn vừa vặn, nút bấm Radio đáp án to bản dễ thao tác, dải câu hỏi vuốt ngang mượt mà.
* **Card-View Transformation:** Toàn bộ bảng dữ liệu quản trị, danh sách học sinh và báo cáo tự động chuyển thành dạng thẻ dọc (Card-view), loại bỏ hoàn toàn lỗi tràn viền ngang.
* **In-Frame Modals Anchor:** Mọi cửa sổ nổi (Modal cảnh báo vi phạm, xác nhận nộp bài, xem video) đều được neo trọn vẹn bên trong màn hình điện thoại mà không tràn ra ngoài.

---

## 6. Kết Quả Kiểm Thử Chấp Nhận Tự Động (E2E Test Suite)

Dự án tích hợp bộ kiểm thử chấp nhận E2E tự động tại [output/test_suite.html](file:///Users/phamkhanh/Documents/Project/Miu/output/test_suite.html) vận hành trên trình duyệt thông qua cơ chế kiểm tra DOM tương tác thực tế với ứng dụng Mockup iFrame:

| Chỉ số nghiệm thu | Kết quả thực tế | Tỷ lệ đạt | Đánh giá |
| :--- | :---: | :---: | :--- |
| **User Stories Kiểm thử** | **52 / 52 User Stories (`US-001` ➔ `US-052`)** | **100%** | Bao phủ trọn vẹn toàn bộ chức năng |
| **Tiêu chí Given-When-Then** | **52 / 52 Test Cases PASSED** | **100%** | Kiểm tra DOM element, state, role switcher thực chất |
| **Lỗi Cú pháp HTML/JS** | **0 Errors / 0 Warnings** | **100%** | Validated qua HTMLParser & Node.js Engine |
| **Tính Nhất Quán Dữ Liệu** | **Đồng bộ 4 Vai trò (HS, GV, PH, Admin)** | **100%** | Dữ liệu học sinh, điểm số, thông báo, vi phạm, Q&A liên kết chặt chẽ |

---

## 7. Cấu Trúc Thư Mục Dự Án

```text
Project/Miu/
├── Init/                               # HỒ SƠ KHỞI TẠO & TÀI LIỆU CĂN CỨ
│   ├── client_request.md               # Yêu cầu cốt lõi ban đầu của khách hàng
│   ├── Flow.md                         # Đặc tả 5 cụm giao diện & 7 giai đoạn vận hành
│   ├── Frame.md                        # Khung quy chuẩn 5 bước chuyển hóa sản phẩm
│   └── BT4-Nhóm7.md                    # Báo cáo nghiệp vụ AZOTA cải tiến (86 bảng biểu)
│
├── specs/                              # BỘ HỒ SƠ THIẾT KẾ & ĐẶC TẢ 5 BƯỚC
│   ├── 01_requirements_ingestion.md    # Bước 1: Trích xuất 53 RAW & 8 kịch bản As-Is/To-Be
│   ├── 02_agile_backlog.md             # Bước 2: Backlog 8 Epics, 33 Feats, 52 Stories & Traceability
│   ├── 03_product_roadmap.md           # Bước 3: Định lượng MoSCoW, 207 SP & Lộ trình 6 Sprints
│   ├── 04_technical_design.md          # Bước 4: Thiết kế kiến trúc SPA, Mobile Engine & Mock APIs
│   └── 05_code_and_tests/              # Bước 5: Mã nguồn SPA & Bộ Test Suite tự động
│       ├── index.html                  # Mã nguồn ứng dụng Mockup SPA hoàn chỉnh
│       ├── test_suite.html             # Bộ Test Runner tự động kiểm tra 52 User Stories
│       ├── README.md                   # Hướng dẫn chi tiết vận hành dự án
│       └── REVIEW_LOG.md               # Nhật ký 9 vòng Code Review & Refactor
│
├── output/                             # GÓI BÀN GIAO CHÍNH THỨC CHO KHÁCH HÀNG
│   ├── index.html                      # Ứng dụng Mockup SPA sẵn sàng triển khai
│   ├── test_suite.html                 # Bộ Test Suite E2E Runner (52/52 Tests Passed)
│   ├── 01_requirements_ingestion.md   # Bản sao đặc tả Bước 1 bàn giao
│   ├── 02_agile_backlog.md             # Bản sao đặc tả Bước 2 bàn giao
│   ├── 03_product_roadmap.md           # Bản sao đặc tả Bước 3 bàn giao
│   ├── 04_technical_design.md          # Bản sao đặc tả Bước 4 bàn giao
│   ├── README.md                       # Tài liệu hướng dẫn khách hàng
│   └── REVIEW_LOG.md                   # Nhật ký nghiệm thu 9 vòng review
│
├── index.html                          # Trang điều hướng gốc chuyển tiếp vào output/index.html
├── README.md                           # Tài liệu tổng quan dự án tại thư mục gốc
└── REVIEW_LOG.md                       # Nhật ký Code Review đầy đủ tại thư mục gốc
```

---

## 8. Hướng Dẫn Vận Hành & Trải Nghiệm Nhanh

1. **Khởi chạy ứng dụng Mockup:**
   - Mở tệp [index.html](file:///Users/phamkhanh/Documents/Project/Miu/index.html) (hoặc trực tiếp [output/index.html](file:///Users/phamkhanh/Documents/Project/Miu/output/index.html)) trên bất kỳ trình duyệt web hiện đại nào (Chrome, Safari, Edge, Firefox).
   - Sử dụng thanh **Demo Control Bar** trên đỉnh màn hình để chuyển đổi nhanh qua lại giữa các kịch bản trình diễn:
     - `1. Vào HS`: Đăng nhập nhanh vào Cổng Học sinh.
     - `2. Vào GV`: Đăng nhập nhanh vào Cổng Giáo viên.
     - `3. Vào PH`: Đăng nhập nhanh vào Cổng Phụ huynh.
     - `4. Vào Admin`: Đăng nhập nhanh vào Cổng Quản trị viên Toàn trường.
     - `Mô phỏng chuyển tab`: Kích hoạt ngay lập tức Modal đỏ cảnh báo và animation hoán đổi mã đề `01 ➔ 04`.
     - `💻 Máy tính` $\leftrightarrow$ `📱 Điện thoại`: Bật/tắt khung mô phỏng iPhone 16 Pro với Dynamic Island.
2. **Khởi chạy bộ kiểm thử tự động:**
   - Mở tệp [output/test_suite.html](file:///Users/phamkhanh/Documents/Project/Miu/output/test_suite.html) trên trình duyệt.
   - Nhấn nút **"Chạy Toàn Bộ Test Suite"** để hệ thống tự động kiểm tra tương tác DOM thực tế trên 52 User Stories. Kết quả đạt chuẩn **52 / 52 PASSED (100%)** với thanh tiến trình xanh hoàn hảo.
