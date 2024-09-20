---
layout: post
title: "Pico W based Internet Clock"
---

You will need these three items.

- Raspberry Pi Pico W with soldered headers - <https://www.raspberrypi.com/products/raspberry-pi-pico-2/>
- Grove Shield for Pi Pico - <https://www.seeedstudio.com/Grove-Shield-for-Pi-Pico-v1-0-p-4846.html>
- Grove - OLED Display 0.66" (SSD1306) - <https://www.seeedstudio.com/Grove-OLED-Display-0-66-SSD1306-v1-0-p-5096.html>

Total cost should be around 15 USD. I attached the OLED display to I2C.

![](/resources/24.jpg)

The code is trying to connect to Wifi and set time from `time.google.com`. The contrast was set to 0 to make it easier to read. You may want to adjust that. I am drawing digits manually to see them clearly. If you have a different display that will make it easier too. 

```python
import network
import ntptime
import time

from machine import Pin, I2C
from ssd1306 import SSD1306_I2C

SSID = "<SSID>"
PASSWORD = "<WIFI PASSWORD>"

led = machine.Pin("LED", machine.Pin.OUT)
wlan = network.WLAN(network.STA_IF)

i2c = I2C(1, scl=Pin(7), sda=Pin(6), freq=200000)
oled = SSD1306_I2C(64, 48, i2c)

def show_text(message):
    oled.fill(0)
    x = 0
    y = 0
    for char in message:
        oled.text(char, x, y)
        x = x + 8
        if x > 64:
            y = y + 8
            x = 0
    oled.show()

def connect_internet():
    led.on()
    wlan.active(True)
    wlan.connect(SSID, PASSWORD)
    
    # Wait for connection to establish
    max_wait = 10
    while max_wait > 0:
        if wlan.status() < 0 or wlan.status() >= 3:
                break
        max_wait -= 1
        
        print('waiting for connection...')
        show_text('waiting' + str(max_wait))
        time.sleep(1)
    
    # Manage connection errors
    if wlan.status() != 3:
        show_text('failed')
        print('Network Connection has failed')
    else:
        show_text('connected')
        print('connected')
        status = wlan.ifconfig()
        print( 'ip = ' + status[0] )
        led.off()

def print_time(display, number, position):
    start_x = position * 16
    
    if number == 0:
        display.fill_rect(start_x + 12,  2,  4, 46, 1)
        display.fill_rect(start_x +  2,  2,  4, 46, 1)
        display.fill_rect(start_x +  2,  2, 14,  4, 1) 
        display.fill_rect(start_x +  2, 44, 14, 14, 1) 
        
    if number == 1:
        display.fill_rect(start_x + 12,  2,  4, 46, 1)
    
    if number == 2:
        display.fill_rect(start_x +  2,  2, 14,  4, 1) 
        display.fill_rect(start_x + 12,  2,  4, 22, 1) 
        display.fill_rect(start_x +  2, 24, 14,  4, 1) 
        display.fill_rect(start_x +  2, 24,  4, 22, 1) 
        display.fill_rect(start_x +  2, 44, 14, 14, 1)
        
    if number == 3:
        display.fill_rect(start_x + 12,  2,  4, 46, 1) 
        display.fill_rect(start_x +  2,  2, 14,  4, 1) 
        display.fill_rect(start_x +  2, 24, 14,  4, 1) 
        display.fill_rect(start_x +  2, 44, 14, 14, 1)
        
    if number == 4:
        display.fill_rect(start_x + 12,  2,  4, 46, 1)
        display.fill_rect(start_x +  2, 24, 14,  4, 1) 
        display.fill_rect(start_x +  2,  2,  4, 24, 1)
        
    if number == 5:
        display.fill_rect(start_x +  2,  2, 14,  4, 1)
        display.fill_rect(start_x +  2,  2,  4, 24, 1)
        display.fill_rect(start_x +  2, 24, 14,  4, 1)
        display.fill_rect(start_x + 12, 24,  4, 24, 1)
        display.fill_rect(start_x +  2, 44, 14, 14, 1)
        
    if number == 6:
        display.fill_rect(start_x +  2,  2, 14,  4, 1)
        display.fill_rect(start_x +  2,  2,  4, 24, 1)
        display.fill_rect(start_x +  2, 24, 14,  4, 1)
        display.fill_rect(start_x + 12, 24,  4, 24, 1)
        display.fill_rect(start_x +  2, 44, 14, 14, 1)
        display.fill_rect(start_x +  2, 24,  4, 22, 1)
        
    if number == 7:
        display.fill_rect(start_x +  2,  2, 14,  4, 1)
        display.fill_rect(start_x + 12,  2,  4, 46, 1)
        
    if number == 8:
        display.fill_rect(start_x + 12,  2,  4, 46, 1)
        display.fill_rect(start_x +  2,  2,  4, 46, 1)
        display.fill_rect(start_x +  2,  2, 14,  4, 1) 
        display.fill_rect(start_x +  2, 24, 14,  4, 1) 
        display.fill_rect(start_x +  2, 44, 14, 14, 1)
        
    if number == 9:
        display.fill_rect(start_x + 12,  2,  4, 46, 1)
        display.fill_rect(start_x +  2,  2, 14,  4, 1) 
        display.fill_rect(start_x +  2, 24, 14,  4, 1)
        display.fill_rect(start_x +  2,  2,  4, 24, 1)

oled.contrast(255)
oled.fill(0)
print_time(oled, 9, 0)
print_time(oled, 6, 1)
print_time(oled, 9, 2)
print_time(oled, 6, 3)
oled.show()

connect_internet()
ntptime.host = "time.google.com"
ntptime.settime()
   
while True:
    now_time = time.localtime(time.time()+7200)
    position = 0
    
    oled.fill(0)
    oled.contrast(0)
    hour = now_time[3]
    
    if hour > 12:
        hour = hour - 12
        
    if len(str(hour)) < 2:
        print_time(oled, 0, position)
        position = 1
    for character in str(hour):
        print_time(oled, int(character), position)
        position = position + 1
        
    if len(str(now_time[4])) < 2:
        print_time(oled, 0, position)
        position = position + 1
        
    for character in str(now_time[4]):
        print_time(oled, int(character), position)
        position = position + 1
        
    oled.show()
    time.sleep(30)
```

The clock in action:

![](/resources/25.jpg)

## Tags

- Pico
- Micropython
- internet clock