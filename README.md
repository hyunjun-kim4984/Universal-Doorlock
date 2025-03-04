YOLOv5 Object Detection with Raspberry Pi
This project utilizes YOLOv5 for object detection and integrates it with servo motors, LEDs, and a buzzer on a Raspberry Pi.
Additionally, detected object information is stored in a CSV file for further analysis.

1. Project Overview
This project uses Raspberry Pi to perform real-time object detection. When specific objects are detected, the system activates LEDs, a buzzer, and controls a servo motor accordingly.

2. Features
Object detection using YOLOv5
GPIO control for servo motor, LED, and buzzer on Raspberry Pi
CSV file logging for detected objects
Recognizing specific object sequences to trigger actions

3. Environment Setup
(1) Install Required Packages
Run the following commands to install the necessary dependencies:
pip install torch torchvision torchaudio
pip install opencv-python numpy pandas
pip install RPi.GPIO

(2) Download YOLOv5 and Install Dependencies
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt

4. How to Run
(1) Run Object Detection
Execute the following command to start object detection:
python detect.py --weights yolov5s.pt --source 0
Options:

--weights yolov5s.pt : Specifies the YOLO model (pre-trained models can be used).
--source 0 : Uses the webcam as the input source (file paths can also be specified).

(2) Raspberry Pi GPIO Pin Connections
Component	GPIO Pin
Servo Motor	12
Buzzer	13
LED 1	17
LED 2	27
LED 3	22

5. Working Principle
Start Object Detection

Uses the YOLOv5 model for real-time object detection.
Trigger Actions Based on Detected Objects

If "A" is detected, LED1 turns on, and the buzzer sounds.
If "K" is detected, LED3 turns on, and the servo motor moves.
If the time limit is exceeded, LED2 turns on, and the buzzer activates before resetting.
Save Detected Object Information

Object names and confidence levels are saved in a predictions.csv file.
6. Output and Logging
Detected objects are stored in the runs/detect/exp/ directory.
The predictions.csv file contains logs of all detected objects.

7. References
YOLOv5 Official Documentation: https://github.com/ultralytics/yolov5
Raspberry Pi GPIO Setup: https://www.raspberrypi.org/documentation/usage/gpio/
