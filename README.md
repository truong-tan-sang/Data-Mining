# Hướng dẫn Cài đặt và Cấu hình Môi trường

Tài liệu này hướng dẫn cách thiết lập môi trường Python với Virtual Environment, cài đặt thư viện và chạy Jupyter Notebook.

---

## 📦 Phần 1: Thiết lập Python Virtual Environment

### 1.1. Tạo Virtual Environment

Mở terminal trong thư mục dự án và chạy lệnh sau:

**Windows (PowerShell/CMD):**
```powershell
python -m venv venv
```

**Linux/MacOS:**
```bash
python3 -m venv venv
```

### 1.2. Kích hoạt Virtual Environment

**Windows (PowerShell):**
```powershell
.\venv\Scripts\Activate.ps1
```

**Windows (CMD):**
```cmd
.\venv\Scripts\activate.bat
```

**Linux/MacOS:**
```bash
source venv/bin/activate
```

> **Lưu ý:** Sau khi kích hoạt thành công, bạn sẽ thấy `(venv)` xuất hiện ở đầu dòng lệnh.

### 1.3. Cài đặt thư viện từ `requirement.txt`

Đảm bảo bạn đã kích hoạt virtual environment, sau đó chạy:

```powershell
pip install -r requirement.txt
```

Lệnh này sẽ cài đặt tất cả các thư viện được liệt kê trong file `requirement.txt`.

### 1.4. Kiểm tra các thư viện đã cài đặt

```powershell
pip list
```

---

## 📓 Phần 2: Chạy Jupyter Notebook với Virtual Environment

### 2.1. Cài đặt Jupyter (nếu chưa có trong requirement.txt)

```powershell
pip install jupyter notebook ipykernel
```

### 2.2. Thêm Virtual Environment vào Jupyter Kernel

```powershell
python -m ipykernel install --user --name=venv --display-name "Python (venv)"
```

### 2.3. Khởi động Jupyter Notebook

**Cách 1: Qua Terminal**
```powershell
jupyter notebook
```

**Cách 2: Sử dụng VS Code**
1. Mở file `.ipynb` trong VS Code
2. Click vào **Select Kernel** ở góc trên bên phải
3. Chọn **Python (venv)** từ danh sách kernel