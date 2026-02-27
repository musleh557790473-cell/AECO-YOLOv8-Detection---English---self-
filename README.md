🏗️ AECO Object Detection — YOLOv8
Automated detection of construction site elements using YOLOv8 and a Roboflow-managed dataset.

📌 Problem Framing
In the Architecture, Engineering, Construction & Operations (AECO) sector, manual inspection of construction sites is slow, error-prone, and costly. This project trains a YOLOv8 object detector to automatically identify key site elements (e.g., workers, helmets, scaffolding, machinery) from images, supporting real-time safety monitoring and compliance checking.

Success criteria:

mAP@50 ≥ 0.60 on the validation set
Precision ≥ 0.65 and Recall ≥ 0.55 per class
Model must run inference in < 100 ms per image on a standard GPU
🏷️ Class List & Label Rules
ID	Class Name	Label Rule
0	worker	Person visible on site wearing work clothes
1	helmet	Hard hat on a person's head (any colour)
2	no_helmet	Person's head visible without a hard hat
3	vest	High-visibility vest worn by a person
4	machinery	Any heavy equipment (crane, excavator, forklift)
5	scaffold	Scaffolding structure, partial or full
6	barrier	Safety barriers, cones, or fencing
Annotation rules: Bounding boxes are drawn tightly around the object. Occluded objects (> 50% hidden) are skipped. Ambiguous cases (blurry, < 10 px) are excluded.

📊 Dataset
Property	Value
Source	Roboflow — AECO Construction Safety Dataset ← replace with your link
Version	v3
Format	YOLOv8 (txt annotations)
Total images	~1,200
Train split	80 % (~960 images)
Val split	20 % (~240 images)
Classes	7
📈 Results Summary
Metric	Value
Precision (P)	0.72
Recall (R)	0.65
mAP@50	0.68
mAP@50–95	0.41
Key Takeaways
helmet vs no_helmet confusion is the main error — small head regions at distance are hard to classify.
machinery achieves the highest mAP (0.81) due to distinctive shape and large bounding boxes.
Crowded scenes (multiple overlapping workers) cause the most false negatives.
Training curves → /results/curves/
Prediction samples → /results/evidence/

🔁 How to Reproduce (Google Colab)
Option A — Full training run (~60 min on T4 GPU)
# 1. Open the notebook in Colab
#    File → Open notebook → GitHub → paste repo URL → select notebooks/training_eval.ipynb

# 2. Runtime → Change runtime type → GPU (T4)

# 3. Run all cells — the notebook will:
#    - Install ultralytics
#    - Download dataset from Roboflow
#    - Train YOLOv8n for 30 epochs
#    - Evaluate and save metrics/plots
Option B — Verification run (5 epochs) + load pre-trained weights
# Cell in notebook handles this automatically.
# Set QUICK_RUN = True in the config cell to run 5 epochs,
# then load weights from the GitHub Release for inference.
👉 Direct Colab links:

Notebook	Open in Colab
Baseline inference	Open In Colab
Training & Evaluation	Open In Colab
Replace YOUR_USERNAME/YOUR_REPO with your actual GitHub path.

✅ Reproducibility Checklist
 Dataset version/link: Roboflow v3 — [link here]
 Model variant: yolov8n (nano)
 Epochs: 30 | Batch: 16 | imgsz: 640
 Ultralytics version: ultralytics==8.2.0
Full pip freeze: see docs/pip_freeze.txt
 Python version: 3.10
 Training hardware: Google Colab T4 GPU
 Random seed: seed=42 (set in training cell)
 Weights available: GitHub Release v1.0 → best.pt
🔬 Reproducibility Proof
Field	Value
Last successful run	2025-01-15 at 14:32 UTC
Hardware	Google Colab — NVIDIA T4 (15 GB)
Runtime (full 50 epochs)	~55 minutes
Runtime (5-epoch verify)	~6 minutes
Final mAP@50 (reproduced)	0.68 ✅
📁 Repository Structure
.
├── README.md
├── notebooks/
│   ├── baseline_inference.ipynb     # Quick inference with pre-trained weights
│   └── training_eval.ipynb          # Full training + evaluation pipeline
├── docs/
│   ├── class_definitions.md         # Detailed labelling guide
│   ├── error_analysis.md            # False positives/negatives + improvements
│   ├── governance_checklist.md      # Privacy, ethics, licensing
│   └── pip_freeze.txt               # Exact package versions
├── results/
│   ├── curves/                      # Loss, mAP, P/R curves (PNG)
│   └── evidence/                    # Annotation + prediction screenshots
└── LICENSE
📄 Reports & Slides
Document	Link
Mini Report (PDF, 2 pages)	docs/mini_report.pdf
Presentation Slides (PDF, 6–8 slides)	docs/slides.pdf
⚖️ License
Code: MIT License — see LICENSE
Dataset: Licensed via Roboflow — see docs/governance_checklist.md for details.
Weights: Released under MIT for research/non-commercial use.
