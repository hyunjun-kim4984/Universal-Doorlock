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
Set Up a Virtual Environment (Optional but Recommended):

bash
복사
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
Install Dependencies:

bash
복사
pip install -r requirements.txt
Install YOLOv5 Dependencies:

Follow the official YOLOv5 installation instructions if additional dependencies are required.

Usage
To run the script with default settings, simply execute:

bash
복사
python your_script.py
Command-Line Options
You can customize the behavior using various command-line arguments. Some examples include:

Specify a Custom Model:

bash
복사
python your_script.py --weights path/to/your_model.pt
Change the Input Source:

bash
복사
python your_script.py --source path/to/your/image_or_video
Adjust Inference Image Size:

bash
복사
python your_script.py --imgsz 640 320
Enable Result Visualization:

bash
복사
python your_script.py --view-img
Save Detection Results as Text and CSV Files:

bash
복사
python your_script.py --save-txt --save-csv
For a complete list of options, run:

bash
복사
python your_script.py --help
Code Structure
Main Script: Contains the detection loop and GPIO control logic.
Modules Imported:
YOLOv5 Utilities: For model loading, image processing, and plotting.
Hardware Control: Using the RPi.GPIO library for interfacing with the servo, buzzer, and LEDs.
Output:
Images/Videos: Processed images are saved with detection overlays.
Labels: Detection results are saved as text files and CSV files in the specified output directory.
Notes
Testing: Always test the system in a controlled environment to ensure safety and prevent hardware damage.
GPIO Cleanup: The script attempts to clean up GPIO resources on exit (using GPIO.cleanup()). However, verify that all GPIO pins are reset properly after execution.
Customization: You can modify the password sequence and hardware action responses based on your project requirements.
License
This project is licensed under the MIT License.

vbnet
복사

This README uses Markdown formatting to clearly outline the project details, features, hardware setup
