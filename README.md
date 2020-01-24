# make-garage25
This make project is a custom LEGO® creation to remote control, via an Android App, a garage model with a microcontroller and connected servo motor, actuators and indicators.
(LEGO® is a trademark of the LEGO Group)

# Objectives
* To create a model of a garage with an automatic sliding door
* To open & close the garage door via outside push-button
* To indicate outside using LEDs, if the garage is free (green) or closed (red)
* To indicate outside, if the garage door is moving by flashing a yellow LED
* To light the garage forecourt with a white LED (outdoor lighting)
* To set the brightness of the outdoor lighting
* To remote control the garage via Bluetooth classic using an Android App
* To have fun exploring and creating technical type of digital custom creations

_Note_: This make project is for private use only.

![garage25-p](https://user-images.githubusercontent.com/47274144/67616597-2ad4d300-f7db-11e9-81d6-f7be962aa5c2.png)
![garage25-ps](https://user-images.githubusercontent.com/47274144/67616607-3fb16680-f7db-11e9-9293-969edb57007d.png)

### Outlook
This is the first version, which had the main goal to explore remote control the creation using Android App.
There is quite some room on the forecourt to add more creations, like a gas station.
See TODO.md with various ideas in mind.

### Creation Rules
* Use as microcontroller an Arduino type microcontroller
* Use standard LEGO components
* Minimize LEGO brick modifications
* LEGO case with modular components
* LEGO ground plate 32x32
* Develop the microcontroller code with B4R
* Develop the remote control app with B4A (other options like B4J or Node-RED under consideration)

### Hardware Parts
* 1x Microcontroller Arduino UNO R3
* 1x Arduino UNO R3 Prototype Shield with mini breadboard
* 1x Servo Motor (Servo Hitec HS-311)
* 1x Bluetooth HC-05 (DSD Tech HC-05 Classic Bluetooth Mini MEGA)
* 1x Voltage Divider 5V > 3.3V (own creation with resistors 1K Ohm & 2K Ohm))
* 1x Push-Button (DFRobot Digital Push-Button)
* 1x TCRT5000 (Reflective Optical Sensor with Transistor Output)
* 1x LED Red
* 1x LED Yellow
* 1x LED Green
* 1x LED White
* 1x LEGO Sliding Garage Door (10-segments)
* Various LEGO Bricks and LEGO Technic parts
* Various wires

### Software
* Arduino IDE 1.8.9 or higher
* B4R 3.00 or higher
* B4A 9.50 or higher

### Brief Solution
The core of the model is a LEGO Sliding Garage Door, built into a garage, moved by a servo motor with an L-arm.
The L-arm has two LEGO Technic "Beam 9" connected with a LEGO Technic "Pin with Lengthwise Friction Ridges and Center Slots" and transforms the servo circular movement to the door horizontal movement.
The end of the L-arm is connected to the first segment of the door
The servo start angle is 5 degrees (=door open) and the end angle 60 degrees (=door closed).
The movement of the door is done in 5 degrees steps with 500ms delay (hardcoded in the microcontroller program).
The servo is connected to the microcontroller PWM pin #10.
_Note_
Tested various servos and concluded the Hitec HS-311 unctions best with a torque of 30ncm (at 4.8V).
The HS-311 is a standard servo from Hitec with reliable three-pole ferrite motor and durable resign gears.

A push-button with big green cap and an LED enables to open or close the door. During door movement, the yellow LED, placed left side of the garage, is flashing.

Beside the yellow LED, there is a red and green LED to indicate if the garage is occupied or free.
This is triggered by a reflective optical sensor placed inside at the end of the garage. If a car enters the garage and is less then 1cm away from the optical sensor, the red LED is turned on and the green LED off.
In addition, there is an outdoor light which can be switched on / off or dimmed.

All devices are connected and controlled by an Arduino UNO.
There are two way to control the garage:
* Basic Control: Push-button to open / close the door
* Advanced Control: Android App to open / close the door, switch outdoor lighting on / off, set the brightness of the outdoor lighting, auto update state changes

The communication between the microcontroller and the Android App is via Bluetooth Classic using software serial.
The Bluetooth device name is "garage25". Note that only one connection to the microcontroller is allowed.

### Usage
Provide power to the Arduino.
The garage door sets initiallty the door closed, then changes to start position open - the yellow led flashing while the door is moving.
If there is a car in the garage, the red led is on, else the green led is on - this is controlled by an optical sensor.
The outdoor lighting is on at full brightness.
Pressing the green button, placed left from the garage, the door will close else, if closed, the door is opened.

On the Android device, open the App garage25.
The app tries to connect to the Bluetooth device garage25 (indicates trying to connect).
If the connection is made, the state is "Connected (garage25)" (and the Connect button is disabled) else "not connected".
If not connected, try again by pressing the Connect button.
After successful connecttion, the data displayed is updated, i.e. garage open and outdoor lighting On.
Press the button Close to close the garage or Off to turn the outdoor light off.
The outdoor light brightness can be set via slider. When changing the slider, confirm by pressing button Brightness which will change the brightness.

![garage25-a](https://user-images.githubusercontent.com/47274144/67616605-3d4f0c80-f7db-11e9-8d1d-de942ea61180.png)

### LEGO Construction
The creation is built using mix of LEGO classic & technic bricks. No modifications to the bricks made.
The foundation is a baseplate 32x32 with a curved driveway (from beginning 14 to 9-stud which is used for the garage) on the right.
The garage, build of a LEGO garage roller door kit (9 transparent sections plus 1 blue handle, size in studs: width=9, height=15, length=19), is build at the end of the road.
The the servo motor is at the back end on top and the moving L-arm outside on the right side.
Dediced to make the arm visible to see it moving. If not visible, then the motor and arm could be placed left and build into some brick construction.

The optical sensor is placed in the garage (at the end , 13 studs from the entry).

Left towards the back of the garage, the microcontroller with its sensors and wiring is placed into a small yellow controller-house.
The back of the controller-house enables to provode power, either 9V DC or 5 USB.

Left towards the front of the garage, the green push-button with LED is placed to enable open / close of the roller door.

As mentioned, there free space on the baseplate to enhance this model by for example a gas stationMore to come ...

### Wiring
![garage25-c](https://user-images.githubusercontent.com/47274144/67616603-36c09500-f7db-11e9-82ed-0fe3847762fd.png)
```
Servo (Hitec HS-311)=Microcontroller
Signal=D10
VCC=5V
GND=GND

Bluetooth (HC-05)=Microcontroller
TX=D8 RX
RX=D9 TX - using a voltage divider 5V > 3.3V
VCC=5V
GND=GND

Reflective Optical Sensor (TCRT5000)=Microcontroller
Signal Analog=A0
Signal Digital=Not used
VCC=5V
GND=GND

Push-Button (DFRobot Digital Push-Button)=Microcontroller
Signal=D3
VCC=5V
GND=GND

LED Outdoor=Microcontroller
Plus=D11 - using R330Ohm; must be a PWM pin to enable setting the brightness value 0-255
GND=GND

LED Red=Microcontroller
Plus=D6 - using R330Ohm
GND=GND

LED Yellow=Microcontroller
Plus=D5 - using R330Ohm
GND=GND

LED Green=Microcontroller
Plus=D4 - using R330Ohm
GND=GND
```

### Communication

#### Bluetooth
The Bluetooth HC-05 module is a Bluetooth SPP (Serial Port Protocol) module and communicates with the microcontroller via the Serial Communication (software serial used).
The HC-05 RX pin is connected to the Microcontroller TX pin and the TX pin to the RX pin.
The microcontroller TX pin outputs 5V, but the HC-05 RX pin supports 3.3V, so a voltage divider (5V > 3.3V) is used.

__Configuration___
To configure the DSD TECH HC-05, AT commands are used, which requires to put the HC-05 in AT command mode.
Setting the Bluetooth module in command mode differs by device. Read the module's datasheet.
These are the steps used for the dSD TECH HC-05 module:

1. Remove power 5V from the HC-05 module
2. Connect HC-05 PIN34 (EN PIN) with microcontroller 3.3V
3. Add power 5V to the HC-05 module
4. The HC-05 LED is blinking fast. The default baudrate is 38400.

Used a simple Arduino sketch created with the Arduino IDE and used the Arduino IDE Tools > Serial Monitor to enter the AT commands.

The Bluetooth name set is __garage25__ via AT command: AT+NAME=garage25

Other AT commands used:
AT+VERSION with response: +VERSION:2.0-20100601
AT+ADDR with response: +ADDR:14:3:614fa
AT+UART with response: +UART:9600,0,0

#### Serializer
The B4R Serializer class is used to transfer data, in both directions, between the Arduino (B4R program) and the Android App (B4A app).
The objects are converted to bytes prior sending and converted from bytes to an array with objects whilst receiving.
The data structure is defined as individual objects. A type structure is not used (see TODO.md).

##### Microcontroller send to Android
Objects: 3
* doorstate (byte) - 0=closed,1=open
* outdoorlightstate (byte) - 0=off, 1=on
* outdoorlightbrightness (byte) - 0-100

##### Microcontroller received from Android
Objects: 4
* refresh (byte) - 0=no refresh request, 1=refresh requested which will send the previous described objects
* dooraction (byte) - 0=closed,1=open
* outdoorlightstate (byte) - 0=off, 1=on
* outdoorlightbrightness (byte) - 0-100

_Notes_
* The refresh object is mainly used by the Android App running first time to get the state of the objects (doorstate etc.)
* The brightness 0-100% is mapped to a value between 0-255 which is used by the outdoor light pin analogwrite to set the brightness.

## Soure Code
The source code is well documented.
See files b4a-source.zip, b4r-source.zip, b4r-additional-libraries.zip.

### Credits
* Anywhere Software for providing B4R & B4A (and of course the whole B4X suite) [Info](https://www.b4x.com/)
* Friends-of-Fritzing foundation for fritzing [Info](https://fritzing.org)

### Licence
GNU GENERAL PUBLIC LICENSE Version 3, 29 June 2007
