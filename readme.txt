import time
from datetime import datetime
from liquidcrystal_i2c import LCD

# LCD 설정
lcd = LCD(bus=1, addr=0x27, cols=16, rows=2)
lcd.clear()
lcd.home()

print("watch program")

try:
    while True:
        # 현재 날짜와 시간을 가져와서 포맷에 맞게 변환
        date_print = datetime.now().strftime('%m.%d, %A')
        time_print = datetime.now().strftime('%p %I:%M:%S') # 사진에는 %P:%H:%M:%S로 되어있으나, 일반적인 12시간제(AM/PM)는 %p %I 입니다.

        # 첫 번째 줄에 날짜 표시
        lcd.setCursor(0, 0)
        lcd.print(date_print)

        # 두 번째 줄에 시간 표시
        lcd.setCursor(0, 1)
        lcd.print(time_print)

        # 1초 대기
        time.sleep(1)

except KeyboardInterrupt:
    # Ctrl+C 입력 시 프로그램 종료
    print('\n프로그램 종료합니다.')

------

sudo apt-get update

sudo apt-get install gstreamer1.0-tools gstreamer1.0-alsa gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav

sudo apt-get install libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libgstreamer-plugins-good1.0-dev libgstreamer-plugins-bad1.0-dev

# Checking the GStreamer-1.0 Version
gst-inspect-1.0 -version

# Installing Accelerated GStreamer plugins
sudo apt-get update
sudo apt-get install nvidia-l4t-gstreamer
sudo ldconfig
rm -rf .cache/gstreamer-1.0/

<해상도 확인>
v4l2-ctl --list-formats-ext

<CSI 카메라 작동 시험>
git clone https://github.com/JetsonHacksNano/CSI-Camera.git
gst-launch-1.0 nvarguscamerasrc sensor_id=0 ! 'video/x-raw(memory:NVMM), width=3280, height=2464, framerate=21/1, format=NV12' ! nvvidconv flip-method=0 ! 'video/x-raw, width=320, height=248' ! nvvidconv ! nvegltransform ! nveglglessink -e

# module 추가 설치
$ sudo apt install libcanberra-gtk-module

# 동작
$ python simple_camera.py

12. AI 얼굴인식

<사진 100장 찍기>
$ git clone https://github.com/codeingschool/Facial-Recognition.git
$ ls
$ cd Facial-Recognition
$ mkdir faces
$ mv Facial_Recognition_Part1.py Facial_Recognition_Part1_v2.py
#파일 수정 - gstreamer pipeline
$ python Facial_Recognition_Part1_v2.py

12-3. 얼굴 인식_part3_v2.py

# 파일 이름 변경
$ mv Facial_Recognition_Part3.py Facial_Recognition_Part3_v2.py

# 파일 수정 - gstreamer pipeline

# 파일 실행
$ python Facial_Recognition_Part3_v2.py
