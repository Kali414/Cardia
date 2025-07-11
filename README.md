<!-- Model training repo - https://github.com/Kali414/DRDO_PROJECT -->

# CARDIAA – Camera-Assisted Real-time Detection of Instantaneous Arterial Activity

## Webcam-Based Heart Rate Detection Using Deep Learning

## Overview

CARDIAA is a real-time, non-contact heart rate monitoring system that uses a standard webcam and advanced deep learning techniques to estimate a person’s heart rate (in BPM) by analyzing facial video streams.

Instead of relying on physical sensors or wearable devices, the system leverages subtle changes in skin tone and facial features captured on camera to infer arterial activity. This makes it suitable for applications in telemedicine, fitness monitoring, and continuous health tracking.



---

## Table of Contents

- [Features](#features)
- [Dataset](#dataset)
- [Methodology](#methodology)
- [Model Architecture](#model-architecture)
- [Installation](#installation)
- [Limitations & Ethical Considerations](#limitations--ethical-considerations)
- [References](#references)
- [License](#license)
- [Contact](#contact)

---

## Features

- Non-contact heart rate estimation using webcam video
- Face detection and region-of-interest (ROI) extraction
- Feature extraction from facial video (mean green channel intensity)
- Deep learning model (CNN-LSTM) for temporal signal processing
- End-to-end pipeline: video input → face detection → feature extraction → heart rate prediction

---

## Dataset

- **UBFC-RPPG Dataset**: Public dataset for remote photoplethysmography (rPPG) and heart rate estimation.
- Contains facial videos and synchronized ground truth heart rate (from pulse oximeter).
- [Dataset details and terms](https://sites.google.com/view/ybenezeth/ubfcrppg)
- **Note**: For subjects 21 and 27, facial images must not be published or shared.

**Ground Truth Format:**
- *Dataset 1*: `.xmp` files (Timestep, Heart Rate, SpO2, PPG)
- *Dataset 2*: `ground_truth.txt` (PPG, Heart Rate, Timestep)

 *Download the UBFC-RPPG dataset (see [Dataset](https://drive.google.com/drive/folders/1o0XU4gTIo46YfwaWjIgbtCncc-oF44Xk?usp=drive_link)) .*

---

## Methodology

1. **Data Preprocessing**:
   - Load video frames and corresponding ground truth Heart Rate.
   - Detect face region using Haar cascade.
   - Extract mean green channel intensity from the face region for each frame.
   - Segment features into windows of 24 frames.

2. **Model Training**:
   - Input: Sequence of mean green values (shape: 24, 1).
   - Output: Corresponding Heart Rate values (shape: 24).
   - Model: CNN-LSTM (see below).

3. **Prediction**:
   - For a new webcam video, repeat face detection and feature extraction.
   - Model predicts heart rate for each window.

---

## Model Architecture

- **Input**: Sequence of 24 mean green channel values.
- **CNN Layers**: 1D convolution + max pooling for local feature extraction.
- **LSTM Layers**: Capture temporal dependencies in the signal.
- **Dense Layers**: Regression output for BPM.
- **Regularization**: Dropout and batch normalization.
- **Loss**: Mean Absolute Error (MAE).

---
## 🚀 Installation & Setup Guide

Follow these steps to run the entire project on your local machine.

### 🧾 Prerequisites

Make sure you have the following installed:
- Python (version < 3.11, e.g., 3.10.x)
- Node.js (v14 or higher)
- npm (comes with Node.js)
- Git

---

### 🛠️ Step-by-Step Setup

#### 1. **Clone the Repository**

```bash
git clone https://github.com/Sumandalai/heartRate-website
cd heartRate-website
```

#### 2. **Start the Backend**

```bash
cd backend
# (Optional) Create and activate a virtual environment
python -m venv venv
source venv/bin/activate       # On Windows: venv\Scripts\activate

# Install backend dependencies
pip install -r requirements.txt

# Run the backend server
python app.py
```

Backend will run at: **http://localhost:5000**

#### 3. **Start the Frontend**

Open a new terminal window (keep backend running)

```bash
cd heartRate-website/frontend

# Install frontend dependencies
npm install

# Run the frontend dev server
npm run dev
```

Frontend will run at: **http://localhost:3000**

---

## ✅ Final Check

✅ **Backend**: http://localhost:5000  
✅ **Frontend**: http://localhost:3000  
✅ **Open** http://localhost:3000 in your browser and use the app


**OR Run using Docker Compose:**
```
docker-compose up --build
```
---

## Limitations & Ethical Considerations

- Accuracy may vary with lighting, movement, and camera quality.
- Application can only detect heart rate for 1 people at a time
- Sudden change can cause incorrect heart rate calculation. In the most case, heart rate can be correctly detected after 10 seconds being stable infront of the camera
- Dataset restrictions: Do not publish or share facial images from restricted subjects.
---


## References
- Real Time Heart Rate Monitoring From Facial RGB Color Video Using Webcam by H. Rahman, M.U. Ahmed, S. Begum, P. Funk
- Remote Monitoring of Heart Rate using Multispectral Imaging in Group 2, 18-551, Spring 2015 by Michael Kellman Carnegie (Mellon University), Sophia Zikanova (Carnegie Mellon University) and Bryan Phipps (Carnegie Mellon University)
- Non-contact, automated cardiac pulse measurements using video imaging and blind source separation by Ming-Zher Poh, Daniel J. McDuff, and Rosalind W. Picard
- Camera-based Heart Rate Monitoring by Janus Nørtoft Jensen and Morten Hannemose
---

## License

This project is licensed under the terms of the MIT License. See the [LICENSE](LICENSE) file for details.


---

## Contribution
For contributions, suggestions, or questions, feel free to reach out to:
- kalicharansahoo91@gmail.com  

---


