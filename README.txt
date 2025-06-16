This project is a C-based simulation of a simplified Von Neumann processor architecture with full support for instruction fetching, decoding, execution, memory access, and write-back stages. The architecture follows a classic 5-stage pipelined processor design, accurately modeling instruction dependencies and execution timing, and supporting 12 distinct 32-bit instructions.

The simulation emphasizes instruction-level parallelism while respecting hardware constraints like shared memory access (between instruction fetch and memory stages). The processor operates on a 2048x32-bit memory, simulates 33 hardware registers, and executes programs cycle-by-cycle, demonstrating how actual hardware-level computation flows.

🧱 Architecture Details
🖥️ Processor Type: Von Neumann Architecture
Unified Memory Space for data and instructions.

Memory Size: 2048 words (each word is 32 bits)

Address range: 0 - 2047

Instruction memory: 0 - 1023

Data memory: 1024 - 2047

Memory is word-addressable

📦 Register File
Total: 33 Registers, all 32-bit

R0: Zero Register, hardwired to 0

R1 - R31: General-purpose registers

PC: Program Counter, stores the address of the current instruction

🔧 Instruction Set Architecture (ISA)
Instruction Size: 32 bits

Instruction Count: 12 instructions

Instruction Types: 3 types (e.g., R-type, I-type, Memory-type)

Example Instructions:

ADD, SUB, AND, OR

SLL, SRL (Shift Left/Right Logical)

LW, SW (Load/Store Word)

BEQ, BNE (Branch if Equal/Not Equal)

Instruction encoding and decoding follow strict bit slicing and opcode standards.

⚠️ Special Format Note:
In shift instructions (SLL, SRL), R3 is reserved and hardcoded to 0.

🚀 Pipelining Model
The processor follows a 5-stage pipeline model:

Instruction Fetch (IF)

Instruction Decode (ID) – 2 cycles

Execute (EX) – 2 cycles

Memory (MEM) – 1 cycle

Write Back (WB) – 1 cycle

⏱️ Pipeline Execution Rules
A maximum of 4 instructions can run in parallel at different pipeline stages.

Due to shared memory, IF and MEM cannot run simultaneously.

Clock cycle scheduling follows the pattern:

java
Copy
Edit
Total clock cycles = 7 + (n - 1) * 2
For example, a 7-instruction program requires: 7 + (6 * 2) = 19 cycles.

📂 Project Structure
bash

project-root/
│
├── src/
│   ├── main.c               # Entry point
│   ├── memory.c             # Memory read/write utilities
│   ├── instruction.c        # Instruction decoding and handling
│   ├── pipeline.c           # Pipeline simulation engine
│   ├── registers.c          # Register file handling
│   └── util.c               # Helpers for printing, parsing, etc.
│
├── include/
│   ├── memory.h
│   ├── instruction.h
│   ├── pipeline.h
│   ├── registers.h
│   └── util.h
│
├── test/
│   └── test_programs.asm    # Sample programs to simulate
│
└── README.md                # Project documentation
🧪 Simulation Features
Load instructions into memory from test files

Simulate instruction flow across stages

Track and visualize:

Clock cycle count

Pipeline stalls due to memory access conflict

Register and memory states per cycle

Output logs for debugging and educational inspection

🎓 Educational Goals
This project helps students understand:

The inner workings of a Von Neumann machine

Memory access bottlenecks in shared architectures

Realistic pipeline stage timing

How instructions are fetched, decoded, executed, and stored

The importance of register files and program counters

🛠️ How to Build & Run
Compile the project using gcc:

bash


gcc src/*.c -Iinclude -o processor_sim
Run the simulation:

bash


./processor_sim test/test_programs.asm
Review the printed output for memory, register, and pipeline state after each clock cycle.

📌 Future Enhancements (Optional Ideas)
Branch prediction simulation

Data hazard handling (forwarding/stalling)

GUI visualization with SDL or web-based display

Adding MIPS-like instruction extensions