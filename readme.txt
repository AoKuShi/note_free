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
