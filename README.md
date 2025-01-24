<h1 align="center">LelitMarax-Monitor-Esp32</h1>
<p align="center"><a href="#project-description">Project Description</a> - <a href="#key-features">Key Features</a> - <a href="#configuration-and-setup">Configuration and Setup (draft)</a> - <a href="#3d-printed-case">3D printed CASE</a></p>

## Project Description

First of all a huge **thanks to dougie996** - author of the <a href="https://github.com/dougie996/M1N1MaraX_Web">M1N1MaraX initial code</a> that I forked. As far as I can tell, code and provided schematic for connections is the only one we should work with because it is well thought and studied before going to public!

LelitMaraX-Minitor-ESP32 project started because I wanted to have a quick look at my Lelit MaraX (V2) coffee machine status while brewing but using an **ESP32 development board** instead of others boards like the ESP8266 used by dougie996. As I had one hanging around unused, I thought that I could make use of it for the monitoring purposes.

Moreover I wanted to have a slightly bigger display than the 0.96'' OLED used in all other projects. So I went for a 1.3'' that is using a different library than the one normally seen for 0.96'' display.

Last but not least, I wanted to integrate the project with MQTT and have data collected in Home Assistant, but the M1N1 project I forked did not foresee the usage of MQTT authentication, which is mandatory in Home Assistant MQTT Mosquito Broker!

So the main difference of this repo can be summarized in the support of:

*   ESP32 boards
*   SPI Oled display (1,3'') with 7 pin, using the library Adafruit\_SH110X.h
*   MQTT Client authentication for Home Assistant MQTT Mosquito broker

## Key Features

What you can expect to see when you connect the board and display toyour MaraX

*   **Idle mode**
    
    In the upper left corner is the Heater Status. While heating, a blinking cursor and Text "Heatup" is shown. In the upper center a WiFi Icon is shown, together with the WiFi Signal Strength, when connected to WiFi. In the upper right the Mara X Mode of operation is shown. A Coffeecup signals Coffee Priority Mode; a Steam Symbol Steam Priority Mode. Lower part left & right: reported Temperature of Heat Exchanger and Steam Boiler.
    
*   **Operation mode**
    
    \- When **coffee brewing** sequence is started:
    
    the Steam Temperature display is replaced by a shot timer, counting seconds up and a filling up Coffeecup is shown on the left, together with the Heat Exchanger Temperature.
    
    \- **After brewing sequence has ended**:
    
    the Display returns to idle Mode.
    
*   **MQTT Published data**:
    
    The following parameters are published via WiFi to a connected MQTT Server  
      
    \*\* Mara Software Version and Mode of Operation  
    \*\* Steam Temp  
    \*\* Target Steam Temp  
    \*\* Heat Exchange Temp  
    \*\* Heating Boost Mode  
    \*\* Heating Element on/off  
    \*\* Pump on/off  
    \*\* WiFiRxLevel  


## Configuration and setup

###   **Software configuration**

In order for the board to work and send data to MQTT broker, you need to modify the file **secrets.h**. 
It contains Parameters like WiFi SSID and Password, MQTT Server Address & Port, MQTT Username and password. 
You can also define the MQTT Update Interval in seconds. You need to match this based on your requirements.

###  **Hardware Configuration**

Let's spluit the hardware configuration in two parts:

1) **Lelit MaraX to ESP32 Board**
	
The best information around Lelit Mara X hardware is available here: https://www.m1n1.de/en/lelit-mara-x-v2-gicar-internals/ 

According to the link above, we do not need to connect the ESP32 Tx Line / Gicar Rx Line. There's in fact no way to program the "brain" of the MaraX through the serial interface.

On the other end, it is super important to consider **how to connect the ESP32 UART pinouts**. In the image below, our friend dougie996, shows how to connect the Lelit MaraX Gicar to an ESP8266 Wemos D1 clone. The same applies for the ESP32. Simply put: you can't have 5V running on the serial/UART pins! They are not meant to work with higher voltage than 3.3v. So, do yourself a favour and follow thes scheme to connect the UART TX/RX/GND between the MaraX and your ESP32 board: 

<img src="https://github.com/dougie996/M1N1MaraX_MQTT/assets/117717919/8c066df9-6e21-4d42-b458-7699bd4b0714" alt="" align="middle" width="auto" height="auto">
<p></p>

2) **OLED Display**

I am using a 1.3'' OLED display, connected to the ESP32 through SPI/7 pins. Here is how you want it to be connected to the dev board in order to work with the code of this repository:    

*TO BE COMPLETED*

## 3D printed CASE

**Other**: *TO BE COMPLETED*



![MaraX_MQTT_final](https://github.com/dougie996/M1N1MaraX_MQTT/assets/117717919/41279506-7fa4-4b17-8ba5-9439497c996f)
