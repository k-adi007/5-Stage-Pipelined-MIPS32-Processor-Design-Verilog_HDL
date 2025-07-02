# 🖥️ MIPS32 5-Stage Pipelined Processor
A Verilog HDL implementation of a MIPS32 processor with a classic 5-stage pipeline architecture: **IF**, **ID**, **EX**, **MEM**, and **WB**.

## 📌 Project Details
- **Author**: Aditya Krishna  
- **Roll No**: 23JE0047  
- **Department**: Electrical Engineering  
- **Design Language**: Verilog HDL  
- **Architecture**: MIPS32 (32-bit)

---

## 📚 Supported Instructions

### ➤ **R-type Instructions**
| Instruction | Format            | Description                     |
|------------|-------------------|---------------------------------|
| `ADD`      | `R1 = R2 + R3`    | Integer addition                |
| `SUB`      | `R1 = R2 - R3`    | Integer subtraction             |
| `AND`      | `R1 = R2 & R3`    | Bitwise AND                     |
| `OR`       | `R1 = R2 \| R3`   | Bitwise OR                      |
| `MUL`      | `R1 = R2 * R3`    | Integer multiplication          |
| `SLT`      | `R1 = (R2 < R3)`  | Set if less than                |

### ➤ **I-type Instructions**
| Instruction | Format                    | Description                  |
|------------|---------------------------|------------------------------|
| `ADDI`     | `R1 = R2 + Imm`           | Add immediate                |
| `SUBI`     | `R1 = R2 - Imm`           | Subtract immediate           |
| `SLTI`     | `R1 = (R2 < Imm)`         | Set if less than immediate   |
| `LW`       | `R1 = Mem[R2 + offset]`   | Load word from memory        |
| `SW`       | `Mem[R2 + offset] = R1`   | Store word to memory         |
| `BEQZ`     | `if (R1 == 0) PC += Imm`  | Branch if zero               |
| `BNEQZ`    | `if (R1 != 0) PC += Imm`  | Branch if not zero           |

### ➤ **J-type Instruction**
- `J target` – Unconditional jump to address

### ➤ **Miscellaneous**
- `HLT` – Halt execution

---

## 🔁 Pipeline Stages

1. **IF** – Instruction Fetch
2. **ID** – Instruction Decode / Register Fetch
3. **EX** – ALU Execution / Address Calculation
4. **MEM** – Memory Access / Branch Completion
5. **WB** – Write back result to register

Each stage uses inter-stage latches: `IF_ID`, `ID_EX`, `EX_MEM`, `MEM_WB`.

---

## 🧪 Testbenches

### ✅ Testbench 1: Add Three Numbers
```assembly
ADDI R1, R0, 10     # R1 = 10
ADDI R2, R0, 20     # R2 = 20
ADDI R3, R0, 30     # R3 = 30
ADD  R4, R1, R2     # R4 = R1 + R2 = 30
ADD  R5, R4, R3     # R5 = R4 + R3 = 60
HLT
---
```


### ✅ Testbench 2: Memory Load + Add + Store
```assembly
ADDI R1, R0, 120    # R1 = 120
LW   R2, 0(R1)      # R2 = Mem[120]
ADDI R2, R2, 45     # R2 += 45
SW   R2, 1(R1)      # Mem[121] = R2
HLT                 # Halt execution
```


### 🔧 File Structure
```
├── Verilog/
│   ├── mips32_pipeline.v      # Top module
│   ├── control_unit.v         # Control logic
│   ├── register_file.v        # Register file
│   ├── alu.v                  # Arithmetic Logic Unit
│   ├── data_memory.v          # Data Memory
│   ├── instruction_memory.v   # Instruction Memory
│   ├── testbench1.v           # Testbench 1
│   ├── testbench2.v           # Testbench 2
├── doc/
│   └── MIPS32_documentation.pdf
├── waves/
│   └── gtkwave_output.vcd
└── README.md
```

### 🧠 Pipeline Visualization
```
Cycle:    1    2    3    4    5    6    7
Instr1:  IF → ID → EX → MEM → WB
Instr2:       IF → ID → EX → MEM → WB
Instr3:            IF → ID → EX → MEM → WB
...
```




