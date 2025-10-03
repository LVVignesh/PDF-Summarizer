# PDF-Summarizer
Generative AI project to summarize PDFs.

# 📄 PDF Summarizer using Generative AI

[![Python](https://img.shields.io/badge/Python-3.12-blue)](https://www.python.org/)  
[![Hugging Face](https://img.shields.io/badge/HuggingFace-Transformers-orange)](https://huggingface.co/transformers/)  

This project uses **Generative AI** to automatically summarize PDF documents into concise notes.  
It leverages **Hugging Face transformers** and Python to create an easy-to-use PDF summarizer.

---

## 🚀 Features
- Upload a PDF file (typed/digital text).  
- Extract text from PDF pages.  
- Split long documents into manageable chunks for AI processing.  
- Summarize each chunk using **transformer models**.  
- Combine summaries into a final concise summary.  
- Save the summary as a text file (`summary.txt`).  
- Optional: OCR support for **handwritten or scanned PDFs**.  

---

## 🛠️ Technologies Used
- **Python 3**  
- [PyPDF2](https://pypi.org/project/PyPDF2/) – extract text from typed PDFs  
- [transformers](https://huggingface.co/transformers/) – AI summarization  
- [pytesseract](https://pypi.org/project/pytesseract/) *(optional for handwritten PDFs)*  
- [pdf2image](https://pypi.org/project/pdf2image/) *(optional for scanned PDFs)*  

---

## ⚙️ Step-by-Step Guide

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/yourusername/PDF-Summarizer.git
cd PDF-Summarizer
2️⃣ Install Dependencies
bash
Copy code
pip install -r requirements.txt
3️⃣ Provide Your PDF
VS Code / Local: Set pdf_file = "path/to/your/file.pdf" in the code.

Google Colab: Use the file upload dialog:

python
Copy code
from google.colab import files
uploaded = files.upload()
pdf_file = list(uploaded.keys())[0]
4️⃣ Extract Text from PDF
Use PyPDF2 to extract text from typed PDFs.

Optional: Use OCR (pytesseract + pdf2image) for handwritten/scanned PDFs.

5️⃣ Split Text into Chunks
Split text into smaller chunks (~500–800 words) to stay within model token limits.

6️⃣ Summarize Each Chunk
python
Copy code
from transformers import pipeline
summarizer = pipeline("summarization", model="facebook/bart-large-cnn")

summaries = []
for chunk in chunks:
    if not chunk.strip():
        continue
    try:
        summary = summarizer(chunk, max_length=500, min_length=200, do_sample=False)
        summaries.append(summary[0]['summary_text'])
    except Exception as e:
        print(f"Skipping a chunk due to error: {e}")
7️⃣ Combine Summaries
Merge all chunk summaries into a final summary:

python
Copy code
final_summary = " ".join(summaries)
8️⃣ Save Summary
python
Copy code
with open("summary.txt", "w") as f:
    f.write(final_summary)
Download: In Colab use files.download("summary.txt").

VS Code / Local: File is saved locally.
