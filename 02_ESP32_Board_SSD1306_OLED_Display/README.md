# Interfacing with OLED Display

![Esp32](/asset/esp32_display.jpg)

 ### Setting Up Your Computer
Assuming you have done the necessary setup [here](https://github.com/gigwegbe/understanding-esp32-with-micropython/tree/main/01_Setting_Up_Micropython_Esp32). Move the `13306.py` to your current directory. 

### Download the ssd1306 library 
We need to download the necessary OLED driver `ssd1306` from [Adafruit](https://github.com/adafruit/micropython-adafruit-ssd1306). 

### Uploading driver to Esp32 board
In order to use the driver we need to move it to the Esp32 board using `ampy` library. 

Move the file to Esp32 board
```
$ ampy --port /dev/cu.SLAB_USBtoUART put ssd1306.py
```
Open the repl on the board, then proceed to check if the driver exist. 

Connect to REPL using rshell
```
rshell --port /dev/cu.SLAB_USBtoUART 
```

```
/Users/george/Documents/embedded_python/understanding-esp32-with-micropython/02_ESP32_Board_SSD1306_OLED_Display> repl
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
['boot.py', 'ssd1306.py']
>>> 

```
### Test OLED Display

Import the necessary libraries
```
import machine, ssd1306
```
Select the pins associated with the OLED screen using I2C protocol. 
For WEMOS/Lolin board
```
i2c = machine.I2C(scl=machine.Pin(4), sda=machine.Pin(5))
oled = ssd1306.SSD1306_I2C(128, 64, i2c)
```
For TTGO-Camera with Microphone board
```
i2c = machine.I2C(scl=machine.Pin(22), sda=machine.Pin(21))
oled = ssd1306.SSD1306_I2C(128, 64, i2c)
```
Add text to the display
```
oled.fill(0)
oled.text('Hello George ^-^',0,0)
oled.show()
```