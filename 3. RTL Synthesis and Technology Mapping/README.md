
# RTL Synthesis and Technology Mapping
 
## 1. What I Learned About RTL Synthesis

I learned that RTL (Register Transfer Level) synthesis is the process of converting Verilog RTL code into a hardware representation that can be implemented using logic gates, flip-flops, and other hardware cells.

I understood that RTL code describes the intended behavior of a digital circuit, while synthesis determines a hardware structure that implements that behavior.

I also learned that synthesis tools perform logic transformations and optimizations to produce a suitable hardware implementation.

### Basic Synthesis Flow

RTL Verilog Code → RTL Processing → Logic Optimization → Technology Mapping → Gate-Level Netlist

## 2. What I Learned About Yosys

I learned about **Yosys**, an open-source synthesis tool used to process Verilog designs and generate synthesized hardware representations.

I explored how Yosys can read RTL files, process modules, perform synthesis, display statistics, and generate a gate-level netlist.

### Commands I Learned

**Step 1: Start Yosys**

```bash
yosys
```

This command opens the Yosys interactive environment if Yosys is installed and available in the system path.

**Step 2: Read the Verilog file**

```tcl
read_verilog good_mux.v
```

I learned that the `read_verilog` command loads the Verilog source file into Yosys.

**Step 3: Check the design hierarchy**

```tcl
hierarchy -top good_mux
```

I learned that the `hierarchy` command checks the module hierarchy and identifies the selected top-level module.

**Step 4: Perform synthesis**

```tcl
synth -top good_mux
```

I learned that the `synth` command runs the synthesis process for the specified top module.

**Step 5: Display synthesis statistics**

```tcl
stat
```

I learned that the `stat` command displays information about the synthesized design, including cell counts and cell types.

**Step 6: Generate the synthesized netlist**

```tcl
write_verilog synthesized_netlist.v
```
<img width="720" height="1080" alt="yosys" src="https://github.com/user-attachments/assets/98952223-f3c7-44fa-8e21-28d528fefd6e" />


I learned that the `write_verilog` command writes the current design representation to a Verilog file.


## 3. What I Learned About the Top Module

I learned that the top module is the main design module selected for synthesis.

For example, consider the following Verilog code:

```verilog
module good_mux (
    input a,
    input b,
    input sel,
    output y
);

assign y = sel ? b : a;

endmodule
```

I understood that:

- `good_mux` is the module name.
- `a` and `b` are the data inputs.
- `sel` is the selection input.
- `y` is the output.
- The conditional operator selects either `a` or `b` based on `sel`.

For this design, the synthesis command is:

```tcl
synth -top good_mux
```

I learned that selecting the correct top module is important because it determines which design hierarchy the synthesis tool processes.

## 4. What I Learned About Combinational Logic Synthesis

I learned that combinational logic produces outputs based on the current inputs, without storing previous input values.

Examples include:

- Multiplexers
- Encoders
- Decoders
- Adders
- Comparators
- Logic gates

I understood that a synthesis tool analyzes the Boolean behavior of the RTL and can implement it using an equivalent network of hardware cells.

For example, a 2:1 multiplexer can be represented by:

```verilog
assign y = sel ? b : a;
```

Its Boolean expression is:

```text
y = (~sel & a) | (sel & b)
```

I learned that different RTL descriptions may implement the same logical function, but their synthesized implementations can differ depending on the tool, constraints, and target library.

## 5. What I Learned About Sequential Logic Synthesis

I learned that sequential logic depends on the current inputs and stored state. Flip-flops are commonly used to store state in synchronous digital circuits.

For example:

```verilog
always @(posedge clk)
begin
    q <= d;
end
```

I understood that this code describes a register that captures `d` on the rising edge of `clk`.

I learned that synthesis recognizes clocked procedural blocks and infers sequential hardware when the RTL describes storage behavior.

Examples of sequential circuits include:

- Registers
- Counters
- Finite State Machines (FSMs)
- Shift registers
- Sequence detectors

## 6. What I Learned About a Gate-Level Netlist

I learned that a gate-level netlist represents a circuit using lower-level hardware cells and their connections.

Depending on the synthesis stage, the netlist may contain generic logic elements or technology-specific standard cells.

I understood the difference between:

- **RTL code:** Describes the intended hardware behavior.
- **Generic synthesized netlist:** Represents the design using technology-independent logic elements.
- **Technology-mapped netlist:** Uses cells from a selected target library.

I also learned that a synthesized netlist can be examined to understand how the RTL has been translated into hardware.

### Command to Generate a Netlist

```tcl
write_verilog synthesized_netlist.v
```

This command exports the current Yosys design representation. The exact contents depend on the synthesis stages already completed.

## 7. What I Learned About Technology Mapping

I learned that technology mapping is the process of implementing synthesized logic using cells available in a specific technology library.

A standard-cell library can contain:

- AND, OR and NOT gates
- NAND and NOR gates
- Multiplexers
- Flip-flops
- Buffers
- More complex logic cells

I understood that the synthesis tool selects suitable cells according to the available library, optimization goals, and design constraints.

Technology mapping helps connect a logical design with the hardware cells available for implementation in a target semiconductor technology.

## 8. What I Learned About the SKY130 Standard-Cell Library

I explored the role of the SKY130 standard-cell library in a digital design flow.

I learned that a standard-cell library provides information about the cells available for implementing digital logic.

Depending on the library files and flow, this information can include:

- Cell functionality
- Area information
- Timing characteristics
- Electrical characteristics

I understood that Yosys can use a Liberty `.lib` file during technology mapping to identify and select supported standard cells.

### Example Command

```tcl
read_liberty -lib path/to/sky130_library.lib
```

I learned that this command reads library information into Yosys. The path must point to an actual compatible Liberty file available in my environment.

The `-lib` option is used to load the library cells as module definitions, which is useful in synthesis flows.

## 9. What I Learned About Technology Mapping with Yosys

I learned that the basic `synth` command can produce a synthesized design, but mapping it to a particular standard-cell library may require additional commands.

For a typical flow using a compatible Liberty file, the process can include:

```tcl
read_verilog good_mux.v
read_liberty -lib path/to/sky130_library.lib
synth -top good_mux
dfflibmap -liberty path/to/sky130_library.lib
abc -liberty path/to/sky130_library.lib
stat
write_verilog mapped_netlist.v
```

I understood the general purpose of these commands:

- `read_verilog` loads the RTL source.
- `read_liberty -lib` loads standard-cell definitions.
- `synth` performs synthesis.
- `dfflibmap` maps supported flip-flops to library cells.
- `abc -liberty` maps combinational logic to library cells.
- `stat` displays design statistics.
- `write_verilog` exports the resulting design.

**Important:** This is an illustrative flow, not a guaranteed command sequence for every design. The correct order and options depend on the Yosys version, RTL design, target library, and synthesis flow. For example, a design containing no flip-flops may not need `dfflibmap`.

## 10. What I Learned About Synthesis Statistics

I learned that synthesis statistics help me understand the structure of the generated design.

The command I explored was:

```tcl
stat
```

I understood that the report may include:

- Total number of cells
- Number of cells by type
- Number of logic elements
- Number of sequential elements, if present
- Area information when supported by the library and reporting flow

I learned that statistics can help compare different implementations of the same logic.

However, I understood that cell count alone does not determine whether a design is better. Timing, area, power, and the design constraints must also be considered.

## 11. What I Learned About Pre-Synthesis and Post-Synthesis

I learned the difference between pre-synthesis and post-synthesis representations.

### Pre-Synthesis

- The design is represented using RTL Verilog.
- Functional simulation can be used to check the intended behavior.
- The code describes the required digital functionality.

<img width="3840" height="2160" alt="pre" src="https://github.com/user-attachments/assets/89e7f996-5ad8-49f5-aaaa-5fc73a5dddf8" />

### Post-Synthesis

- The synthesis tool generates a netlist.
- The netlist represents the synthesized hardware.
- The design can be checked through further verification.

<img width="1600" height="847" alt="post" src="https://github.com/user-attachments/assets/f8051bf1-4a78-4855-838c-a0ba1173e143" />

I understood that synthesis is a transformation of the design, not a replacement for verification.

A post-synthesis simulation may require a compatible gate-level netlist, simulation models for the mapped cells, and an appropriate testbench.

## 12. What I Learned About Good MUX and Bad MUX Comparison

I learned that comparing different RTL implementations of the same function can help me understand how synthesis tools interpret and optimize hardware descriptions.

For example, I can compare two multiplexer implementations and examine their synthesized statistics.

I understood that a shorter RTL description does not automatically guarantee a smaller or faster circuit.

To make a meaningful comparison, I need to use equivalent functionality, the same synthesis settings, and the same target library.

The comparison can include:

- Number and types of cells
- Estimated area, where available
- Logic structure
- Timing information, when available

## 13. Practical Commands I Explored

The following commands are useful when working with Verilog and synthesis tools in Linux.

Check the current directory:

```bash
pwd
```

List files and directories:

```bash
ls
```

Change directories:

```bash
cd directory_name
```

Check whether Yosys is available:

```bash
yosys -V
```

Open Yosys:

```bash
yosys
```

Inside Yosys, a basic synthesis sequence is:

```tcl
read_verilog good_mux.v
hierarchy -top good_mux
synth -top good_mux
stat
write_verilog synthesized_netlist.v
```

I learned that Linux commands are entered in the terminal, while commands such as `read_verilog`, `synth`, and `stat` are entered inside the Yosys environment.

## 14. Key Learning Outcomes

Through this topic, I developed an understanding of:

- The purpose and basic flow of RTL synthesis.
- The use of Yosys for synthesizing Verilog designs.
- The importance of selecting the correct top module.
- The difference between RTL code and a gate-level netlist.
- The role of technology mapping in digital implementation.
- The purpose of a standard-cell library.
- The role of the SKY130 library in a synthesis flow.
- How to inspect synthesis statistics.
- The difference between pre-synthesis and post-synthesis representations.
- The importance of verifying synthesized designs.

## 15. Tools and Technologies I Learned About

- Verilog HDL
- Yosys
- Linux terminal
- SKY130 standard-cell library
- Liberty `.lib` files
- Gate-level netlists
- Icarus Verilog
- GTKWave

## Conclusion

Through this topic, I learned how RTL synthesis transforms a Verilog description into a hardware representation. I explored the basic Yosys workflow, synthesis statistics, gate-level netlists, and the role of technology mapping and standard-cell libraries.

This topic helped me understand the connection between RTL design and the lower-level hardware implementation used in digital VLSI design.
