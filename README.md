# BlockYolobit-CabinCableCar
#### Link Project: https://app.ohstem.vn/#!/share/yolobit/2uGq6jEMkQ2OhWFi41xGQS544xX
#### Code Block:
![image](https://github.com/user-attachments/assets/537db569-8f50-4f97-9a9d-b0f1d6535d2c)
![image](https://github.com/user-attachments/assets/dd9c996f-17d7-4cde-b96a-0f733fe3a4a4)

#### Code Python:
```
from yolobit import *
button_a.on_pressed = None
button_b.on_pressed = None
button_a.on_pressed_ab = button_b.on_pressed_ab = -1
import time

if True:
  isRunning = False
  isForward = True
  edgeLightDetect = True
  light = 100
  speed = 100
  delayCount = 0

while True:
  if button_a.is_pressed():
    while button_a.is_pressed():
      pass
    light = (light if isinstance(light, (int, float)) else 0) + 10
    if light > 200:
      light = 50
    display.scroll(light)
  if button_b.is_pressed():
    isRunning = True
    timer.reset()
  if isRunning and pin2.read_analog() / 10 < light:
    if edgeLightDetect:
      timer.reset()
      edgeLightDetect = False
    delayCount = timer.get()
    if delayCount > 2500:
      isRunning = False
      isForward = not isForward
  else:
    edgeLightDetect = True
  if isRunning and isForward:
    display.show(Image("00500:05000:55555:05000:00500"))
    pin0.servo360_write(speed)
    pin1.servo360_write(speed)
  elif isRunning and not isForward:
    display.show(Image("00400:00040:44444:00040:00400"))
    pin0.servo360_write((0 - speed))
    pin1.servo360_write((0 - speed))
  else:
    display.show(Image.HEART)
    pin0.servo360_write(0)
    pin1.servo360_write(0)
  time.sleep_ms(1)
  print('sens:' + ': ' + str((pin2.read_analog() / 10)))
  time.sleep_ms(10)

