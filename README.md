
# CORE TRAINING RTL-GDSII
## Introduction to Verilog RTL Design and Synthesis

## Overview
In this module, I learned the fundamentals of Verilog RTL design, testbench development, functional simulation, waveform analysis, and logic synthesis using open-source VLSI tools.

## 1. RTL Design Flow

**RTL Design → Testbench → Simulation → Waveform Analysis → Synthesis**

![RTL Design Flow](images/image.png)

## 2. 2:1 Multiplexer (MUX)

A 2:1 Multiplexer selects one of two inputs based on the select signal.

| Select (`sel`) | Output (`y`) |
|---|---|
| 0 | `i0` |
| 1 | `i1` |

## 3. Verilog RTL Design

I learned to describe digital hardware using Verilog HDL and conditional logic.

```verilog
module good_mux (
    input i0,
    input i1,
    input sel,
    output reg y
);

always @(*) begin
    if (sel)
        y <= i1;
    else
        y <= i0;
end

endmodule
```

![Verilog RTL Code](images/muxcode.png)

## 4. Simulation Using Icarus Verilog

I learned to compile and run the Verilog design with its testbench.

```bash
iverilog good_mux.v tb_good_mux.v
./a.out
```

The simulation produces a VCD file containing signal transitions.

![Icarus Verilog Simulation Flow](images/Iverilog%20based%20simulation%20flow.png)

## 5. Waveform Analysis Using GTKWave

I used GTKWave to observe signal transitions and verify the MUX output against its inputs.

```bash
gtkwave tb_good_mux.vcd
```

![GTKWave Waveform](images/goodmuxwave.png)

## 6. RTL Synthesis Using Yosys

I explored how Yosys reads RTL and identifies the top-level design before synthesis.

```tcl
read_verilog good_mux.v
hierarchy -top good_mux
synth -top good_mux
```

![Yosys Setup](images/yosys%20setup.png)

![Yosys Synthesis Flow](images/Synthesiser%20yosys.png)

## 7. Standard-Cell Libraries

I learned that standard-cell libraries provide information about hardware cells, including their timing and power characteristics. Synthesis tools can use these libraries for technology mapping.

![Standard-Cell Library](images/What%20is%20lib.png)

## 8. Simulation vs. Synthesis

| Simulation | Synthesis |
|---|---|
| Verifies functional behavior | Converts RTL into a hardware logic representation |
| Uses RTL and a testbench | Uses RTL and, for technology mapping, a cell library |
| Produces simulation waveforms | Produces a synthesized logic representation or netlist |
| Tool: Icarus Verilog | Tool: Yosys |

## Key Learning Outcomes

- Understood the basic RTL design flow.
- Practiced Verilog coding for a 2:1 MUX.
- Learned testbench-based functional simulation.
- Used GTKWave for waveform analysis.
- Explored RTL synthesis using Yosys.
- Understood the role of standard-cell libraries.

## 7. Flat Synthesis

Flat synthesis converts a hierarchical design into a single-level logic structure by removing submodule boundaries using the `flatten` command.

### Yosys Commands

```bash
flatten
show
write_verilog -noattr multiple_modules_flat.v
```
## Gate-Level Simulation (GLS)

### What Is GLS?

**Gate-Level Simulation (GLS)** is the process of simulating a synthesized gate-level netlist using a testbench and standard-cell simulation models.

### GLS Flow

RTL Design → RTL Synthesis → Gate-Level Netlist → GLS → GTKWave → Waveform Comparison

### Tools Used
- **Yosys:** Synthesizes RTL into a gate-level netlist.
- **Icarus Verilog:** Runs the gate-level simulation.
- **GTKWave:** Displays and compares simulation waveforms.
- **Sky130 Library:** Provides standard-cell models for simulation.

### Why Is GLS Important?
- Verifies the behavior of the synthesized design.
- Helps identify synthesis-simulation mismatches.
- Checks whether the gate-level design behaves as expected compared with RTL simulation.

### Synthesis-Simulation Mismatch

A mismatch occurs when RTL simulation and gate-level simulation produce different behavior.

**Common causes studied:**
- Incomplete sensitivity lists, such as `always @(sel)`.
- Incorrect ordering of blocking assignments (`=`) in combinational logic.

### Key Learning Outcome

Learned the purpose of GLS, the gate-level simulation flow, and how incomplete sensitivity lists and blocking assignment order can cause differences between RTL simulation and synthesized hardware behavior.
# VSD BabySoC – RTL Synthesis and Verification

## Overview

Studied the **VSD BabySoC** environment to understand how RTL modules, testbenches, synthesis, and gate-level netlists are used in a System-on-Chip (SoC) design flow.

## 1. VSD BabySoC

BabySoC was explored as a practical SoC design for understanding RTL structure and synthesis.

![VSD BabySoC](screenshots/vsdbaby_soc.jpeg)

## 2. RVMYTH Module

Inspected the RVMYTH module to understand its role within the BabySoC design hierarchy.

![RVMYTH Module](screenshots/rv_myth.jpeg)

## 3. BabySoC Testbench

Examined the testbench used to provide inputs and verify the SoC design during simulation.

![BabySoC Testbench](screenshots/test_bench%20file.jpeg)

## 4. BabySoC Synthesis Using Yosys

Explored synthesis using Yosys to convert the RTL design into a synthesized hardware representation.

![BabySoC Synthesized Design](screenshots/Baby_soc%20synthesized%20design.jpeg)

## 5. Synthesis Statistics

Reviewed Yosys synthesis statistics to understand the components and structure of the synthesized design.

![BabySoC Synthesis Statistics](screenshots/BabySoC%20Synthesis%20Statistics.jpeg)

## 6. BabySoC Netlist

Inspected the generated netlist to understand the hardware representation after synthesis.

![BabySoC Netlist](screenshots/Baby_Soc_simulation%20_soc_netlist.jpeg)

![Additional BabySoC Netlist View](screenshots/Baby_Soc_simulation%20_soc2_netlist.jpeg)

## 7. Pre-Synthesis and Post-Synthesis Comparison

Studied the comparison between pre-synthesis and post-synthesis results to understand how RTL is represented after synthesis.

![Pre-Synthesis vs Post-Synthesis](screenshots/Comparion%20post_pre.jpeg)

## Key Learning Outcomes

- Explored the BabySoC design hierarchy.
- Inspected the RVMYTH module and testbench.
- Learned the role of Yosys in SoC synthesis.
- Examined synthesis statistics and generated netlists.
- Studied pre-synthesis and post-synthesis comparison.

## Tools and Technologies

- Verilog HDL
- Linux Terminal
- Icarus Verilog
- GTKWave
- Yosys
- SKY130 Standard-Cell Library
- VSD BabySoC Environment
