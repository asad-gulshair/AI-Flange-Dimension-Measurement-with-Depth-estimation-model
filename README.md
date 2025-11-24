# 🔍 AI-Based Flange Dimension Measurement Using Depth Estimation

This repository contains an experimental AI system for measuring flange dimensions using:
- ✅ YOLOv8 object detection (custom flange model)
- ✅ Depth estimation (Apple DepthPro + MiDaS fallback)
- ✅ Geometry-based measurement from depth maps

This project is provided strictly **for research and educational purposes**.

---

# 📌 Features

### 🔹 1. Flange Detection (YOLOv8)
A custom YOLOv8 model trained on flange datasets is included:
``models/yolov8_flange.pt``

It identifies the flange region and extracts ROI for depth processing.

> ⚠️ **Note:**  
> This YOLO model is shared only for academic research.  
> Do NOT use it for commercial, safety-critical, or production environments.

---

### 🔹 2. Depth Estimation
The notebook uses:

### **Primary Model**
- `apple/DepthPro-hf`  
  - High-quality depth estimation model  
  - Loaded using `DepthProImageProcessorFast` and `DepthProForDepthEstimation`

### **Fallback Model**
- `MiDaS_small`
  - Loaded from Intel-ISL using `torch.hub`  
  - Used automatically if DepthPro fails

---

### 🔹 3. Measurement Pipeline
The system pipeline inside the notebook:

1. Detect flange using `yolov8_flange.pt`
2. Crop ROI
3. Run depth estimation (DepthPro → MiDaS fallback)
4. Smooth / normalize depth map
5. Extract geometric features
6. Measure:
   - Outer Diameter (OD)
   - Inner Diameter (ID)
   - PCD
   - Hole diameter
   - Hole count

7. Save:
   - Raw depth map  
   - Normalized depth  
   - Measurement overlays  
   - Output JSON (if enabled)

All sample results are stored in `/output`.

---

# 📁 Included Files

### ✔ Notebook:  
`Depth Estimation model.ipynb`  
Contains:
- DepthPro inference
- MiDaS fallback
- Visualizations
- Measurement logic

### ✔ Model (to be added manually):
`models/yolov8_flange.pt`

### ✔ Sample Input:
Stored in `/input/`.

### ✔ Sample Output:
Stored in `/output/`.

---

# ▶️ Usage

### 1. Install dependencies
