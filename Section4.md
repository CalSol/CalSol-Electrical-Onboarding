# Section 4: PWM Driver Design Concepts and Schematic

> Make sure you finish section 3’s practice section before starting!
> And also make sure you've watched this [video](https://www.youtube.com/watch?v=UPTU6nYSaMo&t=860s) before starting on this section!

As you may know, for this project you will be creating your own PCB for a motor controller using KiCAD. Here are the project requirements: 
- Different ways to power and control LEDs (the schematic you made from the previous section)
- A potentiometer that can control the speed of a motor through a 555 timer and PWM
- Your board will be powered off an external 12V supply with a connector.

However, there are a few concepts you should understand first.

## Pulse Width Modulation

PWM (Pulse Width Modulation) is a technique used to control the power delivered to electronic devices. It works by switching a signal between high (on) and low (off) states at a fast rate, allowing us to average the power. The duty cycle (the percentage of time the signal is high) determines the effective average power. For example, PWM could be used to control the brightness of an LED, lamp, or the speed of a motor.

How it works:
- A higher duty cycle (e.g., 75% high, 25% low) delivers more power.
- A lower duty cycle (e.g., 25% high, 75% low) delivers less power.
- This is efficient because the switching circuit dissipates very little power, as it is either fully on or fully off.

## 555 Timer
The 555 timer is a versatile integrated circuit used for timing, pulse generation, and oscillator applications. For example, 555 timers can be used for generating clock pulses for circuits. The key skill to use here is abstraction from section 2!
You can check out the datasheet if you are interested.

How to use it: 
- Internally, it uses voltage comparators, a flip-flop, and a discharge transistor. 
- By configuring external resistors and capacitors, you set the timing intervals. 

## RC Circuit
An RC circuit is a circuit consisting of a resistor (R) and a capacitor (C). It can be used for filtering and timing. In our case, we use it as a timer.
How it works: 
- The capacitor charges and discharges through the resistor, with the rate determined by the time constant. 
- In a low-pass filter, it allows low frequencies to pass and blocks high frequencies. 
- In a high-pass filter, it allows high frequencies to pass and blocks low frequencies.

### Decoupling Capacitors
Decoupling capacitors are filters used to stabilize voltage in electronic circuits. For example, decoupling capacitors are used to reduce noise in microcontroller circuits. 

How it works: 
- They are placed near integrated circuits (ICs) to filter out noise and provide instantaneous current during transient demands. 
- When the supply voltage fluctuates, the capacitor absorbs or supplies charge, maintaining a stable voltage. 

## MOSFETs
A MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) is a type of transistor used as a switch or amplifier in electronic circuits. For example, MOSFETs are used for switching power to a motor or amplifying audio signals. 
In our case we use it as a switch for the motor or light bulb we are powering to create our on and off PWM signal.

How it works: 
- The MOSFET has three terminals: Gate, Drain, and Source
- Applying voltage to the Gate creates an electric field, controlling the flow of current between the Drain and the Source. 

There are two main types: 
- N-channel: Current flows when the gate voltage is positive 
- P-channel: Current flows when the gate voltage is negative 

MOSFET gate resistors are used for: 
- A gate resistor is used to limit the current into the MOSFET’s gate when switching.
- This helps prevent Damage to the MOSFET from high inrush current and excessive ringing caused by fast switching and parasitic inductance
- They lead to smoother operation in PWM-controlled circuits. 

# Checkpoint and Deliverables (IMPORTANT!)
- In the same file that you made the 3 Led circuits, you will be building your PWM driver (motor controller) circuit.
- You will be building the same functional circuit as the image below (doesn't have to be a carbon copy)!
- Make sure to run the ERC checker (top toolbar) to make sure KiCad is happy about your schematic!
- For CalSol members, take a screenshot of your circuit (both LED and PWM driver) and ERC checker to a lab staff to move on to the next section once your circuit is approved!
- Ask for help if you need it!
Lab Staff to reach out to: Ahmed A, Alex W, David N, Eric L, Jonathan J, Matthew L, Sina K

(Please note in the image below, the led circuit on the left should be the led circuits you made from section 3)

![Onboarding Lab Schematic](https://github.com/user-attachments/assets/a69d805a-5a81-40b7-b31b-0eb244053f46)
