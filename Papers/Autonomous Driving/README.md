# 🚗 Real-Time Autonomous Driving Simulation

This project implements a full simulation-based autonomous driving system using the **Godot game engine**. It integrates deep learning and computer vision models for real-time steering control, object detection, lane change, and autonomous parking maneuvers.

---

## 📌 Project Highlights

### 🔧 System Overview
- Simulation built in **Godot** with **7 test tracks**, each evaluating a specific driving capability:
  - Lane following and steering prediction
  - Lane merging and changing
  - Obstacle avoidance
  - Speed sign detection
  - Autonomous parking

### 🧠 AI Models Used
- **Steering Prediction**: Custom-trained **Nvidia DAVE-2 CNN** model using >15,000 images.
- **Object Detection**: **YOLOv8n**
  - Trained on **GTSRB dataset** for traffic signs.
  - Custom dataset for parking slot detection.

---

## 🛠 System Architecture

- **Client (Simulation)**: Built with **Godot + C#**
  - Captures camera input, sends to server
  - Receives steering angles and detection results via JSON
- **Server (ML Inference)**: Built with **Python + Flask**
  - Uses **Dave-2** for steering prediction
  - Uses **YOLOv8n** for object/traffic sign detection
- Communication via image byte arrays and JSON API
- Real-time performance achieved using **CPU-only setup**

---

## 🚦 Core Features

### 🛣 Lane Change (LC) System
- Five-sensor setup: 3 front, 2 side
- Lane change initiated based on obstacle detection and sensor clearance
- **Bezier Curve** for path planning
- **Pure Pursuit Algorithm** used for trajectory following

### 🅿️ Autonomous Parking System
- Side cameras + YOLO to detect empty slots
- Two-stage parking:
  - Forward alignment trajectory
  - Curved trajectory into the slot
- Enhanced with rear/side sensors to center the vehicle before starting the maneuver

### 🧭 Cruising Mode
- When no detections are triggered, **Dave-2** continuously handles steering control

---

## 📊 Evaluation

- **Autonomous Parking**:
  - Reliable detection and maneuver execution
  - Parking succeeds with or without adjacent cars, though better alignment is achieved when adjacent vehicles are present

- **Lane Change System**:
  - High success rate, some minor drift if server latency increases

- **Dave-2 Model**:
  - Trained on one track, tested on others with strong generalization
  - Smooth lane following even on high-curvature roads and under shadows

- **Performance Limitations**:
  - CPU-based inference leads to increasing latency over time
  - GPU would significantly boost real-time responsiveness

---

## 🔥 Technical Stack

| Component         | Technology             |
|------------------|------------------------|
| Simulation       | Godot (C#)             |
| Server           | Python + Flask         |
| Models           | TensorFlow (Dave-2), YOLOv8n (Ultralytics) |
| Training         | Google Colab (GPU)     |
| Annotation       | Roboflow               |

---

## 📁 Dataset & Training

- **Dave-2**: ~15,000 custom driving images, filtered to avoid bias
- **Traffic Signs**: GTSRB dataset (Kaggle)
- **Parking Slots**: 1,200+ custom-annotated images
- Manual annotation using **Roboflow**

---

## 📺 Demo & Code

- 📹 **[Watch Demo Video](https://youtu.be/6kBQ6Ja8XR0)**
- 💻 **[GitHub Repository](https://github.com/Rami-Si7/Autonomous-Car.git)**

---

## 📚 References

- [Nvidia’s DAVE-2 Paper (arXiv)](https://arxiv.org/pdf/1604.07316)
- [YOLOv8 Paper (arXiv)](https://arxiv.org/pdf/2104.12537)
- [GTSRB Dataset on Kaggle](https://www.kaggle.com/datasets/meowmeowmeowmeowmeow/gtsrb-german-traffic-sign)
- [Traffic Sign Detection YOLO Code](https://www.kaggle.com/code/pkdarabi/traffic-signs-detection-using-yolov8)
- [Pure Pursuit Algorithm](https://thomasfermi.github.io/Algorithms-for-Automated-Driving/Control/PurePursuit.html)
- [YouTube Tutorial Playlist](https://www.youtube.com/watch?v=oLi6mWDXRGM&list=PLMoSUbG1Q_r9JtujskOZkorWKCszT0w2S)

---

> 🚀 *This simulation project lays a strong foundation for real-world autonomous driving research and testing. Future work may include reinforcement learning, MPC, and hardware-level sensor fusion.*
