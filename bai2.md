# BÀI 2: Tối Ưu Hóa Prompt Đặc Tả Yêu Cầu Chức Năng (Dạng Tối ưu Prompt)

## Prompt tối ưu (tuân thủ 5 thành phần + bẫy dữ liệu)

**Vai trò:**  
"Hãy đóng vai trò là một **System Analyst chuyên nghiệp**."

**Mục tiêu:**  
"Viết tài liệu **Functional Requirements** cho module Authentication của dự án Shop AI."

**Ngữ cảnh:**  
"Hệ thống sử dụng chuẩn bảo mật **JWT** và phân quyền **RBAC**. Logic đăng nhập trải qua các bước xác thực, cấp token, và kiểm tra quyền truy cập."

**Ràng buộc:**  
- Đặc tả phải bao gồm **Pre-conditions, Main Flow, Exceptions**.  
- Phải xử lý triệt để các trường hợp ngoại lệ sau:  
  1. Người dùng nhập sai mật khẩu quá 5 lần.  
  2. Token JWT hết hạn trong lúc phiên làm việc đang diễn ra.  
  3. Tài khoản người dùng ở trạng thái khóa (Inactive) nhưng cố tình đăng nhập.  
- Ngôn ngữ: tiếng Việt, định dạng rõ ràng, dễ đọc.  

**Định dạng:**  
"Xuất bản tài liệu dưới dạng **Functional Requirements** chuẩn SRS, có cấu trúc mục lục, đánh số, và phân chia rõ ràng các phần."

---

## Functional Requirements (AI sinh ra)

```markdown
# Functional Requirements – Module Authentication (Shop AI)

## 1. Pre-conditions
- Người dùng đã có tài khoản hợp lệ trong hệ thống.  
- Tài khoản phải ở trạng thái **Active** để có thể đăng nhập.  
- Hệ thống đã triển khai cơ chế JWT và RBAC.  

## 2. Main Flow
1. Người dùng nhập thông tin đăng nhập (username, password).  
2. Hệ thống kiểm tra thông tin:  
   - Nếu hợp lệ → sinh JWT token.  
   - Gắn thông tin phân quyền RBAC vào token.  
3. JWT token được trả về cho client.  
4. Client sử dụng token để truy cập các API bảo mật.  
5. Hệ thống xác thực token và kiểm tra quyền RBAC trước khi cho phép truy cập.  

## 3. Exceptions (Edge Cases)
### 3.1 Sai mật khẩu quá 5 lần
- Hệ thống khóa tạm thời tài khoản trong 15 phút.  
- Ghi log sự kiện bảo mật.  
- Thông báo cho người dùng: "Bạn đã nhập sai mật khẩu quá số lần cho phép. Tài khoản bị khóa tạm thời."  

### 3.2 Token JWT hết hạn trong phiên làm việc
- Hệ thống từ chối yêu cầu API.  
- Trả về mã lỗi `401 Unauthorized`.  
- Thông báo cho người dùng: "Phiên làm việc đã hết hạn. Vui lòng đăng nhập lại."  

### 3.3 Tài khoản Inactive cố tình đăng nhập
- Hệ thống từ chối đăng nhập.  
- Trả về mã lỗi `403 Forbidden`.  
- Thông báo cho người dùng: "Tài khoản của bạn đang bị khóa. Vui lòng liên hệ quản trị viên."  

## 4. Non-functional Requirements (liên quan đến Authentication)
- Thời gian phản hồi đăng nhập < 2 giây.  
- Token JWT có thời hạn mặc định 30 phút.  
- Hệ thống ghi log toàn bộ sự kiện đăng nhập và lỗi bảo mật.  

## 5. Traceability
- Yêu cầu này liên kết trực tiếp với Use Case: **UC-Login**.  
- Liên quan đến các module: **User Repository, JWT Service, RBAC Filter**.
