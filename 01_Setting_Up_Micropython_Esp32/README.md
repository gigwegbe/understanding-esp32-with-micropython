# Setting Up Micropython Esp32

![Esp32](/asset/esp32_1.jpg)

 ### Setting Up Your Computer 
In order to use the Esp32 on machine(Windows, Linux or Mac) we need to first install a driver that allows the computer to recognize the microcontroller as a serial device. Follow the link to download the driver. - [cp210x](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

```
$ cd Setting_Up_Micropython_Esp32
```

We proceed to create a python virtual environment and then install the necessary packages in the `requirements.txt` file. Follow the instruction [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) to setup virtual environment. 

Create  a virtual environment:

```
$ python3 -m venv env
```

Activate the environment:
```
$ source env/bin/activate
```
Install the packages in the virtual environment using the `requirements file`:
```
(env) $ pip3 install -r requirements.txt
```

To deactivate the virtual environment use the `deactivate` command:
```
deactivate
```

 ### Flashing Micropython with esptool.py
To use Micropython we need to install the firmware on Esp32 board. Download the firmware [here](https://micropython.org/download/) in our case is `esp32-idf3-20180511-v1.9.4.bin`. Move it into the current directory. We then proceed to use `esptool.py` to flash the firmware onto the board. 

Flash the board to clean state(press the reset button):
```
(env) $ esptool.py erase_flash 
```
Result from flashing the board:
```
esptool.py v3.0
Serial port /dev/cu.SLAB_USBtoUART
Connecting........_
Chip is ESP32-D0WDQ6 (revision 1)
Features: WiFi, BT, Dual Core, 240MHz, VRef calibration in efuse, Coding Scheme None
Crystal is 40MHz
MAC: 3c:71:bf:8c:0d:20
Uploading stub...
Running stub...
Stub running...
Erasing flash (this may take a while)...
Chip erase completed successfully in 6.2s
Hard resetting via RTS pin...
```
or 

```
esptool.py --chip esp32 --port /dev/cu.SLAB_USBtoUART erase_flash
```

Install the firmware:
```
esptool.py --chip esp32 --port /dev/cu.SLAB_USBtoUART --baud 460800 write_flash -z 0x1000 esp32-idf3-20180511-v1.9.4.bin
``` 


 ### Using Micropython REPL with rshell
 Now we have the Micropython on the board, we can connect to the Read-Eval-Print-Loop(REPL). This is the standard Python prompt that you are similar to regular Python interpreter but this time it is on the board rather than computer. 
 To use REPL with rshell:
 ```
 (env) $ rshell --port <your board serial port name>
 ```
For example:
 ```
 (env) $ rshell --port /dev/cu.SLAB_USBtoUART
 ```
 Result:
 ```
 Using buffer-size of 32
Connecting to /dev/cu.SLAB_USBtoUART (buffer-size 32)...
Trying to connect to REPL  connected
Testing if ubinascii.unhexlify exists ... Y
Retrieving root directories ... /boot.py/
Setting time ... Nov 07, 2020 10:25:34
Evaluating board_name ... pyboard
Retrieving time epoch ... Jan 01, 2000
Welcome to rshell. Use Control-D (or the exit command) to exit rshell.
/Users/george/Documents/embedded_python/understanding-esp32-with-micropython/01_Setting_Up_Micropython_Esp32> 
 ```

To use the REPL enter the `repl` command: 
```
 /Users/george/Documents/embedded_python/understanding-esp32-with-micropython/01_Setting_Up_Micropython_Esp32> repl
Entering REPL. Use Control-X to exit.
>
MicroPython v1.9.4 on 2018-05-11; ESP32 module with ESP32
Type "help()" for more information.
>>> 
>>> 
```

Test the Python interpreter:

```
>>> print("Hello Embedded Python - MicroPython!")
Hello Embedded Python - MicroPython!
>>> 
```