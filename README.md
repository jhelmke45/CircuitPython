# CircuitPython

## Table of Contents
* [Table of Contents](#TableOfContents)
* [Hello_CircuitPython](#Hello_CircuitPython)
* [CircuitPython_Servo](#CircuitPython_Servo)
* [CircuitPython_Ultrasonic_Sensor](#CircuitPython_Ultrasonic_Sensor)
* [CircuitPython_LCD](#CircuitPython_LCD)
---

## Hello_CircuitPython

### Description & Code
The goal for this assignment was to understand some basics of CircuitPython and get everything set up, and get control of the onboard Neopixel.


```python
#Jack Helmke
#This code makes the onboard neopixel flash different colors

import board
import neopixel
import time
import random
ran1 = 0
ran2 = 0
ran3 = 0
var = 0

dot = neopixel.NeoPixel(board.NEOPIXEL, 1)
dot.brightness = 0.3

while True:
    ran1 = random.randint(0, 125) 
    ran2 = random.randint(0, 125) 
    ran3 = random.randint(0, 125) 
    

    dot.fill((ran1, ran2, ran3))
    time.sleep(.1)

```


### Evidence




https://user-images.githubusercontent.com/113116262/193280040-159cefba-b5f6-412e-b17e-2df2534bcac3.mp4



### Wiring

![helloCP](https://user-images.githubusercontent.com/113116262/192556289-57b5692b-f5d3-45b6-aedd-3aee8da0ab58.png)

### Reflection
The tricky part of this assignment really was just getting everything set up, but I didn't have too much trouble. It was fun messing with the RGB capabilities of the onboard Neopixel, and I ended up experimenting with the ``` random.randint() ``` function to make the Neopixel flash random colors. Overall, this was a good introduction into the basics of how CircuitPython works.




## CircuitPython_Servo

### Description & Code
In this assignment I made a servo rotate back and forth

```python
#Jack Helmke
#This code makes a servo rotate back and forth
#Code from Kattni Rembor for Adafruit Industries

"""CircuitPython Essentials Servo standard servo example"""
import time
import board
import pwmio
from adafruit_motor import servo

# create a PWMOut object on Pin D2 (original code has A2)
pwm = pwmio.PWMOut(board.D2, duty_cycle=2 ** 15, frequency=50)

# Create a servo object, my_servo.
my_servo = servo.Servo(pwm)

while True:
    for angle in range(0, 180, 5):  # 0 - 180 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)
    for angle in range(180, 0, -5): # 180 - 0 degrees, 5 degrees at a time.
        my_servo.angle = angle
        time.sleep(0.05)

```

### Evidence



https://user-images.githubusercontent.com/113116262/193279812-11bfe0bf-6a7a-45b2-8bce-f6b39d90ab1b.mp4



### Wiring

![servo](https://user-images.githubusercontent.com/113116262/193041474-d091f6f6-306f-421a-9c83-9b513aab9223.png)

### Reflection!

This assignment wasn't too tricky, as it was pretty easy to find [code from adafruit](https://learn.adafruit.com/adafruit-metro-m4-express-featuring-atsamd51/circuitpython-servo). The setup was hard to understand at first with "PWM" and "duty cycle" thrown around, but the servo library is super helpful and simple commands such as ``` myServo.angle ``` are easy to understand and apply.






## CircuitPython_Ultrasonic_Sensor

### Description & Code

```python
#Jack Helmke
#This code changes the RGB values of the Neopixel based on distance returned by ultrasonic sensor
#Setup code from Graham Gilbert-Schroeer, all logic code and comments by me

import time
import board
import adafruit_hcsr04
import neopixel
import simpleio

sonar = adafruit_hcsr04.HCSR04(trigger_pin=board.D3, echo_pin=board.D2) #pin numbers for sensor
dot = neopixel.NeoPixel(board.NEOPIXEL, 1) #onboard led
dot.brightness = .05 
red = 0 #variables for color mapping
green = 0
blue = 0

while True:
    try:
        cm = sonar.distance #set cm variable to distance
        print((sonar.distance))
        time.sleep(0.01)
        if cm < 5:
            dot.fill((255, 0, 0)) #set color to red when cm less than 5
        if cm > 5 and cm < 20:
            green = 0 #no green for this section
            red = simpleio.map_range(cm, 5, 20, 255, 0) #map red (high-low)
            blue = simpleio.map_range(cm, 5, 20, 0, 255) #map blue (low-high)
            dot.fill((red, green, blue))
        if cm > 20 and cm < 35:
            red = 0 #no red for this section
            green = simpleio.map_range(cm, 20, 35, 0, 255) #map green (low-high)
            blue = simpleio.map_range(cm, 20, 35, 255, 0) #map blue (high-low)
            dot.fill((red, green, blue))
        if cm > 35:
            dot.fill((0, 255, 0)) #set color to green when cm is greater than 35
    except RuntimeError:
        print("Retrying!")
    time.sleep(0.01)

```

### Evidence



https://user-images.githubusercontent.com/113116262/193279039-8a3f4104-4efb-4fac-9704-4bfa79de0970.mp4



### Wiring

![image](https://user-images.githubusercontent.com/113116262/193045426-703ab61c-9731-42fe-be3e-08709906d6d9.png)

### Reflection

I did most of the code myself on this assignment, which was fun. I used the [simpleio](https://docs.circuitpython.org/projects/simpleio/en/latest/api.html) library for the ``` simpleio.map_range ``` function, which was essential to scale the sensor values into the color gradient I wanted. I had originally taken code from [Graham Gilbert-Schroeer](https://github.com/VeganPorkChop/CircutPython), but I ended up only keeping their setup code and redoing all of the logic for the gradients, and commenting on the code myself.


## CircuitPython_LCD

### Description & Code
In this assignment I made an LCD display a number which would change by 1 when a button was pressed, while another button toggled if the change was positive or negative. The number and UP/DOWN state are displayed on the LCD.

```python
#Jack Helmke
#This code makes pressing one button change the number on the LCD by 1, other button toggles positive/negative
#Most of this code taken from Graham Gilbert-Schroeer, UP and DOWN states edited in by me

import board
import time
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
from digitalio import DigitalInOut, Direction, Pull

# get and i2c object
i2c = board.I2C()
btn = DigitalInOut(board.D3)
btn2 = DigitalInOut(board.D2)
btn.direction = Direction.INPUT
btn.pull = Pull.UP
btn2.direction = Direction.INPUT
btn2.pull = Pull.UP
# some LCDs are 0x3f... some are 0x27.
lcd = LCD(I2CPCF8574Interface(i2c, 0x3f), num_rows=2, num_cols=16)
cur_state = True
prev_state = True
cur_state2 = True
prev_state2 = True
buttonPress = 0

while True:
    while btn2.value == False:
        lcd.set_cursor_pos(1,0)
        lcd.print("UP  ")
        cur_state = btn.value
        if cur_state != prev_state:
            if not cur_state:
                buttonPress = buttonPress + 1
                lcd.clear()
                lcd.set_cursor_pos(0,0)
                lcd.print(str(buttonPress))
            else:
                lcd.clear()
                lcd.set_cursor_pos(0,0)
                lcd.print(str(buttonPress))
        prev_state = cur_state
    else:
        lcd.set_cursor_pos(1,0)
        lcd.print("DOWN")
        cur_state2 = btn.value
        if cur_state2 != prev_state2:
            if not cur_state2:
                buttonPress = buttonPress - 1
                lcd.clear()
                lcd.set_cursor_pos(0,0)
                lcd.print(str(buttonPress))
            else:
                lcd.clear()
                lcd.set_cursor_pos(0,0)
                lcd.print(str(buttonPress))
        prev_state2 = cur_state2

```

### Evidence

https://user-images.githubusercontent.com/113116262/193050475-0fadf3bb-b7c2-4c46-88a0-36a07f7f2523.mp4



### Wiring

![lcd](https://user-images.githubusercontent.com/113116262/193049761-4b8ed3e4-7381-49f9-ba08-52bba7c2706b.png)

### Reflection
