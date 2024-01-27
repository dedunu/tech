---
layout: post
title: "How to blink Raspberry Pi Pico onboard LED?"
---

Original documentation for Raspberry Pi documentation shows turning on LED this code. 

```python
from machine import Pin, Timer
led = Pin(25, Pin.OUT)
timer = Timer()

def blink(timer):
    led.toggle()

timer.init(freq=2.5, mode=Timer.PERIODIC, callback=blink)
```

Above code doesn't work. It should be changed to this.

```python
from machine import Pin, Timer
led = machine.Pin("LED", machine.Pin.OUT)
timer = Timer()

def blink(timer):
    led.toggle()

timer.init(freq=2.5, mode=Timer.PERIODIC, callback=blink)
```


### Reference

- <https://projects.raspberrypi.org/en/projects/getting-started-with-the-pico/5>

### Tags

- Pico
- Raspberry Pi
- LED
