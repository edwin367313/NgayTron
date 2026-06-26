# NgàyTrọn — Hướng dẫn tạo file APK

App đã chạy được ngay (mở `www/index.html`). Thư mục này dùng để **build ra file APK** cài trên Android.

Trong môi trường tạo app không tải được Android SDK của Google, nên cách dễ nhất và miễn phí để có APK là **build trên GitHub** (chạy trên máy chủ đám mây, bạn không cần cài gì trên máy mình).

---

## Cách A — Build APK miễn phí trên GitHub (khuyên dùng, không cần cài đặt)

1. Tạo tài khoản tại https://github.com (miễn phí) nếu chưa có.
2. Bấm **New repository** → đặt tên ví dụ `ngaytron` → chọn **Public** → **Create**.
3. Trong repo vừa tạo, bấm **Add file → Upload files**, rồi **kéo thả TẤT CẢ nội dung trong thư mục này lên** (cả thư mục `www`, `.github`, file `package.json`, `capacitor.config.json`). Bấm **Commit changes**.
4. Vào tab **Actions** của repo. Lần đầu có thể phải bấm nút xanh đồng ý chạy Actions.
5. Workflow **Build APK** sẽ tự chạy (mất khoảng 3–6 phút). Khi xong, bấm vào lần chạy đó.
6. Kéo xuống mục **Artifacts**, tải **NgayTron-APK**. Giải nén ra sẽ có file **app-debug.apk**.
7. Chép file `.apk` đó sang điện thoại Android và mở để cài (Android sẽ hỏi cho phép "cài từ nguồn không xác định" → đồng ý).

> Nếu Actions không tự chạy: vào tab **Actions → Build APK → Run workflow**.

---

## Cách B — Build trên máy của bạn (nếu rành kỹ thuật)

Cần cài sẵn: **Node.js**, **Java 17 (JDK)**, **Android Studio / Android SDK**.

```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

File APK nằm ở: `android/app/build/outputs/apk/debug/app-debug.apk`

---

## Chạy trên PC (Windows / Mac / Linux)

App là web offline nên trên PC dùng theo 1 trong 2 cách:

- **Đơn giản nhất:** mở thẳng file `www/index.html` bằng trình duyệt (Chrome/Edge). Dữ liệu vẫn lưu trên máy.
- **Như một app riêng:** mở `www/index.html` trong Chrome/Edge → menu ⋮ → **Cài đặt ứng dụng này** (Install). Nó sẽ thành cửa sổ app riêng, có icon, chạy offline.

> Muốn file `.exe` cho Windows thì cần build bằng Electron/Tauri (phức tạp hơn). Với nhu cầu hằng ngày, cài dạng app từ Chrome ở trên là đủ và gọn nhẹ.

---

## Lưu ý về báo thức / nhắc việc

- Báo thức và nhắc việc kêu (chuông + rung + thông báo) **khi app đang mở**. Đây là giới hạn của app dạng web đóng gói.
- Nếu sau này bạn muốn báo thức kêu cả khi **đã tắt app**, cần thêm plugin native `@capacitor/local-notifications` và chỉnh thêm code — mình có thể hướng dẫn riêng khi bạn cần.

## Dữ liệu của bạn

Toàn bộ dữ liệu (công việc, ghi chú, báo thức) lưu **ngay trên thiết bị**, không gửi lên mạng. Trong app có nút **Cài đặt ⚙️ → Xuất / Nhập dữ liệu** để sao lưu và chuyển sang máy khác.
