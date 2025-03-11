# YOLOv5 Object Detection with Raspberry Pi

This project utilizes **YOLOv5** for real-time object detection on a **Raspberry Pi**. The system is integrated with **servo motors**, **LEDs**, and a **buzzer** to trigger actions when specific objects are detected. Detected object data is saved in a **CSV file** for further analysis.

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
pip install torch torchvision torchaudio
pip install opencv-python numpy pandas
pip install RPi.GPIO

YOLOv5 Installation
Clone the YOLOv5 repository and install the required dependencies:

```bash
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt

Setup
GPIO Pin Connections
Component	GPIO Pin
Servo Motor	12
Buzzer	13
LED 1	17
LED 2	27
LED 3	22
How to Run
1. Run Object Detection
Execute the following command to start object detection:
```bash
python detect.py --weights yolov5s.pt --source 0

Options:

--weights yolov5s.pt: Specifies the YOLO model (you can use pre-trained models).
--source 0: Uses the webcam as the input source (file paths can also be specified).
2. Trigger Actions Based on Detected Objects
If "A" is detected:

LED1 turns on, and the buzzer sounds.
If "K" is detected:

LED3 turns on, and the servo motor moves.
If a time limit is exceeded:

LED2 turns on, and the buzzer activates before resetting.
3. Saving Detected Object Information
Detected object names and confidence levels are saved in a predictions.csv file.

4. Output and Logging
Detected objects are saved in the runs/detect/exp/ directory.
The predictions.csv file logs object names and confidence levels for further analysis.
References
YOLOv5 Official Documentation
Raspberry Pi GPIO Setup
License
This project is licensed under the MIT License - see the LICENSE file for details.
