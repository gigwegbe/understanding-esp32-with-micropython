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


