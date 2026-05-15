
# ALU-RTL-to-GDS

## 8-bit ALU Full RTL-to-GDS Flow Using OpenLane and Sky130 PDK

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![PDK](https://img.shields.io/badge/PDK-Sky130A-blue)
![Tool](https://img.shields.io/badge/Tool-OpenLane_v1.0.2-orange)

## Overview

This project demonstrates the complete implementation of an **8-bit Arithmetic Logic Unit (ALU)** using a full **RTL to GDSII ASIC design flow**. The design was developed for the **Sky130 130nm process design kit (PDK)** and implemented using **OpenLane**, with verification and analysis performed through standard open-source EDA tools.

An ALU is one of the most fundamental digital building blocks in processor architecture. It performs arithmetic operations, bitwise logical operations, and simple shift operations on binary data. In this project, the ALU is designed as a compact combinational datapath module that accepts two 8-bit operands and a 3-bit opcode, then produces the corresponding result according to the selected function.

The objective of this repository is not only to describe the RTL design, but to show the full implementation path used in a real ASIC environment:

**RTL Design → Functional Simulation → Logic Synthesis → Floorplanning → Placement → Clock Tree / Optimization (if applicable) → Routing → GDS Generation**

This makes the project useful for students, beginners in ASIC flow, and anyone studying how a digital design moves from Verilog code to physical silicon layout.

---

## Design Objective

The main goal of the design is to build a reliable and synthesizable 8-bit ALU that:

- supports multiple arithmetic and logic functions,
- uses a simple control interface through opcode selection,
- is compatible with ASIC synthesis and physical design flow,
- produces clean simulation results,
- can be implemented in a standard-cell based flow using open-source tools.

The project emphasizes both **functional correctness** and **physical implementation feasibility**, which is essential in ASIC design.

---

## ALU Functionality

The ALU uses a **3-bit opcode** to select one of eight operations.

| Opcode | Operation | Description |
|--------|-----------|-------------|
| `000`  | ADD       | Adds `A + B` and includes carry handling |
| `001`  | SUB       | Subtracts `B` from `A` |
| `010`  | AND       | Performs bitwise AND operation |
| `011`  | OR        | Performs bitwise OR operation |
| `100`  | XOR       | Performs bitwise XOR operation |
| `101`  | NOT       | Performs bitwise complement of `A` |
| `110`  | LSH       | Logical left shift by 1 |
| `111`  | RSH       | Logical right shift by 1 |

### Notes on behavior

- **ADD** is useful for arithmetic datapath computation.
- **SUB** is used for difference calculation and comparison-based logic.
- **AND, OR, XOR, NOT** are standard bitwise operations used in control, masking, and boolean processing.
- **LSH and RSH** are basic shift operations used in address manipulation, scaling, and simple bit transformations.

Because the ALU is combinational, the output depends directly on the current input values and opcode selection.

---

## Architectural Description

The ALU is built as a simple datapath block with the following inputs and outputs:

### Inputs
- `A[7:0]` : First 8-bit operand
- `B[7:0]` : Second 8-bit operand
- `opcode[2:0]` : Function selector

### Output
- `Y[7:0]` : 8-bit result of selected operation

### Internal concept

The ALU internally evaluates all supported operations and selects the correct output based on the opcode. This kind of implementation is efficient for a compact educational design because:

- it is easy to read and verify,
- it synthesizes cleanly,
- it maps well to standard-cell logic,
- it is suitable for studying gate-level optimization.

For larger processor designs, the same ALU concept may be extended with flags such as:

- carry out,
- zero flag,
- overflow flag,
- sign flag,
- parity flag.

---

## Why This Design Is Important

This project is valuable because it connects **digital logic theory** with **practical ASIC implementation**. A student often learns ALU behavior in theory, but the full RTL-to-GDS flow shows how that theory becomes a real chip layout.

The design demonstrates:

- Verilog-based hardware description,
- RTL simulation using testbench methodology,
- synthesis into gate-level logic,
- physical design flow through OpenLane,
- layout generation on Sky130,
- final GDS view validation using KLayout.

This is a complete example of how open-source digital IC design tools can be used to create an implementable chip block.

---

## Tools Used

| Tool | Version | Purpose |
|------|---------|---------|
| Verilog HDL | - | RTL design |
| Icarus Verilog | 12.0 | Functional simulation |
| GTKWave | 3.3.116 | Waveform visualization |
| Yosys | 0.33 | Logic synthesis |
| OpenLane | v1.0.2 | ASIC implementation flow |
| Sky130A PDK | 130nm | Process design kit |
| KLayout | 0.28.16 | GDS layout viewing |

### Tool roles in the flow

- **Verilog HDL** is used to describe the hardware behavior.
- **Icarus Verilog** compiles the design and executes the testbench.
- **GTKWave** helps inspect input/output transitions and confirm logic correctness.
- **Yosys** converts RTL into a gate-level netlist.
- **OpenLane** handles the physical design stages required for ASIC realization.
- **Sky130A PDK** provides the transistor and standard-cell technology file set.
- **KLayout** is used to inspect the generated layout and final GDS output.

---

## Design Results

| Metric | Value |
|--------|-------|
| Total Cells | 235 |
| Total Wires | 231 |
| Wire Bits | 254 |
| ANDNOT Gates | 89 |
| OR Gates | 65 |
| NOR Gates | 24 |
| XOR Gates | 12 |
| Die Area | 200 × 200 µm |
| PDK | Sky130A 130nm |

### Interpretation of results

- The reported cell count shows a relatively compact synthesized implementation.
- The gate distribution reflects the boolean nature of the ALU logic.
- The die area indicates that the design fits within a small physical footprint.
- The netlist statistics are useful for understanding synthesis complexity and gate utilization.

These results may vary slightly depending on synthesis constraints, optimization settings, and tool versions.

---

## Design Flow

The project follows the standard ASIC implementation sequence:

**RTL Design → Simulation → Synthesis → Floorplanning → Placement → Routing → GDS Generation**

### Flow explanation

#### 1. RTL Design
The ALU is first described in Verilog at the register-transfer level. This stage defines the functional behavior without concern for silicon layout.

#### 2. Simulation
A testbench is written to apply input combinations and verify the correctness of each opcode operation before hardware implementation.

#### 3. Synthesis
The RTL is mapped into a gate-level representation using Yosys. At this stage, the design becomes a logic network built from standard cells.

#### 4. Floorplanning
The chip core is defined and major physical regions are arranged to prepare for standard-cell placement.

#### 5. Placement
Standard cells are placed inside the core area according to optimization objectives such as congestion, timing, and wire length.

#### 6. Routing
Interconnects are generated between placed cells so that the logic can be physically connected on silicon.

#### 7. GDS Generation
The final layout is exported as GDSII, which is the standard file format for semiconductor mask data.

---

## Functional Verification

Functional verification is an essential part of the design process because it ensures that the RTL behavior is correct before synthesis and physical design.

### Verification goals
- confirm each opcode generates the expected output,
- verify arithmetic and logical correctness,
- observe output stability in waveform simulation,
- check that the design responds correctly to all operand combinations.

### Typical test cases
- `A = 8'd10`, `B = 8'd5`, `opcode = 000` → addition result
- `A = 8'd10`, `B = 8'd5`, `opcode = 001` → subtraction result
- `A = 8'b10101010`, `B = 8'b11001100`, `opcode = 010` → bitwise AND
- `A = 8'b10101010`, `opcode = 101` → bitwise NOT
- `A = 8'b00010001`, `opcode = 110` → logical left shift

Waveform inspection in GTKWave is used to confirm that transitions match the expected truth table.

---

## Physical Design Perspective

The significance of this project is that the design does not stop at RTL simulation. It is taken through the full ASIC implementation path, which makes it relevant to semiconductor design methodology.

### Physical implementation aspects

- **Standard-cell mapping** converts logic expressions into manufacturable library cells.
- **Floorplanning** ensures that the design can be physically organized within the chip area.
- **Placement and routing** determine how efficiently the cells are interconnected.
- **Design rule compliance** is necessary so the final GDS can be fabricated using the Sky130 process.

This is important because a design may simulate correctly at RTL but still fail in physical implementation if it is not synthesizable or layout-friendly.

---

## Project Structure

```text
ALU_Project/
├── rtl/
│   └── alu_8bit.v
├── testbench/
│   └── alu_tb.v
├── simulation/
│   └── alu_wave.vcd
├── synth/
│   └── synth.ys
├── reports/
│   └── synth_report.txt
└── docs/
    ├── gtkwave.png
    ├── schematic.png
    ├── layout.png
    └── synthesis.png
````

### Directory purpose

* `rtl/` contains the Verilog source of the ALU.
* `testbench/` contains simulation stimulus files.
* `simulation/` stores waveform and simulation output files.
* `synth/` contains synthesis scripts used by Yosys.
* `reports/` stores synthesis output and analysis reports.
* `docs/` includes figures and screenshots for documentation.

---

## Screenshots

### GTKWave Simulation

[![GTKWave](GTK%20Wave.jpeg)](https://github.com/Devnmakwana/ALU-RTL-to-GDS/blob/main/GTK%20Wave.jpeg)

### Yosys Schematic

[![Schematic](schemetic.jpeg)](https://github.com/Devnmakwana/ALU-RTL-to-GDS/blob/main/schemetic.jpeg)

### KLayout GDS Layout

[![Layout](layout.jpeg)](https://github.com/Devnmakwana/ALU-RTL-to-GDS/blob/main/layout.jpeg)

### Synthesis Report

[![Synthesis](synthesis.jpeg)](https://github.com/Devnmakwana/ALU-RTL-to-GDS/blob/main/synthesis.jpeg)

### NGSpice CMOS Inverter Simulation

[![NGSpice](ngspice.jpeg)](https://github.com/Devnmakwana/ALU-RTL-to-GDS/blob/main/ngspice.jpeg)

The screenshots provide visual confirmation of:

* correct waveform behavior,
* synthesized schematic structure,
* physical layout generation,
* supporting CMOS-level circuit analysis.

---

## How to Reproduce

```bash
# Clone the repository
git clone https://github.com/Devnmakwana/ALU-RTL-to-GDS.git
cd ALU-RTL-to-GDS

# Run simulation
iverilog -o simulation/alu_sim rtl/alu_8bit.v testbench/alu_tb.v
vvp simulation/alu_sim
gtkwave simulation/alu_wave.vcd

# Run synthesis
yosys synth/synth.ys
```

### Reproduction notes

* Ensure that the required EDA tools are installed in your environment.
* The simulation step verifies RTL functionality before synthesis.
* The synthesis step produces the gate-level representation.
* For full ASIC flow execution, OpenLane should be configured with the Sky130 environment.

---

## Learning Value

This repository is useful for understanding the following topics:

* combinational logic design,
* Verilog RTL coding,
* testbench-based validation,
* hardware synthesis,
* standard-cell ASIC flow,
* open-source EDA methodology,
* GDS layout generation,
* chip implementation on Sky130 PDK.

For a student, this project is a strong example of how digital design progresses from abstract logic to a physical chip-ready layout.

---

## Possible Extensions

The design can be extended in several directions:

* add carry, zero, overflow, and sign flags,
* increase operand width from 8-bit to 16-bit or 32-bit,
* support rotate operations,
* include comparison operations,
* pipeline the ALU for higher performance,
* integrate the ALU into a simple CPU datapath,
* improve verification with assertion-based testbenches,
* perform timing analysis under different constraints.

These extensions would increase architectural complexity and make the project more suitable for advanced processor design exploration.

---

## Author

**Dev Makwana**
ECE Student, Government Engineering College, Gandhinagar

[LinkedIn](https://linkedin.com/in/dev-makwana-a8815129a)

---

⭐ If this project helped you understand RTL-to-GDS design, consider starring the repository.

```
