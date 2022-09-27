# CircuitPython
This repository will actually serve as a aid to help you get started with your own template.  You should copy the raw form of this readme into your own, and use this template to write your own.  If you want to draw inspiration from other classmates, feel free to check [this directory of all students!](https://github.com/chssigma/Class_Accounts).
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

Here's how you make code look like code:

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

record the video


### Wiring

![helloCP](https://user-images.githubusercontent.com/113116262/192556289-57b5692b-f5d3-45b6-aedd-3aee8da0ab58.png)

### Reflection
The tricky part of this assignment really was just getting everything set up, but I didn't have too much trouble. It was fun messing with the RGB capabilities of the onboard Neopixel, and I ended up experimenting with randoms to make the Neopixel flash random colors. Overall, this was a good introduction into the basics of how CircuitPython works.




## CircuitPython_Servo

### Description & Code
In this assignment I 

```python
Code goes here

```

### Evidence

Pictures / Gifs of your work should go here.  You need to communicate what your thing does.

### Wiring

### Reflection!





## CircuitPython_LCD

### Description & Code

```python
Code goes here

```

### Evidence

Pictures / Gifs of your work should go here.  You need to communicate what your thing does.

### Wiring

### Reflection





## NextAssignment

### Description & Code

```python
Code goes here

```

### Evidence

### Wiring

### Reflection
