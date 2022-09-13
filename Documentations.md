# CircuitPython Documentations
## Servo
### Code
`import time
import board
import pwmio
from adafruit_motor import servo

pwm = pwmio.PWMOut(board.D2, duty_cycle=2 ** 15, frequency=50)

my_servo = servo.Servo(pwm)

while True:
    for angle in range(0, 180, 5): 
        my_servo.angle = angle
        time.sleep(0.01)
    for angle in range(180, 0, -5): 
        my_servo.angle = angle
        time.sleep(0.01)`
