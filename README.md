## 📌 Table of Contents
- <a href="#overview">Overview</a>
- <a href="#Demo">Demo</a>
- <a href="#problem-statement">Problem Statement</a>
- <a href="#tools--technologies">Tools & Technologies</a>
- <a href="#Result">Results</a>
- <a href="#Deployment">Deployment</a>
- <a href="#future-work">Future Work</a>
- <a href="#Methodology">Methodology</a>

# 🕶️ Smart Glass for Blind: Judging Environment and Directing

An AI-powered assistive system that combines **YOLOv8 object detection** and **MiDaS depth estimation** to help visually impaired users understand their surroundings through real-time environment analysis.

---

<h3><a class="anchor" id="Demo"></a>Demo</h3>

> 📹 **Demo Video:** *(Add your GitHub video link here)*

```
https://github.com/user-attachments/assets/your-demo-video
```

### Project Screenshots

<!-- Replace these with your own screenshots -->

![Detection Result](images/output1.png)

![Depth Estimation](images/output2.png)

![Final Output](images/output3.png)

---

<h3><a class="anchor" id="overview"></a>Overview</h3>

**Smart Glass for Blind: Judging Environment and Directing** is an AI-powered assistive vision system designed to improve mobility and safety for visually impaired individuals.

The system captures real-time images using a camera, detects surrounding objects with **YOLOv8**, estimates their relative distance using **Intel MiDaS**, and displays the object labels along with depth information. This enables users to understand both **what objects are present** and **how far they are**, making navigation safer and more intuitive.

The project is developed using **Python**, **OpenCV**, **PyTorch**, **Ultralytics YOLOv8**, and **Intel MiDaS**.

---

<h3><a class="anchor" id="problem-statement"></a>Problem Statement</h3>

Visually impaired individuals often face challenges in understanding and navigating their surroundings due to limited environmental awareness. Traditional assistive devices provide limited contextual information and often cannot identify nearby objects or estimate their distance.

This project addresses these challenges by:

- Detecting surrounding objects in real time
- Estimating the relative distance of detected objects
- Providing visual information suitable for future audio or haptic feedback
- Enhancing independent and safer navigation using AI-powered computer vision

---

<h3><a class="anchor" id="tools--technologies"></a>Tools & Technologies</h3>

| Category | Tools Used |
|-----------|------------|
| Language | Python |
| Computer Vision | OpenCV |
| Deep Learning | PyTorch |
| Object Detection | Ultralytics YOLOv8n |
| Depth Estimation | Intel MiDaS |
| Dataset | COCO 2017 (Filtered) |
| Model Training | Transfer Learning |
| Visualization | Matplotlib |

---

<h3><a class="anchor" id="Result"></a>Results</h3>

Successfully achieved:

- Real-time object detection using YOLOv8n
- Monocular depth estimation using Intel MiDaS
- Distance estimation for detected objects
- Custom-trained object detection model (Mouse & Book)
- Real-time visualization of object labels and distances
- High-speed inference suitable for assistive applications

### Performance Metrics

| Metric | Value |
|---------|-------|
| Precision | 80.1% |
| Recall | 69.3% |
| F1 Score | 0.74 |
| mAP@0.5 | 0.766 |
| Inference Speed | 1.88 ms/frame |

---

<h3><a class="anchor" id="Deployment"></a>Deployment</h3>

### Install Dependencies

```bash
pip install ultralytics
pip install opencv-python
pip install torch torchvision
pip install timm
```

### Run the Project

```bash
python smart_glasses.py
```

### Update the Following Paths

- YOLO weights → `best.pt`
- Input image → `pic1.png`
- Or enable webcam input inside the script

---

<h3><a class="anchor" id="future-work"></a>Future Work</h3>

- Audio feedback for visually impaired users
- Haptic vibration alerts through smart glasses
- GPS-assisted outdoor navigation
- Raspberry Pi 5 hardware implementation
- Edge deployment using ONNX/TensorRT
- Support for additional object categories
- Improved depth estimation accuracy
- Real-time voice assistant integration

---

<h3><a class="anchor" id="Methodology"></a>Methodology</h3>

```text
Step 1: Image Acquisition
- Capture live webcam feed
- Or load input image

Step 2: Image Preprocessing
- Resize image
- Normalize input
- Prepare frame for inference

Step 3: Object Detection
Input Image
        ↓
YOLOv8 Object Detection
        ↓
Bounding Boxes + Class Labels

Step 4: Depth Estimation
Input Image
        ↓
MiDaS Model
        ↓
Relative Depth Map

Step 5: Distance Calculation
- Extract depth value from detected object
- Estimate relative distance

Step 6: Result Fusion
- Combine YOLO detections with MiDaS depth
- Overlay bounding boxes, labels, and distance

Step 7: Output Visualization
- Display processed frame
- Save output image if required
```

---

## 📦 Dataset Preparation

- COCO 2017 Dataset
- Filtered Classes:
  - Mouse
  - Book
- Downloaded using COCO API
- YOLO annotation format generated
- Custom YAML configuration created

### Dataset Split

| Dataset | Images |
|----------|--------|
| Training | 1500 |
| Validation | 376 |

---

## 🤖 Models Used

### YOLOv8 (Ultralytics)

- Backbone: CSPDarknet53
- Neck: PANet
- Transfer Learning
- Fast and lightweight YOLOv8n model
- High-speed object detection

### Intel MiDaS

- Monocular depth estimation
- Relative depth prediction
- Supports multiple environments
- Distance estimation for detected objects

---

## 📊 System Architecture

```text
Camera
   │
   ▼
Frame Capture
   │
   ▼
Image Preprocessing
   │
   ▼
YOLOv8 Object Detection
   │
   ├──► Bounding Boxes
   └──► Object Labels
   │
   ▼
MiDaS Depth Estimation
   │
   ▼
Depth Map Generation
   │
   ▼
Distance Calculation
   │
   ▼
Final Overlay
(Object + Distance)
   │
   ▼
Display / Future Audio Feedback
```

---

## ⚠ Challenges

### Dataset Imbalance

- Book class contained fewer samples
- Lower recall for minority class
- Required dataset balancing and augmentation

### Real-Time Performance

Challenges:

- CPU-only inference
- High-resolution input images
- Increased latency

Optimizations:

- Reduced input resolution
- FP16 inference
- Frame skipping
- GPU acceleration

---

## 👩‍💻 Team Members

- **Protima Basak**
- **Saachi Sharma**
- **Mili Zankat**

**Project Guide:** Dr. Sameer Sayyad

**Department:** Robotics & Automation Engineering

**Institute:** Symbiosis Institute of Technology, Pune
