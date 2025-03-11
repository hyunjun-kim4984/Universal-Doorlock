# YOLOv5 Object Detection with Raspberry Pi

This project utilizes **YOLOv5** for real-time object detection on a **Raspberry Pi**. The system integrates **servo motors**, **LEDs**, and a **buzzer** to trigger actions when specific objects are detected. Detected object information is stored in a **CSV file** for logging and analysis.

## Features

- **Real-time object detection using YOLOv5**
- **GPIO control for servo motor, LED, and buzzer on Raspberry Pi**
- **CSV file logging for detected objects**
- **Trigger actions based on specific object detections**

## Environment Setup

### 1. Install Required Packages

Run the following commands to install necessary dependencies on the Raspberry Pi:

```bash
pip install torch torchvision torchaudio
pip install opencv-python numpy pandas
pip install RPi.GPIO
2. Download YOLOv5 and Install Dependencies
Clone the YOLOv5 repository and install the required dependencies:

bash
복사
편집
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt
How to Run
1. Run Object Detection
To start the object detection process, execute the following command:

bash
복사
편집
python detect.py --weights yolov5s.pt --source 0
Options:

--weights yolov5s.pt: Specifies the YOLO model (you can use pre-trained models).
--source 0: Uses the webcam as the input source (you can also specify file paths).
2. Raspberry Pi GPIO Pin Connections
Component	GPIO Pin
Servo Motor	12
Buzzer	13
LED 1	17
LED 2	27
LED 3	22
Working Principle
1. Start Object Detection
The system uses the YOLOv5 model for real-time object detection.

2. Trigger Actions Based on Detected Objects
If "A" is detected:
LED1 turns on and the buzzer sounds.
If "K" is detected:
LED3 turns on and the servo motor moves.
If the time limit is exceeded:
LED2 turns on and the buzzer activates before resetting.
3. Save Detected Object Information
Detected object names and confidence levels are saved in a predictions.csv file for further analysis.

Output and Logging
Detected objects are saved in the runs/detect/exp/ directory.
The predictions.csv file logs object names and confidence levels.
References
YOLOv5 Official Documentation
Raspberry Pi GPIO Setup
License
This project is licensed under the MIT License - see the LICENSE file for details.

markdown
복사
편집

### Notes:
- **License**: If you are planning to release your code under a specific license, be sure to include a `LICENSE` file in your repository. You can modify the license information in the README if necessary.
- You can customize this README to fit your repository's structure by updating any folder paths or file references as 
