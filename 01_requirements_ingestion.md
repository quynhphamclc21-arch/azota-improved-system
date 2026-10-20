# BƯỚC 1: TRÍCH XUẤT & CHUẨN HÓA YÊU CẦU (REQUIREMENTS INGESTION)

> **Tài liệu nguồn căn cứ:**
> - [Init/client_request.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/client_request.md) *(Yêu cầu mockup trực quan ban đầu)*
> - [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md) *(Báo cáo nghiệp vụ AZOTA cải tiến - Toàn bộ Chương 1 đến Chương 3)*
> - [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md) *(Đặc tả giao diện chi tiết & Luồng hoạt động 7 giai đoạn hệ thống)*
> - [Init/Frame.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Frame.md) *(Khung quy trình 5 bước và quy tắc vận hành)*

---

## 1. Tổng quan & Phạm vi dự án (Project Scope)

- **Mục tiêu:** Xây dựng sản phẩm **Mockup / Interactive UI Prototype** mô phỏng hoàn chỉnh hệ sinh thái **AZOTA cải tiến**, bao gồm 4 phân hệ vai trò chuẩn mực: **Học sinh**, **Giáo viên**, **Phụ huynh**, và **Quản trị viên (Admin)**, tích hợp giải pháp thi trực tuyến thông minh, phòng chống gian lận đa lớp, quy trình 7 giai đoạn khép kín và bộ mô phỏng giao diện điện thoại di động (Mobile App Simulator).
- **Định hướng kỹ thuật:**
  - Tập trung 100% vào **Giao diện người dùng (Frontend / UI Simulation)** và trải nghiệm tương tác (UX).
  - **Không yêu cầu triển khai backend/database thực tế**; toàn bộ dữ liệu vận hành qua Mock Data Store và Client State (Local State / Storage).
  - Tuân thủ chặt chẽ **Design System của AZOTA** (tông xanh thương hiệu `#1890ff` / `bg-blue-600`, Ant Design + Tailwind CSS, thẻ Card bo tròn `8px`, badge trạng thái màu xanh/cam/đỏ/xám).
  - **Tối ưu hóa kép (Dual Viewport Architecture):** Hỗ trợ chuyển đổi mượt mà giữa chế độ **Máy tính (Desktop View)** và **Mô phỏng Điện thoại di động (Mobile App Simulator)** với bố cục co giãn thích ứng hoàn hảo với khung viền điện thoại.

---

## 2. Client's Wish List (Danh sách yêu cầu thô - RAW Requirements)

Toàn bộ các nhu cầu nguyên văn từ `client_request.md`, `BT4-Nhóm7.md` và `Flow.md` được phân rã thành **53 yêu cầu định danh duy nhất (`RAW-001` đến `RAW-053`)**:

| RAW ID | Phân hệ / Màn hình | Nội dung yêu cầu thô từ khách hàng |
| :--- | :--- | :--- |
| **RAW-001** | Đăng nhập & Phân quyền | Form đăng nhập ở trung tâm màn hình, tối giản, có các Tabs chuyển đổi vai trò: `[Học sinh]` - `[Giáo viên]` - `[Phụ huynh]` - `[Quản trị viên]`. Khi chọn tab nào, màu sắc chủ đạo của form thay đổi để nhận diện vai trò. |
| **RAW-002** | Đăng nhập & Phân quyền | Ô nhập Tên đăng nhập và Mật khẩu. Trong ô Mật khẩu có icon Con mắt (Hiện/Ẩn). Có Checkbox "Ghi nhớ đăng nhập" bên dưới. |
| **RAW-003** | Đăng nhập & Phân quyền | Khi nhấn "Đăng nhập", hệ thống tự động điều hướng ngay sang Trang chủ / Dashboard tương ứng với vai trò đã chọn trên tab mà không lộ menu vai trò khác. |
| **RAW-004** | Trang chủ Học sinh | Danh sách đề thi hiển thị dạng lưới (Grid Card). Mỗi thẻ ghi rõ: Môn học, Thời hạn nộp, Huy hiệu trạng thái (Xanh: Đã nộp, Vàng: Đang mở, Đỏ: Quá hạn). Phía trên có ô Input: "Nhập mã bài thi hoặc dán liên kết". |
| **RAW-005** | Trang chủ Học sinh | Widget cảnh báo đỏ/cam nổi bật bên cạnh danh sách: "Sắp đến hạn!" kèm tên bài thi và đồng hồ đếm ngược thời gian thực, kèm thanh tiến trình (Progress bar) thể hiện thời gian đã trôi qua. |
| **RAW-006** | Màn hình Làm bài thi | Khu vực trung tâm: Hiển thị câu hỏi Toán có đồ thị parabol giải tích sắc nét ở giữa câu hỏi, bên dưới là 4 đáp án dạng nút bấm Radio (A, B, C, D) rõ ràng, trực quan. |
| **RAW-007** | Màn hình Làm bài thi | Sidebar bên phải: Đồng hồ đếm ngược cực lớn ở trên cùng (chuyển đỏ khi sắp hết giờ); bên dưới là Danh sách câu hỏi dạng lưới ô vuông (Grid) đổi màu theo trạng thái: Đã trả lời (Xanh), Chưa trả lời (Trắng), Đang chọn (Viền đậm). |
| **RAW-008** | Màn hình Làm bài thi | Footer thanh điều hướng: Gồm các nút "Câu trước", "Câu sau", "Lưu lựa chọn" và nút "Nộp bài" màu sắc nổi bật. |
| **RAW-009** | Màn hình Làm bài thi | Chỉ báo tự động lưu (Auto-save Indicator): Đặt ở Header/cạnh nút Lưu, hiển thị text nhỏ màu xanh kèm icon tick: *"✓ Đã lưu câu trả lời lúc [HH:mm:ss]"*, chớp sáng nhẹ khi chọn đáp án mới để mô phỏng lưu ngầm. |
| **RAW-010** | Mô phỏng Chống gian lận | Khi học sinh rời màn hình/chuyển tab, lập tức xuất hiện một Pop-up Modal màu đỏ cảnh báo che khuất toàn bộ bài thi. |
| **RAW-011** | Mô phỏng Chống gian lận | Trên Pop-up cảnh báo hiển thị hiệu ứng mũi tên chuyển đổi mã đề: *"Đang cấp mã đề thay thế: Đề cũ 01 ➔ Đề mới 04"*. |
| **RAW-012** | Mô phỏng Chống gian lận | Khi Modal biến mất, học sinh quay lại làm bài với mã đề mới, câu hỏi mới nhưng Đồng hồ đếm ngược vẫn giữ nguyên thời gian còn lại và các câu đã làm trước đó vẫn được bảo lưu kết quả. |
| **RAW-013** | Quản lý Đề (Giáo viên) | Thanh công cụ Lọc (Filter Bar) gồm các Dropdown lọc nhanh câu hỏi theo "Môn học", "Chủ đề" và "Mức độ khó" (Nhận biết, Thông hiểu, Vận dụng). Danh sách hiển thị dạng bảng có gắn tag màu theo độ khó. |
| **RAW-014** | Tạo bài thi (Giáo viên) | Khu vực tải học liệu: Xem trước ảnh tải lên dạng Kéo thả (Drag & Drop) để đính kèm ảnh đề thi; khu vực video theo môn học có nút Phát (Play) để xem thử trực tiếp. |
| **RAW-015** | Tạo bài thi (Giáo viên) | Bảng thiết lập Ma trận đề: Ô input nhập phân bổ số câu hỏi theo từng mức độ (VD: 7 Nhận biết, 7 Thông hiểu, 6 Vận dụng). |
| **RAW-016** | Tạo bài thi (Giáo viên) | Thanh trượt (Slider) thiết lập Tỷ lệ trùng lặp câu hỏi tối đa giữa các phiên bản đề của học sinh (VD: kéo chọn mốc 30%). |
| **RAW-017** | Cấu hình Thi (Giáo viên) | Khu vực công tắc gạt (Toggles) bật/tắt các tính năng chống gian lận: "Trộn câu hỏi", "Trộn đáp án", "Cảnh báo chuyển tab". |
| **RAW-018** | Giám sát Live (Giáo viên) | Bảng trạng thái thí sinh trong phòng thi trực tuyến. Nếu học sinh vi phạm chuyển tab, lập tức hiển thị huy hiệu (Badge) cảnh báo màu đỏ nhấp nháy. |
| **RAW-019** | Giám sát Live (Giáo viên) | Khi nhấn vào một học sinh, một bảng panel trượt ra (Slide-over Timeline) hiển thị Nhật ký sự kiện dạng dòng thời gian: ghi rõ mốc thời gian rời trang, mốc thời gian bị đổi mã đề. |
| **RAW-020** | Báo cáo (Giáo viên) | Trực quan hóa dữ liệu bằng Biểu đồ điểm trung bình (dạng cột) và Tỷ lệ hoàn thành bài thi (dạng tròn/Pie chart) để bao quát chất lượng lớp. |
| **RAW-021** | Cổng Phụ huynh | Giao diện tối ưu dạng Card-view/Mobile-view: Form nhập mã định danh học sinh để liên kết hồ sơ con em. |
| **RAW-022** | Cổng Phụ huynh | Dashboard theo dõi: Thẻ Widget lớn ("Tiến độ học tập", "Bài chưa nộp - đỏ", "Bài sắp đến hạn - cam"); khu vực điểm số có Mini-chart theo dõi tiến bộ; Notification Feed hiển thị nhận xét của giáo viên. |
| **RAW-023** | Cổng Phụ huynh | Bong bóng Chat (Chat Bubble) nổi ở góc phải dưới màn hình để mở khung trao đổi trực tiếp với giáo viên. |
| **RAW-024** | Bối cảnh & Design System | Tuân thủ phong cách giao diện và ngôn ngữ thiết kế của AZOTA (màu xanh thương hiệu `bg-blue-600`, Ant Design/Tailwind CSS, component card, badge trạng thái 5 màu). |
| **RAW-025** | Phạm vi Kỹ thuật | Mockup thuần Frontend (UI/UX Prototype), dữ liệu mô phỏng bằng Mock Data / State, không cần backend logic. |
| **RAW-026** | Đa nền tảng (Mobile Frame) | Khung mô phỏng điện thoại di động (iPhone chassis) với Dynamic Island, Status Bar (giờ 09:41, sóng, pin) và Home bar để kiểm chứng khả năng responsive. |
| **RAW-027** | Cổng Quản trị viên (Admin) | Dashboard Quản trị cấp trường: Hiển thị chỉ số KPIs toàn trường (Tổng số học sinh, giáo viên, lớp học, kỳ thi đang chạy, tài nguyên máy chủ CPU/RAM), thanh điều hướng chuyên biệt của Quản trị viên. |
| **RAW-028** | Quản lý Đội nhóm & RBAC (Admin) | Danh sách người dùng toàn hệ thống; phân quyền theo nhóm (Ban Giám Hiệu, Tổ trưởng chuyên môn, Giáo viên, Học sinh, Phụ huynh); thao tác cấp tài khoản, kích hoạt, khóa/mở khóa tài khoản. |
| **RAW-029** | Cấu trúc Nhà trường & Học sinh (Admin) | Quản lý khối lớp (Khối 10, 11, 12), danh sách lớp học, phân công giáo viên chủ nhiệm & bộ môn; hỗ trợ xem trước danh sách học sinh nhập từ file Excel mẫu. |
| **RAW-030** | Tổ chức Kỳ thi Chung (Admin) | Thiết lập và quản lý các kỳ thi chung toàn trường/toàn khối (Khảo sát chất lượng, Giữa kỳ, Cuối kỳ); phân bổ danh sách học sinh vào các phòng thi ảo tập trung và theo dõi tiến độ thi chung. |
| **RAW-031** | Thống kê Báo cáo Cấp trường (Admin) | Báo cáo chuyên sâu cấp trường: Biểu đồ so sánh phổ điểm giữa các lớp trong khối, xếp hạng chất lượng dạy học theo môn và tỷ lệ hoàn thành kỳ thi chung. |
| **RAW-032** | An toàn, Audit Logs & Giám sát Hệ thống (Admin) | Bảng theo dõi an toàn và nhật ký hệ thống: Ghi vết toàn bộ hành vi quản trị (Audit Logs: đăng nhập, đổi đề, sửa điểm), theo dõi lưu lượng truy cập đồng thời và cảnh báo xâm nhập/bất thường. |
| **RAW-033** | Thông báo & Hỗ trợ Người dùng (Admin) | Quản lý trung tâm gửi thông báo khẩn cấp đến toàn thể giáo viên, học sinh, phụ huynh; danh sách tiếp nhận và xử lý yêu cầu hỗ trợ kỹ thuật (Tickets). |
| **RAW-034** | Thi Thông minh: Câu hỏi Biến đổi Tham số | Module sinh câu hỏi toán học biến đổi tham số ngẫu nhiên: Cùng cấu trúc đề bài nhưng tự sinh bộ tham số $(X, Y)$ khác nhau cho từng thí sinh, tự tính đáp án đúng và đáp án nhiễu theo công thức, triệt tiêu sao chép đáp án. |
| **RAW-035** | Thi Thông minh: Countdown Từng câu & Khóa câu | Chế độ làm bài giới hạn thời gian theo từng câu hỏi: Đồng hồ đếm lùi riêng cho từng câu; khi hết thời gian câu đó, hệ thống tự lưu đáp án, chuyển câu tiếp theo và **KHÓA VĨNH VIỄN** câu cũ (icon ổ khóa 🔒, chặn sửa); hỗ trợ hệ số nới thời gian (VD: $\times 1.25$). |
| **RAW-036** | Giáo viên: Chấm Phiếu tô Trắc nghiệm Offline | Công cụ thi Offline: Xem trước và xuất mẫu phiếu trả lời trắc nghiệm (phiếu tô 20 câu / 50 câu) chuẩn dạng PDF; màn hình mô phỏng camera quét chấm phiếu tô tự động bằng nhận diện quang học. |
| **RAW-037** | Giáo viên: AZOTA Live Phòng thi Trực tiếp | Mô phỏng công cụ AZOTA Live: Phòng thi / kiểm tra trực tuyến có camera giám sát trực tiếp, tính năng giơ tay phát biểu và điểm danh thí sinh theo thời gian thực. |
| **RAW-038** | Học sinh: Phân hệ Tự Luyện tập | Module Luyện tập dành cho học sinh: Chọn chủ đề môn học (Hàm số, Hình học, Tổ hợp xác suất), làm đề luyện tập không giới hạn và xem ngay giải thích chi tiết từng câu sau khi hoàn thành. |
| **RAW-039** | Học sinh: Xem lại Chi tiết Bài thi & Lời phê | Giao diện xem lại bài thi đã nộp: Bảng tổng kết điểm, danh sách câu hỏi kèm đáp án đúng/sai của thí sinh, lời giải chi tiết giải tích và nhận xét đánh giá của giáo viên. |
| **RAW-040** | Tối ưu Giao diện Chế độ Điện thoại (Mobile Refinement) | **Tối ưu hóa toàn diện giao diện khi ở chế độ Điện thoại (Mobile App Simulator UX/UI):**<br>• Bố cục tự động điều chỉnh theo kích thước màn hình smartphone (~390px - 430px) bằng container-scoped CSS, không bị phụ thuộc vào breakpoint của máy tính.<br>• Header chuyển sang dạng **Mobile App Header** gọn gàng kết hợp thanh điều hướng đáy (**Bottom Navigation Bar** 4-5 tabs ứng dụng).<br>• Không gian phòng thi: Đồ thị Parabol co giãn chuẩn mobile, nút chọn đáp án Radio to bản chuẩn cảm ứng (touch-friendly), danh sách câu hỏi chuyển thành dải vuốt ngang (Horizontal Pill Strip) hoặc Bottom Sheet.<br>• Các bảng biểu dữ liệu (Tables) ở trang Quản trị, Giáo viên, Báo cáo tự động chuyển thành thẻ Card dọc (Card-view) trên điện thoại, không bị tràn viền (no horizontal overflow).<br>• Các Modal cảnh báo đỏ, chuyển mã đề, xác nhận nộp bài được neo trọn vẹn bên trong màn hình điện thoại mà không tràn ra ngoài khung viền máy tính. |
| **RAW-041** | Phòng chờ Trước giờ thi (Pre-check Lobby) | Màn hình sảnh chờ trước khi bắt đầu bài thi: Hiển thị trạng thái kiểm tra thiết bị & kết nối mạng ổn định; bảng quy định phòng thi (chuyển tab, đếm ngược từng câu, khóa câu hết giờ) kèm ô xác nhận "Tôi đã đọc và đồng ý quy định phòng thi" trước khi hệ thống cấp mã đề chính thức. |
| **RAW-042** | Mô phỏng Mất mạng & Khôi phục Phiên thi | Chức năng mô phỏng tình huống mất kết nối mạng hoặc tải lại trang: Hệ thống hiển thị thanh cảnh báo mất kết nối, sau đó thông báo tự động khôi phục dữ liệu đã lưu từ local state để thí sinh tiếp tục làm bài (nếu còn thời gian) hoặc tự động nộp bài (nếu đã hết giờ). |
| **RAW-043** | Quy trình Phúc khảo & Chỉnh sửa Điểm số | Quy trình giải trình vi phạm và phúc khảo khép kín: Học sinh có nút "Phúc khảo / Giải trình vi phạm" tại màn hình kết quả để gửi phản hồi; Giáo viên mở bảng Chi tiết vi phạm xem lý do giải trình và thao tác chọn "Giữ nguyên điểm" hoặc "Chỉnh sửa điểm" (+0.5đ, +1.0đ) để cập nhật chốt điểm cuối cùng. |
| **RAW-044** | Biểu mẫu Đăng ký & Điều khoản Chính sách | Tab Đăng ký tài khoản mới trên Form xác thực trung tâm: Cung cấp các trường nhập thông tin theo vai trò kèm checkbox bắt buộc "Tôi đồng ý với các điều khoản sử dụng và chính sách bảo mật của AZOTA" với thông báo kiểm tra tính hợp lệ. |
| **RAW-045** | Quản lý Lớp học của Giáo viên | Công cụ hỗ trợ giáo viên tạo và quản lý lớp học (Bảng 1.1, 1.31, 1.75 BT4-Nhóm 7): Tạo lớp học mới, cấu hình khối/môn học, quản lý danh sách học sinh thuộc lớp, phân nhóm học tập (nâng cao, phụ đạo), cấp mã mời tham gia lớp học và xuất danh sách lớp ra Excel/PDF. |
| **RAW-046** | Kho Học liệu, Bài giảng & Đề cương Lớp học | Quản lý và chia sẻ học liệu số giữa giáo viên và học sinh (Bảng 1.2, 1.10, 1.47, 1.54 BT4-Nhóm 7): Giáo viên tải lên bài giảng PDF, Word, Slide PowerPoint, Video bổ trợ; gắn chuyên đề/chương; cấp quyền tải về hoặc xem trực tuyến; học sinh tra cứu, xem và tải tài liệu ôn tập theo phân loại môn học. |
| **RAW-047** | Giao & Nộp Bài tập Tự luận Kèm Ảnh Chụp Vở & Đối soát Trùng lặp AI | Phân hệ giao và nộp bài tập về nhà tự luận (Bảng 1.71, 1.11, 1.48, 1.55 BT4-Nhóm 7): Giáo viên giao bài tập tự luận có hạn nộp; Học sinh chụp ảnh các trang vở bài làm hoặc gửi PDF đính kèm ghi chú; Công cụ AI Similarity Matrix tự động phân tích đối soát tương đồng ngữ nghĩa và công thức toán học giữa các bài làm nộp gần giờ nhau (cảnh báo trùng lặp 95.4%). |
| **RAW-048** | Gửi thông báo & nhắc hạn nộp cá nhân hóa | Giáo viên soạn thông báo về bài tập, bài thi, nhắc hạn nộp cá nhân hóa theo lớp hoặc từng nhóm học sinh (Bảng 1.6 BT4-Nhóm 7). |
| **RAW-049** | Tương tác & thảo luận Q&A lớp học | Kênh tương tác, giải đáp thắc mắc, hướng dẫn bài học, ghim lời giải chuẩn và thảo luận chuyên đề theo lớp/nhóm (Bảng 1.7 BT4-Nhóm 7). |
| **RAW-050** | Quản lý học liệu & dữ liệu hệ thống | Quản trị viên theo dõi dung lượng lưu trữ đám mây, kiểm tra tình trạng tệp, quản lý học liệu, bài tập, đề thi và bảo trì dữ liệu (Bảng 1.25 BT4-Nhóm 7). |
| **RAW-051** | Chế độ thi bảo mật cao & Cưỡng ép nộp bài | Khóa câu hỏi khi hết thời gian 30s (không được làm lại/xem lại), thi tuyến tính một chiều (khóa câu đã làm xong, chặn quay lại câu trước), và cưỡng ép nộp bài tức thì khi vi phạm chuyển tab vượt quá giới hạn 3/3 lần. |
| **RAW-052** | Học sinh: Tham gia lớp học bằng mã mời | Học sinh sử dụng mã lớp học hoặc liên kết mời do giáo viên cung cấp để tham gia lớp học mới, xác nhận tham gia và nhận quyền truy cập vào nội dung học tập, bài tập, kiểm tra, thông báo của lớp; xem danh sách lớp đang theo học (Bảng 1.8 BT4-Nhóm 7). |
| **RAW-053** | Học sinh: Thảo luận với giáo viên và bạn học | Kênh học sinh đặt câu hỏi thắc mắc bài học/bài tập, gửi ý kiến trao đổi với các bạn cùng lớp, xem lời giải chuẩn mực được giáo viên ghim và nhận giải đáp từ giáo viên (Bảng 1.14 tương ứng hai chiều với Bảng 1.7 BT4-Nhóm 7). |

---

## 3. Phân tích Kịch bản Hiện trạng (As-Is) & Viễn cảnh Mới (To-Be)

### 3.1. Kịch bản 1: Đăng ký, Đăng nhập & Xác định Không gian Làm việc theo 4 Vai trò
- **Hiện trạng (As-Is):** Người dùng nhầm lẫn giữa các đường dẫn; không có luồng đăng ký rõ ràng; dễ bị lẫn quyền giữa phụ huynh, học sinh và giáo viên; thiếu hoàn toàn cổng quản trị nhà trường.
- **Viễn cảnh mới (To-Be):**
  - Màn hình đăng nhập/đăng ký trung tâm với 4 Toggle Tabs: `[Học sinh]` - `[Giáo viên]` - `[Phụ huynh]` - `[Quản trị viên]`.
  - Có tab Đăng ký với checkbox cam kết điều khoản & chính sách.
  - Khi chọn tab, form chuyển màu nhận diện: Xanh dương (Học sinh) $\rightarrow$ Tím (Giáo viên) $\rightarrow$ Xanh ngọc (Phụ huynh) $\rightarrow$ Xanh đen/Chàm (Quản trị viên).
  - Đăng nhập xong lập tức chuyển vào Dashboard chuyên biệt, thanh điều hướng Header cách ly 100% chức năng theo vai trò (RBAC nghiêm ngặt).

### 3.2. Kịch bản 2: Phòng chờ Pre-check Lobby & Trải nghiệm Phòng thi Chuẩn mực
- **Hiện trạng (As-Is):** Học sinh vào thi đột ngột, chưa kịp chuẩn bị tâm lý, không rõ quy định thi, lo lắng mất bài khi mạng chập chờn.
- **Viễn cảnh mới (To-Be):**
  - Học sinh qua **Phòng chờ Pre-check Lobby**: Kiểm tra mạng/thiết bị xanh ổn định, đọc kỹ quy định thi và tích chọn cam kết mới được mở đề.
  - Không gian thi chuyên nghiệp: Đồ thị parabol toán học SVG chuẩn tọa độ $Oxy$ sắc nét, 4 nút Radio to rõ ràng.
  - Sidebar có đồng hồ đếm lùi cỡ lớn và lưới 20 ô vuông tự đổi màu trạng thái (Trắng: chưa làm, Xanh lá: đã làm, Xanh dương: đang chọn, Xám kèm ổ khóa 🔒: đã khóa).
  - Cơ chế **Auto-save ngầm** chớp sáng xanh kèm mốc giờ chính xác `[HH:mm:ss]` mỗi lần chọn đáp án.

### 3.3. Kịch bản 3: Xử lý Hành vi Chuyển Tab & Cơ chế Đổi đề Tương đương (Anti-Cheat)
- **Hiện trạng (As-Is):** Hệ thống chỉ ghi nhận số lần chuyển tab hoặc trừ điểm thụ động, học sinh vẫn có thể tra cứu đáp án rồi quay lại điền vào bài.
- **Viễn cảnh mới (To-Be):**
  - Ngay khi học sinh rời tab, màn hình bị khóa bằng **Modal cảnh báo màu đỏ**.
  - Hệ thống kích hoạt quy trình **Cấp mã đề thay thế**: Animation chuyển đổi `Đề cũ 01 ➔ Đề mới 04`.
  - Học sinh trở lại làm bài với bộ câu hỏi mới cùng độ khó ma trận, thời gian còn lại giữ nguyên và các câu đã làm trước đó được bảo lưu. Lợi ích gian lận bị triệt tiêu hoàn toàn.

### 3.4. Kịch bản 4: Xử lý Mất mạng & Khôi phục Bài làm
- **Hiện trạng (As-Is):** Mất mạng làm học sinh hoảng loạn, bài thi bị reset về trắng hoặc mất trắng kết quả đã làm trước đó.
- **Viễn cảnh mới (To-Be):**
  - Hệ thống hiển thị thanh cảnh báo mất kết nối màu cam/đỏ.
  - Khi mạng phục hồi hoặc thí sinh tải lại trang, hệ thống tự động nhận diện phiên thi đang diễn ra, hiển thị thông báo khôi phục thành công từ bộ nhớ đệm client và đưa thí sinh làm tiếp đúng câu hỏi và số giờ còn lại.

### 3.5. Kịch bản 5: Giáo viên Giám sát Live & Xử lý Phúc khảo / Điều chỉnh Điểm
- **Hiện trạng (As-Is):** Giáo viên chỉ xem điểm cuối cùng, khi học sinh khiếu nại không có căn cứ đối soát minh bạch; học sinh bị oan khi chuyển tab nhầm không có kênh giải trình.
- **Viễn cảnh mới (To-Be):**
  - Màn hình Live Proctoring hiển thị danh sách thí sinh thời gian thực; học sinh chuyển tab lập tức nhấp nháy Badge đỏ cảnh báo.
  - Học sinh gửi yêu cầu **Phúc khảo / Giải trình vi phạm** trực tiếp tại màn hình kết quả.
  - Giáo viên mở bảng Chi tiết vi phạm, đối soát mốc thời gian trong Timeline, xem lý do giải trình và nhấn nút "Giữ nguyên điểm" hoặc "Chỉnh sửa điểm" (+0.5đ, +1.0đ) để chốt điểm chính xác, công bằng.

### 3.6. Kịch bản 6: Quản trị viên Điều hành Toàn trường & Tổ chức Kỳ thi Tập trung
- **Hiện trạng (As-Is):** Nhà trường phải quản lý giáo viên, học sinh và các đợt thi giữa kỳ/cuối kỳ phân tán qua file rời rạc, không có hệ thống tập trung phân quyền và thống kê toàn diện.
- **Viễn cảnh mới (To-Be):**
  - Cổng Quản trị viên điều hành toàn bộ cấu trúc trường: quản lý danh sách khối lớp (10, 11, 12), phân công giáo viên giảng dạy, nhập danh sách học sinh từ file Excel chỉ bằng 1 thao tác.
  - Thiết lập kỳ thi chung cấp trường/khối: tạo đợt thi tập trung, phân phòng thi ảo cho toàn bộ học sinh, theo dõi số lượng thí sinh đang làm bài và giám sát an toàn toàn diện qua Audit Logs.

### 3.7. Kịch bản 7: Thi Thông minh với Đếm ngược từng câu, Khóa câu và Biến đổi Tham số
- **Hiện trạng (As-Is):** Học sinh dồn thời gian của cả bài để tra cứu một vài câu khó hoặc sao chép đáp án từ bạn cùng thi khi đề thi trùng câu số liệu.
- **Viễn cảnh mới (To-Be):**
  - **Câu hỏi biến đổi tham số:** Cùng một mẫu bài toán nhưng mỗi học sinh nhận được các tham số $X, Y$ khác nhau (tự sinh đáp án đúng và đáp án nhiễu tương ứng). Dù học sinh có hỏi bạn cũng không thể chép kết quả trực tiếp.
  - **Countdown & Khóa câu:** Mỗi câu hỏi có đồng hồ đếm ngược riêng (ví dụ 45s, 60s, 90s). Khi hết giờ câu nào, hệ thống tự lưu câu đó và **khóa vĩnh viễn (icon 🔒)**, chuyển sang câu tiếp theo và không cho quay lại câu cũ.

### 3.8. Kịch bản 8: Trải nghiệm Làm bài & Giám sát trên Khung Điện thoại Mô phỏng Hoàn chỉnh
- **Hiện trạng (As-Is):** Khi thu nhỏ hoặc mô phỏng trên điện thoại, giao diện web thường bị vỡ bố cục do vẫn ăn theo breakpoint của màn hình máy tính (`md:`, `lg:`), bảng biểu bị tràn mép, nút bấm quá nhỏ khó chạm, modal cảnh báo tràn ra ngoài khung viền.
- **Viễn cảnh mới (To-Be):**
  - Khi bật chế độ Điện thoại, toàn bộ giao diện tự động ép theo layout mobile chuyên dụng (container-scoped): Header chuyển thành Mobile App Bar với Status Bar (giờ 09:41, pin, 5G), thanh điều hướng đáy (Bottom Navigation Bar) chuẩn iOS/Android.
  - Phòng thi trên điện thoại: Đồ thị parabol co giãn vừa khít chiều ngang màn hình, nút Radio to bản dễ bấm bằng ngón tay cái, dải câu hỏi vuốt ngang tiện lợi.
  - Tất cả bảng biểu Quản trị/Giáo viên tự động chuyển thành Card dọc gọn gàng, và Modal cảnh báo vi phạm khóa trọn vẹn bên trong màn hình điện thoại, mang lại cảm giác chân thực như đang trải nghiệm app AZOTA Mobile thật.

---

## 4. Yêu cầu Phi chức năng (Non-Functional Requirements - NFRs)

| NFR ID | Phân nhóm tiêu chuẩn | Chi tiết yêu cầu kỹ thuật cho bản Mockup |
| :--- | :--- | :--- |
| **NFR-01** | **UI/UX Consistency** | Tuân thủ nghiêm ngặt Design System của AZOTA: Tông xanh thương hiệu (`bg-blue-600`), nền xám nhạt (`bg-gray-50`), thẻ Card trắng, viền bo góc nhẹ (`border-radius: 8px`), badge trạng thái 5 màu chuẩn mực. |
| **NFR-02** | **Client-side Interactivity** | Mọi tương tác chuyển tab, mở modal cảnh báo đỏ, trượt timeline drawer, toggle vai trò và auto-save timestamp phải phản hồi tức thì (< 100ms), chuyển động mượt mà (smooth CSS transitions). |
| **NFR-03** | **Responsive & Container-Scoped Mobile** | Đảm bảo hiển thị hoàn hảo ở cả 2 chế độ: Desktop toàn màn hình và Chế độ Điện thoại (Mobile App Frame 390–430px). Trong chế độ điện thoại, bố cục tự động co giãn theo container, không phụ thuộc vào kích thước màn hình máy tính. |
| **NFR-04** | **Event Simulation Integrity** | Giả lập chính xác các sự kiện trình duyệt: Bắt sự kiện chuyển tab bằng Page Visibility API (`document.visibilitychange` / `window.onblur`) để kích hoạt Modal cảnh báo và quy trình đổi đề thật sự trên giao diện. |
| **NFR-05** | **Zero Backend Dependency** | Toàn bộ trạng thái (danh sách câu hỏi, trạng thái chọn đáp án, log vi phạm, countdown timer, mã đề hiện tại, dữ liệu admin, phúc khảo) được đóng gói tự chủ trong Mock Store / Local State mà không cần cài đặt server. |
| **NFR-06** | **Clarity & Demo Readiness** | Giao diện có bố cục rõ ràng, trực quan, có các dữ liệu mẫu (đồ thị parabol sắc nét, danh sách học sinh mẫu, biểu đồ điểm, danh sách khối lớp của trường) để người xem hiểu ngay luồng hoạt động mà không cần đọc tài liệu hướng dẫn. |
| **NFR-07** | **Role-Based Access Control (RBAC)** | Phân quyền triệt để giữa 4 vai trò (Học sinh, Giáo viên, Phụ huynh, Quản trị viên). Giao diện mỗi vai trò tuyệt đối không hiển thị các menu hay dữ liệu của vai trò khác. |
| **NFR-08** | **High-Fidelity Mobile App Simulator** | Khung điện thoại có đầy đủ Dynamic Island, Status Bar, Home Indicator, hỗ trợ cử chỉ cuộn mượt mà và chuyển đổi linh hoạt chỉ bằng một cú nhấp chuột. |

---

## 5. Kết luận Bước 1 & Sẵn sàng cho Bước 2
Tài liệu trích xuất trên đã bao quát toàn diện **53 yêu cầu nguyên văn (`RAW-001` đến `RAW-053`)**, kế thừa toàn bộ [Init/client_request.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/client_request.md), [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md) (đáp ứng 100% 86 bảng biểu) và [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md), tái hiện đầy đủ **8 kịch bản nghiệp vụ As-Is / To-Be** và thiết lập **8 tiêu chuẩn phi chức năng NFRs** sẵn sàng làm căn cứ vững chắc cho Bước 2.
