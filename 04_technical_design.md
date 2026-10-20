# BƯỚC 4: THIẾT KẾ KỸ THUẬT & KIẾN TRÚC GIAO DIỆN MOCKUP (TECHNICAL DESIGN & MODELING)

> **Căn cứ kế thừa:**
> - [specs/01_requirements_ingestion.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/01_requirements_ingestion.md) (`RAW-001` đến `RAW-053`)
> - [specs/02_agile_backlog.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/02_agile_backlog.md) (52 User Stories & AC chuẩn GWT)
> - [specs/03_product_roadmap.md](file:///Users/phamkhanh/Documents/Project/Miu/specs/03_product_roadmap.md) (Kế hoạch 6 Sprints & 207 SP)
> - [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md) & [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md)

---

## 1. Kiến trúc Hệ thống Tổng thể (Comprehensive Mockup Architecture)

Để vận hành **100% độc lập trên trình duyệt, không cần backend**, kiến trúc của AZOTA Mockup được xây dựng theo mô hình **Single Page Application (SPA) Đa Phân Hệ** tích hợp **Container-Scoped Mobile Viewport Engine** và **Simulated Operational Bus**:

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│                      TẦNG GIAO DIỆN NGƯỜI DÙNG (UI LAYER)                        │
│  [Màn hình Đăng ký / Đăng nhập 4 Tabs] ─ [Phòng chờ Lobby] ─ [Phòng thi Học sinh]│
│  [Quản lý & Giám sát GV] ─ [Cổng Phụ huynh] ─ [Cổng Quản trị viên Toàn trường]   │
│  [Xem kết quả & Phúc khảo] ─ [Thi Thông minh & Chấm Offline] ─ [AZOTA Live]      │
└────────────────────────────────────────┬─────────────────────────────────────────┘
                                         │ (State Dispatches & Layout Adapters)
┌────────────────────────────────────────▼─────────────────────────────────────────┐
│        BỘ ĐIỀU HỐI GIAO DIỆN DI ĐỘNG (CONTAINER-SCOPED MOBILE ENGINE - US-038)   │
│  ├── Viewport Switcher: Chuyển đổi giữa Desktop Web & Khung iPhone 16 Pro        │
│  ├── App Bottom Navigation Bar: Thanh điều hướng đáy 4-5 tabs ứng dụng chạm nhạy│
│  ├── Responsive Scaler: Tự động co giãn đồ thị Parabol & chuyển Table sang Card │
│  └── In-Frame Modals Anchor: Neo giữ toàn bộ modal cảnh báo bên trong khung bezel│
└────────────────────────────────────────┬─────────────────────────────────────────┘
                                         │
┌────────────────────────────────────────▼─────────────────────────────────────────┐
│                    QUẢN LÝ TRẠNG THÁI (CLIENT REACTIVE STORE)                    │
│  ├── AuthState: Phiên làm việc, Đăng ký & Phân quyền RBAC 4 vai trò (HS, GV, PH, Admin)
│  ├── LobbyState: Kiểm tra thiết bị/mạng, cam kết quy định trước khi mở đề        │
│  ├── ExamState: Câu hỏi, đồ thị, auto-save, timer từng câu & khóa câu đã hết giờ │
│  ├── ParametricState: Sinh tham số ngẫu nhiên (X, Y) và đáp án cho từng thí sinh │
│  ├── AntiCheatState: Bắt chuyển tab (Visibility API), animation đổi mã đề 01->04 │
│  ├── RecoveryState: Giả lập mất mạng & tự động khôi phục từ bộ nhớ đệm client   │
│  ├── DisputeState: Tiếp nhận yêu cầu phúc khảo và xử lý điều chỉnh điểm của GV   │
│  ├── ProctoringState: Danh sách thí sinh live, timeline logs vi phạm từng giây  │
│  ├── AdminState: Quản lý user/lớp học, import Excel, kỳ thi chung, Audit Logs    │
│  └── ParentState: Mã liên kết con, widget tiến độ, mini-charts, chat feed        │
└────────────────────────────────────────┬─────────────────────────────────────────┘
                                         │ (Sync / Query / Storage Event Bus)
┌────────────────────────────────────────▼─────────────────────────────────────────┐
│                MOCK DATA REPOSITORY & LOCAL STORAGE ADAPTER                      │
│  ├── Mock Question Bank (Toán Parabol, Tham số biến đổi, 3 mức độ nhận thức)     │
│  ├── Mock Exam Versions (Đề 01, Đề 04, Đề thi chung toàn khối 12)               │
│  ├── Mock School Structure (Khối 10, 11, 12, phân công giáo viên, danh sách lớp) │
│  └── Mock Audit Logs & System Metrics (CPU, RAM, phiên kết nối đồng thời)        │
└──────────────────────────────────────────────────────────────────────────────────┘
```

---

## 2. Mô hình Dữ liệu Mock Data Schema (Client Data Model)

### 2.1. Thực thể Phòng chờ & Cam kết Thi (`PreCheckLobby`)
```json
{
  "PreCheckLobby": {
    "examId": "EXAM-MATH-12",
    "studentId": "USR-001",
    "deviceStatus": "ready", // "checking" | "ready" | "error"
    "networkStatus": "stable", // "stable" | "slow" | "disconnected"
    "pingMs": 18,
    "rulesAccepted": true,
    "initialVersionGranted": "01"
  }
}
```

### 2.2. Thực thể Khôi phục Mất mạng (`SessionRecovery`)
```json
{
  "SessionRecovery": {
    "studentId": "USR-001",
    "examId": "EXAM-MATH-12",
    "isInterrupted": false,
    "lastSyncedAt": "09:15:32",
    "cachedAnswers": {
      "Q-01": "A",
      "Q-02": "B"
    },
    "remainingSecondsAtInterruption": 2340
  }
}
```

### 2.3. Thực thể Phúc khảo / Giải trình Vi phạm (`DisputeAppeal`)
```json
{
  "DisputeAppeal": {
    "id": "APPEAL-2026-001",
    "studentId": "USR-001",
    "studentName": "Nguyễn Tiến Anh",
    "examId": "EXAM-MATH-12",
    "submissionId": "SUB-MATH-01",
    "reason": "Em bấm nhầm phím Windows làm nhảy tab 1s, mong cô xem xét lại câu 4",
    "submittedAt": "2026-10-15 09:45:00",
    "originalScore": 9.0,
    "status": "pending", // "pending" | "approved" | "rejected"
    "adjustedScore": 9.5,
    "teacherFeedback": "Đã xem xét nhật ký timeline (rời trang 1.2s không có hành vi tra cứu). Điều chỉnh +0.5 điểm."
  }
}
```

### 2.4. Thực thể Người dùng & Phân quyền RBAC (`User`)
```json
{
  "User": {
    "id": "USR-004",
    "username": "admin_hieu_truong",
    "fullName": "Thầy Nguyễn Văn Hiệu (Hiệu trưởng)",
    "role": "admin", // "student" | "teacher" | "parent" | "admin"
    "avatar": "https://api.dicebear.com/7.x/avataaars/svg?seed=Admin",
    "schoolName": "THPT Chuyên Thủy Lợi",
    "permissions": ["MANAGE_USERS", "MANAGE_CLASSES", "ORGANIZE_EXAMS", "VIEW_AUDIT_LOGS"]
  }
}
```

### 2.5. Thực thể Câu hỏi Biến đổi Tham số & Khóa câu (`SmartExamItem`)
```json
{
  "SmartExamItem": {
    "id": "Q-PARAM-01",
    "type": "parametric_parabola",
    "template": "Cho hàm số bậc hai y = x² - {b}x + {c}. Hãy xác định tọa độ đỉnh I của đồ thị.",
    "parameterConstraints": {
      "b": [2, 4, 6],
      "c": [1, 3, 5]
    },
    "instantiatedData": {
      "b": 4,
      "c": 3,
      "equation": "y = x² - 4x + 3",
      "vertex": {"x": 2, "y": -1},
      "correctOption": "A",
      "options": [
        {"id": "A", "label": "A", "content": "I(2; -1)", "isCorrect": true},
        {"id": "B", "label": "B", "content": "I(-2; -1)", "isCorrect": false},
        {"id": "C", "label": "C", "content": "I(1; 3)", "isCorrect": false},
        {"id": "D", "label": "D", "content": "I(2; 1)", "isCorrect": false}
      ]
    },
    "timerConfig": {
      "allocatedSeconds": 60,
      "isLocked": false
    }
  }
}
```

### 2.6. Thực thể Kho Học Liệu & Bài Giảng Lớp Học (`ClassMaterial` - US-044)
```json
{
  "ClassMaterial": {
    "id": "MAT-001",
    "classId": "10A1",
    "title": "Chuyên đề 01: Hàm số bậc hai & Ứng dụng thực tế",
    "topic": "Đại số & Giải tích",
    "fileType": "pdf", // "pdf" | "pptx" | "docx" | "mp4"
    "fileSize": "4.2 MB",
    "uploadedAt": "2026-10-14 08:30:00",
    "downloadsCount": 42,
    "allowDownload": true,
    "author": "Cô Trần Thị Mai"
  }
}
```

### 2.7. Thực thể Bài Tập Tự Luận & Ma Trận Đối Soát AI (`HomeworkSubmission` & `SimilarityMatrix` - US-045)
```json
{
  "HomeworkSubmission": {
    "id": "HW-SUB-01",
    "assignmentId": "HW-MATH-03",
    "studentId": "HS-2026-07",
    "studentName": "Trần Thị Bích",
    "uploadedImages": [
      "data:image/svg+xml;base64,...trang1.png",
      "data:image/svg+xml;base64,...trang2.png"
    ],
    "submittedAt": "2026-10-15 21:14:02",
    "status": "submitted", // "pending" | "submitted" | "graded" | "flagged"
    "note": "Em gửi cô 2 trang bài tập hình học không gian câu 3 và câu 4 ạ.",
    "aiAnalysis": {
      "similarityScore": 95.4,
      "flaggedPairWith": "Lê Hoàng Nam (HS-2026-08)",
      "matchedSteps": [
        "Dòng 4: Đặt hệ trục tọa độ Oxyz với A làm gốc",
        "Dòng 7: Tính vector chỉ phương u = (1; 2; -2)",
        "Dòng 12: Sai cùng dấu tại bước tính góc phi = 45 độ"
      ],
      "status": "suspicious_collusion"
    }
  }
}
```

---

## 3. Kiến trúc Thành phần Giao diện (UI Component Hierarchy)

```text
AppContainer (US-023)
├── DemoScenarioToolbar (Thanh trợ năng chuyển 4 vai trò, mô phỏng chuyển tab, mất mạng & đăng xuất)
├── GlobalDeviceSimulator (US-024 & US-038: Mobile App Viewport Engine)
│    ├── DeviceSwitcherControls (Nút chuyển [💻 Máy tính] ↔ [📱 Điện thoại])
│    ├── SmartphoneChassis (Khung iPhone 16 Pro, Dynamic Island, Status Bar 09:41, Pin, Home Bar)
│    └── ScopedLayoutContainer (#phone-screen-container: Áp dụng class `.mobile-frame-mode`)
│         ├── MobileTopBar (Header ứng dụng di động có Logo, Icon chuông và Avatar)
│         ├── MobileBottomNav (Thanh điều hướng đáy 4 tabs: Trang chủ, Phòng thi, Giám sát, Sổ liên lạc)
│         └── ViewportContentArea (Vùng hiển thị nội dung tự động co giãn)
│
├── [View 1] AuthModalView (US-001, US-002, US-003, US-042)
│    ├── RoleTabsSwitcher ([Học sinh] - [Giáo viên] - [Phụ huynh] - [Quản trị viên])
│    ├── LoginForm (Tự đổi sắc thái màu Accent Color theo 4 vai trò, EyeIconToggle, RememberCheckbox)
│    └── RegisterForm (Tạo tài khoản mới, Checkbox cam kết Điều khoản & Chính sách)
│
├── [View 2] StudentPortalView (US-004, US-005, US-025, US-026, US-039, US-041, US-044, US-045)
│    ├── UrgentDeadlineWidget (Đếm ngược thời gian thực, progress bar)
│    ├── ExamCardsGrid (Danh sách bài thi, badge màu 🟢🟡🔴, ô nhập mã)
│    ├── PreCheckLobbyModal (US-039: Kiểm tra mạng, thiết bị, bảng quy định thi & checkbox cam kết)
│    ├── PracticeWorkspace (Tự luyện tập theo chủ đề: Hàm số, Hình học, Tổ hợp)
│    ├── ExamReviewView (Xem lại bài thi đã nộp, bảng đối chiếu đáp án & lời giải)
│    ├── DisputeAppealModal (US-041: Form gửi yêu cầu phúc khảo và giải trình vi phạm)
│    ├── ClassMaterialsExplorer (US-044: Danh mục tài liệu học tập, bài giảng PDF/PPTX & nút tải về)
│    └── HomeworkSubmitModal (US-045: Modal kéo thả ảnh nhiều trang vở bài làm và lời nhắn gửi giáo viên)
│
├── [View 3] ExamWorkspaceView (US-006 -> US-009, US-027, US-028, US-040)
│    ├── NetworkRecoveryBanner (US-040: Thanh cảnh báo mất mạng & thông báo khôi phục thành công)
│    ├── ExamHeader (Chỉ báo Auto-save ngầm ✓ [HH:mm:ss], đếm lùi tổng thể & đếm lùi từng câu)
│    ├── QuestionCanvas (Toán Parabol SVG chuẩn giải tích, nút Radio touch-friendly)
│    ├── QuestionLockIndicator (Banner thông báo trạng thái câu hỏi: [ĐANG LÀM] hoặc [ĐÃ KHÓA 🔒])
│    ├── ExamFooter (Trước, Sau, Nộp bài; trên mobile chuyển thành dải nút chạm nhạy)
│    └── ExamSidebar / MobileSwipePills (Lưới 20 câu hoặc dải vuốt ngang trên điện thoại)
│
├── [Modal Overlay] AntiCheatModal (US-010, US-011, US-012)
│    ├── RedWarningOverlay (Bắt sự kiện visibilitychange/blur, khóa trọn màn hình điện thoại)
│    ├── CodeSwapAnimation (Hiệu ứng mũi tên động 01 ➔ 04)
│    └── AutoResumeController (Bảo lưu thời gian còn lại và câu đã làm)
│
├── [View 4] TeacherManagementView (US-013 -> US-019, US-029, US-030, US-041, US-043, US-044, US-045)
│    ├── TeacherClassroomManager (US-043: Quản lý danh sách lớp, tạo lớp mới, mã mời, bảng học sinh, phân nhóm học tập & xuất Excel)
│    ├── ClassMaterialsRepository (US-044: Kho lưu trữ bài giảng số, tài liệu tham khảo theo lớp & modal upload học liệu)
│    ├── AISimilarityMatrixChecker (US-045: Modal đối soát trùng lặp bài tập tự luận 95.4%, phân tích từng dòng giải tích)
│    ├── QuestionBankFilterBar (3 Dropdowns lọc đa tiêu chí + tags màu độ khó)
│    ├── ExamMatrixBuilder (Ma trận đề, Slider trùng lặp, toggles chống gian lận)
│    ├── LiveProctoringBoard (Bảng thí sinh real-time, badge đỏ nhấp nháy pulse; chuyển Card trên mobile)
│    ├── SlideOverTimelineDrawer (Ngăn trượt dòng thời gian lịch sử vi phạm từng giây)
│    ├── TeacherDisputeManager (US-041: Bảng rà soát phúc khảo, nút "Giữ nguyên" hoặc "Chỉnh sửa điểm")
│    ├── OfflineSheetScanner (Mô phỏng xuất phiếu tô trắc nghiệm & camera quét chấm tự động)
│    ├── AzotaLiveVirtualRoom (Phòng thi tương tác trực tuyến với camera & điểm danh)
│    └── PerformanceAnalytics (Biểu đồ cột phổ điểm, biểu đồ tròn hoàn thành)
│
├── [View 5] ParentPortalView (US-020, US-021, US-022)
│    ├── StudentCodeLinker (Form kết nối mã học sinh `HS-2026-07`)
│    ├── ProgressDashboard (Widget bài nợ đỏ, sắp hạn cam, mini-chart điểm số)
│    ├── TeacherFeedbackFeed (Danh sách nhận xét chi tiết của thầy cô)
│    └── FloatingChatBubble (Bong bóng nổi góc phải mở Mini Chat Window)
│
└── [View 6] AdminPortalView (US-031 -> US-037)
     ├── AdminKpiCards (Tổng học sinh 1.250, 68 GV, 32 lớp, 3 kỳ thi chung, CPU 28% / RAM 42%)
     ├── UserRbacManagement (Bảng danh sách người dùng, gán nhóm quyền, khóa/mở tài khoản)
     ├── SchoolStructureManager (Cây khối lớp 10, 11, 12, phân công GV, Modal import Excel)
     ├── CentralizedExamManager (Thiết lập kỳ thi chung khối 12, phân bổ phòng thi ảo)
     ├── SchoolWideAnalytics (Biểu đồ so sánh điểm giữa các lớp 12A1, 12A2, 12A3)
     ├── SystemAuditLogBoard (Bảng Audit Logs truy vết thời gian thực, cảnh báo an toàn)
     └── SchoolNotificationCenter (Gửi thông báo toàn trường & xử lý tickets hỗ trợ)
```

---

## 4. Động cơ Chuyển cảnh & Hiệu ứng Thị giác Mượt mà (CSS Transition Engine & Device Viewport Morphing)

Để loại bỏ hoàn toàn các lỗi giật hiển thị, không có hiệu ứng chuyển đổi trạng thái khi chuyển vai trò, chuyển chế độ máy tính sang điện thoại và các tương tác nút bấm, hệ thống tích hợp bộ động cơ CSS Transitions & Keyframes Animation chuyên biệt:

### 4.1. Keyframe Animations & Active View Transitions
- **`fadeInView`:** Áp dụng cho container chính của các view (`.view-active-animate`):
  ```css
  @keyframes fadeInView {
    0% { opacity: 0; transform: translateY(6px); }
    100% { opacity: 1; transform: translateY(0); }
  }
  .view-active-animate { animation: fadeInView 0.25s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
  ```
- **`tabSlideFade`:** Áp dụng cho các tab nội bộ (`.tab-content-animate`):
  ```css
  @keyframes tabSlideFade {
    0% { opacity: 0; transform: translateX(8px); }
    100% { opacity: 1; transform: translateX(0); }
  }
  .tab-content-animate { animation: tabSlideFade 0.2s ease-out forwards; }
  ```

### 4.2. Hiệu ứng Chuyển Vai trò Đăng nhập (Role Morphing Transitions)
- Khi bấm chọn giữa 4 tab `[Học sinh]`, `[Giáo viên]`, `[Phụ huynh]`, `[Quản trị viên]`, hệ thống tự động:
  - Cập nhật huy hiệu vai trò `#auth-role-badge` với icon động và gradient màu sắc tương ứng:
    - **Học sinh:** `from-blue-600 to-indigo-600` (Icon Mũ cử nhân)
    - **Giáo viên:** `from-purple-600 to-pink-600` (Icon Bảng phấn)
    - **Phụ huynh:** `from-teal-600 to-emerald-600` (Icon Trái tim gia đình)
    - **Quản trị viên:** `from-slate-700 to-gray-900` (Icon Khiên bảo mật)
  - Chuyển màu nền Header Card (`from-blue-50`, `from-purple-50`, `from-teal-50`, `from-indigo-50`) qua CSS transition mượt mà.
  - Điền sẵn tài khoản demo tương ứng và kích hoạt hiệu ứng `.tab-content-animate` trên form input.

### 4.3. Hiệu ứng Chuyển Chế độ Thiết bị Máy tính ↔ Điện thoại (Device Viewport Morphing)
- `#global-device-wrapper` được cấu hình transition đa thuộc tính:
  ```css
  #global-device-wrapper {
    transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
  }
  ```
- Khi chuyển sang Chế độ Điện thoại:
  - Container co lại chuẩn xác `max-width: 430px`, bo góc `rounded-[48px]`, viền Bezel đen bóng `border-[10px] border-slate-900`.
  - Hiển thị thanh trạng thái đỉnh `#phone-status-bar` (đồng hồ 09:41, biểu tượng sóng 5G, pin đầy) và thanh đáy `#phone-home-indicator`.
  - Hai nút chuyển đổi trên Header (`#btn-device-desktop` / `#btn-mode-desktop`, `#btn-device-mobile` / `#btn-mode-mobile`) cập nhật đồng bộ trạng thái Active/Inactive kèm hiệu ứng phóng to thu nhỏ nhẹ.
  - Toàn bộ bảng biểu tự động chuyển sang layout Card dọc, loại bỏ 100% lỗi tràn mép ngang.

### 4.4. Phản hồi Xúc giác Nút bấm (Button Interactive Micro-feedbacks)
- Tất cả các nút hành động chính đều được trang bị hiệu ứng:
  - `active:scale-95` tạo cảm giác chạm nhạy như trên màn hình cảm ứng thật.
  - `transition-all duration-150` kết hợp `hover:shadow-md`.
  - Trạng thái Toggle mật khẩu chuyển đổi icon mắt (`eye` ↔ `eye-off`) với hiệu ứng scale êm ái.

### 4.5. Phân hệ Quản Trị Học Liệu, Thông Báo & Chống Gian Lận Nghiêm Ngặt (Strict Anti-Cheat & Asset Engines)
1. **TeacherAnnouncementDispatcher (US-046 / Bảng 1.6):** Soạn thông báo, phân nhóm đối tượng nhận (Toàn lớp, Nhóm cần phụ đạo, Nhóm nâng cao), kích hoạt cơ chế nhắc hạn nộp cá nhân hóa trước deadline 2 tiếng và đồng bộ tức thì sang Cổng Học sinh và Cổng Phụ huynh.
2. **ClassDiscussionForum (US-047 / Bảng 1.7):** Diễn đàn hỏi đáp môn học, hỗ trợ học sinh gửi thắc mắc bài tập, giáo viên trả lời và ghim lời giải chuẩn mực, tự động cập nhật trạng thái đã giải đáp.
3. **AdminStorageManager (US-048 / Bảng 1.25):** Module giám sát lưu trữ đám mây (Cloud Metrics: 412.5 GB / 1 TB, 1.240 bài giảng, 2.850 đề thi), kiểm duyệt tệp tin học liệu toàn trường, dọn dẹp cache rác và kích hoạt bản sao lưu AWS S3.
4. **StrictLinearExamController (US-049):** Kiểm soát luồng làm bài thi tuyến tính một chiều. Đếm lùi 30s/câu, tự động khóa câu hỏi khi hết giờ. Khi thí sinh chuyển câu, câu hỏi đã hoàn thành bị khóa cứng vĩnh viễn, vô hiệu hóa nút Câu trước (🔒) và chặn quay lại trên danh sách câu hỏi.
5. **ForcedSubmissionEngine (US-050):** Theo dõi số lần vi phạm chuyển tab/rời màn hình (Strikes). Khi số lần vi phạm chạm ngưỡng 3/3 lần, hệ thống dừng đồng hồ, kích hoạt lệnh CƯỠNG ÉP THU BÀI ngay lập tức, tính điểm các câu đã làm, hiển thị modal đỏ khẩn cấp và đồng bộ trạng thái Bị đình chỉ thi sang Giám sát viên và Audit Logs.
6. **StudentClassEnrollmentManager (US-051 / Bảng 1.8):** Module quản lý tham gia lớp học của học sinh qua mã mời hoặc liên kết trực tuyến; kiểm tra tính hợp lệ của mã mời (ví dụ: `10A1-TOAN`, `10A2-TOAN`), thêm lớp vào danh sách lớp đã liên kết, cập nhật sĩ số và đồng bộ quyền truy cập tài liệu bài học.
7. **StudentDiscussionQABus (US-052 / Bảng 1.14 tương ứng Bảng 1.7):** Kênh thảo luận và hỏi đáp trực tuyến hai chiều giữa học sinh và giáo viên; tiếp nhận câu hỏi thắc mắc từ học sinh, đồng bộ sang bảng điều khiển của giáo viên, hiển thị câu trả lời ghim chuẩn mực và cho phép học sinh trao đổi chuyên đề theo lớp/nhóm.

---

## 5. Đặc tả Quy chuẩn Màu sắc & Trạng thái (Design System Tokens theo Flow.md)

| Trạng thái | Mã màu CSS (Tailwind) | Mã HEX | Vị trí ứng dụng |
| :--- | :--- | :--- | :--- |
| **Màu chủ đạo (Primary)** | `bg-blue-600 text-white` | `#2563EB` | Nút bấm chính, header thương hiệu AZOTA, active tab. |
| **Màu nền (Background)** | `bg-gray-50` / `#F3F4F6` | `#F3F4F6` | Nền tổng thể toàn trang (sạch sẽ, dịu mắt). |
| **Nền thẻ / Bảng / Modal** | `bg-white` | `#FFFFFF` | Thẻ Card, bảng dữ liệu, sidebar, popup modal. |
| **An toàn / Đã làm / Đúng hạn** | `bg-green-100 text-green-700` | `#DCFCE7` / `#15803D` | Badge đề thi đã nộp, ô câu hỏi đã làm, tick auto-save. |
| **Đang làm / Đang chọn** | `bg-blue-600 text-white` | `#2563EB` | Ô câu hỏi đang chọn, lựa chọn đáp án Radio active. |
| **Cảnh báo / Sắp đến hạn** | `bg-amber-100 text-amber-700` | `#FEF3C7` / `#B45309` | Widget sắp đến hạn, bài thi chờ duyệt, mất mạng. |
| **Vi phạm / Chuyển tab / Quá hạn** | `bg-red-100 text-red-700 border-red-500`| `#FEE2E2` / `#B91C1C` | Badge đỏ chuyển tab, modal cảnh báo vi phạm, bài quá hạn. |
| **Bị khóa / Chưa làm** | `bg-gray-100 text-gray-400` kèm icon 🔒 | `#F1F5F9` / `#94A3B8` | Câu hỏi đã hết giờ bị khóa vĩnh viễn, câu chưa làm. |

---

## 6. Đặc tả Hợp đồng Dịch vụ Giả lập Mới (Simulated RESTful API Contracts)

### 6.1. `POST /api/mock/exam/precheck`
- **Request Payload:** `{"studentId": "USR-001", "examId": "EXAM-MATH-12"}`
- **Response JSON (200 OK):** `{"status": "ready", "device": "OK", "ping": "18ms", "allowStart": true}`

### 6.2. `POST /api/mock/exam/recover-session`
- **Request Payload:** `{"studentId": "USR-001", "examId": "EXAM-MATH-12"}`
- **Response JSON (200 OK):** `{"status": "recovered", "retainedAnswers": {"Q-01": "A"}, "remainingSeconds": 2340}`

### 6.3. `POST /api/mock/dispute/submit`
- **Request Payload:** `{"studentId": "USR-001", "examId": "EXAM-MATH-12", "reason": "Nhảy tab do phím tắt"}`
- **Response JSON (200 OK):** `{"status": "submitted", "appealId": "APPEAL-2026-001", "message": "Đã gửi đơn phúc khảo đến giáo viên"}`

### 6.4. `POST /api/mock/dispute/resolve`
- **Request Payload:** `{"appealId": "APPEAL-2026-001", "action": "ADJUST_SCORE", "newScore": 9.5, "notes": "Chấp thuận giải trình"}`
- **Response JSON (200 OK):** `{"status": "resolved", "finalScore": 9.5, "updatedAt": "2026-10-15 10:00:00"}`

### 6.5. `POST /api/mock/materials/upload`
- **Request Payload:** `{"classId": "10A1", "title": "Chuyên đề Đồ thị Hàm số", "fileType": "pdf", "fileSize": "3.8 MB"}`
- **Response JSON (200 OK):** `{"status": "created", "materialId": "MAT-005", "message": "Tải lên học liệu thành công"}`

### 6.6. `POST /api/mock/homework/submit`
- **Request Payload:** `{"studentId": "HS-2026-07", "assignmentId": "HW-MATH-03", "imagesCount": 2, "note": "Bài làm câu 3, 4"}`
- **Response JSON (200 OK):** `{"status": "submitted", "submissionId": "HW-SUB-01", "submittedAt": "2026-10-15 21:14:02"}`

### 6.7. `GET /api/mock/homework/similarity-matrix`
- **Request Query:** `assignmentId=HW-MATH-03&threshold=80`
- **Response JSON (200 OK):** `{"status": "success", "flaggedPairs": [{"pair": ["Trần Thị Bích", "Lê Hoàng Nam"], "score": 95.4, "status": "suspicious"}]}`

---

## 7. Kết luận Bước 4 & Sẵn sàng cho Bước 5
Bản thiết kế kỹ thuật trên đã tích hợp đầy đủ các luồng hoạt động 7 giai đoạn từ [Init/Flow.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/Flow.md) và toàn bộ 86 Bảng biểu chức năng theo [Init/BT4-Nhóm7.md](file:///Users/phamkhanh/Documents/Project/Miu/Init/BT4-Nhóm7.md). Đặc biệt, hệ thống đã chuẩn hóa toàn bộ kiến trúc hiệu ứng chuyển cảnh mượt mà (CSS Keyframes & Viewport Transitions), xóa bỏ hoàn toàn các lỗi hiển thị khi chuyển trạng thái. Hệ thống đã sẵn sàng bước vào **Bước 5: Đồng Bộ Toàn Bộ Mã Nguồn Ứng Dụng (index.html) và Bộ Kiểm Thử E2E DOM (test_suite.html)**.
