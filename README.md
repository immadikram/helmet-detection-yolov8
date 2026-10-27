# Helmet Detection System Using YOLOv8

AIRI Team PITB - AI Internship Task 1

## Overview
Object-detection system that detects **helmet**, **no_helmet** and **person** in images to support basic safety monitoring. Output: bounding boxes, labels and confidence scores.

## Classes
| ID | Class |
|----|-------|
| 0 | helmet |
| 1 | no_helmet |
| 2 | person |

## Dataset
- 176 images uploaded, **157 annotated and used** (109 train / 31 val / 17 test)
- Source: Roboflow Universe "helmet detection" - https://universe.roboflow.com/project-pdvie/helmet-srsz5
- Annotation tool: Roboflow Annotate, exported in YOLOv8 format
- Boxes: helmet 125, no_helmet 57, person 182 (0 invalid label lines)
- Preprocessing: auto-orient, resize 640x640; no augmentation

## Training
YOLOv8n (pretrained), 30 epochs, imgsz 640, batch 8, Google Colab Tesla T4, training time 1.9 minutes.

## Results
| Split | Precision | Recall | mAP@0.5 | mAP@0.5:0.95 |
|---|---|---|---|---|
| Validation | 0.598 | 0.496 | 0.553 | 0.232 |
| Test | 0.585 | 0.586 | 0.630 | 0.312 |

Best class: person. Weakest class: no_helmet (validation). The test set has only 3 no_helmet objects, so that test score is not very reliable.

## Folder structure
```
cv_project/
  dataset/ (images, labels, data.yaml)
  notebooks/training_notebook.ipynb
  outputs/ (training_results, predictions, demo_results)
  models/best.pt
  report/final_report.pdf
  app/app.py
  README.md, requirements.txt
```

## How to run
1. Upload the Roboflow export to `MyDrive/cv_project/raw_export/` and open `notebooks/training_notebook.ipynb` in Google Colab (T4 GPU).
2. Run the cells in order.
3. Demo: `pip install -r requirements.txt` then `streamlit run app/app.py`

## Error analysis (summary)
14 of the 17 test images had differences between prediction and ground truth. Most common problem: missed helmets (9 of the 14 images), plus helmet / no_helmet confusion. See the report for the full table.

## Future improvements
More and more balanced images (especially no_helmet and small helmets), YOLOv8s or longer training, annotation review, low-light examples, Streamlit / Hugging Face demo, video inference.
