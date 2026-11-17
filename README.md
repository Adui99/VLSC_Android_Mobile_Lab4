# Lab 4B: Kotlin Coroutines

## Thông tin Sinh viên
* **Họ và tên:** Hoàng Khương Duy
* **MSSV:** 2500114656

---

## Nội dung cơ bản của Bài Lab
Bài thực hành áp dụng **Kotlin Coroutines** để xử lý bất đồng bộ trên Android, giúp giải quyết tình trạng treo giao diện (lỗi ANR) khi chạy các tác vụ nặng:
* **Đồng hồ đếm ngược:** Chạy liên tục 60 giây trên luồng chính bằng `lifecycleScope.launch(Dispatchers.Main)` mà không làm gián đoạn giao diện[cite: 6].
* **Mô phỏng chặn luồng (Gây lỗi ANR):** Sử dụng `Thread.sleep(5000)` trực tiếp trên Main Thread khiến giao diện bị đơ và `ProgressBar` ngừng xoay trong 5 giây[cite: 5].
* **Xử lý bất đồng bộ với Coroutines:** Đẩy tác vụ nặng sang luồng nền thông qua `lifecycleScope.launch(Dispatchers.IO)` kết hợp hàm `suspend` và `delay(5000)`, sau đó cập nhật kết quả lên giao diện an toàn bằng `withContext(Dispatchers.Main)`[cite: 5, 6].

---

## Hình ảnh Minh họa
**1. Trạng thái khởi động (Đồng hồ đếm ngược và ProgressBar chạy bình thường)**
<img width="692" height="841" alt="image" src="https://github.com/user-attachments/assets/a7cab71c-0ac6-4eae-83fe-55af970cdad6" />
**2. Khi nhấn nút chặn luồng (Giao diện bị đơ, ProgressBar đứng im trong 5 giây)**
<img width="687" height="801" alt="image" src="https://github.com/user-attachments/assets/9c8bf728-3050-493c-93a3-f2ac5ddf9069" />
**3. Khi nhấn nút chạy Coroutines (Xử lý ngầm hoàn tất, giao diện vẫn mượt mà)**
<img width="688" height="847" alt="image" src="https://github.com/user-attachments/assets/2cc2026e-db47-41c2-bc19-a0a5deb2680b" />
