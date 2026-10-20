# BƯỚC 3: ƯU TIÊN BACKLOG & LẬP KẾ HOẠCH SPRINT (PRODUCT ROADMAP)

> **Căn cứ kế thừa:** 
> - [specs/01_requirements_ingestion.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/01_requirements_ingestion.md) (`RAW-001` đến `RAW-053`)
> - [specs/02_agile_backlog.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/02_agile_backlog.md) (52 User Stories & GWT Acceptance Criteria)
> - [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md) & [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md)

---

## 1. Phương pháp luận Ưu tiên & Ước lượng

### 1.1. Phân loại Ưu tiên theo MoSCoW
- **Must-have (M):** Các tính năng cốt lõi bắt buộc phải có để hoàn thành luồng nghiệp vụ 7 giai đoạn của 4 vai trò, cơ chế chống gian lận, pre-check lobby, phục hồi mạng, tuyến tính 30s, cưỡng ép thu bài, tham gia lớp học (Bảng 1.8), thảo luận Q&A (Bảng 1.14) và tối ưu giao diện điện thoại.
- **Should-have (S):** Các tính năng mở rộng nâng cao chất lượng quản trị và sự chân thực của hệ sinh thái AZOTA (báo cáo, audit logs, luyện tập, phúc khảo điểm).
- **Could-have (C):** Các tính năng tiện ích bổ trợ (AZOTA Live, video player, chấm phiếu tô offline).

### 1.2. Ước lượng Nỗ lực Kỹ thuật (Story Points theo Fibonacci)
Dãy số Fibonacci: `1, 2, 3, 5, 8` đánh giá trên độ phức tạp logic UI, hiệu ứng mô phỏng và khối lượng dữ liệu client state.

---

## 2. Bảng Định lượng Ưu tiên & Story Points cho 52 User Stories

| Story ID | Tên User Story | Epic | MoSCoW | Story Points (SP) | Ghi chú & Độ phức tạp |
| :--- | :--- | :--- | :---: | :---: | :--- |
| **US-001** | Form đăng nhập 4 tabs đổi màu nhận diện | EPIC-01 | **Must-have** | **3** | Dynamic CSS theme cho 4 vai trò: HS, GV, PH, Admin. |
| **US-002** | Hiện/Ẩn mật khẩu & Checkbox ghi nhớ | EPIC-01 | **Should-have** | **1** | Toggle input type và lưu cờ localStorage. |
| **US-003** | Điều hướng tức thì & Cách ly RBAC 4 vai trò | EPIC-01 | **Must-have** | **3** | Phân quyền nghiêm ngặt, cách ly header chuyên biệt. |
| **US-042** | Form Đăng ký tài khoản mới kèm Điều khoản | EPIC-01 | **Should-have** | **2** | Tab Đăng ký, validate form, checkbox cam kết điều khoản. |
| **US-004** | Grid đề thi học sinh & input mã/link | EPIC-02 | **Must-have** | **3** | Card layout responsive, badge màu trạng thái AZOTA. |
| **US-005** | Widget sắp đến hạn & Countdown thời gian thực | EPIC-02 | **Must-have** | **3** | Bộ đếm ngược lùi từng giây + thanh progress bar. |
| **US-039** | Phòng chờ Pre-check Lobby & Cam kết quy định | EPIC-02 | **Must-have** | **3** | Kiểm tra thiết bị/mạng xanh, bảng quy định thi + checkbox. |
| **US-006** | Câu hỏi Toán đồ thị parabol SVG & Radio | EPIC-02 | **Must-have** | **5** | Đồ thị vector SVG giải tích chuẩn tọa độ $Oxy$ + 4 nút Radio. |
| **US-007** | Sidebar countdown lớn & Lưới ô vuông câu hỏi | EPIC-02 | **Must-have** | **5** | Đếm lùi giờ thi, đổi đỏ khi < 5p; Lưới 20 câu 4 màu trạng thái. |
| **US-008** | Footer điều hướng & Nút nộp bài | EPIC-02 | **Must-have** | **2** | Chuyển câu next/prev mượt mà, modal xác nhận nộp bài. |
| **US-009** | Chỉ báo Auto-save ngầm kèm Timestamp | EPIC-02 | **Must-have** | **3** | Hiệu ứng chớp sáng (fade flash) + cập nhật mốc giờ chính xác. |
| **US-025** | Phân hệ Tự Luyện tập theo Chủ đề môn học | EPIC-02 | **Should-have** | **3** | Lựa chọn chủ đề, làm bài luyện tập và xem ngay giải thích. |
| **US-026** | Màn hình Xem lại Chi tiết Bài thi & Lời phê | EPIC-02 | **Should-have** | **3** | Xem lại câu đúng/sai, lời giải chi tiết và phản hồi thầy cô. |
| **US-041** | Quy trình Phúc khảo & Chỉnh sửa Điểm số | EPIC-02 | **Should-have** | **5** | HS gửi lý do giải trình; GV duyệt & chỉnh sửa điểm trực tiếp. |
| **US-010** | Modal đỏ cảnh báo khi chuyển tab | EPIC-03 | **Must-have** | **5** | Bắt sự kiện `visibilitychange` / `blur`, khóa màn hình tức thì. |
| **US-011** | Animation cấp đổi mã đề 01 ➔ 04 trên modal | EPIC-03 | **Must-have** | **5** | Hiệu ứng thị giác mũi tên chuyển đổi mã đề, đếm ngược tự đóng. |
| **US-012** | Đổi đề tương đương, bảo lưu giờ và câu đã làm | EPIC-03 | **Must-have** | **8** | Logic hoán đổi câu hỏi mới trong mock store, giữ nguyên timer. |
| **US-040** | Mô phỏng Mất mạng & Khôi phục phiên thi | EPIC-03 | **Must-have** | **3** | Banner cảnh báo mất kết nối & tự khôi phục dữ liệu đệm. |
| **US-027** | Câu hỏi Toán học Biến đổi Tham số Ngẫu nhiên | EPIC-04 | **Must-have** | **5** | Sinh tham số $X, Y$ ngẫu nhiên theo công thức toán học. |
| **US-028** | Đếm ngược Từng câu & Khóa Câu hỏi Đã Hết Giờ | EPIC-04 | **Must-have** | **5** | Countdown riêng từng câu, tự động khóa vĩnh viễn (icon 🔒). |
| **US-013** | Bộ lọc ngân hàng câu hỏi 3 cấp độ kèm tags | EPIC-05 | **Should-have** | **3** | 3 Dropdown lọc đa tiêu chí (Môn, Chủ đề, Độ khó), render tags. |
| **US-014** | Kéo thả ảnh đề thi & Xem thử video học liệu | EPIC-05 | **Could-have** | **3** | Drag & Drop tải file giả lập + Modal xem thử video. |
| **US-015** | Ma trận đề 3 mức độ & Slider tỷ lệ trùng lặp | EPIC-05 | **Must-have** | **5** | Input tính toán phân bổ câu hỏi + Slider kéo thả hiển thị %. |
| **US-016** | Toggles cấu hình chống gian lận | EPIC-05 | **Must-have** | **2** | Toggle switches chuẩn UX Azota (trộn câu, đếm giờ, khóa câu). |
| **US-017** | Bảng Live Proctoring nhấp nháy badge đỏ | EPIC-05 | **Must-have** | **5** | Bảng danh sách thí sinh, hiệu ứng pulse badge đỏ khi vi phạm. |
| **US-018** | Drawer Timeline nhật ký sự kiện chi tiết | EPIC-05 | **Must-have** | **5** | Slide-over panel trượt ra từ bên phải, chuỗi sự kiện từng giây. |
| **US-019** | Biểu đồ cột phổ điểm & Biểu đồ tròn hoàn thành | EPIC-05 | **Should-have** | **3** | Trực quan hóa dữ liệu thống kê bằng biểu đồ SVG/Canvas. |
| **US-029** | Chấm Phiếu tô Trắc nghiệm Offline giả lập | EPIC-05 | **Could-have** | **3** | Xuất phiếu tô PDF và mô phỏng camera quét chấm điểm tự động. |
| **US-030** | Mô phỏng Phòng thi Tương tác AZOTA Live | EPIC-05 | **Could-have** | **3** | Lưới ô camera thí sinh thu nhỏ, điểm danh và giơ tay phát biểu. |
| **US-043** | Tạo & Quản lý Lớp học của Giáo viên | EPIC-05 | **Must-have** | **5** | Tạo lớp, cấu hình khối/môn, quản lý danh sách học sinh, phân nhóm, mã mời. |
| **US-044** | Kho Học liệu, Bài giảng & Đề cương Lớp học | EPIC-05 | **Should-have** | **3** | Danh mục tài liệu theo lớp, tải lên bài giảng PDF/PPTX/Video, xem/tải trực tuyến. |
| **US-046** | Gửi thông báo & nhắc hạn nộp cá nhân hóa (Bảng 1.6) | EPIC-05 | **Must-have** | **3** | Soạn thông báo, chọn nhóm, nhắc tự động trước deadline 2h. |
| **US-047** | Tương tác & diễn đàn thảo luận Q&A lớp học (Bảng 1.7) | EPIC-05 | **Must-have** | **3** | Diễn đàn hỏi đáp, ghim câu trả lời chuẩn của giáo viên. |
| **US-048** | Quản lý học liệu, giám sát lưu trữ & dữ liệu hệ thống (Bảng 1.25) | EPIC-07 | **Must-have** | **5** | Giám sát 412.5 GB / 1 TB, duyệt học liệu, dọn cache rác, backup đám mây. |
| **US-049** | Chế độ thi bảo mật cao: Tuyến tính 1 chiều & Khóa câu hết 30s | EPIC-04 | **Must-have** | **5** | Đếm lùi 30s/câu, khóa câu hết giờ, khóa câu đã làm, chặn quay lại. |
| **US-050** | Cơ chế Cưỡng ép nộp bài khi vi phạm gian lận 3/3 lần | EPIC-03 | **Must-have** | **5** | Phát hiện vi phạm lần 3, đình chỉ thi, tính điểm, đồng bộ proctoring & audit. |
| **US-051** | Tham gia lớp học bằng mã mời & Quản lý lớp học (Bảng 1.8) | EPIC-02 | **Must-have** | **3** | Nhập mã mời, liên kết lớp, quản lý danh sách lớp đang theo học. |
| **US-052** | Kênh tương tác & thảo luận Q&A với giáo viên và bạn học (Bảng 1.14) | EPIC-02 | **Must-have** | **3** | Gửi câu hỏi thắc mắc, xem lời giải chuẩn ghim, trao đổi với bạn cùng lớp. |
| **US-045** | Giao & Nộp Bài tập Tự luận Kèm Ảnh & Đối soát AI | EPIC-02 | **Must-have** | **5** | Học sinh tải ảnh nhiều trang vở bài làm; Ma trận đối soát AI cảnh báo trùng khớp 95.4%. |
| **US-020** | Form liên kết mã học sinh cho phụ huynh | EPIC-06 | **Should-have** | **2** | Input mã học sinh, xác thực giả lập và mở khóa dashboard con. |
| **US-021** | Dashboard phụ huynh: Widgets, Mini-chart & Feed | EPIC-06 | **Should-have** | **5** | Layout Card/Mobile view: 3 widget cảnh báo, mini-chart điểm. |
| **US-022** | Bong bóng Chat nổi trao đổi với giáo viên | EPIC-06 | **Should-have** | **3** | Floating chat bubble cố định góc phải dưới, click mở chat mini. |
| **US-031** | Dashboard Quản trị Tổng thể & KPIs Toàn trường | EPIC-07 | **Must-have** | **5** | Bảng điều khiển quản trị cấp trường: học sinh, GV, phòng thi, server. |
| **US-032** | Quản lý Người dùng & Đội nhóm Phân quyền RBAC | EPIC-07 | **Must-have** | **5** | Bảng danh sách người dùng, gán nhóm quyền, khóa/mở tài khoản. |
| **US-033** | Cấu trúc Nhà trường, Khối lớp & Import Excel | EPIC-07 | **Must-have** | **5** | Danh sách khối lớp 10, 11, 12, phân công GV, modal import Excel. |
| **US-034** | Thiết lập & Tổ chức Kỳ thi Chung Toàn trường | EPIC-07 | **Must-have** | **5** | Tạo kỳ thi tập trung, phân phòng thi ảo, theo dõi thí sinh live. |
| **US-035** | Thống kê & Báo cáo Chuyên sâu Cấp trường | EPIC-07 | **Should-have** | **5** | So sánh phổ điểm các lớp trong khối, xếp hạng môn học. |
| **US-036** | Giám sát An toàn, Audit Logs & Máy chủ | EPIC-07 | **Should-have** | **3** | Bảng nhật ký Audit Logs ghi vết đăng nhập/đổi đề/sửa điểm. |
| **US-037** | Thông báo Toàn trường & Tiếp nhận Ticket Hỗ trợ | EPIC-07 | **Should-have** | **3** | Form gửi thông báo diện rộng và quản lý danh sách ticket sự cố. |
| **US-023** | Chuẩn hóa Design System AZOTA & Mock Store | EPIC-08 | **Must-have** | **5** | Bộ Token màu sắc, Component thư viện dùng chung, Mock Store. |
| **US-024** | Mô phỏng Khung Điện thoại (Mobile Frame) | EPIC-08 | **Should-have** | **5** | Khung viền iPhone 16 Pro mockup chassis, Dynamic Island, status bar. |
| **US-038** | Tinh chỉnh Bố cục & Trải nghiệm Chế độ Điện thoại | EPIC-08 | **Must-have** | **8** | Container-scoped layout, Bottom Navigation Bar, touch radio, auto-scale graph, card-view tables, in-frame modals. |

---

## 3. Tổng hợp Nỗ lực & Phân tích Vận tốc (Team Velocity)

- **Tổng số User Stories:** 52 User Stories
- **Tổng Story Points (SP):** **207 SP**
  - **Must-have:** 34 stories = **149 SP** *(Chiếm ~72% khối lượng)*
  - **Should-have:** 15 stories = **49 SP** *(Chiếm ~24% khối lượng)*
  - **Could-have:** 3 stories = **9 SP** *(Chiếm ~4% khối lượng)*
- **Ước tính Vận tốc nhóm (Velocity):** **35 – 37 SP / Sprint**
- **Kế hoạch phát hành:** Chia làm **6 Sprints phát triển** liên tục (5 Sprints nền tảng + Sprint 6 hoàn thiện nghiệp vụ chuyên sâu theo REV-SPRINT-06 & REV-SPRINT-09).

---

## 4. Kế hoạch Phát hành 6 Sprints (Release Roadmap)

```text
                                LỘ TRÌNH PHÁT HÀNH 6 SPRINTS
┌───────────────────────────────────────────────────────────────────────────────────┐
│ SPRINT 1: Nền tảng AZOTA, Đăng ký/Đăng nhập 4 Vai trò, Pre-check Lobby & Thi (35) │
│ [US-023] ➔ [US-001] ➔ [US-002] ➔ [US-003] ➔ [US-042] ➔ [US-004] ➔ [US-005]       │
│ ➔ [US-039] ➔ [US-006] ➔ [US-007] ➔ [US-008] ➔ [US-009]                            │
├───────────────────────────────────────────────────────────────────────────────────┤
│ SPRINT 2: Chống Gian lận Chuyển tab, Đổi mã đề, Phục hồi Mạng & Quản lý Lớp (39) │
│ [US-010] ➔ [US-011] ➔ [US-012] ➔ [US-040] ➔ [US-013] ➔ [US-015] ➔ [US-016]       │
│ ➔ [US-017] ➔ [US-018] ➔ [US-043]                                                  │
├───────────────────────────────────────────────────────────────────────────────────┤
│ SPRINT 3: Cổng Phụ huynh, Luyện tập, Phúc khảo, Học liệu & Bài tập AI (42 SP)     │
│ [US-014] ➔ [US-019] ➔ [US-020] ➔ [US-021] ➔ [US-022] ➔ [US-024] ➔ [US-025]       │
│ ➔ [US-026] ➔ [US-041] ➔ [US-044] ➔ [US-045]                                      │
├───────────────────────────────────────────────────────────────────────────────────┤
│ SPRINT 4: Cổng Quản trị viên Toàn trường, Kỳ thi Chung & Audit Logs (31 SP)       │
│ [US-031] ➔ [US-032] ➔ [US-033] ➔ [US-034] ➔ [US-035] ➔ [US-036] ➔ [US-037]       │
├───────────────────────────────────────────────────────────────────────────────────┤
│ SPRINT 5: Thi Thông minh, Tinh chỉnh Mobile & Transitions/Polishing (34 SP)       │
│ [US-027] ➔ [US-028] ➔ [US-029] ➔ [US-030] ➔ [US-038] + Smooth UI Transitions/E2E │
├───────────────────────────────────────────────────────────────────────────────────┤
│ SPRINT 6: Nghiệp Vụ Chuyên Sâu, Lớp Học, Học Liệu & Chống Gian Lận Đột Phá (26 SP)│
│ [US-046] ➔ [US-047] ➔ [US-048] ➔ [US-049] ➔ [US-050] ➔ [US-051] ➔ [US-052]        │
└───────────────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Kết luận Bước 3 & Sẵn sàng cho Bước 4
Kế hoạch phát hành 6 Sprints (207 SP) đã bao phủ khép kín 100% các giai đoạn từ [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md) và toàn bộ 86 Bảng biểu chức năng theo [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md). Hệ thống sẵn sàng bước sang **Bước 4: Cập nhật Thiết kế Kỹ thuật**.
