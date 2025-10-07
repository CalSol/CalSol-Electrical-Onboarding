# Section 10: Basics of Firmware

Now that you have all the necessary software, we want to actually work with our microcontrollers! This section will go over the basics of firmware to start working with it. 
- I am going to assume that you understand basic coding syntax like for loops, print statements, etc. If not here is a great resource: [WIP]
- This is a *starter* guide. You will learn more with the team!

### We will focus on the following:
- Analog vs. digital signals
- GPIO pins
- Pull-up resistors
- A basic PWM (Pulse Width Modulation)
- A simple firmware example

## Setting the stage: Microcontroller Basics: 
A microcontroller is a tiny computer that directly talks to the hardware. Unlike your PC, there is no operating system. Instead we write firmware that directly runs on the chip!

The way you interact with the MCU are through **pins**. Each MCU has their own pin config that is specified in their datasheet (For example here is the ESP32 pinout [WIP]) and each pin can be a combination of:
- GPIO (Digital General purpose IN/OUT pins)
- PWM (For when you want a pin to be "analog like")
- Analog IN: For when you want to make an ADC 
- "Special function": These are your VCC, GND, res pins. They are used for that and that only. Please do not try to turn on an LED with it
- Some pins are **multiplexed**: These pins can be used as GPIO or a special role the datasheet will describe (I2C, UART, SPI, etc)

Here is an example of a pinout for the ESP32. We developed ours in house so it may be a little different.
[!ESP32](./images/ESP32Pinout.png)

## Pullups, Analog, Digital, PWM, Input/Output
This section is to clarify the common terminology. If you understand this feel free to skip

Digital: Computers love binary: 1 (HIGH) or 0 (LOW). Think of this like a switch that is either on or off. 
Analog: A continuous range of values between a and b. For example 3v3 to 5v. Let's say you wanted to control a fan speed (BMS have these). Greater voltage is greater speed. We can control this with a potentiometer (steering has this) and hook up the signal to an Analog in pin.

Input/Output:
- Self explanatory but for examples: Buttons are an INPUT. An LED responding to the button press is an OUTPUT

PWM: 
- Remember the hardware lab? Well our MCUs actually can use (most) pins to simulate an analog signal. Then we can wire a potentiometer to a pin that has a built in ADC (read the datasheets yall).

## How do we write firmware
Now theory is cool and all but how do we actually write firmware? I believe the best way is to see an example and explain each bit. Now I want to add a disclaimer: this code is assuming the Mbed framework. Chances are for the ESP32 (the MCU we will use going forwards) will NOT use the mbed framework. However I believe it is a good idea to be able to read Excalibur's old code. 

```Cpp
#include "mbed.h"

UnbufferedSerial pc(USBTX, USBRX, 115200);
PwmOut servo(PA_15); //servo pin
AnalogIn pot2(PC_1); //potentiometer input pin
PwmOut led1(PB_13); //Led with PWM not digital control
int pulseMin = 500; 
int pulseMax = 2500;

int main()
{
    while(true) {
        float voltage = pot2.read();
        int millivolts = voltage * 3.3f * 1000;
        int servoValue = pulseMin + (millivolts * (pulseMax - pulseMin)) / 3300;
        //printf("Servo Value: %d \n", servoValue);

        servo.period_ms(20);
        servo.pulsewidth_us(servoValue);
        led1.write((float)(servoValue - pulseMin) / (pulseMax - pulseMin));

        int servoAngle = (millivolts * 180) / 3300;
        printf("Voltage: %d mV\n", millivolts);
        printf("Servo Angle: %d degrees\n", servoAngle);

        ThisThread::sleep_for(2s);
    }
}
```

This block of code is something I wrote when I first started firmware! It tells an STM32 to turn an LED on/off 

Let us go step by step: 

```cpp
#include "mbed.h"
```
This is our mbed library. Allows use to use mbed functions like PwmOut, AnalogIn, UnbufferedSerial, etc

```cpp
Unbuffered serial pc(USBTX, USBRX, 115200)
```
USBTX/USBRX are the default pins for UART (not going over that)
115200 is the baud rate. This is the speed of communication. 115200 is a common default

```cpp
PwmOut servo(PA_15); //servo pin
PwmOut led1(PB_13); //Led with PWM not digital control
AnalogIn pot2(PC_1); //potentiometer input pin
```
**Defining our output pins**
- Servo: A PWM-controlled output connected to a servo
- led1: A PWM-controlled LED (we can vary the brightness!)
- pot2. Its a potentiometer reading
In Mbed you define varname(pinout)
- For an ESP32 it would be like GPIO32 instead of PC_1

1 ...2 ...skip a few

```cpp
float voltage = pot2.read();
int millivolts = voltage * 3.3f * 1000; 
```
pot2.read() will return a float from 0.0 to 1.0 proportional to input voltage
To get to the 3.3v (standard for MCU), mutliply by 3.3f. Then multiply by 1000 to get to volts. 

```cpp
int servoValue = pulseMin + (millivolts * (pulseMax - pulseMin)) / 3300;
```
This linearly maps the potentiometer voltage

```cpp
servo.period_ms(20);
servo.pulsewidth_us(servoValue);
```
Sets the PWM period to 20ms (50hz). This is very standard for hobby servos
Sets the high-time of the PWM signal to control the angle

The rest is fairly self explanatory. I just wanted to overexplain in the case it is not. 

If we are using the arduino libraries and cpp, here is what it is:
```
#include <Arduino.h>

const int servoPin = 15;
const int potPin = 32;
const int ledPin = 13;

int pulseMin = 500;
int pulseMax = 2500;

void setup() {
  Serial.begin(115200);
  ledcSetup(0, 50, 16);
  ledcAttachPin(servoPin, 0);
  ledcSetup(1, 5000, 8);
  ledcAttachPin(ledPin, 1);
}

void loop() {
  int potValue = analogRead(potPin);
  float voltage = (potValue / 4095.0) * 3.3;
  int millivolts = voltage * 1000;
  int servoValue = pulseMin + (millivolts * (pulseMax - pulseMin)) / 3300;

  int duty = map(servoValue, pulseMin, pulseMax, 0, 65535);
  ledcWrite(0, duty);
  ledcWrite(1, map(servoValue, pulseMin, pulseMax, 0, 255));

  int servoAngle = (millivolts * 180) / 3300;
  Serial.print("Voltage: ");
  Serial.print(millivolts);
  Serial.println(" mV");
  Serial.print("Servo Angle: ");
  Serial.print(servoAngle);
  Serial.println(" degrees");

  delay(2000);
}
```





