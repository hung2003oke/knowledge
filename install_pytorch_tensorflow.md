Dưới đây là hướng dẫn cài đặt PyTorch và TensorFlow phiên bản GPU trên máy Windows với GPU (GPU được thử trong bài viết là: RTX 2050)

## Bước 1: Cài đặt CUDA và cuDNN

Trước khi cài đặt PyTorch GPU, bạn cần cài đặt CUDA và cuDNN tương thích với GPU của mình

### 1. Cài đặt CUDA:

Kiểm tra xem GPU có được bật hay không?
```bash
nvidia-smi
```

Một số máy sẽ bị thiếu drive GPU, khi này sẽ phải tải và cài đặt drive  
Link: https://www.nvidia.com/en-us/drivers/

Truy cập trang web chính thức của CUDA và tải xuống phiên bản tương thích với GPU  
Link: https://developer.nvidia.com/cuda-toolkit

Với bài viết này, mình sẽ sử dụng phiên bản 11.2.  
Link: https://developer.nvidia.com/cuda-11.2.0-download-archive

Cài đặt CUDA (tải và chạy file .exe).

Kiểm tra đã cài đặt thành công:
```bash
nvcc --version
```

### 2. Cài đặt cuDNN:

Truy cập trang web của cuDNN và tải phiên bản cuDNN tương thích với CUDA bạn đã cài.  
link: https://developer.nvidia.com/rdp/cudnn-archive

Tạo thư mục mới `cuDNN` trong thư mục 'C:\Program Files'. Giải nén file zip vào thư mục mới này.

Sau đó, thêm đường dẫn các thư mục `bin`, `include`, và `lib/x64` vào đường dẫn PATH của hệ thống bằng cách
Chuột phải vào nút Start (biểu tương Window ở thanh Task bar dưới cùng) > Chọn vào `System` ở gần trên cùng > Tìm và chọn vào nút `Advanced System Settings` khi này sẽ có 1 cửa sổ nhỏ mở ra >
Mở tab `Advanced` > Chọn vào nút `Environment Variables` ở gần dưới, khi này sẽ mở ra cửa số mới > Ở khu vực `System Variables` bên dưới, kéo xuống và click đúp vào dòng `PATH`.
Nhấn nút `New` để thêm các đường dẫn. Khi này đường dẫn các PATH sẽ có dạng như sau (phiên bản của cuDNN có thể khác nhau):
```
C:\Program Files\cuDNN\cudnn-windows-x86_64-8.9.7.29_cuda11-archive\bin
C:\Program Files\cuDNN\cudnn-windows-x86_64-8.9.7.29_cuda11-archive\include
C:\Program Files\cuDNN\cudnn-windows-x86_64-8.9.7.29_cuda11-archive\lib\x64
```

## Bước 2. Tạo môi trường ảo Python

Bạn có thể sử dụng các môi trường ảo như Conda venv

### 1. Conda

Bạn có thể tải và cài đặt Conda hoặc Miniconda.

| Mục đích | Lệnh |
| -------- | ---- |
| Tạo một môi trường mới tên là my_env với Python 3.10 | conda create --name my_env python=3.10 |
| Kích hoạt môi trường | conda activate my_env |
| Liệt kê các môi trường | conda env list |
| Cài thư viện | conda install numpy |
| Cài thư viện bằng pip | pip install numpy |
| Xuất môi trường ra file | conda env export > environment.yml |
| Phục hồi môi trường từ file | conda env create -f environment.yml |
| Xóa môi trường | conda remove --name my_env --all |


### 2. venv

Python tích hợp sẵn công cụ `venv`, vì vậy không cần cài đặt thêm bất kỳ thư viện nào.

| Mục đích | Lệnh |
| -------- | ---- |
| Tạo một môi trường mới tên là my_env (không chọn được phiên bản python) | python -m venv my_env |
| Kích hoạt môi trường | my_env\Scripts\activate |
| Kích hoạt môi trường (macOS/Linux) | source my_env/bin/activate |
| Cài thư viện | pip install numpy |
| Xuất môi trường ra file | pip freeze > requirements.txt |
| Phục hồi môi trường từ file | pip install -r requirements.txt |
| Hủy kích hoạt môi trường | deactivate |
| Xóa môi trường | Xóa thư mục `my_env` |

## Bước 3. Cài đặt PyTorch

Truy cập PyTorch Get Started để chọn đúng phiên bản.  
link: https://pytorch.org/

Lệnh cài đặt PyTorch GPU cho CUDA 11.2
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu112
```

Kiểm tra cài đặt
```python
import torch
print(torch.cuda.is_available())  # In ra True nếu cài đặt đúng
```

## Bước 4. Cài đặt TensorFlow

Đối với TensorFlow cần phải chọn phiên bản phù hợp với phiên bản cuda và python. Bạn cần phải kiểm tra và chọn phiên bản cho đúng.
Link: https://www.tensorflow.org/install/source#gpu

Lệch cài đặt cho phiên bản TensorFlow 2.8
```bash
pip install tensorflow-gpu==2.8
```

Kiểm tra cài đặt
```python
import tensorflow as tf
print(len(tf.config.experimental.list_physical_devices('GPU')) > 0)  # In ra True nếu cài đặt đúng
```
