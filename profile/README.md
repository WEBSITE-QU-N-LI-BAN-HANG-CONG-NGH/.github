Chắc chắn rồi! Dưới đây là một file README tổng hợp, được cấu trúc lại một cách rõ ràng và chuyên nghiệp để hướng dẫn cài đặt toàn bộ hệ thống từ các phần bạn đã cung cấp.

File README này tập trung vào trình tự cài đặt hợp lý, giúp người mới dễ dàng làm theo.

---

# Hướng Dẫn Cài Đặt Hệ Thống Bán Hàng

Chào mừng bạn đến với dự án Website Quản lý Bán hàng! Tài liệu này sẽ hướng dẫn bạn cách cài đặt và khởi chạy toàn bộ các thành phần của hệ thống trên máy cục bộ.

## 📋 Tổng Quan Hệ Thống

Hệ thống bao gồm các thành phần riêng biệt sau:

* **Backend (Java Spring Boot):** Chịu trách nhiệm xử lý toàn bộ logic nghiệp vụ, quản lý cơ sở dữ liệu và cung cấp API cho các ứng dụng frontend.
* **Frontend Customer (Vite + React):** Giao diện dành cho khách hàng mua sắm.
* **Frontend Seller (Vite + React):** Giao diện dành cho người bán quản lý sản phẩm, đơn hàng.
* **Frontend Admin (Vite + React):** Giao diện dành cho quản trị viên quản lý toàn bộ hệ thống.
* **AI Chat Service (Python Flask):** Dịch vụ chatbot sử dụng AI để hỗ trợ người dùng.

Để hệ thống hoạt động chính xác, bạn cần cài đặt theo đúng thứ tự được nêu dưới đây.

## ⚙️ Yêu Cầu Chung

Trước khi bắt đầu, hãy đảm bảo bạn đã cài đặt các công cụ sau trên máy của mình:

* **Git:** Để sao chép mã nguồn.
* **Java Development Kit (JDK):** phiên bản **21** hoặc cao hơn.
* **Apache Maven:** phiên bản **3.9** hoặc cao hơn.
* **MySQL Server:** phiên bản **8.0** hoặc cao hơn.
* **Node.js:** phiên bản **18.x** hoặc cao hơn.
* **Python:** phiên bản **3.x**.
* **IDE/Trình soạn thảo mã:** IntelliJ IDEA, VS Code, hoặc tương tự.

---

## 🚀 Các Bước Cài Đặt

### Phần 1: Cài Đặt Backend (Java)

Đây là thành phần cốt lõi, cần được cài đặt và khởi chạy đầu tiên.

**Bước 1: Clone Repository**

```bash
git clone https://github.com/WEBSITE-QU-N-LI-BAN-HANG-CONG-NGH/BACKEND
cd BACKEND
```

**Bước 2: Thiết lập Cơ sở dữ liệu**

Script `Script_Database.sql` đã bao gồm tất cả các lệnh cần thiết để tạo database, bảng và dữ liệu mẫu.

* Mở Terminal hoặc Command Prompt và chạy lệnh sau (thay `your_username` bằng tên người dùng MySQL của bạn):

```bash
# Điều hướng đến thư mục gốc của backend
mysql -u your_username -p ecommerce < ./Script_Database.sql
```

* Nhập mật khẩu MySQL của bạn khi được yêu cầu.

**Bước 3: Cấu hình `application.properties`**

1.  Trong thư mục `src/main/resources/`, tạo một tệp mới có tên là `application.properties`.
2.  Sao chép toàn bộ nội dung dưới đây và dán vào tệp vừa tạo.
3.  **Quan trọng:** Thay thế tất cả các giá trị có dạng `your_...` bằng thông tin cấu hình thực tế của bạn.

```properties
server.port=8080

# API Prefix
api.prefix=/api/v1

# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce_shop
spring.datasource.username=your_mysql_username
spring.datasource.password=your_mysql_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA / Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.open-in-view=true

# JWT Configuration
auth.token.jwtSecret=your_jwt_secret_key
auth.token.accessExpirationInMils=3600000999
auth.token.refreshExpirationInMils=864000000

# Cookie Configuration
app.useSecureCookie=false

# OAuth2 Configuration
spring.security.oauth2.client.registration.google.client-id=your_google_client_id
spring.security.oauth2.client.registration.google.client-secret=your_google_client_secret
spring.security.oauth2.client.registration.google.scope=email,profile

spring.security.oauth2.client.registration.github.client-id=your_github_client_id
spring.security.oauth2.client.registration.github.client-secret=your_github_client_secret
spring.security.oauth2.client.registration.github.scope=user:email

app.oauth2.redirectUri=http://localhost:5173/oauth2/redirect
app.oauth2.failureRedirectUri=http://localhost:5173/login

# OTP Configuration
app.otp.expiration-minutes=10
app.otp.resend-cooldown-minutes=2

# CORS Configuration
cors.allowed-origins=http://localhost:5173,http://localhost:5174,http://localhost:5175

# Mail Configuration
# ⚠️ Lưu ý: Sử dụng "Mật khẩu ứng dụng" của Google, không dùng mật khẩu tài khoản.
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=your_gmail_address@gmail.com
spring.mail.password=your_gmail_app_password
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true

# VNPAY Configuration
vnpay.tmn-code=your_vnpay_tmn_code
vnpay.hash-secret=your_vnpay_hash_secret
vnpay.pay-url=https://sandbox.vnpayment.vn/paymentv2/vpcpay.html
vnpay.return-url=http://localhost:5173/payment/result

# Cloudinary Configuration
cloudinary.cloudName=your_cloudinary_cloud_name
cloudinary.apiKey=your_cloudinary_api_key
cloudinary.apiSecret=your_cloudinary_api_secret
cloudinary.apiSecure=true

# Company Info
app.company.logo.url=https://res.cloudinary.com/dgygvrrjs/image/upload/v1745387610/ChatGPT_Image_Apr_5_2025_12_08_58_AM_ociguu.png
contact.info.phone=+1111111111
contact.info.email=sonvtthanhthanh@gmail.com
contact.info.address=212F2/11 Nguyen Huu Canh, Phuong Thang Nhat, TP Vung Tau
contact.info.businessHours=8:00 - 22:00, Mon - Sun
contact.info.facebook=https://www.facebook.com/techshop
contact.info.instagram=https://www.instagram.com/techshop
contact.info.youtube=https://youtube.com/techshop
```

**Bước 4: Build và Chạy ứng dụng**

* Mở terminal tại thư mục gốc của dự án và chạy lệnh (khuyên dùng):

```bash
mvn spring-boot:run
```

* Hoặc chạy từ IDE bằng cách mở tệp `TeamProjectApplication.java` và nhấn nút Run.

➡️ **Backend sẽ chạy tại:** `http://localhost:8080`

### Phần 2: Cài Đặt AI Chat Service (Python)

**Bước 1: Tạo và kích hoạt môi trường ảo**

```bash
# Clone repository
git clone https://github.com/WEBSITE-QU-N-LI-BAN-HANG-CONG-NGH/Chat-w-Gemini
cd Chat-w-Gemini
```

# Trên macOS/Linux
```bash
python3 -m venv venv
source venv/bin/activate
```

# Trên Windows
```bash
python -m venv venv
.\venv\Scripts\activate
```

**Bước 2: Cài đặt các thư viện**

```bash
pip install -r requirements.txt
```

**Bước 3: Chạy ứng dụng**

```bash
python app.py
```

➡️ **AI Chat Service sẽ chạy tại cổng được cấu hình trong `app.py` (ví dụ: `http://localhost:5000`).**

### Phần 3: Cài Đặt Các Ứng Dụng Frontend (Node.js)

Thực hiện các bước sau cho từng ứng dụng Frontend: Customer, Seller và Admin.

#### 3.1. Trang Khách Hàng (Customer)

1.  **Clone & Cài đặt:**
    ```bash
    git clone https://github.com/WEBSITE-QU-N-LI-BAN-HANG-CONG-NGH/FrontEnd-Customer
    cd FrontEnd-Customer
    npm install
    ```
2.  **Khởi chạy:**
    ```bash
    npm run dev
    ```
➡️ **Ứng dụng sẽ chạy tại:** `http://localhost:5173`

#### 3.2. Trang Bán Hàng (Seller)

1.  **Clone & Cài đặt:**
    ```bash
    git clone https://github.com/WEBSITE-QU-N-LI-BAN-HANG-CONG-NGH/FrontEnd-Seller
    cd FrontEnd-Seller
    npm install
    ```
2.  **Khởi chạy:**
    ```bash
    npm run dev
    ```
➡️ **Ứng dụng sẽ chạy tại:** `http://localhost:5174`

#### 3.3. Trang Quản Trị (Admin)

1.  **Clone & Cài đặt:**
    ```bash
    git clone https://github.com/WEBSITE-QU-N-LI-BAN-HANG-CONG-NGH/FrontEnd-Admin
    cd FrontEnd-Admin
    npm install
    ```
2.  **Khởi chạy:**
    ```bash
    npm run dev
    ```
➡️ **Ứng dụng sẽ chạy tại:** `http://localhost:5175`

---

## ✅ Tổng Kết & Trạng Thái Hoạt Động

Sau khi hoàn tất tất cả các bước trên, hệ thống của bạn sẽ hoạt động với các dịch vụ chạy tại các cổng sau:

* **Backend API:** `http://localhost:8080`
* **AI Chat Service:** `http://localhost:5000` (hoặc cổng tương ứng)
* **Trang Khách Hàng:** `http://localhost:5173`
* **Trang Bán Hàng:** `http://localhost:5174`
* **Trang Quản Trị:** `http://localhost:5175`

Bạn cần đảm bảo **Backend** và **AI Chat Service** đang chạy trước khi khởi động các ứng dụng Frontend để đảm bảo đầy đủ chức năng. Chúc bạn thành công!
