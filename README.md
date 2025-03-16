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

##How to Run

1. Run Object Detection
Execute the following command to start object detection:
```bash
python detect.py --weights yolov5s.pt --source 0
```

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

5. Working Principle
Start Object Detection
The YOLOv5 model is used for real-time object detection.
It will classify objects and return predictions along with their confidence levels.
Trigger Actions Based on Detected Objects
Object "A" detected:
Turn on LED1 and activate the buzzer.
Object "K" detected:
Turn on LED3 and move the servo motor.
Time Limit Exceeded (e.g., no object detected for a while):
Turn on LED2 and activate the buzzer before resetting.
Save Detected Object Information
All detected object names and their confidence levels are logged into a predictions.csv file.
6. Output and Logging
Detected objects are stored in the runs/detect/exp/ directory.
The predictions.csv file contains logs of all detected objects, including their names and confidence scores.
7. Code for Object Detection and GPIO Control
Here is the Python code that integrates YOLOv5 object detection with Raspberry Pi GPIO control:

```python
import torch
import RPi.GPIO as GPIO
import time
import pandas as pd
import cv2

# GPIO Setup
GPIO.setmode(GPIO.BCM)
GPIO.setup(12, GPIO.OUT)  # Servo motor
GPIO.setup(13, GPIO.OUT)  # Buzzer
GPIO.setup(17, GPIO.OUT)  # LED 1
GPIO.setup(27, GPIO.OUT)  # LED 2
GPIO.setup(22, GPIO.OUT)  # LED 3

# Load YOLOv5 model
model = torch.hub.load('ultralytics/yolov5', 'yolov5s')

# Start video capture (webcam)
cap = cv2.VideoCapture(0)

# CSV setup
columns = ['Object', 'Confidence']
predictions_df = pd.DataFrame(columns=columns)

# Action functions
def trigger_led_buzzer(led_pin, buzzer_pin):
    GPIO.output(led_pin, GPIO.HIGH)
    GPIO.output(buzzer_pin, GPIO.HIGH)
    time.sleep(1)
    GPIO.output(led_pin, GPIO.LOW)
    GPIO.output(buzzer_pin, GPIO.LOW)

def move_servo_motor(servo_pin):
    pwm = GPIO.PWM(servo_pin, 50)
    pwm.start(0)
    pwm.ChangeDutyCycle(7)  # Move servo to a position
    time.sleep(1)
    pwm.stop()

# Detection loop
while True:
    ret, frame = cap.read()
    if not ret:
        break
    
    # Perform detection
    results = model(frame)
    
    # Parse the results
    detected_objects = results.pandas().xywh[0]  # Get results as a pandas dataframe
    
    for _, row in detected_objects.iterrows():
        object_name = row['name']
        confidence = row['confidence']
        
        # Log detected object to CSV
        predictions_df = predictions_df.append({'Object': object_name, 'Confidence': confidence}, ignore_index=True)
        
        if object_name == "A":
            trigger_led_buzzer(17, 13)  # Turn on LED1 and buzzer
        elif object_name == "K":
            move_servo_motor(12)  # Move servo motor
            GPIO.output(22, GPIO.HIGH)  # Turn on LED3
            
    # Save to CSV after each frame
    predictions_df.to_csv('predictions.csv', index=False)
    
    # Display the frame with detections
    cv2.imshow('Object Detection', results.render()[0])
    
    # Exit condition
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```
# Cleanup
cap.release()
cv2.destroyAllWindows()
GPIO.cleanup()
8. References
YOLOv5 Official Documentation: https://github.com/ultralytics/yolov5
Raspberry Pi GPIO Setup: https://www.raspberrypi.org/documentation/usage/gpio/
This code integrates YOLOv5 object detection with GPIO components on the Raspberry Pi, enabling actions like lighting LEDs, sounding a buzzer, and controlling a servo motor based on detected objects. Detected object data is saved to a CSV file for further analysis.