# 🕶️ Smart Glass for Blind: Judging Environment and Directing

An AI-powered assistive system that combines **YOLOv8 object detection** and **MiDaS depth estimation** to help visually impaired users understand their surroundings through real-time environment analysis.

---

## ⭐ **Overview**

This project aims to enhance mobility and safety for visually impaired individuals using affordable computer-vision–based smart glasses. A camera captures the live environment, **YOLOv8** detects objects, and **MiDaS** estimates their relative depth. The system provides real-time information about *what* an object is and *how far* it is, enabling safer navigation.

The project is built using Python, OpenCV, PyTorch, Ultralytics YOLO, and Intel MiDaS.

---

## 🚀 **Key Features**

* **Real-time object detection** using YOLOv8n
* **Monocular depth estimation** using MiDaS (DPT-Large / Hybrid / Small)
* **Distance calculation** for each detected object
* **Custom-trained YOLO model** using COCO data (mouse + book classes)
* **High-speed inference (1.88ms per frame)** suitable for live usage
* Integrated workflow for **image testing**, **webcam input**, and **result visualization**

---

## 🧠 **System Architecture**

```
Camera → Frame Preprocessing
       → YOLOv8 Object Detection → Bounding Boxes + Labels
       → MiDaS Depth Estimation → Depth Map
       → Distance Calculation → Final Overlay (Boxes + Distance)
       → Display/Feedback
```

---

## 📦 **Dataset Preparation**

Based on your report:

* Used **COCO 2017** dataset
* Filtered classes: **mouse**, **book**
* Downloaded using COCO API
* Train/Test split: **80/20**
* Total used:

  * **1500 training images**
  * **376 validation images**
* YOLO-formatted annotations auto-generated
* Custom YAML file created for training

---

## 🤖 **Models Used**

### 🔹 **YOLOv8 (Ultralytics)**

* Backbone: CSPDarknet53
* Neck: PANet
* Advantages: High speed, accurate bounding boxes
* Best performing variant: **YOLOv8n** (fast with good mAP)

### 🔹 **MiDaS (Intel ISL)**

* Monocular depth estimation
* Produces relative depth map
* Works well across diverse environments
* Computes distance for each detected object bounding box

---

## 🛠️ **Methodology (Simplified)**

1. Load and filter COCO dataset for selected categories
2. Preprocess images
3. Train YOLOv8 using transfer learning
4. Load MiDaS for depth estimation
5. Run inference on images/webcam
6. Convert depth map into meaningful distance values
7. Overlay depth + labels on image output
8. Display or save results

This aligns with the **Methodology section (pages 10–13)** of your PDF.

---

## 📊 **Performance Results**

From your report:

* **F1 Score:** 0.74 @ confidence 0.269
* **Precision:** 80.1%
* **Recall:** 69.3%
* **mAP@0.5:** 0.766
* **Inference Speed:** 1.88 ms per frame
* **Depth estimation:** Reliable relative depth maps with clear gradients

These results demonstrate suitability for real-time assistive use.

---

## 📷 **Sample Outputs**

### ✔ YOLOv8 detection on custom dataset

* Mouse/book detection
* High-confidence bounding boxes
* Consistent predictions across multiple test images

### ✔ MiDaS depth maps

* Clear foreground–background separation
* Relative depth used to compute target distance

---

## 🧪 **How to Run the Project**

### 1️⃣ Install requirements:

```
pip install ultralytics
pip install opencv-python
pip install torch torchvision
pip install timm
```

### 2️⃣ Run object detection + depth estimation:

```
python smart_glasses.py
```

### 3️⃣ Update paths in code:

* YOLO weights → `best.pt`
* Image path → `pic1.png` or webcam input

---

## ⚠️ **Challenges (from PDF)**

### 1. **Imbalanced Dataset**

* Book class underrepresented
* YOLO confusion matrix showed missing entries
* Required dataset rebalancing

### 2. **Real-time Lag**

Caused by:

* CPU-only inference
* High-resolution frames
* Non-optimized models

**Solutions:**

* Lower resolution (320×320)
* Use FP16
* Skip alternate frames
* Enable GPU

---

## 🔮 **Future Scope**

* Integrate audio feedback for blind users
* Add vibration cues in smart glasses frame
* GPS-based outdoor navigation
* Hardware prototype with Raspberry Pi 5
* ONNX conversion for edge deployment

---

## 👩‍💻 Team Members

* **Protima Basak**
* **Saachi Sharma**
* **Mili Zankat**

**Guide:** Dr. Sameer Sayyad
Symbiosis Institute of Technology
