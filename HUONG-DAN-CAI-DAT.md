# Hướng dẫn cài đặt đồng bộ tiến độ – Cảng Gói Tin

Làm một lần, khoảng 30 phút. Tài khoản GitHub: `linhnq2209-otb`.

## 1. Kho app (Public) và GitHub Pages
1. github.com → **New repository** → tên `cang-goi-tin` → **Public** → Create.
2. **Add file → Upload files** → kéo toàn bộ nội dung thư mục `cang-goi-tin/` (index.html, cau-hinh.js, README.md, thư mục tram/) → Commit.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch `main`, thư mục `/ (root)` → Save.
4. Sau 1–2 phút, app chạy ở: `https://linhnq2209-otb.github.io/cang-goi-tin/` (lúc này chỉ lưu trên máy).

## 2. Kho dữ liệu (Private)
1. **New repository** → tên `cang-goi-tin-data` → **Private** → Create.
2. Upload toàn bộ nội dung thư mục `cang-goi-tin-data/`.

## 3. Token GitHub chỉ ghi được kho dữ liệu
1. Ảnh đại diện → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Tên: `tram-cang-goi-tin`; Expiration: 1 năm (ghi lịch gia hạn).
3. Repository access: **Only select repositories** → chọn `cang-goi-tin-data`.
4. Permissions → Repository permissions → **Contents: Read and write**. Không cấp quyền nào khác.
5. Generate → chép token (chỉ hiện một lần). Không dán token này vào app hay gửi cho ai.

## 4. Mã đăng nhập Google (Client ID)
1. Vào console.cloud.google.com → tạo dự án `Cang Goi Tin`.
2. **APIs & Services → OAuth consent screen**: User type *External*; tên ứng dụng `Cảng Gói Tin`; email hỗ trợ là email thầy; chỉ dùng các quyền cơ bản (email, profile). Bấm **Publish app** để mọi tài khoản Gmail đăng nhập được.
3. **Credentials → Create credentials → OAuth client ID** → loại *Web application*.
4. **Authorized JavaScript origins**: thêm `https://linhnq2209-otb.github.io` → Create → chép **Client ID** (dạng `....apps.googleusercontent.com`).

## 5. Trạm Apps Script
1. script.google.com → **New project** → đặt tên `Tram Cang Goi Tin`.
2. Xoá mã mẫu, dán toàn bộ `tram/Code.gs`.
3. **Project Settings → Script properties** → thêm 4 dòng:
   - `GITHUB_TOKEN` = token ở bước 3
   - `REPO` = `linhnq2209-otb/cang-goi-tin-data`
   - `CLIENT_ID` = Client ID ở bước 4
   - `SECRET` = một chuỗi ngẫu nhiên dài (ví dụ 40 kí tự gõ bừa). **Không đổi chuỗi này về sau**, đổi là mọi học sinh thành người mới.
4. Chọn hàm `kiemTraCaiDat` → **Run** → cấp quyền → xem nhật ký phải có dòng "Đọc được kho".
5. **Deploy → New deployment** → loại **Web app** → Execute as: **Me** → Who has access: **Anyone** → Deploy → chép **Web app URL** (dạng `https://script.google.com/macros/s/.../exec`).
6. **Triggers** (biểu tượng đồng hồ) → Add trigger → hàm `gopKetQua` → Time-driven → Day timer → 1–2 giờ sáng.

## 6. Bật đồng bộ trong app
1. Trong kho `cang-goi-tin`, mở `cau-hinh.js` → bút chì (Edit) → điền `clientId` và `relay` (Web app URL) → Commit.
2. Đợi 1–2 phút, mở lại trang. Đầu khung câu hỏi hiện nút **Đăng nhập Google**.

## 7. Kiểm tra
1. Máy tính: đăng nhập Google, làm một lượt 10 câu → thanh trên cùng báo "Đã lưu tiến độ lúc …".
2. Kho `cang-goi-tin-data` → thư mục `tiendo/` có một tệp `<mã băm>.json`.
3. Điện thoại: mở trang, đăng nhập cùng tài khoản → nguyên liệu, trang phục, tiến độ giống máy tính.
4. Máy phòng tin dùng chung: học sinh bấm **Đăng xuất** khi xong; máy được xoá sạch cho bạn sau.

## Lưu ý
- Nếu học sinh dùng tài khoản Google do trường cấp (Google Workspace for Education), quản trị viên của trường có thể chặn ứng dụng bên ngoài; khi đó dùng Gmail cá nhân hoặc nhờ quản trị viên cho phép.
- Sửa app sau này: chỉ thay `index.html`; `cau-hinh.js` giữ nguyên.
- Mỗi lần sửa `Code.gs`: **Deploy → Manage deployments → Edit → Version: New version** (giữ nguyên địa chỉ URL).
