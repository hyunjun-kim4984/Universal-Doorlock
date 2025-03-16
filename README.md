# YOLOv5 Object Detection with Raspberry Pi

This project utilizes **YOLOv5** for real-time object detection on a **Raspberry Pi**. The system is integrated with **servo motors**, **LEDs**, and a **buzzer** to trigger actions when specific objects are detected. Detected object data is saved in a **CSV file** for further analysis.
# 1. Project Overview
This project leverages YOLOv5 for real-time object detection on a Raspberry Pi. The system activates LEDs, a buzzer, and controls a servo motor when specific objects are detected. It also logs detected object information into a CSV file for further analysis.

## Features

- Real-time object detection using **YOLOv5**.
- GPIO control for **servo motors**, **LEDs**, and **buzzer** on the Raspberry Pi.
- Logging detected object information to a **CSV file**.
- Triggering actions based on specific object detections.

## Requirements

### Hardware
- **Raspberry Pi** (any version with GPIO support)
- **Servo Motor**
- **LEDs**
- **Buzzer**
- **Webcam** (for object detection)
  
### Software Dependencies

Run the following commands to install the necessary packages:

```bash
## 2. Features
Object Detection: Real-time object detection using YOLOv5.
GPIO Control: Control servo motors, LEDs, and buzzer using Raspberry Pi GPIO.
CSV Logging: Detected object names and confidence levels are logged to a CSV file.
Action Triggers: Recognizes specific objects and triggers predefined actions.
## 3. Environment Setup
(1) Install Required Packages
Install the necessary dependencies for object detection and Raspberry Pi GPIO control:

```bash

pip install torch torchvision torchaudio
pip install opencv-python numpy pandas
pip install RPi.GPIO

YOLOv5 Installation
Clone the YOLOv5 repository and install the required dependencies:

```bash
(2) Download YOLOv5 and Install Dependencies
Clone the YOLOv5 repository and install required dependencies:
```

```bash

git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt
```

Setup
GPIO Pin Connections
4. How to Run
(1) Run Object Detection
Execute the following command to start object detection using the YOLOv5 model. The webcam (or other input sources) will be used for detection:

```bash
python detect.py --weights yolov5s.pt --source 0
Options:
--weights yolov5s.pt: Specifies the YOLOv5 pre-trained model.
--source 0: Uses the webcam as the input source (you can replace 0 with a video file path).
```

(2) Raspberry Pi GPIO Pin Connections
Connect the following components to the GPIO pins on the Raspberry Pi:

| Component    | GPIO Pin |
|--------------|----------|
| Servo Motor  | 12       |
| Buzzer       | 13       |
| LED 1        | 17       |
| LED 2        | 27       |
| LED 3        | 22       |

# YOLOv5 Object Detection with Raspberry Pi GPIO Control

## How to Run

### Run Object Detection

Execute the following command to start object detection:

```bash
python detect.py --weights yolov5s.pt --source 0
Options:

--weights yolov5s.pt: Specifies the YOLO model (you can use pre-trained models).
--source 0: Uses the webcam as the input source (file paths can also be specified).
Trigger Actions Based on Detected Objects
If "A" is detected:
LED1 turns on, and the buzzer sounds.
If "K" is detected:
LED3 turns on, and the servo motor moves.
If a time limit is exceeded:
LED2 turns on, and the buzzer activates before resetting.
Saving Detected Object Information
Detected object names and confidence levels are saved in a predictions.csv file.
Output and Logging
Detected objects are saved in the runs/detect/exp/ directory.
The predictions.csv file logs object names and confidence levels for further analysis.
References
YOLOv5 Official Documentation
Raspberry Pi GPIO Setup
License
This project is licensed under the MIT License - see the LICENSE file for details.

Working Principle
Start Object Detection
The YOLOv5 model is used for real-time object detection.
It classifies objects and returns predictions along with their confidence levels.
Trigger Actions Based on Detected Objects
Object "A" detected: Turn on LED1 and activate the buzzer.
Object "K" detected: Turn on LED3 and move the servo motor.
Time Limit Exceeded: (e.g., no object detected for a while): Turn on LED2 and activate the buzzer before resetting.
Save Detected Object Information
All detected object names and their confidence levels are logged into a predictions.csv file.
Output and Logging
Detected objects are stored in the runs/detect/exp/ directory.
The predictions.csv file contains logs of all detected objects, including their names and confidence scores.
Code for Object Detection and GPIO Control
Below is the Python code that integrates YOLOv5 object detection with Raspberry Pi GPIO control:
