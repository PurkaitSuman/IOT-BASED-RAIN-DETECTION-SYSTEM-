# PROJECT OBJECTIVE

Water managed from rainfall aims to reduce economic impact and risk of lives. Most developing countries depend on rainfall for their water needs. However with poor management of rainfall water, it is difficult for example to determine water losses to evaporation or ground water recharge, how much is still available etc. Therefore rainfall measurement and monitoring is an important factor when it comes to water management as this determines the current rainfall and future prediction of rainfall hence leading to better management of water. Rainfall measurement devices like rain gauges have been a useful tool in the weather monitoring systems for a very long time. Since a rain gauge was one of the devices that were proven to be beneficial, particularly to agriculture, the rain gauge system has been improved as technology advanced. In the water control and management systems for example, these sensors can be used to help obtain and process information such as rainfall, soil moisture, and soil temperature over large geographical areas. The network uses a tipping bucket rain gauge (TBRG), temperatures and humidity sensors, GPRS module and a micro-controller to relay rainfall data to a remote server, while a solar panel is used to convene energy to critical components of the wireless sensor network.


# INDEX

1. PROJECT COMPONENT LIST
2. DESCRIPTION OF EACH COMPONENT
3. PROJECT DISCUSSION
4. PROJECT STEPS
5. PROJECT PICTURE
6 .PROJECT CIRCUIT DIAGRAM
7. RESULT
8. CONCLUSION


# PROJECT COMPONENT LIST

1. Nodemcu board x 1 
2. Rain sensor x 1
3. LED x1
4. Resistor 1k ohm
5. Breadboard x 1 
6. Jumper wires


# DESCRIPTION OF EACH COMPONENT

Nodemcu board:-  NodeMCU is an open source firmware for which open source prototyping board designs are available. The name "NodeMCU" combines "node" and "MCU" (micro-controller unit). The firmware uses the Lua scripting language. The firmware is based on the eLua project, and built on the Espressif Non-OS SDK for ESP8266.

 ![image](https://user-images.githubusercontent.com/65341291/180371637-2cc73e60-13a1-447f-b486-0badc0c1b64b.png)
                                       

Rain sensor:- A rain sensor or rain switch is a switching device activated by rainfall. There are two main applications for rain sensors. The first is a water conservation device connected to an automatic irrigation system that causes the system to shut down in the event of rainfall.

![image](https://user-images.githubusercontent.com/65341291/180372711-fc81e8fb-9be7-42db-9f8a-837d6424dfe8.png)


LED: A light-emitting diode (LED) is a semiconductor light source that emits light when current flows through it. Electrons in the semiconductor recombine with electron holes, releasing energy in the form of photons.
 
![image](https://user-images.githubusercontent.com/65341291/180372753-8686c0d2-1eac-49ff-b3b9-15cf3e1c5295.png)


Resistor :  A resistor is a passive two-terminal electrical component that implements electrical resistance as a circuit element. In electronic circuits, resistors are used to reduce current flow, adjust signal levels, to divide voltages, bias active elements, and terminate transmission lines, among other uses.   
 
![image](https://user-images.githubusercontent.com/65341291/180372783-b06fbf9a-d2bb-4429-bac9-14fec1760832.png)


Breadboard: A thin plastic board used to hold electronic components (transistors, resistors, chips, etc.) that are wired together. Used to develop prototypes of electronic circuits, breadboards can be reused for future jobs. They can be used to create one-of-a-kind systems but rarely become commercial products.
 
![image](https://user-images.githubusercontent.com/65341291/180372802-1b3d5438-31ae-46c7-975b-b5e0b4d4fa7c.png)


Jumper wires: Jumper wires are simply wires that have connector pins at each end, allowing them to be used to connect two points to each other without soldering. Jumper wires are typically used with breadboards and other prototyping tools in order to make it easy to change a circuit as needed. Fairly simple.
 
![image](https://user-images.githubusercontent.com/65341291/180372830-549a3a48-b066-444a-9962-7d689375f472.png)


# PROJECT DISCUSSION

In this project we'll see how to Interface raindrop sensor to NodeMcu and get alarm whenever the rain intensity crosses some threshold. It can be used as a switch when raindrop falls through the raining board and also for measuring rainfall intensity. The module features, a rain board and the control board that is separate for more convenience, power indicator LED and an adjustable sensitivity though a potentiometer.
Raindrop sensor is basically a board on which nickel is coated in the form of lines. It works on the principal of resistance. When there is no rain drop on board. Resistance is high so we gets high voltage according to V=IR. When rain drop present it reduces the resistance because water is conductor of electricity and presence of water connects nickel lines in parallel so reduced resistance and reduced voltage drop across it.


# PROJECT STEPS
Step 1
Firstly, identify these components.
  
                   ESP8266 Nodemcu                              Rain sensor

  
                            LED                                       Breadboard                            
                          Jumper wires

Step 2
Secondly, connect these components. To do this, use the circuit diagram below.

 ![image](https://user-images.githubusercontent.com/65341291/180372135-d41ad4bc-09b0-426d-a84b-be1aedc29b3a.png)


Step 3
Thirdly, we set up the Thingspeak app. To do this, follow the steps below.
•	First, go to the Thingspeak website and create a new account using my email address. Then, click the “New channel” button.

 ![image](https://user-images.githubusercontent.com/65341291/180372191-acfa3d33-f04a-4d4b-93d8-929a4844d73f.png)
![image](https://user-images.githubusercontent.com/65341291/180372215-474c9ec6-ed6c-46a2-a6be-12dff7687b71.png)
![image](https://user-images.githubusercontent.com/65341291/180372239-ac2b4f62-b4a9-47aa-be23-c26a28448704.png)

Next, enter my project name as my like. Then, activate the four fields and name “Rain_level”. After, click the “Save channel” button.

 ![image](https://user-images.githubusercontent.com/65341291/180372251-94149f06-392f-48a9-aefc-7e2fd70d0513.png)
![image](https://user-images.githubusercontent.com/65341291/180372346-ca8de9f1-c70a-449f-849f-42c5b7108431.png)
![image](https://user-images.githubusercontent.com/65341291/180372366-7f0b3f74-8df1-4061-b05f-0514f39a7eeb.png)

  
•	So, now we can see the interface of this project.

 ![image](https://user-images.githubusercontent.com/65341291/180372390-e70c6afe-4cca-48d7-b64a-ba0558e94e5d.png)


Step 4
Now, let’s create the program for this project. It is as follows.
•	WI-Fi library — Download
Code:
#include "ThingSpeak.h"
#include <ESP8266WiFi.h>

const char* ssid     = "CHATTERJEE HOUSE";
const char* password = "Tatha@1234";
const char* server="api.thingspeak.com";
int status = WL_IDLE_STATUS;

unsigned long channel =1510198;
unsigned int soil = 1;
const char* APIkey = "I3XEJVKB9JMRQK3T";

WiFiClient  client;

void setup() 
{
  Serial.begin(9600);  
  pinMode(A0, INPUT);
  WiFi.begin(ssid, password);
  ThingSpeak.begin(client);
  Serial.begin(9600);
}

void loop() 
{
  int sensor = analogRead(A0);
  
  Serial.println(sensor);

  ThingSpeak.setField(1, sensor);
  ThingSpeak.writeField(channel, 1, sensor, APIkey);
  Delay(5000);
}


Step 6
Now, go back to the Thingspeak app and click the private view tab. 
 ![image](https://user-images.githubusercontent.com/65341291/180372041-338b55b0-4036-4e6f-9ae6-cb2ee62e99ab.png)
![image](https://user-images.githubusercontent.com/65341291/180372079-895dda5d-cfff-4641-b6f4-bdfc58522b74.png)

 


# PROJECT PICTURE
 ![image](https://user-images.githubusercontent.com/65341291/180372017-69a6d7fb-337d-45f1-a47c-b9b7e77a0c08.png)



# PROJECT CIRCUIT DIAGRAM
![image](https://user-images.githubusercontent.com/65341291/180371976-a8c07f9f-ef00-43d8-a29c-a187acc4315c.png)


# RESULT

This system works in such a way that, when there is rain, the rainwater acts as a trigger, which switches on the buzzer. In the Rain Drop Sensor Arduino Code, we defined that pins 5, and A0 are buzzer and rainfall. By doing this, we can change the pins in the defined part of the function, and the remaining part of the code will be untouched. This will make the programmer in editing the pins easily.
In the void loop, the analogRead command reads the value from the sensor. In the next line, the command Serial.println(value), prints the value on the serial monitor. This will be helpful while debugging. The map function maps the incoming value between 0 -225. The function format for the map is a map (value, min value, maximum value, value to be mapped for minimum value, value to be mapped for maximum value). The buzzer will be switched ON or OFF, depending on the set value and the output of the sensor. This value is compared if function, with the set value. If the value is greater than the set value, it will switch on the buzzer. If the value is less than the set value, the buzzer will be switched off.


# CONCLUSION

A simple Rain Detection System can be easily built by interfacing an Arduino with Rain Sensor. The sensor will detect any rainfall falling on it and the Arduino board will sense it and can perform required actions. A system like this can be used in many different fields, such as agriculture and automobile fields. Rainfall detection can be used to automatically regulate the Irrigation process. Also, continuous rainfall data can help farmers use this smart system to automatically water the crop only when absolutely required. Similarly, in the automobiles sector windshield wipers can be made fully automatic by using the rain detection system. And the Home Automation Systems can also use rain detection to automatically close windows and adjust room temperature. In this tutorial, we will build a basic rain sensor using Arduino with a buzzer. You can then use this set-up to build anything you wish on top of it. Also, note that the rain sensor module is also referred to as a raindrop sensor or rain gauge sensor or rainwater sensor based on usage, but they all refer to the same sensor used in this project and they all work on the same principle.
We have also built a simple Rain Alarm and an automatic car wiper by using 555 Timer only, you might want to check that as well if you do not want to use an Arduino.That being said, let’s get back to this project and start building our Arduino Rain Gauge.

REFERENCES

ThingSpeak:https://thingspeak.com/channels/1510198/private_show
Arduino: https://www.arduino.cc
Rain Sensor :https://lastminuteengineers.com/rain-sensor-arduino-tutorial
ESP8266 NodeMCU:https://lastminuteengineers.com/esp8266-nodemcu-arduino-tutorial/



