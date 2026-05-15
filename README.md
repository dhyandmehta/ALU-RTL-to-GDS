# ALU RTL to GDS
## 8-bit ALU Full RTL-to-GDS Flow Using OpenLane and Sky130 PDK

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![PDK](https://img.shields.io/badge/PDK-Sky130A-blue)
![Tool](https://img.shields.io/badge/Tool-OpenLane_v1.0.2-orange)

## Overview

This project presents the design and implementation of a fully functional **8-bit Arithmetic Logic Unit (ALU)** using a complete ASIC design flow, starting from RTL design and ending at GDSII generation. The design was implemented using the **Sky130 130nm PDK** with **OpenLane**.

---

## Supported Operations

| Opcode | Operation | Description |
|--------|-----------|-------------|
| `000`  | ADD       | `A + B` with carry |
| `001`  | SUB       | `A - B` |
| `010`  | AND       | `A & B` |
| `011`  | OR        | `A | B` |
| `100`  | XOR       | `A ^ B` |
| `101`  | NOT       | `~A` |
| `110`  | LSH       | `A << 1` |
| `111`  | RSH       | `A >> 1` |

---

## Tools Used

| Tool | Version | Purpose |
|------|---------|---------|
| Verilog HDL | - | RTL design |
| Icarus Verilog | 12.0 | Simulation |
| GTKWave | 3.3.116 | Waveform viewing |
| Yosys | 0.33 | Synthesis |
| OpenLane | v1.0.2 | ASIC physical design flow |
| Sky130A PDK | 130nm | Process design kit |
| KLayout | 0.28.16 | GDS viewing |

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

---

## Design Flow

**RTL Design → Simulation → Synthesis → Floorplanning → Placement → Routing → GDS Generation**

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

---

## Screenshots

### GTKWave Simulation

![GTKWave](GTK%20Wave.jpeg)

### Yosys Schematic

![Schematic](schemetic.jpeg)

### KLayout GDS Layout

![Layout](layout.jpeg)

### Synthesis Report

![Synthesis](synthesis.jpeg)

### NGSpice CMOS Inverter Simulation

![NGSpice](ngspice.jpeg)

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

---

## Author

**Dev Makwana**
ECE Student, Government Engineering College, Gandhinagar

[LinkedIn](https://linkedin.com/in/dev-makwana-a8815129a)

---

⭐ If you found this project useful, please consider starring the repository.

```


If you want, I can also remake it into a **more attractive GitHub README with badges, sections, and a stronger project-description style**.
```
