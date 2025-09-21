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








## Writing firmware. Pullups, analog, digital, read/write




