YOLOv5 Object Detection with Raspberry Pi
이 프로젝트는 YOLOv5를 활용하여 Raspberry Pi에서 실시간 객체 탐지를 수행합니다. 특정 객체가 탐지되면 서보 모터, LED, 부저가 작동하도록 설정하였으며, 탐지된 객체 정보는 CSV 파일에 저장되어 이후 분석에 활용됩니다.

📌 프로젝트 개요
이 프로젝트에서는 Raspberry Pi에서 YOLOv5를 사용해 실시간 객체 탐지를 수행합니다. 특정 객체가 감지되면 LED, 부저 및 서보 모터가 동작하며, 감지된 객체의 정보는 CSV 파일에 기록됩니다.

🚀 주요 기능
✅ 실시간 객체 탐지

YOLOv5를 활용한 실시간 객체 탐지
✅ GPIO 제어

Raspberry Pi의 GPIO 핀을 통해 서보 모터, LED 및 부저 제어
✅ CSV 저장

탐지된 객체의 이름 및 신뢰도를 CSV 파일에 저장
✅ 객체 기반 동작 트리거

특정 객체가 감지되면 사전에 설정된 동작 수행
🛠️ 준비 사항
💡 하드웨어
Raspberry Pi (GPIO 지원 버전)
서보 모터
LED
부저
웹캠
🖥️ 소프트웨어
필요한 패키지를 다음 명령어로 설치합니다:

bash
복사
편집
pip install torch torchvision torchaudio
pip install opencv-python numpy pandas
pip install RPi.GPIO
🔧 환경 설정
YOLOv5 설치
YOLOv5 저장소를 클론하고 필요한 종속성을 설치합니다:

bash
복사
편집
git clone https://github.com/ultralytics/yolov5.git
cd yolov5
pip install -r requirements.txt
⚡ GPIO 핀 연결
다음과 같이 Raspberry Pi의 GPIO 핀에 하드웨어를 연결합니다:

구성 요소	GPIO 핀 번호
서보 모터	12
부저	13
LED 1	17
LED 2	27
LED 3	22
▶️ 실행 방법
1. 객체 탐지 실행
YOLOv5 모델을 사용해 객체 탐지를 시작합니다. 웹캠(또는 다른 입력 소스)을 통해 객체 탐지를 실행합니다:

bash
복사
편집
python detect.py --weights yolov5s.pt --source 0
옵션 설명

--weights yolov5s.pt : 사전 학습된 YOLOv5 모델 지정
--source 0 : 입력 소스로 웹캠 사용 (파일 경로도 입력 가능)
2. 객체 기반 동작 트리거
"A" 객체 감지 시 → LED1이 켜지고 부저가 작동
"K" 객체 감지 시 → 서보 모터가 작동하고 LED3이 켜짐
시간 초과 시 → LED2가 켜지고 부저가 작동 후 재설정
3. 탐지 결과 저장
탐지된 객체 이름 및 신뢰도는 predictions.csv 파일에 저장됩니다.
또한 YOLOv5 출력은 runs/detect/exp/ 디렉토리에 저장됩니다.

📝 코드 예제
YOLOv5 객체 탐지와 Raspberry Pi GPIO 제어가 통합된 코드입니다:

python
복사
편집
import torch
import RPi.GPIO as GPIO
import time
import pandas as pd
import cv2

# GPIO 설정
GPIO.setmode(GPIO.BCM)
GPIO.setup(12, GPIO.OUT)  # 서보 모터
GPIO.setup(13, GPIO.OUT)  # 부저
GPIO.setup(17, GPIO.OUT)  # LED 1
GPIO.setup(27, GPIO.OUT)  # LED 2
GPIO.setup(22, GPIO.OUT)  # LED 3

# YOLOv5 모델 로드
model = torch.hub.load('ultralytics/yolov5', 'yolov5s')

# 비디오 캡처 시작
cap = cv2.VideoCapture(0)

# CSV 설정
columns = ['Object', 'Confidence']
predictions_df = pd.DataFrame(columns=columns)

# 동작 함수 정의
def trigger_led_buzzer(led_pin, buzzer_pin):
    GPIO.output(led_pin, GPIO.HIGH)
    GPIO.output(buzzer_pin, GPIO.HIGH)
    time.sleep(1)
    GPIO.output(led_pin, GPIO.LOW)
    GPIO.output(buzzer_pin, GPIO.LOW)

def move_servo_motor(servo_pin):
    pwm = GPIO.PWM(servo_pin, 50)
    pwm.start(0)
    pwm.ChangeDutyCycle(7)  # 서보 모터 이동
    time.sleep(1)
    pwm.stop()

# 탐지 루프 시작
while True:
    ret, frame = cap.read()
    if not ret:
        break
    
    # 객체 탐지 수행
    results = model(frame)
    
    # 결과 파싱
    detected_objects = results.pandas().xywh[0]
    
    for _, row in detected_objects.iterrows():
        object_name = row['name']
        confidence = row['confidence']
        
        # 탐지된 객체 정보 CSV에 저장
        predictions_df = predictions_df.append({'Object': object_name, 'Confidence': confidence}, ignore_index=True)
        
        if object_name == "A":
            trigger_led_buzzer(17, 13)  # LED1 + 부저 작동
        elif object_name == "K":
            move_servo_motor(12)  # 서보 모터 작동
            GPIO.output(22, GPIO.HIGH)  # LED3 켜기
            
    # CSV 파일에 저장
    predictions_df.to_csv('predictions.csv', index=False)
    
    # 화면 출력
    cv2.imshow('Object Detection', results.render()[0])
    
    # 종료 조건 (q 입력 시 종료)
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# 종료 처리
cap.release()
cv2.destroyAllWindows()
GPIO.cleanup()
📂 디렉토리 구조
복사
편집
├── yolov5
│   ├── detect.py
│   ├── runs/
│   ├── weights/
│   ├── predictions.csv
├── README.md
📎 참고 자료
YOLOv5 공식 문서
Raspberry Pi GPIO 설정
📄 라이선스
이 프로젝트는 MIT 라이선스에 따라 배포됩니다. 자세한 내용은 LICENSE 파일을 참조하세요.

✅ 프로젝트 요약
YOLOv5로 실시간 객체 탐지
객체 이름 및 신뢰도 반환
특정 객체 탐지 시 GPIO를 통해 하드웨어 동작
탐지 결과를 CSV에 저장 및 화면 출력
🚀 YOLOv5와 Raspberry Pi를 활용한 객체 탐지 프로젝트가 성공적으로 동작합니다! 😎
필요한 추가 수정 사항이나 궁금한 점이 있으면 알려주세요! 😄
