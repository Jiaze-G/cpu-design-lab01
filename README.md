# CPU Design Lab

A SystemVerilog-based processor design project focused on CPU architecture, pipeline optimization, and memory subsystem design.

## Overview

This project explores the design and development of a modular processor using SystemVerilog. Building on foundational digital design concepts, it aims to extend a basic processor architecture with additional microarchitectural features and improved verification.

The project emphasizes modular RTL development, functional correctness, and performance evaluation through simulation.

## Project Objectives

- Develop reusable and modular RTL components.
- Extend a basic processor with advanced pipeline features.
- Explore memory subsystem design and optimization.
- Implement systematic verification using simulation and testbenches.
- Evaluate architectural performance through measurable metrics.

## Planned Features

### Processor Architecture
- 64-bit processor datapath
- Five-stage instruction pipeline (IF, ID, EX, MEM, WB)
- Instruction decoding and control logic

### Pipeline Optimization
- Data forwarding
- Hazard detection
- Pipeline stalling and flushing
- Branch prediction using 2-bit saturating counters and a Branch Target Buffer (BTB)

### Memory Subsystem
- Set-associative cache
- LRU replacement policy
- Write-back cache management
- Memory interface design

### Verification and Analysis
- SystemVerilog testbenches
- Functional assertions
- Directed and regression testing
- Performance analysis using CPI, cache hit rate, and branch prediction accuracy

## Tools and Technologies

- **HDL:** SystemVerilog, Verilog
- **Simulation:** ModelSim / Questa
- **Development:** Git, GitHub

## Repository Structure

```text
cpu-design-lab/
├── rtl/
│   ├── core/
│   ├── datapath/
│   ├── pipeline/
│   ├── hazard/
│   └── memory/
├── verification/
│   ├── unit/
│   ├── integration/
│   └── testbenches/
├── programs/
├── simulation/
└── README.md
```

## Development Status

This project is under active development.

Implementation and verification will be completed incrementally, with each major component tested independently before system-level integration.

## Project Scope

This is an independent hardware design project building upon foundational processor design concepts. The implementation, extensions, and verification are developed and evaluated incrementally.

---

*Focus: RTL Design · Processor Architecture · SystemVerilog Verification*
