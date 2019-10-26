### ToDo Make Project garage25
Status 20191026

Ideas come to mind whilst making ...

#### Forecourt Push-Button Outdoorlight
Push-Button to switch the outdoorlight on off.
The number of available pins is getting limited.
Available would be pin 12 (0x0C).

#### Ambientlight Control Outdoorlights
Control the outdoorlight(s) to control all lights when below lux threshold.
Two options:
1. Photoresistor (LDR, Analog) - the photoresistor changes resistance according amount of light received. 
2. Ambientlight sensor (BH1750, I2C) - digital light sensor breakout board

Preferred is option 1 as limited pins available. The LDR could be connected to A1 (A0 is used by the Reflective Optical Sensor).

#### Door Moving Speed
Option to set the speed of door moving.
For now hardcoded in the B4R program.
Solution idea: set parameter in ms in B4A. Use preferences actvity or a dedicated options activity.

#### Log date door opened / closed
In B4A log the dates the door was opened or closed.
Use a separate activity with a listbox.
Storage: Keep the last 10 entries in a plain text file.
Consider other storage possibilities.

#### LED Controlling Shift Register
As the number of available pins is getting low, consider to use a Shift Register 74HC595.
With this solution, only 3 pins are required to control number f LEDs.

#### Data Transfer Custom Type
Consider to use a custom type serialized (converted to bytes) with B4RSerializator instead of variables.
Example:
```
Sub Process_Globals
	Type messageType (doorState As Byte, outdoorLightState As Byte, outdoorLightBrightness As Byte)
	Private messageData as messageType

Sub ASyncStream_SetData
	asyncStream.write(serializeData.ConvertbjectToBytes(messageData))
End Sub
Sub ASyncStream_GetData(Buffer() As Byte)
	messagedata = serializeData.ConvertBytesToObject(Buffer)
End Sub

instead of
Sub Process_Globals
	Private doorState As Byte						'Used for serialized data transfer to B4A
	Private outdoorLightState As Byte				'Used for serialized data transfer to B4A
	Private outdoorLightBrightness As Byte = 100	'Used for serialized data transfer to B4A

Sub ASyncStream_SetData
	asyncStream.write(serializeData.ConvertArrayToBytes(Array As Object(doorState,outdoorLightState, outdoorLightBrightness)))
End Sub
etc.
```

#### Send / receive data Node-RED
Node-RED is one of my favourite tools.
Thinking about how to control by direct connecting a Windows PC (or Raspberry Pi server or Ubuntu PC) running Node-RED to the serial line with the Arduino.
The data communication between B4R & B4A is via B4RSerializer.
Node-RED is not able to read this data (Bytes) = need to think about a solution, like using simple JSON.

#### Data Transfer Format JSON
Consider using JSON format instead of objects or structure.
The JSON format makes it easier to handle updatesi.e. instead of sending all objects, just ent the objact which has changed and handle by new data events.
