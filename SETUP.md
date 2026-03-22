# Hướng dẫn cài đặt và chạy Face AI System Project

## 1. Mô tả chung
Dự án Python này dùng Flask để chạy web service và OpenCV + face_recognition để nhận diện khuôn mặt.
- File chính: `scripts/face_recognition_system.py`
- Template UI: `scripts/templates/index.html`
- Folder lưu ảnh: `uploads/`
- API chính: `/` (web), `/upload`, `/capture`

## 2. Chuẩn bị môi trường (Windows)
1. Mở terminal ở thư mục dự án: `f:\Face AI System Project`
2. Tạo virtualenv (nếu chưa):
   - `python -m venv .venv`
3. Kích hoạt (PowerShell):
   - `& ".\.venv\Scripts\Activate.ps1"`
4. Cập nhật pip:
   - `python -m pip install --upgrade pip`

## 3. Cài thư viện cần thiết
```powershell
pip install flask opencv-python face_recognition pillow numpy
```
Nếu gặp lỗi `face_recognition` thì cài thêm:
```powershell
pip install cmake
pip install dlib
pip install face_recognition
```

## 4. Cấu hình (nếu cần)
- Thư mục lưu ảnh upload đã auto tạo:
  - `UPLOAD_FOLDER = 'uploads'`
- camera index mặc định `droidcam_index = 1`.
- Hoặc dùng `list_camera_indices()` ở đầu file để xác định camera index sẵn.

## 5. Chạy ứng dụng
```powershell
python scripts/face_recognition_system.py
```
Mở `http://127.0.0.1:5000/` trên trình duyệt.

## 6. Dùng tính năng
- Upload ảnh: UI gọi `/upload`, trả JSON vị trí khuôn mặt.
- Capture ảnh: UI gọi `/capture`, nhận base64 image, trả JSON.
- DroidCam realtime: `capture_from_droidcam()` hiển thị window OpenCV, ấn `q` để dừng.

## 7. Ghi chú mở rộng
- Dự án hiện chưa có database, chỉ so sánh face tĩnh.
- Muốn dùng production: cấu hình Gunicorn/Waitress, tắt debug ở Flask.
- Để nhận diện chính xác, cân nhắc thêm feature: ghi encoding vào file, xử lý nhiều khuôn mặt.
