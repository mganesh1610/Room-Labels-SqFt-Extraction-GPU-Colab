# 🧾 FloorPlan OCR Notebook — Room Labels + SqFt Extraction (Audit-Ready CSV)

This repo contains a **Google Colab / Jupyter Notebook** pipeline that extracts **room labels + areas (sqft)** from floor plan images (colored or black/white) and exports **clean label → sqft** pairs to CSV.

✅ **Impact:** Replaced a ~2-week manual extraction workflow with an automated process completed in ~2 days for **4K+ rooms** across **3 buildings**:
- **Building A:** 4 floors  
- **Building B:** 4 floors  
- **Building C:** 6 floors  

---

## ✨ What it does

Extracts pairs like:

| label   | sqft |
|--------|------|
| AL1-57 | 614  |
| AA     | 448  |
| AG     | 227  |

Supports:
- **Main rooms:** `AL…` patterns (e.g., `AL1-57`)
- **Subrooms/zones:** `AA..AZ` and `A4` style labels (e.g., `AA`, `AB`, `A4`)
- **Strict parsing using `SF` suffix** to reduce false positives (e.g., avoids `46` from `464sf`)

---

## 🧠 Approach (AI-assisted OCR)

This notebook uses **Tesseract’s LSTM-based OCR engine** (via `pytesseract`) plus a floorplan-specific preprocessing strategy:

- **Strong CV preprocessing:** upscale (default **6×**), grayscale, contrast/sharpness boost, Otsu binarization, stroke thickening  
- **Dense tiling:** **6×6** with overlap to capture small labels  
- **Multi-rotation OCR:** **0°, 90°, 270°** to catch vertical text  
- **Dual OCR outputs:** full text + word-level tokens (with confidence filtering)  
- **Auditability:** saves raw OCR logs for QA/debugging

---

## 📦 Outputs

After running the notebook:

- `outputs/floorplan_preprocessed_strong.png` — preprocessed image (QA/debug)
- `outputs/tesseract_all_text.txt` — raw OCR logs (audit/debug)
- `outputs/floorplan_label_sqft_pairs.csv` — final extracted dataset

---

## ▶️ How to run (Google Colab)

1. Open **`OCR_Extract.ipynb`** in Google Colab  
2. Run cells **top to bottom**  
3. Update the image source (file path / Drive ID) inside the notebook if needed  
4. Download the CSV from `outputs/`

---

