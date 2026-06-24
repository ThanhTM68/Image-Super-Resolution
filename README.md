# Super Resolution ảnh vệ tinh

Đồ án môn Thị giác máy tính về bài toán siêu phân giải ảnh vệ tinh. Notebook so sánh 3 mô hình:

- SRCNN
- EDSR
- Real-ESRGAN

Các mô hình được đánh giá bằng PSNR và SSIM, sau đó hiển thị demo trực quan trên ảnh test.

## Cấu trúc chính

```text
.
├── code_do_an_tgmt.ipynb   # Notebook chính đã sắp xếp lại
├── WorldStrat/             # Dataset vệ tinh gốc
├── Clean_HR_Data/          # Ảnh HR sau khi tiền xử lý
├── Dataset/
│   ├── Train/
│   ├── Val/
│   └── Test/
├── Saved_Models/
│   ├── SCRNN model/x2/
│   ├── EDSR model/x2/
│   └── REAL-ESRGAN model/x2/
├── result/
│   └── Training_Progress/  # Ảnh tiến trình từng Epoch train của srcnn
└── README.md
```

## Tải dữ liệu và mô hình

Do kích thước lớn, dataset và model checkpoint được lưu trên Google Drive.

### Google Drive

- Dataset WorldStrat: https://drive.google.com/drive/folders/1rj0XjjtRpZDzb8QDArGZf814oVsfnDnB?usp=sharing
- Clean_HR_Data (có thể chạy code để tạo): https://drive.google.com/drive/folders/13i9W2jDcPFtRURc0Hfb80Iuz9-yAkO6c?usp=drive_link
- Model Checkpoints: https://drive.google.com/drive/folders/1O_1P4aExB8dHwx_Q7kuS0ZzLUNhsv5b4?usp=sharing

Sau khi tải về, đặt các thư mục theo đúng cấu trúc:

```text
WorldStrat/
Clean_HR_Data/

Saved_Models/
├── SCRNN model/x2/
├── EDSR model/x2/
└── REAL-ESRGAN model/x2/
```

## Nội dung notebook

Notebook được chia thành 11 phần:

1. Import và cấu hình
2. Tiền xử lý dữ liệu
3. Phân tích dữ liệu EDA
4. Dataset và DataLoader
5. Mô hình SRCNN
6. Mô hình EDSR
7. Mô hình Real-ESRGAN
8. Huấn luyện
9. Đánh giá PSNR và SSIM
10. Biểu đồ so sánh kết quả
11. Demo cuối cùng

Pipeline tổng quát:

```text
Raw Image Ảnh Gốc
↓
Tiền xử lý
↓
Tạo LR
↓
Train Mô hình
↓
Output ảnh siêu phân giải (SR)
↓
Đánh giá
```

## Cài đặt môi trường

Yêu cầu:

- Python 3.10
- pip
- Jupyter Notebook hoặc VS Code

Tạo môi trường ảo:

```powershell
py -3.10 -m venv .venv
.\.venv\Scripts\activate
```

Cài thư viện cần thiết:

```powershell
pip install torch torchvision torchaudio
pip install numpy matplotlib pillow scikit-image tqdm lpips piq notebook
```

Nếu dùng GPU, cần cài PyTorch đúng phiên bản CUDA theo máy.

## Cách chạy lần đầu

Mở file:

```text
code_do_an_tgmt.ipynb
```

Chạy lần lượt:

1. Phần 1: Import và cấu hình
2. Phần 2: Tiền xử lý dữ liệu
3. Phần 3: EDA
4. Phần 4: Dataset và DataLoader
5. Phần 5, 6, 7: Định nghĩa mô hình
6. Phần 8: Huấn luyện
7. Phần 9, 10: Đánh giá và vẽ biểu đồ
8. Phần 11: Demo cuối cùng

Lưu ý: Phần tiền xử lý và chia dữ liệu chỉ cần chạy một lần. Nếu dữ liệu đã tồn tại, notebook sẽ tự bỏ qua bước này.

## Cách chạy khi demo

Không cần train lại. Chỉ chạy các phần sau:

1. Phần 1: Import và cấu hình
2. Phần 4.1: Dataset class
3. Phần 4.3: Test DataLoader
4. Phần 5: SRCNN
5. Phần 6: EDSR
6. Phần 7.2: Real-ESRGAN
7. Phần 11.1: Nạp model đã lưu
8. Phần 11.2: Demo cuối cùng

Demo cuối hiển thị:

```text
LR | SRCNN | EDSR | Real-ESRGAN | HR
```

Kèm theo:

- Crop zoom của từng ảnh
- PSNR/SSIM của từng mô hình trên ảnh demo

## Model đã lưu

Các checkpoint chính:

```text
Saved_Models/SCRNN model/x2/best_srcnn_x2.pth
Saved_Models/EDSR model/x2/EDSR_Finetuned_Satellite.pth
Saved_Models/REAL-ESRGAN model/x2/RealESRGAN_Finetuned_Satellite.pth
```

Nếu thiếu model checkpoint, cần chạy lại phần huấn luyện tương ứng trong notebook.
