
# 🎨 Manga Editor – Desktop App

Professional desktop tool for **cleaning, improving, and editing manga/webtoon pages**.

### ✨ Key Features

* 🧹 **Clean Pages** – Remove noise & artifacts
* 🎨 **Enhance Images** – Improve quality & readability
* 💬 **Speech Bubbles** – Detect for editing
* 🔐 **Secure Processing** – Sensitive data handled safely
* 🖥️ **Windows App** – No browser needed

### 🚀 Install

1. Go to [Releases](https://github.com/abderhmandev-dot/manga_editor_studio/releases)
2. Download `MangaEditor.exe`
3. Run directly (no install required)

### 🔄 Updates

* App checks for new versions automatically
* Simply download the latest release to update



---


----------------------


Here's a cleaner and more readable version of the setup guide:

---

# AI Environments (CPU/GPU) Setup

This project isolates heavy AI dependencies **outside** the main application environment and **EXE build** to keep the EXE small, make updates easier, and enable automatic **GPU/CPU fallback**.

---

## Installation Directory Layout

The application uses virtual environments located at:

```
%LOCALAPPDATA%\MangaEditorV2\python\
  venv-cpu\    # For CPU-only AI stack
  venv-gpu\    # For CUDA-enabled GPU stack
  venv-bubble\ # Optional for bubble detection
```

---

## Environments Overview

### CPU Environment (`venv-cpu`)

Installed Packages (CPU-only):

* `torch`
* `torchvision`
* `ultralytics` (YOLO)
* `easyocr`
* `opencv-python`
* `simple-lama-inpainting`
* Other dependencies like `numpy`, `pillow`

### GPU Environment (`venv-gpu`)

Installed Packages (CUDA-enabled):

* `torch` + CUDA wheels
* `torchvision` + CUDA wheels
* `ultralytics` (YOLO)
* `easyocr`
* `opencv-python`
* `simple-lama-inpainting`

> **Note**: CPU and GPU versions of `torch` should **NOT** be in the same virtual environment.

### Optional Bubble Environment (`venv-bubble`)

For bubble detection, create a dedicated environment:

* `torch`
* `torchvision`
* `ultralytics`
* `easyocr`
* `opencv-python`

---

## How the App Selects Python Environments

The pipeline uses the following resolver to select the appropriate Python environment:

1. **AppData venvs** (`venv-gpu`, `venv-cpu`, `venv-bubble`)
2. **Portable Python** (if configured)
3. **Local `venv-gpu`** (if present)
4. **Project-local `.venv`** (for small utility dependencies)
5. **System Python** (`sys.executable`)

The resolver checks for the required modules to ensure it doesn't select a broken environment.

---

## Installation Instructions

### Prerequisites

* Windows 10/11
* Python 3.11 (recommended)
* For GPU: NVIDIA drivers installed

Check GPU driver with:

```powershell
nvidia-smi
```

---

### 1) Create `venv-cpu`

```powershell
py -3.11 -m venv "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu"
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\python.exe" -m pip install -U pip
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\pip.exe" install torch torchvision
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\pip.exe" install ultralytics easyocr opencv-python simple-lama-inpainting
```

Quick Verify:

```powershell
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\python.exe" -c "import torch, ultralytics, easyocr, cv2, numpy; print('OK')"
```

---

### 2) Create `venv-gpu` (CUDA)

If you want GPU support, follow these steps:

```powershell
py -3.11 -m venv "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu"
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\python.exe" -m pip install -U pip
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\pip.exe" install torch torchvision --index-url https://download.pytorch.org/whl/cu124
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\pip.exe" install ultralytics easyocr opencv-python simple-lama-inpainting
```

Verify CUDA:

```powershell
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\python.exe" -c "import torch; print(torch.cuda.is_available())"
```

---

## Logging

To view package origin logs during the pipeline:

* Shows which Python executables are being used
* Logs package imports and their versions

Disable logs with:

```powershell
$env:MANGA_LOG_PY_INFO="0"
```

---

## Size Considerations

AI dependencies like `torch` and `ultralytics` are large, but storing them in LocalAppData avoids bloating the EXE.

---

## Troubleshooting

### 1) App selects `venv-gpu` but imports fail

This suggests missing packages in the selected environment. Install the required packages, or rename/remove the environment to trigger a fallback.

### 2) GPU detected but Torch reports CUDA as unavailable

Ensure you've installed CUDA-enabled PyTorch wheels in `venv-gpu`.

Verify with:

```powershell
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\python.exe" -c "import torch; print(torch.cuda.is_available())"
```

---

## Security Note

**Never hardcode API keys** in the repository or application.

---

This version is simplified, well-spaced, and easy to follow.
