# Section 2: EE Fundamentals

### What is a PCB?

A **PCB** (Printed Circuit Board) is a compact circuit made out of various electrical components and wire traces. In this section of the lab we will explain the different parts that make up a PCB, but firstly we must learn the basics of electricity.

## Introduction to Electricity

Let’s learn how we can mathematically analyze circuits with **Ohm’s law**. Ohm's law relates current, voltage, and resistance in a circuit. Let’s tackle each part of this triangle separately.

![Ohms Law](https://github.com/user-attachments/assets/6206285b-92ac-403f-9860-03dffe5d3d73)

### Current

**Current** is the flow of electricity! More specifically, it is the flow of electrons. We denote the flow of the conventional current opposite the flow of electrons with an arrow on a circuit diagram. The unit of current is amps (A).

### Voltage

But what causes electrons to flow? Power sources contain energy, called **voltage**, creating a difference in potential energy that causes electrons to flow. Picture water flowing downhill, with the hill's height representing voltage. At the top, the water has high potential energy, similar to a high voltage. As the water moves down, it flows naturally to lower points, just like current flows from high voltage to low voltage in a circuit. The steeper the hill (or the greater the voltage difference), the stronger the flow of water, much like a greater voltage difference creates a stronger current. The unit of voltage is voltage (V).

### Resistance

However, the flow of electrons, or current, can be restricted. This is called **resistance**. The unit of resistance is ohms (Ω). Resistance, along with voltage and current are related together by Ohm's law which states V = IR.

Together, using the triangle of Ohm’s law, we can analyze a simple circuit!

### Example

What is the current of this circuit? Note, that the resistor (denoted with the zig-zag line) is what creates resistance in a circuit.

![Ohm's Law Example](https://github.com/user-attachments/assets/08a97061-4578-4e5f-ba22-7a47f4808ac4)

## Components and Nodal Analysis

**Components** are a part that makes up an electrical circuit. Now we will discuss a variety of common components and how to use them:

### Power Supply

First, we need a **power source**. A power source is something that has voltage and thus powers the circuit itself. Here is a wide range of power sources you might have to work with, but for this lab the **direct current (DC)** power supply will be used.

![Power Symbols](https://github.com/user-attachments/assets/82e676c1-cb27-4912-be61-d7c9323fe407)

### Resistors

Next, we have the **resistor** we just saw before. These add resistance to the circuit. We add resistance to control the flow of current and the levels of voltage around the circuit. Controlling current and voltage is especially important for adjusting levels of signals and preventing problems like shorts which will be discussed later.

When calculating the total resistance across a path of wire with multiple resistors using Ohm’s law, we need to learn how to calculate resistors in series or in parallel. Here are pictures of both concepts, each with the method of calculation. 

![Resistors in Series and Parallel](https://github.com/user-attachments/assets/e34f8b16-ee6d-4a5d-af94-dcd6ba0adcc0)

### Voltage Divider Example

With these two components we can construct a common circuit element called a voltage divider, which can be used to explain a few more concepts.

![Voltage Divider](https://github.com/user-attachments/assets/52e14943-2c3a-401b-a43e-191a8f2327d4)

A resistor can divide two different voltages, as we think of wires as ideal conductors with zero resistance. Each conductive wire that connects two or more components together is called a node and each node has a given voltage! Each node is color coded in the picture. When we calculate the voltage and current in a circuit, we are measuring these values at certain nodes. To aid in calculating voltage and current at certain nodes, we can use **Kirchhoff’s Laws**.

### Kirchhoff's Laws

![Kirchhoff's Laws](https://github.com/user-attachments/assets/903ad1e2-ed55-463e-9411-91b1f4364417)

Kirchhoff’s Current Law (KCL) states that the amount of current entering a node is equal to the amount exiting the node. Kirchhoff's Voltage Law (KVL) states that the sum of voltage around a loop is zero. Think of these as a form of conservation of energy.

With this we can calculate the voltage at each node using KVL:

![KVL Problem](https://github.com/user-attachments/assets/06eacd0f-be9d-4eb1-918d-a8631d08f7ab)

The triangle symbol attached to the green node at the bottom represents ground. Ground is defined as a place on a circuit with no voltage. 

For future reference, we can calculate a voltage divider with this equation:

![Voltage Divider Rule](https://github.com/user-attachments/assets/d84b608d-3dd2-4cd9-8d5e-779f0e671e2f)

### Power

You may also have to deal with power in a circuit. This is calculated with this equation:

![Electric Power](https://github.com/user-attachments/assets/ea7f302d-5b70-48b1-bb71-4fc8c105e4a2)

This idea of power explains why a **short circuit** is so dangerous. A short is where there is some low resistance path that bypasses resistance in a circuit. As seen, a conductor connecting a very high potential and low potential node will create a massive amount of power. If the conductor inherently has some low resistance value like 0.0005, the power going through the light will change from some manageable value to wattage in the hundred thousands. We should be careful of shorts as they can break components and destroy our circuits. 

### Short Circuit

![Short Circuit](https://github.com/user-attachments/assets/37458df0-a9cd-43a9-b9d0-2b81b3857697)

### Open Circuit

Another important concept is an **open circuit**, which is caused by a break in the circuit. This mathematically can be represented as the circuit at the break having infinite resistance. By Ohm’s law, an open circuit must have zero current flow which will cause the circuit to no longer work.

![Open Circuit](https://github.com/user-attachments/assets/5eb74d1b-1add-4eb4-bdb1-511036a08e0b)

### Diodes

As you work with different circuits, you’ll start to see a few common components (aside from resistors and batteries). The first you’ll probably run into is a **diode**. 

![Diode](https://github.com/user-attachments/assets/8df944ea-b27f-4f9d-a501-61b39a8dbcad)

A diode is a one-way path that moves in the direction of the arrow. Current can flow from high potential to low potential (right to left), but if the diode is flipped, current won’t flow through. In your schematic, current will flow in the direction of the arrow, and in a real circuit, current flows from the longer (positive) leg to the shorter (ground) leg. Diodes can be a great way to protect your components in case of circuit failure. The most common form of a diode is a **light-emitting diode (LED)**. 

![LED](https://github.com/user-attachments/assets/1ddf7aa1-5fd8-4d70-864c-1a06daa83e66)

LEDs work the exact same as other diodes but with the added effect of emitting light as current flows through them - hence the name.

### Capacitors

Another important component you’ll see often is a **capacitor**. Capacitors are made up of two identical parallel conductive plates. 

![Capacitor](https://github.com/user-attachments/assets/fe6a9f2f-af77-47c5-b018-1beaa58021a4)

You can think of a capacitor as a bucket. As current flows through the circuit, charge will accumulate on the positive side of the capacitor, storing energy in the capacitor. You can think of it as taking water from a lake and storing it in a bucket for later use. That energy can be accessed if, for example, a switch is flipped that disconnects the capacitor from the power source. The energy in the capacitor will act as a super short temporary battery, draining through the rest of the circuit until it runs out. 

Capacitors, similar to resistors, can also be placed in parallel or series and thought about using these equations:

![Capacitors Series and Parallel](https://github.com/user-attachments/assets/7b31f106-b2e0-43ad-921d-0c7d5a63f431)

### Switches

Another simple component is a **switch**. A switch is a mechanical component that changes the flow of current between multiple states. An example is one state being an open circuit and another being a closed circuit.

![Switch](https://github.com/user-attachments/assets/cc6b51a7-96f4-4b7e-b01a-36ccd9bbda16)

### Integrated Circuits (ICs)

In this lab, we’ll be using an integrated circuit (IC). An integrated circuit is a chip or component that has its own subcircuits inside. In our case, we’ll be using a 555 timer. While it’s important to know WHAT an IC does, we don’t necessarily need to know HOW it works. This concept is called abstraction. If you’ve taken CS61A, you’re very familiar with this concept. 

<img width="939" alt="Screen Shot 2025-01-29 at 9 18 27 PM" src="https://github.com/user-attachments/assets/a01d96a9-a736-467e-ba74-94677d9c2801" /> (examples of different IC packages)

For example, many of you may have worked with Arduinos in the past. The Arduino is made up of a number of complex and interconnected circuits, but we don’t actually have to know anything about these circuits to work with the Arduino. All we need to know is that it has input and output pins and can be used as a power source, among other things. In the same way, while we don’t need to explicitly understand what is going on inside our 555 timer, we can still use it in our circuit by abstracting its use to a timer that can be used to control a motor driver. 

## Conclusion

Now that you have some foundational understanding of the components you will be using in the lab, you will now learn how to actually design a PCB in KiCad!

### Answer to practice question:
0.02 A
