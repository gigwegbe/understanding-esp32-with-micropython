# Interfacing with Ultrasonic Sensor

![Esp32](/asset/hc_sro4.jpg)

 ### Setting Up Your Computer
Assuming you have done the necessary setup [here](https://github.com/gigwegbe/understanding-esp32-with-micropython/tree/main/01_Setting_Up_Micropython_Esp32). 
### Download the mpu6050 library 
We need to download the necessary Ultrasonic Sensor driver `hcsr04.py` from [here](https://github.com/rsc1975/micropython-hcsr04). Move the `hcsr04.py` to your current directory. 


### Uploading driver to Esp32 board
In order to use the driver we need to move it to the Esp32 board using `ampy` library. 

Move the file to Esp32 board
```
$ ampy --port /dev/cu.SLAB_USBtoUART put hcsr04.py
```
Open the repl on the board, then proceed to check if the driver exist. 

Connect to REPL using rshell
```
rshell --port /dev/cu.SLAB_USBtoUART 
```

```
Users/george/Documents/embedded_python/understanding-esp32-with-micropython/05_UltraSonic_Sensor> repl
```

```
import os
os.listdir()
```
Result: 

```
MicroPython v1.9.4 on 2018-05-11; ESP32 module with ESP32
Type "help()" for more information.
>>> 
>>> import os
>>> os.listdir()
['boot.py', 'hcsr04.py']
>>> 

```
### Test UltraSonic Sensor

Import the necessary libraries
```
from machine import I2C, Pin
from hcsr04 import HCSR04
```
Connect trigger pin and echo to pin 16 and 5 respectively. 
```
>>>sensor = HCSR04(trigger_pin=16, echo_pin=5)
>>>distance = sensor.distance_cm()
>>>print('Distance:', distance, 'cm')
```
Result: 
```>>> print('Distance:', distance, 'cm')
Distance: 2.886598 cm
```
