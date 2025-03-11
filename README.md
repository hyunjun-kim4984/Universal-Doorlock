# YOLOv5 Object Detection with Raspberry Pi  

This project utilizes YOLOv5 for real-time object detection and integrates it with servo motors, LEDs, and a buzzer on a Raspberry Pi. Additionally, detected object information is stored in a CSV file for further analysis.



## 🚀 Project Overview  
This project leverages Raspberry Pi to perform real-time object detection using YOLOv5. When specific objects are detected, the system activates LEDs, a buzzer, and controls a servo motor accordingly. Detected object data is logged in a CSV file for future analysis.  



## 🎯 Features  
✅ Object detection using YOLOv5  
✅ GPIO control for servo motor, LED, and buzzer on Raspberry Pi  
✅ CSV file logging for detected objects  
✅ Recognizing specific object sequences to trigger actions  



## 🛠️ Environment Setup  

### (1) Install Required Packages  
Run the following commands to install the necessary dependencies:  
```bash
pip install torch torchvision torchaudio  
pip install opencv-python numpy pandas  
pip install RPi.GPIO  
