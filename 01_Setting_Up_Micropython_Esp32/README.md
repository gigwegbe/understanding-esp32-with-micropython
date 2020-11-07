# Setting Up Micropython Esp32

![Esp32](/asset/esp32.jpg)

 ### Setting Up Your Computer 
In order to use the Esp32 on machine(Windows, Linux or Mac) we need to first install a driver that allows the computer to recognize the microcontroller as a serial device. Follow the link to download the driver. - [cp210x](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)

```
$ cd Setting_Up_Micropython_Esp32
```

We proceed to create a python virtual environment and then install the necessary packages in the `requirements.txt` file. Follow the instruction [here](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/) to setup virtual environment. 

Create  a virtual environment. 

```
$ python3 -m venv env
```

Activate the environment.
```
$ source env/bin/activate
```
Install the packages in the virtual environment using the `requirements file`.
```
(env) $ pip3 install -r requirements.txt
```

To deactivate the virtual environment use the `deactivate` command
```
deactivate
```

 ### Flashing Micropython with esptool.py
To use Micropython we need to install the firmware on Esp32 board. Download the firmware [here](https://micropython.org/download/) in our case is `esp32-idf3-20180511-v1.9.4.bin`. Move it into the current directory. We then proceed to use `esptool.py` to flash the firmware onto the board. 

Flash the board to clean state 
```
(env) $ esptool.py erase_flash 
```
Result from flashing the board
```
esptool.py --chip esp32 --port /dev/ttyUSB0 erase_flash
```
Install the firmware 
```
esptool.py --chip esp32 --port /dev/ttyUSB0 --baud 460800 write_flash -z 0x1000 esp32-idf3-20180511-v1.9.4.bin
``` 


 ### Using Micropython REPL with rshell
 Now we have the Micropython on the board, we can connect to the Read-Eval-Print-Loop(REPL). This is the standard Python prompt that you are similar to regular Python interpreter but this time it is on the board rather than computer. 
 To use REPL with rshell
 ```
 (env) $ rshell --port <your board serial port name>
 ```
For example
```
 (env) $ rshell --port /dev/ttyUSB0
 ```