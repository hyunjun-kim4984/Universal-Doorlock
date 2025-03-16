# YOLOv5 Object Detection with Raspberry Pi  

이 프로젝트는 **YOLOv5**를 활용하여 **Raspberry Pi**에서 실시간 객체 탐지를 수행합니다. 특정 객체가 탐지되면 **서보 모터**, **LED**, **부저**가 작동하도록 설정하였으며, 탐지된 객체 정보는 **CSV 파일**에 저장되어 이후 분석에 활용됩니다.  

---

## 📌 프로젝트 개요
이 프로젝트에서는 Raspberry Pi에서 YOLOv5를 사용해 실시간 객체 탐지를 수행합니다. 특정 객체가 감지되면 LED, 부저 및 서보 모터가 동작하며, 감지된 객체의 정보는 CSV 파일에 기록됩니다.  

---

## 🚀 주요 기능
- ✅ **실시간 객체 탐지**: YOLOv5를 활용한 실시간 객체 탐지  
- ✅ **GPIO 제어**: Raspberry Pi의 GPIO 핀을 통해 서보 모터, LED 및 부저 제어  
- ✅ **CSV 저장**: 탐지된 객체의 이름 및 신뢰도를 CSV 파일에 저장  
- ✅ **객체 기반 동작 트리거**: 특정 객체가 감지되면 사전에 설정된 동작 수행  

---

## 🛠️ 준비 사항

### 💡 **하드웨어**
- Raspberry Pi (GPIO 지원 버전)  
- 서보 모터  
- LED  
- 부저  
- 웹캠  

### 🖥️ **소프트웨어**
필요한 패키지를 다음 명령어로 설치합니다:

```bash
pip install torch torchvision torchaudio
pip install opencv-python numpy pandas
pip install RPi.GPIO
