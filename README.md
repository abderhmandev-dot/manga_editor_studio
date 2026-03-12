
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

أكيد — دي نسخة أقصر وأوضح:

````md
# AI Setup (CPU / GPU)

المشروع بيثبت مكتبات الـ AI الثقيلة خارج البرنامج وملف الـ EXE داخل:

`%LOCALAPPDATA%\MangaEditorV2\python\`

## المجلدات

```text
%LOCALAPPDATA%\MangaEditorV2\python\
  venv-cpu\
  venv-gpu\
  venv-bubble\   # اختياري
````

## الاستخدام

* `venv-cpu` → تشغيل على **CPU**
* `venv-gpu` → تشغيل على **GPU**
* `venv-bubble` → اختياري لعزل Bubble Detection

> مهم: ماينفعش CPU Torch و GPU Torch يبقوا في نفس البيئة.

## ترتيب اختيار البيئة

التطبيق بيحاول يشتغل بالترتيب ده:

1. `venv-gpu`
2. `venv-cpu`
3. `venv-bubble` عند الحاجة
4. Python المحلي أو النظام كـ fallback

وكمان بيتأكد إن الباكدجات المطلوبة موجودة قبل ما يستخدم البيئة.

## إنشاء بيئة CPU

```powershell
py -3.11 -m venv "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu"
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\python.exe" -m pip install -U pip
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\pip.exe" install torch torchvision ultralytics easyocr opencv-python simple-lama-inpainting
```

## إنشاء بيئة GPU

```powershell
py -3.11 -m venv "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu"
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\python.exe" -m pip install -U pip
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\pip.exe" install torch torchvision --index-url https://download.pytorch.org/whl/cu124
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\pip.exe" install ultralytics easyocr opencv-python simple-lama-inpainting
```

## فحص سريع

### CPU

```powershell
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-cpu\Scripts\python.exe" -c "import torch, ultralytics, easyocr, cv2; print('OK')"
```

### GPU

```powershell
& "$env:LOCALAPPDATA\MangaEditorV2\python\venv-gpu\Scripts\python.exe" -c "import torch; print(torch.cuda.is_available())"
```

## ملاحظات

* نقل المكتبات إلى `LocalAppData` بيقلل حجم الـ EXE
* لو `venv-gpu` موجودة لكن ناقصها مكتبات، التطبيق يعمل fallback أو يفشل حسب الحالة
* لو مش محتاج GPU، يكفي `venv-cpu`

```

لو عايز أعملهولك كمان **بأسلوب Documentation احترافي جدًا ومختصر في 10 سطور فقط**.
```
