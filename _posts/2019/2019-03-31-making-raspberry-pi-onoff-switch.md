---
title: "라즈베리파이 전원 스위치 만들기"
last_modified_at: 2019-03-31T00:00:00
category: dev
tag: 
    - raspberry pi
    - GPIO
    - PYTHON
---

라즈베리파이로 [광고차단기](./2019-03-30-adblock-with-raspberry-pi.md)를 만들고 보니 종료할 때가 문제였다. 따로 전원 제어 버튼이 없어서 안전하게 종료하려면 터미널에서 명령어를 쳐줬어야 했기 때문. 헤드리스 서버로 쓸건데 매번 끌 때마다 저런 노가다를 할 수도 없고, 전원 뽑아서 강제 종료 시키긴 찜찜해서 입출력 키트로 간단하게 전원 버튼을 만들었다.  
<br>

---
### 회로 연결

일단 내가 쓰는 모델의 GPIO 위치는 이렇다.  
<figure style="width:80%">
    <img src="/assets/images/2019/making-raspberry-pi-onoff-switch/RasPiB-GPIO_reference.png">
</figure>  

그리고 여기에 다음과 같이 스위치와 LED를 연결했다. (LED는 안 해도 됨) 
<figure style="width:90%">
    <img src="/assets/images/2019/making-raspberry-pi-onoff-switch/Sketch.png">
</figure> 


---
**여기서부터 언급하는 핀 번호는 보드 기준 번호(왼쪽 위 1번 ~ 오른쪽 아래 40번) 이다.**
{: .notice--warning}

### 스위치
스위치의 저항이 전압쪽에 있으므로 스위치를 떼면 1, 누르면 0이 출력된다. (풀업 저항[^1])  

GPIO 핀은 5번을 사용했다. 스위치를 기기를 끌 때만 사용할 거라면 다른 핀을 사용해도 되지만, 켜는 것도 하려면 5번을 사용하자. (다른 핀에 연결해서 테스트 해봤는데 켜지는 건 안 되더라.)  

종료 스크립트는 파이썬으로 작성했다. [여기](https://github.com/gilyes/pi-shutdown/blob/master/pishutdown.py)에서 일부만 수정했다. 작성해서 적당한 위치에 저장하자.    

```python
#! /usr/bin/env python

import RPi.GPIO as GPIO
from time import sleep
from subprocess import call
from datetime import datetime

btn_pin = 5
shutdown_sec = 2 

GPIO.setmode(GPIO.BOARD)
GPIO.setup(btn_pin, GPIO.IN)

press_time = None

def button_state_changed(pin):
    global press_time
    if GPIO.input(pin) == 0:    # btn down
        if press_time is None:
            press_time = datetime.now()
    else:                       # btn up
        if press_time is not None:
            elapsed = (datetime.now() - press_time).total_seconds()
            press_time = None 
            if elapsed >= shutdown_sec:
                call(["shutdown", "-h", "now"], shell=False)
        
# subscribe to button presses
GPIO.add_event_detect(btn_pin, GPIO.BOTH, callback=button_state_changed)

while True:
sleep(5)
```
<figcaption>shutdown.py</figcaption>

기본적으로 파이썬2와 GPIO 모듈이 이미 있기 때문에 추가로 설치할 건 없다.  
참고로 이 스크립트로는 스위치를 눌렀다가 일정 시간 후 **떼는 순간** 종료 커맨드가 실행된다. 만약 떼지 않고 누르고만 있어도 일정 시간 후 커맨드가 실행되길 원한다면, [이 글](https://m.cafe.naver.com/raspigamer/7890)에 있는 스크립트를 참고하자. (해봤는데 잘 됨.)  

이제 이 스크립트를 부팅 시 자동 실행되게 만들어야 한다.  
일단 작성한 스크립트 파일을 실행 가능한 모드로 변경한다.   
```
$ sudo chmod +x /home/pi/shutdown.py
```
<br>
그리고 `/etc/rc.local` 파일을 열고 하단의 `exit 0` 보다 위에 다음 줄을 추가한다. `&`를 적어야만 스크립트가 백그라운드에서 돌아가니 꼭 적어준다.   
```
/home/pi/shutdown.py &
```

---
### LED  
기기가 켜져있으면 기판 자체에 초록불이 들어와서 별 의미는 없는데 그냥 궁금해서 해 봤다.  

LED를 serial console을 모니터링하는 TxD 핀에 연결하면 따로 프로그램을 쓰지 않아도 기기의 온오프 상태를 알 수 있다.[^2] 
LED의 (-)극과 6번 핀(Ground), (+)극은 8번 핀(TXD)에 연결하고 사이에 330Ω 짜리 저항을 넣었다. (사실 어느 정도의 저항 값이 적절한건지 잘 몰라 주로 쓰이는 것 같은걸로 대강 골랐다...) 
  
회로도대로 연결하고 추가 작업이 하나 필요하다. serial 포트가 기본적으론 disable 되어있기 때문에 able 하게 바꿔줘야 한다.  
`/boot/config.txt` 파일을 열고 다음 줄을 추가해준다.  
```
enable_uart=1
```
<br>

---

이제 재부팅 후 스위치를 눌러 잘 꺼지는 지 테스트해보자. 그리고 다시 스위치를 눌러 잘 켜지는 지도 테스트 해보자.  

<figure style="width:70%" class="align-center">
    <img src="/assets/images/2019/making-raspberry-pi-onoff-switch/pic1.jpg">
    <figcaption>조잡하지만 잘 돌아간다.</figcaption>
</figure> 

**끝!**
{: style="text-align: center; font-size: 30px;"}

---
## 참조
<http://www.raspberry-pi-geek.com/howto/GPIO-Pinout-Rasp-Pi-1-Model-B-Rasp-Pi-2-Model-B>  

[^1]: 풀업, 풀다운 저항에 대해: <https://blog.xcoda.net/77>
[^2]: <https://howchoo.com/g/ytzjyzy4m2e/build-a-simple-raspberry-pi-led-power-status-indicator>  