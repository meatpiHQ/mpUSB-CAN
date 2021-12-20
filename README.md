<img src="https://github.com/slimelec/ollie-hw/blob/master/images/mpi_logo.png" width=300>

[www.meatpi.com](https://www.meatpi.com)
---
**All applications are available [Here](https://bit.ly/3yGgGTm)**

![image](https://user-images.githubusercontent.com/94690098/146773960-5d2bcb26-4532-49b1-88ed-c5d18794a0c0.png)
### Flash new Firmware:
Download mpFlasher Tool. [Link](https://bit.ly/3yGgGTm)
1. Set the 1.27mm DFU jumper
2. Plug in the USB cable, both LEDs should start blinking
3. Once in DFU mode, the device will appear as "USB Serial Device"
4. If you have multiple USB Serial devices connected make sure to choose the right one
5. Click the "Three Dots" button to select the firmware file
6. Then Click flash button. 

## 1. CANtact Firmware:
CANtact firmware is compatible with slcan-interface and can be used with socketcan and slcand with Linux. Under Windows it can be directly driven by the serial interface.

**Drivers:** On windows mpCAN-USB will appear as a comport (COMxx) in the devices manager. Under Linux and Mac as a USB CDC device, /dev/ttyUSBX for linux and /dev/cu.usbmodemXXXX on MacOS

**Windows and Mac application:**

CANtact App can be used to monitor and send packets on CAN bus. No drivers are needed just choose the right serial port and set the baud rate and it's all set.
![image](https://user-images.githubusercontent.com/94690098/146773923-76c28e38-fcff-4499-b50b-921561072199.png)

**Linux:**

In Linux CAN interface can be brought up using [slcand](https://elinux.org/Bringing_CAN_interface_up).
**Example:**

`sudo slcand -o -c -s0 /dev/ttyUSB0 can0`

`sudo ifconfig can0 up`

`sudo ifconfig can0 txqueuelen 1000`

`cansend can0 123#11223344 	# Send a CAN frame ID:0x123 payload:0x11223344`

`candump can0                	# Receive CAN packets on CAN0`

## 2. candleLight Firmware:

candleLight firmware generally has a better performance than slcan. Under Windows and Ubuntu it can be used with MicroBus or Cangaroo APP.

**Linux:**
candleLight is natively supported under linux using gs_usb driver. Just plug it in and using this command: 

`ip link set can0 up type can bitrate 500000`


**candleLight Python:**
For development you can install candle-driver 


![image](https://user-images.githubusercontent.com/94690098/146776619-c8d04ee8-6a10-4300-8b9d-c7074e0080b7.png)

## 3. CAN-Analyzer

CAN-Analyzer firmware is based on slcan firmware, it also uses CDC serial interface. This firmware was ported for the sole purpose of interfacing with [realdash](http://realdash.net/).


---

© 2021 meatPi Electronics | www.meatpi.com | PO Box 5005 Clayton, VIC 3168, Australia
