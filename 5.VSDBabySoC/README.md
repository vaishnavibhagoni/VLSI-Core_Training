 
#  VSD BabySoC Design Flow

## 1. What I Learned About BabySoC

I learned about BabySoC, a small System-on-Chip (SoC) design used to understand the integration of different hardware modules in a digital system.

I explored how a SoC combines multiple functional blocks to form a larger system rather than operating as a single independent circuit.

I understood that studying BabySoC helps me connect individual RTL modules, simulation, synthesis, and standard-cell libraries within a digital VLSI design flow.

## 2. What I Learned About System-on-Chip (SoC)

I learned that a System-on-Chip integrates different functional components into one chip.

Depending on the design, these components may include:

- A processor or CPU core.
- Memory or memory interfaces.
- Clock-generation circuitry.
- Data converters and peripheral interfaces.
- Control and communication logic.

I understood that these components must be connected correctly so that the overall system functions as intended.

## 3. What I Learned About BabySoC Architecture

I explored the BabySoC design hierarchy and learned about the roles of its main modules.

### RVMYTH Processor

I learned that RVMYTH is a processor design used in the BabySoC environment.

I explored how a processor module forms part of the overall SoC and interacts with other design components through its interfaces.

### Phase-Locked Loop (PLL)

I learned that a Phase-Locked Loop is a circuit used for clock generation or clock synchronization.

I understood that clock-related circuitry is important because digital systems depend on suitable clock signals for sequential operations.

### Digital-to-Analog Converter (DAC)

I learned that a Digital-to-Analog Converter converts digital input values into corresponding analog signals.

I explored the role of the DAC as one of the functional blocks associated with the BabySoC design.

### Top-Level Integration

I learned that the top-level module connects the different modules and provides the overall design interface.

I understood that the connections between modules, their ports, and their dependencies must be handled correctly for the integrated design to work.

## 4. What I Learned About Verilog Modules and Design Hierarchy

I learned that a Verilog design can contain multiple modules, with one module instantiating other modules.

I understood that this hierarchical structure makes complex digital designs easier to organize and maintain.

For example, a top-level module may instantiate a processor and other supporting modules.

I explored how the top-level design depends on the availability of the required source files, module definitions, and compatible interfaces.

## 5. What I Learned About the BabySoC Project Structure

I explored the BabySoC project directory and learned that source code, include files, library files, and testbenches may be organized into separate directories.

I understood the importance of checking the project structure before running synthesis or simulation commands.

Useful Linux commands I learned include:

### Check the Current Directory

```bash
pwd
```

I learned that `pwd` displays the current working directory.

### List Files and Directories

```bash
ls
```

I learned that `ls` displays the files and directories available in the current location.

### Navigate into a Directory

```bash
cd directory_name
```

I learned that `cd` changes the current working directory.

### List Files in a Specific Directory

```bash
ls src/module
```

I learned that this command lists the contents of the `src/module` directory when that path exists in the current project.

## 6. What I Learned About Reading Verilog Files in Yosys

I learned that Yosys can read Verilog source files and prepare the design for synthesis.

For example:

```tcl
read_verilog src/module/vsdbabysoc.v
```

I understood that the command loads the specified Verilog file into Yosys. However, reading only the top-level file may not be sufficient if the design depends on other modules.

A command to read another source file may look like:

```tcl
read_verilog src/module/rvmyth.v
```

I learned that the actual file paths depend on the repository version and directory structure.

When the design uses Verilog include files, the appropriate include paths and source files must also be provided.

## 7. What I Learned About Verilog Include Files

I learned that Verilog projects can use include files to define macros, parameters, and other shared declarations.

I understood that the synthesis tool must be able to locate these files when processing the design.

An example command is:

```tcl
read_verilog -I src/include src/module/rvmyth.v
```

I learned that `-I` specifies a directory where the tool can search for included files.

The correct include path must be based on the actual project directory structure.

## 8. What I Learned About Simulation

I learned that simulation helps check the behavior of a design before proceeding further in the implementation flow.

I explored the role of a testbench in providing inputs, generating clock and reset signals when required, and observing the outputs.

A typical Icarus Verilog command has the following form:

```bash
iverilog -o simulation.out testbench.v design.v
```

To run the compiled simulation:

```bash
vvp simulation.out
```

I understood that these are example commands and that the actual BabySoC simulation may require additional modules, include paths, macros, or library models.

I also learned that simulation errors can occur when source files are missing, module names do not match, or dependencies have not been included.

## 9. What I Learned About Waveform Analysis

I learned that simulation waveforms help me observe how signals change over time.

I explored GTKWave as a waveform viewer and learned that VCD files can store signal transitions generated during simulation.

An example command to open a waveform is:

```bash
gtkwave pre_synth_sim.vcd
```

I understood that the filename must match the VCD file generated by the simulation.

I also learned that the testbench must contain appropriate waveform-dumping statements and that the required signals must be selected in GTKWave for analysis.

## 10. What I Learned About the Synthesis Flow

I learned that synthesis converts an RTL design into a lower-level hardware representation.

I explored how Yosys commands can be used to read source files, select a top module, synthesize the design, and examine the resulting statistics.

A basic example is:

```tcl
read_verilog design.v
hierarchy -top top_module
synth -top top_module
stat
```

I understood that a complete BabySoC synthesis flow may require multiple source files, library definitions, appropriate include paths, and flow-specific configuration.

The commands above demonstrate the basic concept and are not a complete BabySoC synthesis script.

## 11. What I Learned About Standard-Cell Libraries

I explored the role of standard-cell libraries in the synthesis flow.

I learned that standard-cell libraries provide information about cells available for implementing digital logic.

I also learned that a Liberty `.lib` file and a Verilog simulation model serve different purposes.

- Liberty files provide cell information used by synthesis and timing tools.
- Verilog cell models describe cell behavior for simulation.

I understood that the appropriate library and models depend on the design and the tools being used.

## 12. What I Learned About Common BabySoC Setup Errors

While exploring the project environment, I learned the importance of checking paths and dependencies carefully.

### Missing File or Directory

I learned that a missing-file error can occur when a command uses an incorrect relative path or when the required file is not present.

### Command Not Found

I learned that an error such as `iverilog: command not found` means the shell cannot locate the executable. The tool may need to be installed or its location added to the system path.

### Missing Module

I learned that a synthesis or simulation tool may report an unknown module if its definition has not been provided or the relevant source file has not been loaded.

### Waveform Not Displaying

I learned that a waveform may be missing if the simulation did not generate the VCD file, the simulation stopped unexpectedly, or the waveform viewer is displaying the wrong file or signals.

These experiences helped me understand why checking the environment and project structure is an important part of digital design work.

## 13. What I Learned About the Overall BabySoC Flow

I learned the general sequence used to work with an RTL-based SoC project:

1. Explore the repository and understand its directory structure.
2. Identify the top-level module and supporting modules.
3. Check source files, include files, and dependencies.
4. Run RTL simulation where the required environment is available.
5. Inspect the simulation output and waveforms.
6. Run synthesis using the appropriate design and library configuration.
7. Examine the synthesis statistics and generated netlist.
8. Perform further verification as required by the flow.

I understood that each stage depends on the correct setup of the previous stages.

## 14. Key Learning Outcomes

Through this topic, I developed an understanding of:

- The purpose of a System-on-Chip.
- The role of different functional modules in BabySoC.
- The importance of design hierarchy and module integration.
- Linux commands for navigating a project directory.
- Reading Verilog source files in Yosys.
- Managing source files and include paths.
- The purpose of testbenches and waveform analysis.
- The basic RTL synthesis workflow.
- The role of standard-cell libraries.
- Troubleshooting common simulation and synthesis setup errors.

## 15. Tools and Technologies I Explored

- Verilog HDL
- VSD BabySoC
- RVMYTH processor module
- Yosys
- Icarus Verilog
- GTKWave
- Linux terminal
- SKY130 standard-cell library

## Conclusion

Through this topic, I learned how a small SoC design brings together multiple hardware modules and how these modules are handled within an RTL development flow.

I explored the BabySoC project structure, Verilog source files, simulation tools, synthesis commands, and standard-cell libraries.

This topic helped me understand the connection between individual RTL modules and a larger SoC design workflow.
