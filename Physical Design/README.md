
# Physical Design Concepts

## 1. Introduction to Physical Design

I learned that physical design is the process of converting a synthesized gate-level netlist into a physical layout that can be manufactured as an integrated circuit (IC).

Synthesis describes the circuit in terms of logic gates and registers, while physical design determines the physical locations of these cells and the interconnections between them.

The main objectives of physical design are:

- Achieve the required timing performance.
- Optimize power consumption.
- Minimize chip area where practical.
- Reduce routing congestion.
- Maintain reliable power distribution.
- Satisfy manufacturing design rules.

The quality of physical design directly affects the power, performance, and area (PPA) of a digital chip.

## 2. Main Components of a Chip

Before learning physical design, I explored the major components of an integrated circuit.

- **Die:** The piece of semiconductor material containing the fabricated circuit.
- **Core:** The main region where standard cells and functional blocks are placed.
- **I/O Pads:** Provide electrical connections between the chip and external signals.
- **Standard Cells:** Pre-designed logic cells such as inverters, NAND gates, multiplexers, and flip-flops.
- **Macros:** Larger blocks such as SRAMs, ROMs, and other reusable IP blocks.
- **Power Rails:** Conductive structures that distribute power and ground.
- **Metal Interconnects:** Wires that connect cells and circuit blocks.
- **Package:** Protects the die and provides electrical connections to the external system.

I understood that these components work together to implement the required digital functionality.

# Physical Design Flow

## 3. Floorplanning

### What I Learned

I learned that floorplanning is the first major stage of physical implementation after synthesis. It establishes the initial physical organization of the chip and determines how much space is available for cells, macros, and routing.

### Main Activities

1. **Define the Die Area:** Determine the overall area available for the chip.
2. **Define the Core Area:** Establish the region where the main circuit components will be placed.
3. **Place Macros:** Assign locations to large blocks such as memories and analog IPs.
4. **Plan I/O Pins:** Decide where external signal connections should be located.
5. **Estimate Routing Resources:** Consider the metal layers and space needed for interconnections.
6. **Evaluate Congestion:** Identify regions that may have excessive routing demand.

### Core Utilization

Core utilization represents the percentage of the core area occupied by the cells included in the calculation.

Formula:

Utilization = (Cell Area / Core Area) × 100%

Example:

If the cell area is 60,000 µm² and the core area is 100,000 µm²:

Utilization = (60,000 / 100,000) × 100% = 60%

I learned that high utilization leaves less space for routing and optimization. Low utilization provides more space but may increase the core area.

### Aspect Ratio

Aspect ratio describes the shape of the core.

Aspect Ratio = Core Height / Core Width

- Aspect ratio = 1: square-shaped core.
- Aspect ratio greater than 1: taller than it is wide.
- Aspect ratio less than 1: wider than it is tall.

### Importance of Floorplanning

A good floorplan helps reduce congestion, supports shorter connections, and provides enough space for power distribution and future optimization.

Poor floorplanning can cause routing difficulties, longer interconnects, and timing problems in later stages.

## 4. Power Planning

### What I Learned

I learned that power planning creates the power-distribution network that delivers supply voltage and ground connections to cells throughout the chip.

Standard cells require a reliable power supply to operate correctly. As cells switch, they draw current through the power network.

### Main Activities

1. **Power and Ground Network Design:** Establish connections for the supply voltage and ground.
2. **Power-Ring Creation:** Create power-distribution structures around regions of the design where required.
3. **Power-Stripe Creation:** Distribute power through wider metal structures across the chip.
4. **Power-Rail Connections:** Connect standard-cell power pins to the power network.
5. **Power Integrity Analysis:** Evaluate voltage drop and current-density concerns.

The specific power structures depend on the technology and design requirements.

### Important Concepts

- **Power Distribution Network (PDN):** The network that distributes power and ground throughout the chip.
- **IR Drop:** Voltage loss caused by resistance in the power-distribution network.
- **Electromigration:** Movement of metal atoms caused by current flow, which can damage interconnects over time.
- **Decoupling Capacitors:** Help reduce local power-supply fluctuations by supplying transient current.
- **Voltage Droop:** A temporary reduction in local supply voltage.
- **Ground Bounce:** A temporary change in local ground voltage caused by switching-related effects.

### Importance of Power Planning

Poor power planning can lead to excessive voltage drop, reliability problems, and incorrect circuit operation.

A robust power network helps supply the required voltage to cells across the chip.

## 5. Placement

### What I Learned

I learned that placement determines the physical locations of standard cells inside the core.

The placement tool uses the synthesized netlist, timing constraints, floorplan, and cell-library information to arrange the cells.

### Main Activities

1. **Initial Placement:** Assign approximate locations to standard cells.
2. **Timing Optimization:** Adjust cell locations and, where appropriate, cell sizes to improve timing.
3. **Wirelength Optimization:** Reduce unnecessary distances between connected cells.
4. **Congestion Analysis:** Identify areas where too many connections compete for routing resources.
5. **Placement Legalization:** Move cells into legal locations while avoiding overlaps and satisfying placement rules.

### Global Placement

Global placement determines approximate cell locations while optimizing objectives such as wirelength, density, and timing.

At this stage, some cell locations may not yet satisfy all detailed placement constraints.

### Detailed Placement

Detailed placement refines cell positions and ensures that cells occupy legal sites without overlapping.

It may also improve local timing and reduce placement-related problems.

### Importance of Placement

Good placement can reduce wirelength, interconnect delay, and congestion.

Poor placement can cause long signal paths, routing difficulties, and timing violations.

## 6. Clock Tree Synthesis (CTS)

### What I Learned

I learned that Clock Tree Synthesis creates a clock-distribution network that delivers the clock signal to sequential elements such as flip-flops.

A clock signal must reach many registers across the chip with controlled timing differences.

### Main Activities

1. **Clock Endpoint Identification:** Identify the sequential elements that need the clock.
2. **Clock Network Construction:** Build a network connecting the clock source to the required endpoints.
3. **Clock Buffer Insertion:** Insert buffers or other suitable cells to drive the clock load.
4. **Clock Skew Optimization:** Control differences in clock arrival times.
5. **Clock Timing Analysis:** Check clock latency, skew, and the effects on setup and hold timing.

### Important Concepts

- **Clock Latency:** The time taken for the clock signal to reach a destination.
- **Clock Skew:** The difference in clock arrival times between relevant endpoints.
- **Clock Insertion Delay:** The delay introduced by the clock-distribution network.
- **Clock Buffer:** A cell used to help distribute the clock signal to its loads.

### Importance of CTS

Poor clock distribution can cause setup and hold timing violations.

CTS aims to distribute the clock reliably while balancing skew, latency, power consumption, and routing requirements.

## 7. Routing

### What I Learned

I learned that routing creates the physical connections between standard cells, macros, and other circuit components.

After placement, the locations of the cells are known, but the required electrical connections must still be implemented using metal wires and vias.

### Main Activities

1. **Determine Connection Paths:** Identify the routes needed to connect each net.
2. **Allocate Routing Resources:** Assign suitable routing regions and metal layers.
3. **Create Metal Interconnects:** Draw the physical wires connecting the pins.
4. **Insert Vias:** Connect wires across different metal layers.
5. **Resolve Congestion:** Modify routes when routing resources are insufficient.
6. **Check Design Rules:** Ensure that routed wires follow the technology's geometric rules.

### Global Routing

Global routing estimates the paths of nets and allocates routing resources.

It helps identify congestion and determines approximate routes before detailed implementation.

### Detailed Routing

Detailed routing creates the actual wire geometry and vias while following manufacturing rules.

It must consider wire spacing, wire width, via rules, obstacles, and available metal layers.

### Important Routing Concepts

- **Net:** A logical electrical connection between circuit pins.
- **Wirelength:** The total length of the interconnect.
- **Via:** A structure that connects conductive layers.
- **Routing Congestion:** A condition where routing demand exceeds available resources.
- **Parasitic Resistance and Capacitance:** Electrical properties of interconnects that affect delay and signal behavior.

### Importance of Routing

Routing affects signal delay, power consumption, signal integrity, and the ability to complete the physical layout successfully.

## 8. Static Timing Analysis (STA)

### What I Learned

I learned that Static Timing Analysis checks whether a digital circuit meets its timing requirements without requiring simulation input vectors.

STA evaluates timing paths using cell timing information, interconnect delays, clock information, and timing constraints.

### Main Activities

1. **Read Timing Constraints:** Load the clock definitions and timing requirements.
2. **Identify Timing Paths:** Examine paths between registers, input ports, and output ports.
3. **Calculate Delays:** Determine the timing contribution of cells and interconnects.
4. **Calculate Slack:** Compare actual timing with the required timing.
5. **Identify Violations:** Locate paths that fail setup, hold, or other applicable timing checks.
6. **Optimize the Design:** Apply suitable changes to improve timing.

### Important Concepts

**Setup Time:** The minimum time data must remain stable before the active clock edge.

**Hold Time:** The minimum time data must remain stable after the active clock edge.

**Critical Path:** A timing path that limits the achievable performance of the circuit.

**Slack:** The difference between required timing and actual timing according to the report's timing convention.

- Positive slack generally indicates that the timing requirement is met.
- Negative slack indicates a timing violation.

### Setup and Hold Violations

A setup violation can occur when data arrives too late for the receiving register.

A hold violation can occur when data changes too soon after the active clock edge.

### Importance of STA

STA helps determine whether the design can operate at its intended clock frequency and whether timing requirements are satisfied after implementation.

## 9. CMOS Layout and Standard-Cell Characterization

### What I Learned

I learned that CMOS layout describes the physical arrangement of transistor structures and interconnections used to implement a circuit.

A standard cell may have a transistor-level design, a physical layout, and a corresponding timing and power model.

### Main Concepts

**Stick Diagram:** A simplified representation of layout layers and connectivity that helps plan the physical arrangement of a circuit.

**Euler Path:** A graph-based technique that can help determine suitable transistor arrangements for certain CMOS logic gates.

**CMOS Inverter:** A basic logic circuit that produces the complement of its input using PMOS and NMOS transistors.

**Standard-Cell Library:** A collection of reusable cells with logical, physical, and electrical information.

**Cell Characterization:** The process of measuring or calculating cell properties such as timing, power, and electrical behavior under defined conditions.

### Importance of Characterization

Synthesis, placement, and timing-analysis tools use library information to estimate cell area, delay, and power.

Accurate characterization helps tools make better implementation decisions.

## 10. Timing Characterization

### What I Learned

I learned that timing characterization describes the timing behavior of a cell under different input transitions and output loads.

### Important Parameters

- **Propagation Delay:** The time between a defined input transition and its corresponding output transition.
- **Transition Time:** The time taken for a signal to move between specified voltage thresholds.
- **Input Slew:** The transition rate of an input signal.
- **Output Load:** The electrical load driven by a cell's output.
- **Cell Delay:** The delay associated with a cell's response under specified conditions.

### Timing Tables

Standard-cell timing models often use tables that relate input transition time and output load to cell delay or output transition time.

I learned that larger output loads and slower input transitions can affect cell timing.

The actual effect depends on the cell and the characterized operating conditions.

## 11. Routing Algorithms

### What I Learned

I learned that routing algorithms find physical paths between connected circuit elements while avoiding obstacles and following routing constraints.

### Maze Routing

Maze routing explores possible paths through a routing grid to connect a source and a target.

### Lee's Algorithm

Lee's algorithm explores reachable grid locations and assigns distance values. Once the target is reached, a path can be traced back through the distance values.

It can find a shortest path on the defined grid when a valid path exists.

However, practical routing tools must also consider congestion, multiple metal layers, vias, design rules, and optimization objectives.

### Importance of Routing Algorithms

Routing algorithms help automate the creation of interconnections for complex digital circuits containing many nets.

## 12. Physical Verification

### What I Learned

I learned that physical verification checks whether a layout follows manufacturing rules and represents the intended circuit connectivity.

### Design Rule Checking (DRC)

DRC checks the physical layout against technology-specific manufacturing rules.

Examples include:

- Minimum wire width
- Minimum wire spacing
- Via dimensions and spacing
- Minimum area requirements
- Other layer-specific geometric constraints

A DRC violation indicates that the layout breaks one or more checked rules.

### Layout Versus Schematic (LVS)

LVS compares the circuit connectivity extracted from the physical layout with the intended reference netlist.

It can identify missing connections, unwanted shorts, and other connectivity mismatches.

### Parasitic Extraction

Parasitic extraction determines the resistance and capacitance associated with physical interconnects.

These parasitics can then be used in timing and other electrical analyses.

### Importance of Physical Verification

DRC checks manufacturing geometry, while LVS checks circuit connectivity.

Both are important, but passing these checks alone does not guarantee that every functional, timing, or reliability requirement has been met.

## 13. Power, Performance, and Area (PPA)

### What I Learned

I learned that physical design involves balancing three important objectives.

### Power

Power includes dynamic power and leakage power.

Dynamic power is related to switching activity, capacitance, supply voltage, and operating frequency.

### Performance

Performance depends on whether the circuit meets its timing requirements, including the delays along critical paths.

### Area

Area depends on the standard cells, macros, and other physical structures used in the implementation.

### PPA Trade-Offs

I learned that improving one objective can affect the others.

For example, using larger cells may reduce some delays but increase area and power consumption.

Similarly, reducing area too aggressively can increase congestion and make timing closure more difficult.

## 14. Final Layout Generation

### What I Learned

I learned that final layout generation produces a physical layout database for the manufacturing flow.

GDSII is a commonly used format for representing integrated-circuit layout geometry.

Before final layout delivery, the design flow may include:

1. Completing placement and routing.
2. Checking setup and hold timing.
3. Performing physical verification.
4. Extracting parasitic information.
5. Checking power integrity and other required constraints.
6. Generating the final layout database.

The exact sign-off checks depend on the technology, design requirements, and manufacturing flow.

## 15. Summary of the Physical Design Flow

The major stages of a typical physical design flow are:

1. **Floorplanning:** Define the chip's physical organization and available area.
2. **Power Planning:** Build the network that distributes power and ground.
3. **Placement:** Assign physical locations to standard cells.
4. **Clock Tree Synthesis:** Build the clock-distribution network.
5. **Routing:** Connect cells using metal wires and vias.
6. **Static Timing Analysis:** Check timing requirements and identify violations.
7. **Physical Verification:** Check layout rules and circuit connectivity.
8. **Final Layout Generation:** Produce the physical layout database for the manufacturing flow.

These stages work together to transform a synthesized netlist into a physical implementation of the digital circuit.

## Conclusion

Through this topic, I learned the major concepts and steps involved in physical design, including floorplanning, power planning, placement, Clock Tree Synthesis, routing, timing analysis, CMOS layout, and physical verification.

I understood how each stage affects the physical implementation of a chip and why power, performance, area, and manufacturing requirements must be considered throughout the design flow.
