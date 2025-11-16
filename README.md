# Hướng dẫn Cài đặt và Cấu hình Môi trường

Tài liệu này hướng dẫn cách thiết lập môi trường Python với Virtual Environment, cài đặt thư viện, chạy Jupyter Notebook, và cấu hình LaTeX trong VS Code.

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

### 2.4. Kiểm tra Kernel đang sử dụng

Trong Jupyter Notebook, chạy cell sau để kiểm tra:

```python
import sys
print(sys.executable)
```

Đảm bảo đường dẫn trỏ đến thư mục `venv` của bạn.

---

## 📝 Phần 3: Cấu hình LaTeX trong VS Code

### 3.1. Cài đặt LaTeX Distribution

Trước tiên, bạn cần cài đặt LaTeX distribution:

**Windows:**
- Tải và cài đặt [MiKTeX](https://miktex.org/download)
- Đảm bảo `pdflatex` và `bibtex` có trong PATH

**Linux:**
```bash
sudo apt-get install texlive-full
```

**MacOS:**
```bash
brew install --cask mactex
```

### 3.2. Cài đặt Extension LaTeX Workshop

1. Mở VS Code
2. Vào Extensions (Ctrl+Shift+X)
3. Tìm kiếm **LaTeX Workshop** (by James Yu)
4. Click **Install**

### 3.3. Cấu hình VS Code Settings

Mở file `settings.json` của VS Code (Ctrl+Shift+P → `Preferences: Open User Settings (JSON)`) và thêm cấu hình sau:

```json
{
    "[latex]": {
        "editor.defaultFormatter": "James-Yu.latex-workshop"
    },
    "workbench.editorAssociations": {
        "*.pdf": "latex-workshop-pdf-hook"
    },
    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
    "latex-workshop.synctex.afterBuild.enabled": true,
    "latex-workshop.latex.autoBuild.run": "onSave",
    "latex-workshop.latex.recipes": [
        {
            "name": "pdfLaTeX",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "pdfLaTeX x2 (for references)",
            "tools": [
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "pdfLaTeX → BibTeX → pdfLaTeX x2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
                "%DOCFILE%"
            ]
        }
    ]
}
```

### 3.4. Giải thích các thiết lập LaTeX

| Thiết lập | Mô tả |
|-----------|-------|
| `latex-workshop.view.pdf.viewer` | Hiển thị PDF trong tab của VS Code |
| `latex-workshop.view.pdf.internal.synctex.keybinding` | Double-click để sync giữa PDF và source code |
| `latex-workshop.synctex.afterBuild.enabled` | Tự động sync sau khi build |
| `latex-workshop.latex.autoBuild.run` | Tự động build khi save file |
| `latex-workshop.latex.recipes` | Các công thức build LaTeX (pdfLaTeX, BibTeX, etc.) |
| `latex-workshop.latex.tools` | Định nghĩa các công cụ compile (pdflatex, bibtex) |

### 3.5. Sử dụng LaTeX trong VS Code

1. Mở file `.tex` trong VS Code
2. Nhấn **Ctrl+Alt+B** để build (hoặc save file nếu đã bật auto-build)
3. Nhấn **Ctrl+Alt+V** để xem PDF
4. Double-click vào PDF để jump đến vị trí tương ứng trong code

### 3.6. Build Recipes

- **pdfLaTeX**: Compile đơn giản, phù hợp cho tài liệu không có tài liệu tham khảo
- **pdfLaTeX x2**: Compile 2 lần để cập nhật references và cross-references
- **pdfLaTeX → BibTeX → pdfLaTeX x2**: Compile đầy đủ với bibliography (cho file có `\bibliography{}`)
