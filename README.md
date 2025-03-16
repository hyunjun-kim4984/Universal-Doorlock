# YOLOv5 Door Unlocking System with GPIO

This project integrates the YOLOv5 object detection model with Raspberry Pi GPIO control to create an automated door unlocking system. The system detects specific labels that form a password (in this example, the sequence `A`, `K`, `I`) and, when the correct sequence is detected, actuates a servo motor to unlock a door. Visual and audio feedback is provided using LEDs and a buzzer.

## Features

- **Real-Time Object Detection:** Utilizes YOLOv5 for detecting objects from images or video streams.
- **Password Verification:** Monitors for a specific sequence (`A`, `K`, `I`) to trigger the door unlocking mechanism.
- **Hardware Integration:** 
  - **Servo Motor:** Controls door unlocking (connected to GPIO pin 12).
  - **Buzzer:** Provides audio feedback (connected to GPIO pin 13).
  - **LEDs:** Indicate system status and error conditions (connected to GPIO pins 17, 27, and 22).
- **Flexible Input Sources:** Supports images, videos, webcams, and screenshots.
- **Result Logging:** Saves detection outputs as text and CSV files, and optionally crops detected objects for further review.
- **Configurable Parameters:** Easily adjust settings like image size, confidence threshold, and detection limits through command-line arguments.

## Hardware Setup

- **Raspberry Pi:** Ensure your Raspberry Pi has Python 3.7+ and the RPi.GPIO library installed.
- **Servo Motor:** Connected to GPIO pin 12.
- **Buzzer:** Connected to GPIO pin 13.
- **LEDs:** Connected to GPIO pins 17, 27, and 22.
- **Camera:** Use a USB camera or the Raspberry Pi Camera Module for capturing images or video streams.

> **Note:** Verify that your hardware connections match the pin configuration defined in the source code.

## Requirements

- Python 3.7 or higher
- [PyTorch](https://pytorch.org/)
- [RPi.GPIO](https://pypi.org/project/RPi.GPIO/)
- OpenCV (`cv2`)
- Additional dependencies as listed in the `requirements.txt` file (e.g., ultralytics, numpy, etc.)

## Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/yourusername/your-repo.git
   cd your-repo
