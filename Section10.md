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

## How do we write firmware
Now theory is cool and all but how do we actually write firmware? I believe the best way is to see an example and explain each bit.

```Cpp
#include "mbed.h"

UnbufferedSerial pc(USBTX, USBRX, 112500);
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



