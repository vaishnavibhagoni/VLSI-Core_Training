
# Gate-Level Simulation (GLS)

## 1. What I Learned About Gate-Level Simulation

I learned that Gate-Level Simulation (GLS) is the process of simulating a digital design using a synthesized gate-level netlist instead of the original RTL code.

I understood that GLS helps verify whether the synthesized hardware behaves as expected when appropriate simulation models and testbenches are provided.

I also learned that GLS is useful for checking the behavior of a design after synthesis and, in some flows, for investigating timing-related effects.

## 2. What I Learned About RTL Simulation and Gate-Level Simulation

I learned the difference between RTL simulation and gate-level simulation.

### RTL Simulation

- Uses the original Verilog RTL code.
- Checks the functional behavior of the design.
- Is commonly performed before synthesis.
- Can be simulated using Icarus Verilog and viewed using GTKWave.

### Gate-Level Simulation

- Uses a synthesized gate-level netlist.
- May require simulation models for the cells used in the netlist.
- Uses a testbench to apply inputs and check outputs.
- Can be used to verify the synthesized implementation.

I understood that RTL and gate-level simulations should produce equivalent functional results when the netlist and simulation setup correctly represent the same design.

## 3. What I Learned About a Gate-Level Netlist

I learned that a gate-level netlist represents a digital circuit using logic elements and their connections.

After synthesis, the original RTL design can be represented using generic logic cells or cells from a specific standard-cell library.

I understood that a technology-mapped netlist may contain instances of library cells such as NAND gates, buffers, and flip-flops.

The netlist is an important input for gate-level simulation.

## 4. What I Learned About the Testbench in GLS

I learned that a testbench is used to apply input signals to a design and observe its outputs during simulation.

I understood that a testbench can generate a clock, apply reset, provide test inputs, and check whether the outputs match the expected behavior.

For gate-level simulation, the testbench must connect correctly to the synthesized design.

I also learned that the simulation setup must include the necessary cell models when the netlist instantiates technology-specific cells.

## 5. What I Learned About Pre-Synthesis and Post-Synthesis Simulation

I learned that simulation can be performed at different stages of the digital design flow.

### Pre-Synthesis Simulation

- Uses the RTL Verilog design.
- Checks the intended functional behavior.
- Helps identify logical errors before synthesis.

### Post-Synthesis Simulation

- Uses the synthesized netlist.
- Checks the behavior of the synthesized implementation.
- May require additional library models and simulation configuration.

I understood that successful RTL simulation alone does not prove that every later implementation stage is correct.

## 6. What I Learned About Icarus Verilog

I learned that Icarus Verilog is an open-source Verilog compiler and simulator.

It can compile a testbench together with a design and produce simulation output.

### Example Commands

Compile an RTL design and its testbench:

```bash
iverilog -o rtl_sim.out testbench.v design.v
```

Run the simulation:

```bash
vvp rtl_sim.out
```

I learned that these commands are examples for RTL simulation. The actual filenames and compilation options depend on the design.

For gate-level simulation, I must compile the synthesized netlist, testbench, and any required standard-cell simulation models.

## 7. What I Learned About GTKWave and VCD Files

I learned that GTKWave is a waveform viewer used to examine digital signal transitions.

I understood that simulation tools can generate VCD (Value Change Dump) files that record changes in selected signals over time.

### Example Commands

Run a simulation that generates a VCD file:

```bash
vvp simulation.out
```

Open the generated waveform:

```bash
gtkwave waveform.vcd
```

I learned that the testbench must include suitable waveform-dumping statements, such as `$dumpfile` and `$dumpvars`, to generate the VCD file.

I also understood that I need to add the required signals in GTKWave to inspect their behavior.

## 8. What I Learned About Timing in Gate-Level Simulation

I learned that a gate-level netlist may include timing information, depending on the netlist and simulation models being used.

I understood the difference between:

- **Functional gate-level simulation:** Checks logic behavior without necessarily modeling realistic delays.
- **Timing-aware gate-level simulation:** Uses suitable timing models to represent delays in the circuit.

I learned that timing-aware simulation may help reveal issues associated with signal propagation and timing assumptions.

However, I understood that GLS does not replace Static Timing Analysis (STA), which is used to analyze timing requirements more systematically.

## 9. What I Learned About Standard-Cell Simulation Models

I learned that a technology-mapped netlist can contain instances of cells from a standard-cell library.

To simulate such a netlist, the simulator needs compatible Verilog simulation models for those cells.

I understood that a Liberty `.lib` file generally describes library characteristics for synthesis and timing analysis, while Verilog cell models are used to simulate cell behavior.

These files serve different purposes and cannot automatically be substituted for one another.

## 10. What I Learned About the GLS Workflow

I learned the general steps involved in a gate-level simulation flow:

1. Complete RTL design and functional simulation.
2. Synthesize the RTL design.
3. Generate the gate-level netlist.
4. Prepare the required cell simulation models.
5. Compile the netlist and testbench.
6. Run the simulation.
7. Inspect the outputs and waveforms.
8. Compare the observed behavior with the expected behavior.

I understood that the exact commands depend on the synthesis tool, target library, simulator, and project structure.

## 11. What I Learned About Common Simulation Errors

I learned that gate-level simulation can fail for several reasons.

### Missing Module Errors

I understood that an error about an unknown module may occur when the synthesized netlist instantiates a cell whose simulation model has not been included.

### File-Path Errors

I learned that incorrect file paths or missing source files can prevent the simulator from compiling the design.

### Undefined or Unexpected Outputs

I learned that unexpected signal values can result from reset behavior, uninitialized registers, incorrect testbench inputs, or missing and incompatible simulation models.

### Missing Waveforms

I understood that a waveform may not appear if the VCD file was not generated, the simulation did not run as expected, or the waveform viewer is not displaying the required signals.

## 12. What I Learned About Comparing RTL and GLS Results

I learned that comparing RTL simulation and gate-level simulation helps verify that the synthesized design preserves the expected functionality.

I understood that the comparison should use equivalent input sequences and examine corresponding output signals.

If the results differ, I learned that the testbench, reset sequence, synthesis configuration, simulation models, and timing assumptions should be checked.

## 13. Practical Commands I Explored

The following commands illustrate a basic simulation workflow.

Check the current directory:

```bash
pwd
```

List available files:

```bash
ls
```

Compile a simulation:

```bash
iverilog -o simulation.out testbench.v netlist.v
```

Run the simulation:

```bash
vvp simulation.out
```

Open the waveform:

```bash
gtkwave waveform.vcd
```

I learned that the example filenames must be replaced with the actual files in my project. For a technology-mapped netlist, I may also need to include the appropriate cell simulation models and additional compiler options.

## 14. Key Learning Outcomes

Through this topic, I developed an understanding of:

- The purpose of Gate-Level Simulation.
- The difference between RTL and gate-level simulation.
- The role of a synthesized netlist.
- The importance of a testbench.
- The use of Icarus Verilog for simulation.
- The use of GTKWave for waveform analysis.
- The role of VCD files in recording signal changes.
- The difference between functional and timing-aware GLS.
- The purpose of standard-cell simulation models.
- The importance of comparing simulation results.

## 15. Tools and Technologies I Learned About

- Verilog HDL
- Yosys
- Icarus Verilog
- GTKWave
- Gate-level netlists
- VCD waveform files
- Standard-cell simulation models
- SKY130 standard-cell library

## Conclusion

Through this topic, I learned how Gate-Level Simulation is used to verify a synthesized digital design. I understood the importance of netlists, testbenches, simulation models, and waveform analysis in the digital VLSI design flow.

This topic helped me understand how verification continues after RTL synthesis and how the synthesized implementation can be checked before proceeding to later design stages.
