# OCR
Devnagari_OCR
# Devanagari OCR with Tesseract in Python
This project extracts text from scanned documents in Devanagari script using Python and Tesseract OCR.  

## ✅ What You Need

- A MacBook 
- Python 3 installed (most Macs already have it)
- [Homebrew](https://brew.sh) (to install software easily)

#1️ Open Terminal
- Press `Command + Space`, type `Terminal`, and press Enter.

# 2 Install Homebrew (if you don't have it yet):
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 3 Install Tesseract OCR and Devanagari language data:
brew install tesseract
brew install tesseract-lang

# 4  Install Python packages:
pip3 install pytesseract pillow pdf2image
brew install poppler

# 5 How to Convert PDF Pages to Images

This step will let you convert scanned pages of your PDF into individual PNG images, which you can then run OCR on.

---

## A) Create your Python script

First, open a text editor (like VS Code, Sublime Text, or even nano in Terminal) and paste the following code. Replace `X` and `Y` with the page numbers you want to convert (e.g., first_page=11, last_page=15):

```python
from pdf2image import convert_from_path

images = convert_from_path("rajvilas.pdf", dpi=300, first_page=X, last_page=Y)

for i, image in enumerate(images):
    filename = f"page{X + i}.png"
    image.save(filename, "PNG")
    print(f"✅ Saved {filename}")


#6 How to Run OCR on Images

After you have your `pageX.png` image files from the previous step, you can extract text from each page using Tesseract OCR.

---

## 📄 1) Create your OCR script

Open a text editor and create a new file called `run_ocr.py`. Paste the following code into it:

```python
from PIL import Image
import pytesseract

for i in range(11, 16):
    filename = f"page{i}.png"
    print(f"🔍 Running OCR on {filename}...")

    img = Image.open(filename)
    text = pytesseract.image_to_string(img, lang='hin')

    with open(f"output_page{i}.txt", "w", encoding="utf-8") as f:
        f.write(text)

    print(f"✅ Saved extracted text to output_page{i}.txt\n")

#7
python3 run_ocr.py






