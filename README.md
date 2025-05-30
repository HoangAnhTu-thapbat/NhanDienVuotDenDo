# Smart City Traffic Violation Detection

## Mô tả
Đây là dự án phát hiện vi phạm giao thông tại vạch dừng đèn tín hiệu trong bối cảnh Smart City. Hệ thống sử dụng hai mô hình YOLO để:

1. Phát hiện và theo dõi ô tô (dùng `yolov8n.pt`).
2. Nhận diện trạng thái đèn giao thông (đỏ/xanh/vàng) (dùng `best_traffic_nano_yolo.pt`).

Khi ô tô vượt vạch dừng khi đèn đỏ, hệ thống sẽ đánh dấu vi phạm, hiển thị thông báo và lưu ảnh bằng chứng.

## Yêu cầu
- Python 3.12+
- Windows / Linux / macOS
- Thư viện Python: `opencv-python`, `torch`, `ultralytics`

## Cài đặt
1. **Tạo virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate    # Linux/Mac
   venv\Scripts\activate     # Windows PowerShell
   ```
2. **Cài dependencies**
   Nếu có `requirements.txt`:
   ```bash
   pip install -r requirements.txt
   ```
   Hoặc cài thủ công:
   ```bash
   pip install opencv-python torch ultralytics
   ```

## Cấu trúc thư mục
```
NhanDienVuotDenDo/
├─ README.md                # File hướng dẫn này
├─ traffic_light_violation.py # Script chính
├─ yolov8n.pt               # Model YOLO nano để phát hiện ô tô
├─ best_traffic_nano_yolo.pt# Model YOLO để nhận diện đèn tín hiệu
├─ hi2.mp4                  # Video mẫu
└─ vi_pham/                 # Thư mục lưu ảnh vi phạm
```

## Cách sử dụng
Chạy script với video mẫu hoặc camera:
```bash
python traffic_light_violation.py --source <đường_dẫn_hoặc_index_camera>
```
- Thay `<đường_dẫn_hoặc_index_camera>` bằng:
  - Đường dẫn tới file MP4, ví dụ `hi2.mp4` hoặc đường dẫn đầy đủ.
  - Số `0`, `1`,... để dùng camera mặc định.

## Chọn vạch dừng (Select Line)
1. Cửa sổ "Select Line" sẽ hiện lên frame đầu tiên.
2. **Click trái** 2 lần để chọn đầu và cuối của vạch dừng.
3. Nhấn **`s`** để xác nhận hoặc **`q`** để hủy và thoát.

## Màn hình Tracking & Violation
- **Bounding box ô tô**: Xanh dương (chuyển đỏ khi vi phạm).
- **Bounding box đèn**: Đỏ/ Xanh/ Vàng tương ứng.
- Góc trên trái hiển thị:
  ```
  Light: <state>
  Violations: <số_lần>
  ```
- Khi vi phạm (
  ô tô vượt vạch khi đèn đỏ):
  - Box ô tô chuyển đỏ.
  - Hiện chữ **VI PHẠM** trong 1 giây.
  - Lưu ảnh crop vào `vi_pham/`.
- Nhấn **`q`** để thoát chương trình.

## Kết quả
- Video đầu ra với bounding box nằm trong `runs/track/` hoặc file `output.mp4`.
- Ảnh vi phạm trong `vi_pham/`.
