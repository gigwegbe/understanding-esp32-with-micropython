# Interfacing with OLED Display

![Esp32](/asset/mpu6050.png)

 ### Setting Up Your Computer
Assuming you have done the necessary setup [here](https://github.com/gigwegbe/understanding-esp32-with-micropython/tree/main/01_Setting_Up_Micropython_Esp32). 
### Download the mpu6050 library 
We need to download the necessary Accelerometer/Gyroscope driver `mpu6050.py` from [here](https://github.com/adamjezek98/MPU6050-ESP8266-MicroPython). Move the `mpu6050.py` to your current directory. 


### Uploading driver to Esp32 board
In order to use the driver we need to move it to the Esp32 board using `ampy` library. 

Move the file to Esp32 board
```
$ ampy --port /dev/cu.SLAB_USBtoUART put mpu6050.py
```
Open the repl on the board, then proceed to check if the driver exist. 

Connect to REPL using rshell
```
rshell --port /dev/cu.SLAB_USBtoUART 
```

```
/Users/george/Documents/embedded_python/understanding-esp32-with-micropython/04_Accelerometer_and_Gyroscope> repl
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
['boot.py', 'mpu6050.py']
>>> 

```
### Test Accelerometer/Gyroscope

Import the necessary libraries
```
from machine import I2C, Pin
```
Select the pins associated with the accelerometer using I2C protocol. 
SCL connected to pin 5, SDA to pin 4 example usage: 
```
>>>i2c = I2C(scl=Pin(5), sda=Pin(4))
>>>accelerometer = mpu6050.accel(i2c)
>>>accelerometer.get_values()
{'GyZ': -235, 'GyY': 296, 'GyX': 16, 'Tmp': 26.64764, 'AcZ': -1552, 'AcY': -412, 'AcX': 16892}
```
