# ARM Single-Cycle CPU

##  Overview
This project implements a simple 64-bit ARM single-cycle CPU using SystemVerilog. It was originally developed as part of Lab 03 for UW's EE 469 (Computer Design and Organization) course.
  
### Design Objectives:
- Implement a functional datapath and control unit.
- Support a subset of ARM instructions.
- Understand instruction execution and processor organization.
- Verify CPU functionality through simulation.

## Instruction Set

```systemverilog
ADDI Rd, Rn, Imm12: Reg[Rd] = Reg[Rn] + ZeroExtend(Imm12).
ADDS Rd, Rn, Rm: Reg[Rd] = Reg[Rn] + Reg[Rm].  Set flags.
B Imm26: PC = PC + SignExtend(Imm26 << 2).
B.LT Imm19: If (flags.negative != flags.overflow) PC = PC + SignExtend(Imm19<<2).
BL Imm26: X30 = PC + 4 (instruction after this one), PC = PC + SignExtend(Imm26<<2).
BR Rd: PC = Reg[Rd].
CBZ Rd, Imm19: If (Reg[Rd] == 0) PC = PC + SignExtend(Imm19<<2).
LDUR Rd, [Rn, #Imm9]: Reg[Rd] = Mem[Reg[Rn] + SignExtend(Imm9)].
STUR Rd, [Rn, #Imm9]: Mem[Reg[Rn] + SignExtend(Imm9)] = Reg[Rd].
SUBS Rd, Rn, Rm: Reg[Rd] = Reg[Rn] - Reg[Rm].  Set flags.
```

## CPU Architecture
### Datapath diagram
![CPU Datapath](images/datapath.png)

### Single-cycle execution flow
- Instruction Fetch (IF)
- Instruction Decode (ID)
- Execute (EX)
- Memory Access (MEM)
- Write Back (WB)

## RTL Modules and Components

| Hardware Component | Files | Usage |
|---|---|---|
| Program Counter (PC) | `pc.sv` | Stores the address of the current instruction and updates the PC for sequential execution or branching. |
| Instruction Memory | `instructmem.sv` | Stores and provides instructions based on the PC address. |
| PC Logic | `pc_logic.sv` | Determines the next PC value for sequential execution and branch operations. |
| Register File | `regfile.sv` | Stores CPU registers and supports register read and write operations. |
| ALU | `alu.sv` | Performs arithmetic and logical operations. |
| Data Memory | `datamem.sv` | Handles memory read and write operations for load and store instructions. |
| Control Unit | `control.sv` | Generates control signals based on the instruction opcode. |
| Sign Extender | `sign_extender.sv` | Extends the sign bit to 64 bits. |
| Zero Extender | `zero_extender.sv` | Fills upper bits with zeros. |
| Multiplexers | `mux2_64.sv` | Selects between multiple data inputs based on control signals. |
| CPU Top Module | `cpu.sv` | Integrates all components into a complete single-cycle CPU. |

## Datapath and Control
### Datapath diagram
![CPU Datapath](images/datapath.png)

### Control Signals
| Control Signal | ADDI | ADDS | SUBS | LDUR | STUR | CBZ | B | B.LT | BL | BR |
|---|---|---|---|---|---|---|---|---|---|---|
| UncondBranch | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 |
| PCSrc | 00 | 00 | 00 | 00 | 00 | 01 | 10 | 01 | 10 | 10 |
| Reg2Loc | X | 0 | 0 | X | 1 | 1 | X | X | X | X |
| RegWrite | 1 | 1 | 1 | 1 | 0 | 0 | 0 | 0 | 1 | 0 |
| ALUSrc | 1 | 0 | 0 | 1 | 1 | 0 | X | X | X | X |
| ALUOp | 00 | 10 | 10 | 00 | 00 | 01 | XX | XX | XX | XX |
| MemWrite | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
| MemRead | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 |
| MemtoReg | 0 | 0 | 0 | 1 | X | X | X | X | 0* | X |
| imm_sel | IMM12 | X | X | IMM9 | IMM9 | IMM19 | IMM26 | IMM19 | IMM26 | X |
| FlagWrite | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| Link | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 |

## Project Structure
[RTL Source Files](rtl/)  
[Testbench Files](testbench/)  
[Simulation Results](simulation/)  

## Verification and Testing
- Testbench methodology
- Test programs
- Expected vs. actual results
- Simulation waveforms

## Simulation Results
- Instruction execution examples
- Register updates
- Memory operations
- PC behavior

## Limitations
- Unsupported instructions
- Architectural limitations
- Current design assumptions

## Future Improvements
- Pipeline implementation
- Hazard detection and forwarding
- Cache and memory hierarchy
