<img src="https://github.com/slimelec/ollie-hw/blob/master/images/mpi_logo.png" width=300>

[www.meatpi.com](https://www.meatpi.com)
---
**All applications are available [Here](https://bit.ly/3yGgGTm)**

![image](https://user-images.githubusercontent.com/94690098/146773960-5d2bcb26-4532-49b1-88ed-c5d18794a0c0.png)
### Flash new Firmware:
Download mpFlasher Tool. [**Link**](https://bit.ly/3yGgGTm)
1. Available API for **LabView, C#, VB.Net, Delphi, Python**
2. Supports **BUSMaster** using SocketCAN Firmware (VSCOM)
3. Set the 1.27mm DFU jumper
4. Plug in the USB cable, both LEDs should start blinking
5. Once in DFU mode, the device will appear as "USB Serial Device"
6. If you have multiple USB Serial devices connected make sure to choose the right one
7. Click the "Three Dots" button to select the firmware file
8. Then Click flash button. 

## 1. SocketCAN Firmware (VSCOM API):
SocketCAN is similar CANtact firmware below, but support some extra features like **BUSMaster** compatiblity and availability of APIs in different languages such as **LabView, C#, VB.Net, Delphi, Python and more**.

## [**Programming Examples**](https://github.com/meatpiHQ/programming_examples/tree/master/CAN)

### BUSMaster
You need to download the right version of BUSMaster provided in the [**Link**](https://bit.ly/3yGgGTm) above. Here is how to setup the hardware. **Remember to set both Acceptance Code and Mask to '00000000'.**
1. Select VSCom CAN-API by clicking on 'Driver Selection -> VSCom CAN-API"
2. Then Click on 'Channel Configuration -> Advanced' 
3. Click on 'Search for Devices on COM-Ports', the device should appear in the drop downlist or fill the right COM port number
4. Check the 'Hardware Timestamps' check box.
5. Choose the Baudrate.
6. **Most importantly set both Acceptance Code and Mask to '00000000'**.
7. Click 'OK', then Click the Connect button on the top left corner.

![image](https://user-images.githubusercontent.com/94690098/152467965-3bc36968-4de3-470f-bf0e-b39237e86d7f.png)

## 2. CANtact Firmware:
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

**Python-CAN:**
```python
import can

bus = can.interface.Bus(bustype='slcan', channel='COM70', bitrate=500000)           #Windows
#bus = can.interface.Bus(bustype='slcan', channel='/dev/ttyACM0', bitrate=500000)   #Linux
msg = can.Message(arbitration_id=0x112233,
                  data=[1, 2, 3, 4, 5, 6, 7, 8],
                  is_extended_id=True)
try:
    bus.send(msg)
    print("Message sent")
except can.CanError:
    print("Message NOT sent")
for msg in bus:
    print(msg)  ## Print received messages
```
## 3. candleLight Firmware:

candleLight firmware generally has a better performance than slcan. Under Windows and Ubuntu it can be used with MicroBus or Cangaroo APP.

**Linux:**
candleLight is natively supported under linux using gs_usb driver. Just plug it in and using this command: 

`ip link set can0 up type can bitrate 500000`


**candleLight Python:**
For development you can install [candle-driver](https://pypi.org/project/candle-driver/) 


![image](https://user-images.githubusercontent.com/94690098/146776619-c8d04ee8-6a10-4300-8b9d-c7074e0080b7.png)

## 4. CAN-Analyzer

CAN-Analyzer firmware is based on slcan firmware, it also uses CDC serial interface. This firmware was ported for the sole purpose of interfacing with [realdash](http://realdash.net/).


---

© 2021 meatPi Electronics | www.meatpi.com | PO Box 5005 Clayton, VIC 3168, Australia
