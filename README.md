# Universal Doorlock

**Universal Doorlock** is a system that implements door unlocking through hand gesture recognition based on YOLOv5. This project addresses the limitations of touch-based systems, offering a safer and more hygienic door access solution for a diverse range of users, including visually impaired individuals.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Hardware Setup](#hardware-setup)
- [System Design and Implementation](#system-design-and-implementation)
- [How to Run](#how-to-run)
- [Output and Logging](#output-and-logging)
- [References](#references)
- [License](#license)
- [Contributing and Contact](#contributing-and-contact)

---

## Project Overview

This project leverages the deep learning-based object detection algorithm **YOLOv5** to recognize hand gestures in real time using a camera. When a predefined sequence of hand gestures (e.g., "A", "K", "I") is detected, the door is unlocked.  
The system improves upon existing methods by addressing the following issues:

- **Security Issues:**  
  Traditional touch-based systems may leave fingerprints and can be vulnerable to unauthorized access through camera surveillance. The hand gesture approach enhances security.

- **Hygiene Issues:**  
  By eliminating the need for direct contact, the system provides a more hygienic method for door unlocking.

---

## Demo Screenshots

![Image](https://github.com/user-attachments/assets/af1654b7-d81f-46f1-9ceb-4fefe2773ad3)


---

## Key Features

- **Real-time Hand Gesture Recognition:**  
  Uses the YOLOv5 model to detect hand gestures from the video feed.

- **Password Input:**  
  Recognized gestures (e.g., "A", "K", "I") are sequentially used as a password; the door unlocks when the correct sequence is detected.

- **Visual and Audio Feedback:**  
  - **When "A" is detected:** LED1 lights up, and the buzzer sounds at 200Hz.  
  - **When "K" is detected:** LED3 lights up, and the buzzer sounds at 300Hz.  
  - **When "I" is detected:** LED1 lights up, and the buzzer sounds at 400Hz.  
  - **On timeout or incorrect input:** LED2 lights up, and the buzzer sounds at 500Hz before the password input is reset.

- **Result Logging:**  
  Detected object labels and their confidence scores are recorded in a `predictions.csv` file, and the result images are saved in the `runs/detect/exp/` directory.

---

## Hardware Setup

### Key Components

- **Raspberry Pi 4** (for control and model inference)
- **Webcam** (for real-time video input)
- **LEDs, Piezo Buzzer, Servo Motor** (for visual/audio feedback and door lock control)

### GPIO Pin Connections

| Component    | GPIO Pin |
|--------------|----------|
| Servo Motor  | 12       |
| Buzzer       | 13       |
| LED 1        | 17       |
| LED 2        | 27       |
| LED 3        | 22       |

*All pins use the BCM numbering system.*

---

## System Design and Implementation

### Design Overview

1. **YOLOv5-based Hand Gesture Recognition:**  
   The system detects hand gestures in real time from the video input.  
   - The model is trained using a preprocessed hand gesture dataset provided by Roboflow.
   - The YOLOv5 model is trained in a Colab environment and then used for inference on the Raspberry Pi.

2. **GPIO Control:**  
   - **Controlling LEDs, Buzzer, and Servo Motor:**  
     Each device is activated based on the recognized hand gestures.
   - **Timeout Mechanism:**  
     If no valid input is detected within a specified time period, a warning is triggered (LED2 and 500Hz buzzer tone) and the password input is reset.

3. **Password Verification:**  
   The system treats the detected gesture labels as a password. When the correct sequence ("A" → "K" → "I") is input, the door (via the servo motor) is unlocked.

### Implementation Details

- **Dataset Download:**  
  Hand gesture image data is downloaded and preprocessed from Roboflow.

- **YOLOv5 Model Training:**  
  The training script provided by YOLOv5 is executed in a Colab environment to train the model.

- **GPIO Setup and Control:**  
  The Raspberry Pi's GPIO library is used to configure and control the pins for each device.

- **Inference and Logging:**  
  The system displays object detection results in real time and saves them to CSV and image files.

---

## How to Run

### Execution Command

Run the following command to start the object detection and door lock control system:

```bash
python detect.py --weights yolov5s.pt --source 0
```

## Option Descriptions

- `--weights yolov5s.pt`: Specifies the pre-trained YOLOv5 model file.
- `--source 0`: Uses the webcam as the input source (a file path can also be specified).

---

## Output and Logging

**Result Images:**  
Detected result images (or videos) are saved in the `runs/detect/exp/` directory.

**Log File:**  
Detected object labels and their confidence scores are recorded in the `predictions.csv` file.

---

## References

- [YOLOv5 Official Documentation](https://github.com/ultralytics/yolov5)
- [Raspberry Pi GPIO Setup](https://www.raspberrypi.org/documentation/usage/gpio/)

**Related Tutorials and Blog Posts:**

- YOLOv5 Environment Setup and Training
- Controlling Servo Motors and Buzzers with Raspberry Pi

---

## License

This project is distributed under the **MIT License**.

---

## Contributing and Contact

**College of Engineering, Hankuk National University**

**Project Contributors:**

- Jaeyoung Yoon (Student ID: 2019265088)
- Hyunjun Kim (Student ID: 2019265040)

For questions or contribution-related matters, please open an issue in the project repository.

---

*This README file comprehensively covers the project overview, key features, hardware connections, system design and implementation, running instructions, output and logging, references, license, and contributor information. Feel free to modify or add any additional details as necessary.*
