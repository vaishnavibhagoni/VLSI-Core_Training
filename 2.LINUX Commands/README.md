 
# Linux Environment for VLSI Design

## 1. Introduction

Linux is widely used in VLSI design because it provides a powerful command-line environment for running hardware design, simulation, synthesis, and verification tools.

During my VLSI core training, I worked with the Linux terminal to navigate project directories, access Verilog source files, locate standard-cell libraries, execute simulation commands, and explore RTL synthesis using Yosys.

Understanding Linux commands is important because VLSI workflows often involve multiple source files, library dependencies, configuration files, and generated output files. The terminal helps manage these files and execute tools efficiently.

## 2. Basic Linux Commands

Linux commands allow users to interact with the operating system through a command-line interface.

### 2.1 Common Commands

| Command | Description | Example |
|---|---|---|
| `pwd` | Displays the current working directory. | `pwd` |
| `ls` | Lists files and directories. | `ls` |
| `ls -l` | Displays files with additional details. | `ls -l` |
| `cd` | Changes the current directory. | `cd project` |
| `cd ..` | Moves to the parent directory. | `cd ..` |
| `mkdir` | Creates a new directory. | `mkdir rtl` |
| `cat` | Displays the contents of a text file. | `cat README.md` |
| `clear` | Clears the terminal display. | `clear` |
| `cp` | Copies files or directories. | `cp design.v backup.v` |
| `mv` | Moves or renames files. | `mv old.v new.v` |
| `rm` | Removes files. | `rm temporary.txt` |

**Important:** Commands such as `rm` can permanently remove files. Check the filename and path before executing them.

### 2.2 Understanding Command Execution

A Linux command is generally entered in the terminal and executed by pressing Enter.

For example:

    pwd
    ls
    cd project_folder

The first command displays the current location, the second lists the available files and directories, and the third moves into the specified directory.

The directory name used with `cd` must match an existing directory relative to the current location, unless an absolute path is provided.

### What I Learned

- How to execute basic Linux commands.
- How to identify the current working directory.
- How to list and inspect files.
- How to move between directories.
- How to create and manage project folders.

## 3. Directory and File Navigation

VLSI projects contain different types of files, including Verilog source code, testbenches, simulation waveforms, synthesis scripts, standard-cell libraries, and generated netlists.

Correct directory navigation helps ensure that the required files can be found by the tools.

### 3.1 Understanding File Paths

A file path specifies the location of a file or directory.

**Absolute path:** Specifies the complete path from the root directory.

Example:

    /home/vsduser/baby_soc/src/module/testbench.v

**Relative path:** Specifies the location relative to the current working directory.

Example:

    src/module/testbench.v

The relative path works only when the current directory makes that path valid.

### 3.2 Navigating a VLSI Project

Example project structure:

    project/
    ├── src/
    │   ├── design.v
    │   └── testbench.v
    ├── lib/
    ├── simulation/
    └── README.md

To inspect and navigate the project:

    pwd
    ls
    cd src
    ls
    cd ..

These commands help locate source files and understand the project structure before running simulation or synthesis commands.

### 3.3 Checking Files and Directories

Before executing a tool command, it is useful to check whether the required file exists.

Examples:

    ls src
    ls src/module
    ls src/lib

This is particularly useful when a tool reports an error such as `No such file or directory`.

### What I Learned

- How to navigate project directories.
- How to distinguish absolute and relative paths.
- How to locate Verilog files and supporting libraries.
- How to inspect project structures.
- How incorrect paths can cause command execution errors.

## 4. Running Icarus Verilog from Linux

Icarus Verilog is an open-source Verilog compiler and simulator. It is used to compile a design together with its testbench and execute the resulting simulation.

The Linux terminal provides a way to run these operations directly from the project directory.

### 4.1 Compilation

Example command:

    iverilog -o simulation.out testbench.v design.v

Explanation:

- `iverilog` invokes the Verilog compiler.
- `-o simulation.out` specifies the output executable filename.
- `testbench.v` is the testbench source file.
- `design.v` is the design source file.

The filenames must match the actual files in the project. Additional source files or include directories may be required for larger designs.

### 4.2 Running the Simulation

    vvp simulation.out

The `vvp` command executes the compiled simulation.

Depending on the testbench, the simulation may print messages, finish after a specified simulation time, or generate a waveform file.

### 4.3 Generating Waveforms

A testbench can include commands to create a VCD waveform file.

For example:

    $dumpfile("waveform.vcd");
    $dumpvars(0, testbench);

These are Verilog system tasks placed inside the testbench, not Linux terminal commands.

The VCD file records signal changes during simulation and can be inspected using a waveform viewer.

### What I Learned

- How to compile Verilog source files.
- How to execute a compiled simulation.
- How source files are passed to the compiler.
- How simulation output and errors are displayed.
- How waveform files are generated for later analysis.

## 5. Running GTKWave

GTKWave is a waveform viewer used to analyze signal transitions over simulation time.

It is useful for examining how inputs, outputs, clock signals, reset signals, and internal registers behave during a simulation.

### 5.1 Opening a Waveform

Example command:

    gtkwave waveform.vcd

The filename must match the VCD file generated by the testbench.

### 5.2 Waveform Analysis

After opening the file:

1. Locate the required signals in the signal list.
2. Add the signals to the waveform display.
3. Adjust the time scale to inspect relevant events.
4. Observe signal values and transitions.
5. Compare the observed behavior with the expected circuit functionality.

For a sequential circuit, waveform analysis can help determine whether state transitions occur at the expected clock edges and whether reset behaves correctly.

### What I Learned

- How to launch GTKWave from the terminal.
- How to open VCD waveform files.
- How to select and inspect signals.
- How to understand signal transitions over time.
- How simulation and waveform analysis work together during verification.

## 6. Introduction to Yosys Synthesis

Yosys is an open-source RTL synthesis framework used to process supported hardware descriptions and transform them into a synthesized logic representation.

Unlike simulation, which checks the behavior of a design, synthesis analyzes the RTL and prepares a hardware representation for implementation.

### 6.1 Reading Verilog Files

Example Yosys command:

    read_verilog design.v

This command reads a Verilog source file into Yosys.

For a design with multiple modules, the required source files and dependencies must be loaded before synthesis.

### 6.2 Specifying the Top Module

    hierarchy -top top_module

This command identifies the top-level module for the design hierarchy.

The module name must match the top-level module declared in the Verilog source.

### 6.3 Running Synthesis

    synth -top top_module

The `synth` command performs synthesis for the specified design.

The synthesis process transforms the RTL into a logic representation and applies synthesis optimizations.

### 6.4 Inspecting Synthesis Results

    stat

The `stat` command reports information about the synthesized design, including cell statistics.

A synthesized netlist can also be written to a file using an appropriate Yosys command, depending on the intended output format and workflow.

### What I Learned

- How Yosys reads Verilog source files.
- How a top-level module is selected.
- How RTL synthesis is initiated.
- How synthesis statistics are inspected.
- How synthesis produces a representation of the hardware logic.

*Note: These are basic example commands. A complete synthesis flow may require additional commands, libraries, and configuration steps.*

## 7. Working with the SKY130 Standard-Cell Library

The SKY130 library contains standard-cell definitions and associated information used in supported digital implementation flows.

Standard cells include logic gates, buffers, inverters, and sequential cells such as flip-flops.

A Liberty (`.lib`) file commonly contains timing, power, and other cell-characterization information used by synthesis and implementation tools.

### What I Learned

- How standard-cell library files fit into the synthesis workflow.
- How to locate library files within a project.
- Why correct library paths are important.
- How technology mapping relates a synthesized logic design to available standard cells.
- How synthesis results can be inspected after mapping.

A missing or incorrectly referenced library file can prevent a technology-mapping step from completing successfully.

## 8. Exploring the VSD BabySoC Environment

BabySoC is a System-on-Chip learning project that helps demonstrate how different hardware modules work together in a larger design.

During training, I explored the VSD BabySoC project environment, including its source files, module hierarchy, testbench, library dependencies, and synthesis-related files.

### 8.1 Design Files and Module Hierarchy

A hierarchical design is organized into modules, with higher-level modules connecting lower-level components.

The RVMYTH module is one of the components explored in the BabySoC environment.

Understanding the hierarchy helps identify the top-level module and determine which source files are required for simulation or synthesis.

### 8.2 Testbench and Simulation Files

The testbench provides the inputs required to exercise the design during simulation.

Simulation outputs and VCD files can be used to inspect the behavior of the design, while synthesis output files represent the processed hardware logic.

### 8.3 Library Dependencies

The BabySoC environment uses supporting library files for its design components and synthesis workflow.

Correct paths and dependencies must be provided when running the relevant tools.

### What I Learned

- How to inspect the BabySoC project structure.
- How to locate RTL modules and testbench files.
- How to understand the role of RVMYTH in the design hierarchy.
- How library files are referenced by synthesis commands.
- How to inspect synthesis reports and generated netlists.

This exercise helped connect Linux file navigation with the practical use of simulation and synthesis tools.

## 9. Troubleshooting and Debugging

Errors are common when working with command-line tools. Understanding the error message and checking the environment systematically can help resolve them.

### 9.1 No Such File or Directory

**Possible cause:** The filename or directory path is incorrect, or the terminal is in a different directory than expected.

**Approach:**

    pwd
    ls
    ls src/module

Check the current directory and verify the path before rerunning the command.

### 9.2 Command Not Found

**Possible cause:** The tool may not be installed, or its executable may not be available through the system's `PATH`.

**Approach:**

    command -v iverilog
    command -v gtkwave
    command -v yosys

These commands check whether the executables can be located by the shell.

### 9.3 Missing Library File

**Possible cause:** The library path may be incorrect, or the required file may not be present in the project.

**Approach:**

- Check the library directory.
- Verify the exact filename and capitalization.
- Confirm the current working directory.
- Check whether the expected library file is available.

### 9.4 Simulation or Waveform Problems

**Possible cause:** Compilation may have failed, the simulation may not have generated a VCD file, or GTKWave may have been given the wrong path.

**Approach:**

- Check the compiler output.
- Confirm that the simulation executable runs.
- Check whether the VCD file exists.
- Open the correct VCD file in GTKWave.

### What I Learned

I learned to diagnose command-line errors by checking the current directory, verifying filenames, examining tool output, and confirming that required files and executables are available.

## 10. Complete VLSI Command-Line Workflow

A basic RTL simulation and synthesis workflow can be summarized as follows:

1. Navigate to the project directory using Linux commands.
2. Inspect the source files and project structure.
3. Compile the RTL design and testbench using Icarus Verilog.
4. Execute the simulation and examine its output.
5. Generate and inspect waveforms using GTKWave.
6. Load the RTL design into Yosys.
7. Select the top-level module and run synthesis.
8. Inspect synthesis statistics and the resulting netlist.
9. Check library paths and dependencies when technology mapping is required.

Simulation and synthesis serve different purposes: simulation verifies functional behavior, while synthesis transforms the RTL into a hardware representation.

## 11. Learning Outcomes

Through this training, I developed practical familiarity with the Linux command line and its role in VLSI development.

The main skills gained include:

- Executing basic Linux commands.
- Navigating directories and locating source files.
- Understanding relative and absolute file paths.
- Compiling and running Verilog simulations.
- Opening and analyzing waveform files.
- Exploring RTL synthesis using Yosys.
- Understanding the role of standard-cell libraries.
- Inspecting the VSD BabySoC project structure.
- Troubleshooting common file-path, tool, and simulation errors.

## 12. Tools and Technologies

- Linux Terminal
- Verilog HDL
- Icarus Verilog
- GTKWave
- Yosys
- SKY130 Standard-Cell Library
- VSD BabySoC Environment

## Conclusion

Linux is an important part of the VLSI design workflow because it provides the environment for managing source files, executing design tools, and inspecting generated results.

Learning Linux command-line operations made it easier to navigate Verilog projects, run simulations, explore synthesis, and understand the dependencies involved in practical digital design workflows.
