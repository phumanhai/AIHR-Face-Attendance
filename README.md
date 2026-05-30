# AIHR - Hệ thống Quản trị Nhân sự & Chấm công Sinh trắc học 3D (Face ID & HRM System)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Platform: Web](https://img.shields.io/badge/Platform-Web-orange.svg)]()
[![Deploy: GitHub Pages](https://img.shields.io/badge/Deploy-GitHub_Pages-green.svg)]()

**AIHR** là một giải pháp Web App (SPA) quản trị nhân sự và chấm công sinh trắc học khuôn mặt hiện đại, tích hợp công nghệ giả lập AI nhận diện nâng cao, định vị GPS Geofencing, liveness challenge chống giả mạo, tự động đồng bộ hóa offline và tuân thủ nghiêm ngặt **Nghị định 13/2023/NĐ-CP** về bảo vệ dữ liệu cá nhân sinh trắc học tại Việt Nam.

Hệ thống được thiết kế tối ưu hóa trải nghiệm UI/UX cao cấp, tích hợp Dashboard báo cáo động dành cho HR/Admin, Trưởng phòng (Manager), và Nhân viên (Employee).

---

## 🌟 Tính Năng Cốt Lõi

### 1. 📍 Định Vị GPS Geofencing (Chống gian lận vị trí)
*   **Với các phòng ban văn phòng (HCNS, Kế toán, MKT, v.v.):** Tự động đối chiếu vị trí bằng GPS (`navigator.geolocation`). Ranh giới giới hạn là **100 mét** tính từ tâm văn phòng (Bitexco Tower). Nếu vượt quá ranh giới, hệ thống sẽ khóa nút Check-in/Check-out.
*   **Với Phòng Kinh doanh (Sales Reps):** Cho phép chấm công từ xa linh hoạt (tại văn phòng công ty hoặc tại các địa điểm đối tác/khách hàng theo lịch trình). Hệ thống không khóa nút chấm công mà ghi nhận chính xác tọa độ GPS thực tế của nhân sự kèm dòng ghi chú `"Ngoài văn phòng (Kinh doanh: [vĩ độ], [kinh độ])"` trên lịch sử và bảng công của HR.
*   *Tính năng giả lập (Developer Override):* Cung cấp bộ công cụ giả lập tọa độ văn phòng ngay trên giao diện để phục vụ chạy demo nhanh chóng.

### 2. 🎭 Challenge-Based Liveness Check (Chống chấm công hộ & Giả mạo)
*   **Chống chấm công hộ:** Nhờ tích hợp cơ chế **Nhận dạng khuôn mặt (Face ID)** thực tế kết hợp với ảnh quét biểu mẫu sinh trắc học. Khi chấm công, webcam sẽ quét sinh trắc học và đối sánh ảnh khuôn mặt trực tiếp với mẫu Face ID đã đăng ký.
*   **Chống giả mạo ảnh chụp/video:** Khi quét, hệ thống đưa thách thức liveness ngẫu nhiên (ví dụ: *"Vui lòng chớp mắt 2 lần"* hoặc *"Vui lòng mỉm cười"*). Chỉ khi người thực hiện tương tác động đạt 100%, check-in mới được phê duyệt.
*   **Lịch sử ảnh quét:** Hệ thống ghi nhận lưới sinh trắc học 2D để quản lý/HR có thể xem lại ảnh quét khuôn mặt ngay trên bảng chốt công chi tiết của từng ngày.

### 3. 💾 Offline Storage & Tự Động Đồng Bộ (Auto-Sync)
*   **Hoạt động không ngắt quãng:** Khi mất kết nối Internet, dữ liệu chấm công sẽ tự động lưu vào hàng đợi đệm (Pending Queue) trên LocalStorage dưới trạng thái `offline_pending` (đánh dấu đỏ).
*   **Đồng bộ tự động:** Ngay khi hệ thống phát hiện kết nối mạng được khôi phục, ứng dụng lập tức đẩy dữ liệu đệm lên hệ thống, cập nhật lại bảng thống kê và báo cáo biểu đồ SVG động theo thời gian thực mà không cần tải lại trang.

### 4. ⚖️ Tuân Thủ Nghị Định 13/2023/NĐ-CP (Personal Data Consent)
*   Trước khi tiến hành đăng ký Face ID lần đầu hoặc quét lại khuôn mặt, hệ thống hiển thị biểu mẫu **Cam kết & Đồng ý Xử lý Dữ liệu Sinh trắc học** chi tiết về mục đích, phạm vi, thời hạn lưu trữ và quyền lợi của người lao động.
*   Nhân sự bắt buộc phải xác nhận đồng ý tích chọn mới có thể mở camera ghi nhận khuôn mặt, đảm bảo tuân thủ pháp lý tối đa.

### 5. 👥 Quản Lý Cơ Cấu Tổ Chức & Nhân Sự Động (Full CRUD)
*   **Quản lý Phòng ban:** Cho phép HR tự do thêm mới, sửa đổi người quản lý/ca mặc định, hoặc xóa phòng ban. Khi đổi tên phòng ban, hệ thống sẽ tự động cập nhật liên đới đến hồ sơ toàn bộ nhân viên thuộc phòng ban đó.
*   **Quản lý Ca làm việc:** Cấu hình linh hoạt giờ làm, giờ nghỉ trưa, số phút đi muộn cho phép, và các phòng ban áp dụng. Hệ thống ngăn chặn việc xóa ca làm việc nếu ca đó đang được thiết lập làm mặc định cho bất kỳ phòng ban hoặc nhân sự nào.
*   **Danh bạ Nhân sự đầy đủ:** Lọc động, tìm kiếm nhanh theo tên/mã số, thiết lập quỹ phép năm, đăng ký/quét lại Face ID, sửa đổi chi tiết hồ sơ hoặc xóa nhân sự (xóa liên đới lịch sử chấm công và đơn từ để bảo toàn tính toàn vẹn dữ liệu).
*   **Khóa tài khoản nhanh:** HR dễ dàng khóa tài khoản nhân sự nghỉ việc chỉ với 1 click, lập tức chặn quyền đăng nhập và chấm công trên hệ thống.

### 6. 📊 Quy Trình Đơn Từ, Bảng Công & Quy định Lỗi chấm công
*   **Quy định Lỗi chấm công (Đi muộn / Về sớm):**
    *   **Đi muộn:** Người lao động check-in muộn quá số phút cho phép của ca làm việc (mặc định là **10 phút** đối với ca hành chính và ca kinh doanh). Trễ hơn thời gian này sẽ bị ghi nhận lỗi "Đi muộn".
    *   **Về sớm:** Người lao động thực hiện check-out sớm quá **10 phút** trước khi kết thúc ca làm việc quy định sẽ bị ghi nhận lỗi "Về sớm".
*   **Giải trình chấm công:** Nhân viên đi muộn, về sớm, vắng mặt hoặc quên check-in/out sẽ gửi đơn giải trình đính kèm lý do (tắc đường, hỏng xe, công tác ngoài...) trực tiếp từ màn hình lịch sử công cá nhân để cấp quản lý duyệt.
*   **Quản lý Nghỉ phép 3 cấp:** Nhân viên theo dõi quỹ phép còn lại trực quan -> Trưởng phòng duyệt -> HR ghi nhận tổng hợp. Tự động cộng/trừ ngày phép khi được phê duyệt thành công.
*   **Chốt bảng công tháng:** Bảng tính công tổng hợp tự động tính toán số ngày công thực tế, số ngày nghỉ phép, đi muộn/về sớm. HR có quyền chốt khóa (Lock) bảng công để khóa chỉnh sửa trước khi xuất lương.

---

## 🛠️ Công Nghệ Sử Dụng

*   **Ngôn ngữ chính:** HTML5, JavaScript (ES6+), Vanilla CSS (Custom Design System).
*   **Họa tiết & Icons:** Lucide Icons (CDN) tải động theo cấu trúc vector nhẹ nhàng.
*   **Font chữ:** Outfit & Inter (Google Fonts) tạo cảm giác giao diện UI/UX công nghệ, cao cấp và dễ nhìn.
*   **Lưu trữ dữ liệu:** LocalStorage client-driven database schema phiên bản V5 (`AIHR_HRM_DATABASE_V5`) đảm bảo lưu trữ trạng thái offline và hoạt động mượt mà không cần cài đặt database server phức tạp trong giai đoạn demo/MVP.

---

## 📁 Cấu Trúc Thư Mục Dự Án

```text
├── assets/                  # Tài nguyên hình ảnh, logo của dự án
│   ├── logo-aihr.png        # Logo chính của thương hiệu AIHR
│   └── icon.svg             # Biểu tượng vector ứng dụng hiển thị trên điện thoại
├── index.html               # File chạy duy nhất (Single Page Application - SPA) chứa HTML, CSS và logic JS
├── manifest.json            # File cấu hình cài đặt ứng dụng di động (PWA Manifest)
├── sw.js                    # Service Worker xử lý cache và hỗ trợ chấm công offline
└── README.md                # File hướng dẫn tài liệu dự án trên GitHub (đang xem)
```

---

## 🚀 Hướng Dẫn Cài Đặt & Sử Dụng

### Chạy trực tiếp từ local
Vì đây là ứng dụng Single Page Client-side hoàn toàn, bạn có thể khởi động hệ thống rất dễ dàng:
1.  **Cách 1:** Nhấp đúp trực tiếp vào file [index.html](file:///c:/Users/ADMIN/Desktop/App%20Cham%20cong/index.html) để chạy trên mọi trình duyệt (Chrome, Edge, Firefox, Safari).
2.  **Cách 2 (Khuyên dùng):** Sử dụng các công cụ Local Server như **Live Server** (VS Code) hoặc chạy lệnh dưới đây tại thư mục dự án để có trải nghiệm các API định vị tốt nhất:
    ```bash
    npx http-server ./
    ```

### Đưa dự án lên GitHub
Để chia sẻ sản phẩm này lên GitHub cá nhân/công ty của bạn:
1.  Khởi tạo git tại thư mục dự án:
    ```bash
    git init
    ```
2.  Thêm tất cả các file vào git:
    ```bash
    git add .
    ```
3.  Tạo commit đầu tiên:
    ```bash
    git commit -m "feat: init project AIHR HRM & Attendance System PWA V5"
    ```
4.  Tạo repository trên trang GitHub của bạn, sau đó thực hiện liên kết và đẩy code lên:
    ```bash
    git remote add origin https://github.com/USERNAME/REPOSITORY-NAME.git
    git branch -M main
    git push -u origin main
    ```

### Cấu hình GitHub Pages (Deploy tự động)
Do ứng dụng được viết dạng Client-Side SPA không cần build server, bạn có thể hosting ứng dụng miễn phí trên **GitHub Pages** chỉ trong vài giây:
1.  Vào Repository của bạn trên **GitHub**.
2.  Chọn tab **Settings** -> Mục **Pages** ở thanh menu bên trái.
3.  Tại phần **Build and deployment** -> **Source**, chọn nhánh `main` và thư mục `/root`. Nhấn **Save**.
4.  Đợi khoảng 1-2 phút, GitHub sẽ cung cấp đường link chạy trực tiếp trực tuyến dạng: `https://USERNAME.github.io/REPOSITORY-NAME/` để bạn chia sẻ cho khách hàng hoặc đối tác trải nghiệm ngay lập tức.

### 📲 Hướng dẫn Cài đặt ứng dụng lên Điện thoại (PWA)
Nhờ tính năng Progressive Web App (PWA) đã được tích hợp sẵn, người dùng có thể tải ứng dụng về điện thoại trực tiếp từ trình duyệt khi truy cập link HTTPS (như link GitHub Pages của bạn):

*   **Trên hệ điều hành iOS (iPhone/iPad):**
    1. Mở trình duyệt **Safari** và truy cập vào đường link GitHub Pages của dự án.
    2. Nhấn vào biểu tượng **Chia sẻ (Share)** (hình vuông có mũi tên hướng lên) ở thanh menu dưới.
    3. Chọn **Thêm vào MH chính (Add to Home Screen)**.
    4. Nhấn **Thêm (Add)**. Ứng dụng sẽ lập tức xuất hiện ngoài màn hình chính của máy dưới dạng một ứng dụng độc lập.
*   **Trên hệ điều hành Android (Samsung, Oppo, Xiaomi...):**
    1. Mở trình duyệt **Google Chrome** và truy cập vào đường link GitHub Pages.
    2. Một thông báo *"Thêm AIHR vào màn hình chính"* sẽ hiển thị ở cuối trang, hoặc nhấp vào dấu 3 chấm góc trên bên phải Chrome chọn **Cài đặt ứng dụng (Install App)**.
    3. **Hoặc:** Đăng nhập vào App, điều hướng đến mục **Bảo mật & Tài khoản**, nhấp vào nút **[Cài đặt App di động]** để kích hoạt trình cài đặt tự động.

---

## 📘 Tài Khoản Giả Lập Mặc Định

Để kiểm tra các luồng nghiệp vụ khác nhau, bạn có thể đăng nhập bằng các tài khoản giả lập được tạo sẵn trong cơ sở dữ liệu (tất cả mật khẩu mặc định đều là `123456`):

1.  **HR/Admin (Quyền quản trị cao nhất):**
    *   Mã nhân viên: `NV003` - **Ngô Phú Mạnh** (Trưởng phòng Nhân sự)
    *   Mã nhân viên: `NV001` - **Nguyễn Văn An** (Giám đốc Điều hành)
2.  **Trưởng phòng (Quản lý duyệt đơn):**
    *   Mã nhân viên: `NV008` - **Bùi Ngọc Linh** (Trưởng phòng TCKT)
    *   Mã nhân viên: `NV014` - **Ngô Mỹ Linh** (Trưởng phòng Marketing)
    *   Mã nhân viên: `NV022` - **Phạm Hùng Dũng** (Trưởng phòng Kinh doanh)
3.  **Nhân viên (Chỉ có quyền chấm công, xem lịch sử và gửi đơn):**
    *   Mã nhân viên: `NV005` - **Đỗ Minh Quân** (Nhân viên phòng HCNS)
    *   Mã nhân viên: `NV010` - **Trần Quốc Bảo** (Thủ quỹ phòng TCKT)

---

## ⚖️ Giấy Phép & Bản Quyền

Dự án được phân phối dưới giấy phép phần mềm mã nguồn mở **MIT License**. Bạn có toàn quyền sử dụng, chỉnh sửa và phân phối cho mục đích phi thương mại hoặc thương mại.

Thiết kế bởi **Ngô Phú Mạnh** (Trưởng phòng Nhân sự / Project Manager).
