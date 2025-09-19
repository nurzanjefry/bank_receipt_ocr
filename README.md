# OCR Extraction with PaddleOCR

This project demonstrates how to use [PaddleOCR](https://github.com/PaddlePaddle/PaddleOCR) inside a Jupyter Notebook to extract structured information from images (e.g., receipts, transaction slips, or bank confirmations).  

The notebook processes an image using OCR, then maps detected text into a structured dictionary with specific keys such as **Status**, **Transaction date**, and **Beneficiary Name**.

---

## Features

- Performs OCR (Optical Character Recognition) on images using PaddleOCR.
- Supports English text extraction (`lang='en'`).
- Filters and structures OCR results into a key-value dictionary.
- Prints both **raw OCR results** (with confidence scores and bounding boxes) and **structured output**.

---

## Example Code

```python
from paddleocr import PaddleOCR

ocr = PaddleOCR(use_textline_orientation=True, lang='en')
img_path = "converted_image.png"

results = ocr.predict(img_path)

structured = {}

# Define the keys you care about
keys = [
    "Status:",
    "Reference number:",
    "Transaction date:",
    "Amount:",
    "Beneficiary Name:",
    "Receiving Bank:",
    "Beneficiary Account Number:",
    "Recipient Reference:"
]

for res in results:
    texts = res['rec_texts']
    scores = res['rec_scores']
    polys = res['rec_polys']

    # Print raw OCR results
    for text, score, box in zip(texts, scores, polys):
        print(f"{text} (conf: {score:.2f}) at {box.tolist()}")

    # Build structured dictionary
    for i, text in enumerate(texts):
        if text in keys and i + 1 < len(texts):
            structured[text.replace(":", "").strip()] = texts[i+1]

print("\nStructured output:")
print(structured)
```

---

## Example Output

**Raw OCR results (snippet):**
```
Status: (conf: 0.98) at [[50,20],[200,20],[200,50],[50,50]]
Successful (conf: 0.97) at [[210,20],[350,20],[350,50],[210,50]]
...
```

**Structured output:**
```python
{
    "Status": "Successful",
    "Reference number": "123456789",
    "Transaction date": "2025-09-18",
    "Amount": "RM 250.00",
    "Beneficiary Name": "John Doe",
    "Receiving Bank": "ABC Bank",
    "Beneficiary Account Number": "123-456-789",
    "Recipient Reference": "Invoice 001"
}
```

---

## Requirements

- Python 3.8+
- Jupyter Notebook
- PaddleOCR

Install dependencies:
```bash
pip install paddleocr
pip install paddlepaddle  # required backend
```

---

## How to Use

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```
2. Navigate to the project folder and launch Jupyter:
   ```bash
   jupyter notebook
   ```
3. Open the notebook and run the cells.
4. Replace `converted_image.png` with your own image.

---

## Notes

- Accuracy depends on image quality and clarity of text.
- You can expand the `keys` list if you need to capture more fields.
- Works best with structured documents like receipts, invoices, or bank slips.

---

## License

This project is released under the MIT License.
