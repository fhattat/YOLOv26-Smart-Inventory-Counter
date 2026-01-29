# YOLOv26-Smart-Inventory-Counter
High-performance real-time object counting system for conveyor belts using YOLOv26 and custom coordinate-based logic.

# 🍎 Smart Inventory Counter with YOLOv26

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![YOLO](https://img.shields.io/badge/Model-YOLOv26-orange)
![OpenCV](https://img.shields.io/badge/Library-OpenCV-green)

This project implements a robust object counting system using the state-of-the-art **YOLOv26** model.

🍎 Smart Inventory & Object Tracking System (YOLOv26)
📌 Project Overview
This project involves the development of a real-time computer vision system designed to automate inventory counting in manufacturing and logistics environments. Using the state-of-the-art YOLOv26 object detection model, the system identifies, tracks, and counts items (specifically fruits) moving on a conveyor belt.

Unlike standard counting solutions, this project implements a Custom Coordinate-Based Buffer Logic to achieve 100% counting accuracy, eliminating double-counting issues common in high-speed video feeds.

🏗️ Architecture & Methodology
The pipeline leverages Deep Learning for detection and distinct mathematical logic for counting.

Detection Engine: Uses YOLOv26 (fine-tuned) to identify objects with high precision.

Tracking Algorithm: Implements persistent tracking IDs (ByteTrack/BoT-SORT) to distinguish between unique objects across video frames.

Custom Counting Logic: Instead of a simple line-crossing algorithm, I engineered a "Buffer Zone" mechanism. Objects are counted only when their centroid coordinates enter a specific vertical tolerance range (e.g., X ± 30px) in the center of the frame.

🛠️ Tech Stack
Model: YOLOv26 (Transfer Learning on Custom Dataset).

Computer Vision: OpenCV (cv2) for frame processing, drawing, and video writing.

Data Management: Roboflow (Dataset acquisition and preprocessing).

Environment: Google Colab (GPU-accelerated training and inference).

Language: Python 3.10+

🔄 Pipeline Workflow
1. Data Acquisition (Roboflow) 📥
Integrated the Roboflow API to programmatically download the "Fruit Detection" dataset.

Dataset includes annotated images of apples with bounding box coordinates, formatted specifically for YOLO architecture.

2. Model Training (Fine-Tuning) 🧠
Base Model: Loaded pre-trained YOLO weights.

Training: Fine-tuned the model on the custom dataset for 20 epochs to specialize in fruit detection.

Result: Achieved high Mean Average Precision (mAP) for the 'Apple' class.

3. Real-Time Inference & Tracking 🎥
Processed video input frame-by-frame.

Applied Persistent Tracking (persist=True) to assign a unique ID to each apple. This ensures that an apple is recognized as "Object #45" throughout its entire journey across the screen, preventing it from being counted multiple times.

4. The "Buffer Zone" Counting Logic 🧮
Defined a vertical reference line at the center of the video.

Created a Buffer Zone (Safety Corridor) of +/- 30 pixels around the line.

Algorithm:
if (Line_X - Offset) < Object_Center_X < (Line_X + Offset):
    if Object_ID not in Counted_List:
        Count += 1
        Mark Object_ID as Counted

This logic makes the system robust against video lag, object speed variations, and jitter.

5. Visualization & Dashboard 📊
Dynamic Overlay: Draws bounding boxes and tracking IDs on detected objects.

Visual Feedback: The reference line flashes GREEN instantly when an object is successfully counted.

On-Screen Dashboard: Displays the total real-time count in a high-contrast panel at the bottom-left corner.

🚀 Key Results
Accuracy: Achieved 100% counting accuracy on the test video, successfully handling closely spaced objects.

Performance: Capable of real-time processing using GPU acceleration.

Output: Generates a processed video file (.mp4) with visual analytics embedded.

📂 Repository Structure
├── notebooks/
│   └── YOLOv26_Inventory_Counter.ipynb  # Main Colab Notebook (Training + Inference)
├── data/
│   └── (Dataset downloaded via Roboflow API)
├── output/
│   └── final_smart_counter.mp4          # The final result video with the dashboard
└── README.md                            # Project Documentation
