# Section 5: PCB Layouts

To make a good layout, you must know how to select proper components, how to place components, signal integrity, trace width and how to calculate it, decoupling capacitors, and vias. Let’s break them down for you. 

## Component Selection (see more on this later)
- Electrical Requirements:
  - Components must meet voltage, current, and power dissipation needs with safety margins
- Footprint and Packaging
  - Match footprints to PCB space and layout constraints
  - Choose packages suitable for hand-soldering or your own application
- **Cost!!!**
  - Always go for cheaper (but correct!) choices to reduce cost
- Design Specifics
  -  Select components tailored to the project

## Component placement
- Place components logically: group related components in different subcircuits close together.
  - Maybe even divide the PCB into different subsections
- Minimize trace lengths for high-speed or sensitive signals. (not applicable to this lab)
- To maximize signal integrity do things like avoiding sharp corners in traces or use ground planes to minimize noise (more on this later)
- Position decoupling capacitors as close as possible to power pins of ICs (more on this later)
- Align components for a clean layout (avoid random orientations).
- You are allowed to run traces over/under component footprints.
- Good practice to keep boards smaller, and reduce unnecessary spacing.

## Signal integrity
- Avoid sharp corners in traces; use 45-degree angles for bends!! (More applicable to high-speed PCB design but it is a good practice)
- Keep high-speed signals (like clock lines) short and away from noisy traces (other high-speed signal traces).
- Use ground planes to minimize noise and improve signal return paths.

## Trace width
- Calculate trace width based on current using online calculators like PCB Trace Width Calculator.
- Tutorial video: (https://www.youtube.com/watch?v=Jjl1qh8-0BA)

## Decoupling capacitors
- Place them as close as possible to IC power pins.

## Vias
- Use vias to connect traces between layers.
- Keep via count minimal to reduce parasitics.

# How to assign footprints?
Here are some things you should know when assigning footprints on KiCad.
#### Why assign footprints?
In section 4 you had symbols of different electrical components, but each component can come in many different sizes and packages. (Ex a resistor of 1k Ohmns can come in a tiny size, a huge size, a different power rating, etc). So we need to tell KiCad which footprints (or specific component size) we are using for each component we added in our schematic. 

### For passive components (resistors, capacitors, etc)
  - There are standard component sizes
  - Search for components on DigiKey or Mouser by filtering parameters such as package type, value, and voltage ratings
  - Read the datasheet to see if they use a standard package.
  
> For CalSol we use 603 handsolder footprint size for all passives (resistor and capacitor)**
  
### Surface Mounted Devices (SMD) vs Through-hole Technology
  - SMD’s are components that connect directly to pads on the board on the top surface/
    - Smaller (save space), generally more expensive, easier industrial assembly
  - THT’s are components that connect through drilled holes on the board
    - Larger, generally cheaper, easier to hand solder, withstands mechanical stress better

#### Components we’re using for this lab

![Components](https://github.com/CalSol/Sp25-CalSol-Electrical-Training/blob/ea8b3a9f7142656ea9ba4345da6d108cf24544d3/images/Footprint%20Assignment.png)

- Be reminded that footprint selections vary from project to project, and for certain projects you have to make specific choices for certain components. (For example, D4 (diode used for motor circuit) uses a through-hole component as it was the only device that matched the requirements of this project). For this project, we did the hard work for you. 
- Sometimes KICAD might not have the footprint you want to use (for example the potentiometer we are using), to address this, there are two methods:
    - Download online
      - In short: Search online for the specific component - download the footprint - go to PCB Layout Editor - Preferences(Toolbar) - Manage Footprint Libraries - ![2](https://github.com/CalSol/Sp25-Electrical-Training/blob/main/images/2.png) - open the file that ends with .pretty - OK
      - A Video that might help: (https://www.youtube.com/watch?v=W9cLnIjvybo)
    - Create a footprint by yourself
      - (https://www.youtube.com/watch?v=W9cLnIjvybo)
- Link for the potentiometer footprint: (https://www.digikey.com/en/models/2408877) (The schematic from Section 4 has wrong symbols for the potentiometer that we are using.)

### Layouts on KiCAD:
So how do we do this on KiCAD? Let’s find out! Below is everything you need to know in order to achieve this. But make sure you have footprints correctly assigned! 

### How to fill in constraints
- Each PCB manufacturer will have different manufacturing tolerances (for example they can’t make via holes smaller than 0.02mm)
- For this project we will be following JCLPCB’s rigid pcb manufacturing constraints seen here (https://jlcpcb.com/capabilities/pcb-capabilities)
Now you must go into KiCad and fill in these constraints for KiCad can warn you with the DRC checker if you are making a fatal mistake. You can follow the link here: (https://learn.pcbcupid.com/pcb-design/kicad-tutorial/kicad-constraints-net-class-directive/#:~:text=Constraints%E2%80%8B&text=Go%20to%20the%20board%20setup,design%20within%20the%20manufacturing%20limit).
- You can also look at this [video](https://www.youtube.com/watch?v=Fv9zQ3nkLqk&list=PLn6004q9oeqGl91KifK6xHGuqvXGb374G&index=8) about how to change the constraints in setting. 
 
### How do draw edge cuts in KiCad
- Use the Edge.Cuts Layer to define the PCB's size, shape, and outline.
- Draw using the Line Tool.

### Layers in KiCad
- Top Layer: Components and traces.
- Bottom Layer: Ground plane and additional traces.
- Use the Layer Manager to switch between layers.

### Traces, vias in KiCad
- Use the Route Tracks Tool to connect components.
- Switch layers by adding vias (make sure they're bigger than JCLPCB's min size!).
- When adding vias you have to define what "node" or "net" the via belongs to! You can press "e" to change its properties. 
- Follow trace width guidelines from earlier.

### Filling planes
- Add a ground plane on the bottom layer
  - Use the Add Filled Zone Tool.
  - Assign it to GND net.

### Design Rules Checker (DRC)
- Enable the Design Rules Checker (DRC) to avoid placement issues (top tool bar like ERC).

### Some shortcut buttons.
- `M`: Move component.
- `R`: Rotate component.
- `B`: to fill in fill tools. 
- `X`: Route trace.
- `V`: Add via.

# Layout instructions and constraints specific to the lab. 

Here is a walkthrough [video](https://www.youtube.com/watch?v=4Plw6e2EKes) (feel free to watch at a faster speed)
Here is another [helpful YT link](http://youtube.com/watch?v=3FGNw28xBr0&t=399s)
- Refer to “Component placement” above
- Things to be mindful of:
  - Try placing the 555 timer in the center as it has the most number of pins.
  - Try to put the components that belong to the same subcircuit on the same section of the board.
  - When routing, maintain a sufficient distance (if possible) between the trace and pads/holes/vias, since not doing so -   - might result in error for DRC (Design rule checker) due to the constraints filled in.
  - Use thicker copper trace width for +12V and Net-(D9-A).
  - Try to avoid using vias, but if inevitable, try to make the length of the trace between two vias as short as possible(Blue trace), that is to say, position your vias close to the intersection but not too close.
  - Connect all the GND pads to GND vias instead of connecting all the GND pads together.
    - To do so: Add a via next to your GND pad, select the via and press E on your keyboard, select GND for the dropdown named “Net”, and connect the GND pad to the GND via (Repeat this procedure for all GND pads)
  - Important: For the footprints of the potentiometers, you will see a huge rectangle with three holes, you are allowed to place passives (resistors, capacitors, diodes etc.) within the rectangle (so that we can save space)
    - Reason we can do this is because of the physical shape of the potentiometer: ![last](https://github.com/CalSol/Sp25-Electrical-Training/blob/main/images/last.png), as you can see, there is plenty of space under the body of the potentiometer. However, connectors, MOSFET and D4 CANNOT fit in the space under the body of the potentiometer, so make your considerations.
> Tip: You can hang the ends of the potentiometers off the edge to save space. (i.e. - cut the empty space of potentiometer footprint when defining the PCB size using Edge.cuts)
  - Again, try to make your board as small as possible!
### Ask for help if you need it!

# Checkpoint and Deliverables (Important!)
As you can see, unlike the schematic, there is no pre-designed layout for you to follow (this is where learning happens!). After you think you have a good layout submit a screenshot of your layout along with the DRC checker to a lab staff. Or you can come get checked off during office hours (the better choice).

### You will receive feedback for your layout so you might not pass on your first try!

