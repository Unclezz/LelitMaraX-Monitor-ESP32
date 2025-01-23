///////////////////////////////////////////////////////////////////////////////////////////////////

First of all a huge **thanks to dougie996** - author of the [M1N1MaraX initial code](https://github.com/dougie996/M1N1MaraX_Web) that I forked

This fork has a few modifications to support:
	
 	* ESP32 boards
  	* SPI Oled display (1,3'') with 7 pin, using the library Adafruit_SH110X.h
   	* MQTT Client authentication with username and password (mandatory for Home Assistant MQTT Mosquito broker)

//////////////////////////////////////////////////////////////////////////////////////////////////

From original README of M1N1MaraX repository:

This is a quick and dirty implementation of a Display and MQTT Client for Lelit MaraX V2 Espresso Machines.

What it does: 

1) In idle mode:
In the upper left corner is the Heater Status. While heating, a blinking cursor and Text "Heatup" is shown.
In the upper center a WiFi Icon is shown, together with the WiFi Signal Strength, when connected to WiFi.
In the upper right the Mara X Mode of operation is shown. A Coffeecup signals Coffee Priority Mode; a Steam Symbol Steam Priority Mode.
Lower part left & right: reported Temperature of Heat Exchanger and Steam Boiler.

2) In operation mode:
As soon the coffee brewing sequence is started, der Steam Temperature display is replaced by a shot timer, counting seconds up and a filling up Coffeecup is shown on the left, together with the Heat Exchanger Temperature.
After brewing sequence has ended, the Display returns to idle Mode. 

3) The following parameters are published via WiFi to a connected MQTT Server

      1. Mara Software Version and Mode of Operation
      2. Steam Temp
      3. Target Steam Temp
      4. Heat Exchange Temp
      5. Heating Boost Mode
      6. Heating Element on/off
      7. Pump on/off
      8. WiFiRxLevel

4. Configuration can primarily be done via the secrets.h file.
   It contains Parameters like WiFi SSID and Password and MQTT Server Address & Port. You can also define the MQTT Update Interval in seconds.
   You need to match this based on your requirements.

Despite many other similar projects, this one is using the correct Mara X V2 wiring and coding!
Please TAKE CARE, as most information in the Web regarding how to interface with Mara X Gicar Control Box is WRONG! 

Please also visit https://www.m1n1.de/en/lelit-mara-x-v2-gicar-internals/ for details.

The Arduino Tx Line / Gicar Rx Line dones not need to be connected. There's no program code inside the Gicar, which would work with data recieved via the serial interface. 
The Memory of the Gicar Processor is quite full. 50% are already occupied by a huge Table with 921 Values for the Temp Sensor evaluation plus the STM8 Compiler Runtime. 

You need to add your WLAN SSID and Password to the secrets.h file, for getting acces to your WLAN. The Machine will appear in your router as "MaraX".
Add IP Address and port of your MQTT Broker and desired update interval in seconds.  

Hardware used is an ESP8266 on a Wemos D1 clone and 128x64 Adafruit SSD1306 SPI OLED Display.

![image](https://github.com/dougie996/M1N1MaraX_MQTT/assets/117717919/8c066df9-6e21-4d42-b458-7699bd4b0714)


![MaraX_MQTT_final](https://github.com/dougie996/M1N1MaraX_MQTT/assets/117717919/41279506-7fa4-4b17-8ba5-9439497c996f)
