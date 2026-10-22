# 4-Stage Pipelined ALU (Verilog)

## Overview
A 4-stage pipelined processor datapath in Verilog containing a register file,
an ALU, and a data memory. Each instruction flows through register read,
execute, write-back, and memory access stages, with pipeline latches
(L12, L23, L34) between stages.

## Pipeline Stages
| Stage | Function |
|-------|----------|
| S1 | Register file read (rs1, rs2), latch rd/func/addr |
| S2 | ALU execute |
| S3 | Register file write-back |
| S4 | Memory store and output latch |

## Supported ALU Operations
| func | Operation |
|------|-----------|
| 0 | ADD |
| 1 | SUB |
| 2 | MUL |
| 5 | AND |
| 6 | OR |
| 7 | XOR |

## Block Diagram
<img width="2600" height="1000" alt="pipeline_diagram" src="https://github.com/user-attachments/assets/e2c280ef-fe54-4f15-9860-9174deaadd3d" />


## Module Hierarchy
- `alu_pipeline_top`: top level
  - `alu_control`: generates stage enable signals
  - `alu_datapath`: register file, ALU, memory, pipeline latches

## Testbench
`tb_alu_pipeline_top.v` runs three back-to-back instructions:
1. `reg[1] + reg[2]` (10 + 5) → write to reg[4] → **15**
2. `reg[3] - reg[2]` (15 - 5) → write to reg[5] → **10**
3. `reg[1] * reg[2]` (10 × 5) → store to mem[10] → **50**

## Simulation Waveform
<img width="1620" height="922" alt="Screenshot 2026-10-22 181455" src="https://github.com/user-attachments/assets/efc4ebe8-1357-40bc-8983-c2115089c192" />


## Tools Used
Xilinx Vivado (behavioral simulation)

## How to Run
1. Open Vivado → Create Project → add `rtl/*.v` as design sources
2. Add `tb/tb_alu_pipeline_top.v` as a simulation source
3. Flow Navigator → Run Simulation → Run Behavioral Simulation
4. Run for about 200 ns and check the Tcl console output
