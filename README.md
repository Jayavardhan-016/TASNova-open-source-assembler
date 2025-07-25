# TASNova Open-Source Assembler and Processor Simulator

TASNova is a modular, synthesizable 40-bit custom processor architecture implemented in SystemVerilog. This project includes a full assembler, instruction decoder, ALU, register file, and processor simulator to demonstrate instruction execution and register tracing in a real-world pipeline environment.

---

## DESCRIPTION

- Modular 40-bit processor with 30+ ALU instructions  
- Assembler converts human-readable assembly into machine instructions  
- Supports multiple operand modes (Reg–Reg, Reg–Imm, Imm–Reg, Imm–Imm)  
- Includes instruction decoder, ALU, and register file modules  
- Processor simulator runs instructions step-by-step with detailed logging  
- Designed for education, debugging, and practical RTL design practice
- The assembler is customizable to your specific processor design. Currently, the assembler supports 64 unique instructions, with several opcodes reserved for future expansion.
- We can use our own instruction set over their

---

## Project Phases and Structure

### Phase 1: Assembler Design (Core Project)  
**Module:** `assembler.sv`  

The assembler is the core of this project. It converts human-readable assembly instructions (e.g., `ADD R1, R2`, `MOV R3, #25`) into 40-bit machine instructions.

- **Instruction Format**:
  - 6 bits — Opcode  
  - 2 bits — Operand mode  
  - 32 bits — Operands (split into two 16-bit fields)  
- **Operand Modes**:
  - `00`: Register to Register (Reg–Reg)  
  - `01`: Register to Immediate (Reg–Imm)  
  - `10`: Immediate to Register (Imm–Reg)  
  - `11`: Immediate to Immediate (Imm–Imm)  
- **Output**: `output.txt` containing hex-encoded 40-bit instructions  

> This is the **main IP module** — all other modules are built to validate and simulate the assembler's output.

---

### Phase 2: Module Integration for Assembler Testing  

The following modules form a minimal but complete processor environment to test the assembler output.

#### Instruction Decoder (`instruction_decoder.sv`)  
- Reads 40-bit instructions from `output.txt`  
- Extracts opcode, mode, and two 16-bit operands  
- Supports all operand modes with proper zero/sign extension  

#### ALU (`alu_top.sv`)  
- Executes instructions based on opcode and operands  
- Supports 30+ ALU operations, including:  
  - Arithmetic: ADD, SUB, MUL, DIV, MOD, INC, DEC  
  - Logic: AND, OR, XOR, NOT, NAND, NOR, XNOR  
  - Shifting/Rotating: SHL, SHR, SAR, ROL, ROR  
  - Comparison: EQ, NE, GT, LT, GE, LE  
  - Special: MOV, NEG, ZERO, MAX, MIN, SWAP, REV  

#### Register File (`register_file.sv`)  
- Contains 256 general-purpose 32-bit registers  
- Supports dual write operations per clock cycle  
- All register values are accessible for logging and debugging  

---

### Phase 3: Processor Simulation and Execution  

#### Processor Simulator (`processor_simulator.sv`)  
- Loads instructions from `output.txt`  
- Decodes and executes instructions step-by-step  
- Updates registers with ALU results  
- Includes basic error detection (e.g., uninitialized register usage)  
- Logs every instruction and final register states in a human-readable format  

> The simulator runs in single-step mode — ideal for debugging and understanding execution flow.

---

## Output Files  

- `output.txt`: Machine code generated by the assembler  
- `execution_log.txt`: Detailed instruction decoding and register output logs  

---

## Sample Log Output  

-Final Register Values:
- R1 = 25
- R2 = 10
- Instruction 0: MOV R1 #25
- MOV: R1 <- 25
- Instruction 1: ADD R1 R2
- ADD: R1 <- 25 + 10 = 35

---

  ## 👤 Author

**Nakka Jayavardhan**  
[LinkedIn](https://linkedin.com/in/nakkajayavardhan) 

---
