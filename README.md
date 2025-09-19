# 🧾 Bank Receipt OCR

This project extracts **structured transaction details** from bank receipt images using [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR).  
It automates the process of turning raw OCR text into clean, machine‑readable data for downstream use (validation, storage, or integration into financial systems).

---

## 🚀 Features
- OCR text extraction from receipt images (`.png`, `.jpg`)  
- Handles rotated or skewed text lines with orientation detection  
- Prints raw OCR results with confidence scores and bounding boxes  
- Maps recognized text into a **structured dictionary** of key fields:  
  - Status  
  - Reference number  
  - Transaction date  
  - Amount  
  - Beneficiary Name  
  - Receiving Bank  
  - Beneficiary Account Number  
  - Recipient Reference  

---

## 📂 Project Structure
bank_receipt_ocr/ │ ├── converted_image.png # Example input image ├── main.py # OCR + structuring script ├── requirements.txt # Python dependencies └── README.md # Project documentation

Code

---

## ⚙️ Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/nurzanjefry/bank_receipt_ocr.git
   cd bank_receipt_ocr
Install dependencies:

bash
pip install -r requirements.txt
(Optional) Install GPU version of PaddlePaddle for faster inference:

bash
pip install paddlepaddle-gpu
▶️ Usage
Run the script with your receipt image:

bash
python main.py
Example Output
python
{
  "Status": "Successful",
  "Reference number": "8729043745",
  "Transaction date": "17 Nov 2020 18:20:41",
  "Amount": "RM50.00",
  "Beneficiary Name": "ADVANCE CELL CORPORATION SDN. BHD.",
  "Receiving Bank": "CIMB BANK BERHAD",
  "Beneficiary Account Number": "8600131277",
  "Recipient Reference": "rne ventures"
}
🛠 Requirements
Python 3.8+

PaddleOCR

PaddlePaddle

Install via:

bash
pip install paddleocr
pip install paddlepaddle -U
📌 Notes
Works best with clear, high‑resolution images.

For large‑scale use, consider batch processing and GPU acceleration.

Extendable: add new keys to the keys list in main.py to capture more fields.

📜 License
This project is licensed under the MIT License. See LICENSE for details.