``md
COMPUTER ARCHITECTURE

Aakash

Syllabus
Unit-I: Basic Computer Organization and Design

1.1 Instruction Codes  
1.2 Computer Registers  
1.3 Common bus system  
1.4 Computer Instructions  
1.5 Instruction formats  
1.6 Instruction Cycle  
1.7 Fetch and Decode  
1.8 Flowchart for Instruction cycle  
1.9 Register reference instructions

Unit-II: Register Transfer and Micro-operation

2.1 Register Transfer Language  
2.2 Register Transfer  
2.3 Bus and Memory Transfer  
2.4 Three state bus buffers  
2.5 Memory Transfer  
2.6 Arithmetic Micro operations  
2.7 Logic Micro operations

Unit-III: Micro programmed Control Unit & Central Processing Unit

3.1 Design of Control Unit  
3.2 Introduction to Central Processing Unit  
3.3 General Register Organization  
3.4 Stack Organization  
3.5 Register stack  
3.6 Memory stack  
3.7 Instruction Formats  
3.8 Addressing Modes

Unit-IV: Input Output Organization

4.1 Peripheral devices  
4.2 Input Output interface  
4.3 Modes of Data Transfer  
4.4 Priority Interrupt  
4.5 Direct Memory Access

Unit-V: Memory Organization

5.1 Memory Hierarchy  
5.2 Main Memory  
5.3 Auxiliary Memory  
5.4 Associative Memory  
5.5 Cache Memory  
5.6 Virtual Memory

Unit-I
Basic Computer Organization and Design

1.1 Instruction Codes  
1.2 Computer Registers  
1.3 Common bus system  
1.4 Computer Instructions  
1.5 Instruction formats  
1.6 Instruction Cycle  
1.7 Fetch and Decode  
1.8 Flowchart for Instruction cycle  
1.9 Register reference instructions

1.1 Instruction Codes

An instruction code is the "command" given to the computer in binary form (only 0s and 1s). It tells the CPU exactly what to do (like add, load, store, jump, etc.).

How an Instruction Code looks

In the basic computer (the one you are studying), one instruction is 16 bits long.

It is divided into 3 parts:

| Part | Number of Bits | What it does | Example |
| --- | --- | --- | --- |
| I (Indirect bit) | 1 bit (bit 15) | Tells whether address is direct or indirect | 0 = direct, 1 = indirect |
| Opcode (Operation Code) | 3 bits (bits 14-12) | Tells WHAT operation to perform (ADD, LOAD, etc.) | 000 = AND, 001 = ADD, etc. |
| Address (or Operand) | 12 bits (bits 11-0) | Tells WHERE the data is (memory location) | 000000001010 = memory address 10 |

Simple example: Suppose the instruction code is: 0 001 000000001010 → I=0 (direct), Opcode=001 (ADD), Address=10  
Meaning: "Add the number present at memory location 10 to the accumulator."

Types of Instructions (based on opcode)
Memory-Reference Instructions - Work with memory (ADD, LDA, STA, etc.)
Register-Reference Instructions - Work only inside CPU registers (CLA, CLE, INC, etc.)
Input/Output Instructions - For taking input or giving output (INP, OUT)

1.2 Computer Registers

Registers are super-fast, small storage places inside the CPU. They are much faster than main memory (RAM). The CPU uses them to hold data, addresses, and instructions while working.

| Register | Size | Full Name | Simple Function (in easy words) |
| --- | --- | --- | --- |
| AC | 16 bits | Accumulator | Main working register. All calculations (add, subtract) happen here. |
| DR | 16 bits | Data Register | Temporary storage for data coming from or going to memory. |
| PC | 12 bits | Program Counter | Holds the address of the next instruction to be executed. |
| AR | 12 bits | Address Register | Holds the memory address when we want to read or write. |
| IR | 16 bits | Instruction Register | Holds the current instruction that is being executed. |
| TR | 16 bits | Temporary Register | Extra temporary storage. |
| INPR | 8 bits | Input Register | Holds data coming from keyboard/input device. |
| OUTR | 8 bits | Output Register | Holds data to be sent to screen/printer. |

Easy way to remember: Think of registers as the CPU's pockets. AC is the biggest pocket where most work happens. PC is like a bookmark that says "next page to read".

1.3 Common Bus System

If we connect every register to every other register with separate wires, we need hundreds of wires → very costly and messy.

So, we use a Common Bus - like a single shared road (highway) inside the CPU.

• Only one register can put data on the bus at a time.
• Other registers can take (read) that data when needed.

How it works (very simple)
• There is a 16-bit common bus.

Each register has:
• LD (Load) → to take data FROM the bus
• INR (Increment) → to increase value by 1
• CLR (Clear) → to make it zero

• Three select lines S2, S1, S0 decide which register will put its data on the bus (like choosing which car enters the highway).

Example: To move data from DR to AC:
DR puts data on the bus (S2 S1 S0 select DR).
AC gives LD=1 → AC loads the data from the bus.

This common bus system saves a lot of wires and makes the design simple and clean.

Bus Types

Bus Types are the shared pathways (wires) that connect the CPU to memory, input/output devices, and other parts of the computer. They carry information in parallel (multiple bits at once) like a multi-lane highway. There are three main types, and together they form the system bus. Buses are bidirectional where needed and synced by the clock signal to avoid chaos.

Types of Bus Types

| Bus Type | Simple Meaning | Width (Bits) Example | Direction (Unidirectional/Bidirectional) | What It Carries |
| --- | --- | --- | --- | --- |
| Address Bus | Specifies locations (like house numbers) for where to read/write data. | 32-bit (accesses 4GB addresses) | Unidirectional (CPU → devices) | "Go to memory spot 100" |
| Data Bus | Transfers actual information (numbers, instructions) between parts. | 64-bit (handles big data fast) | Bidirectional (both ways) | "Send the number 50 here" |
| Control Bus | Sends commands and status signals (like traffic lights) to manage operations. | 8-16 lines (signals/flags) | Bidirectional (commands/status both ways) | "Read now" or "Interrupt!" |

Easy way to remember: Buses = "Mail system" — Address Bus = envelope address, Data Bus = letter inside, Control Bus = stamps/instructions. Without them, CPU can't "talk" to RAM or keyboard!

How Buses Work (Step-by-Step)

Buses operate in cycles (e.g., one clock tick = one transfer). They use buffers/drivers to boost signals over long distances and arbitration (priority system) if multiple devices compete. Here's a memory read cycle example (CPU fetching data from RAM at address 100):

Prepare Address: CPU loads address 100 into its Address Register (AR).
Address Bus Transmits: Address 100 (in binary, e.g., 00000000000001100100) is placed on Address Bus → RAM decodes it and selects the right spot.
Control Bus Commands: Control Bus sends "Read Enable" signal (high voltage = 1) → RAM knows to output data; "Write Disable" is low (0).
Data Bus Fetches: RAM puts data (e.g., instruction "ADD 5") on Data Bus → CPU's Data Register (DR) loads it.
Control Bus Confirms: Control Bus sends "Ready" status back → Cycle ends; buses clear for next use (e.g., write cycle reverses data flow).

This takes 1-3 clock cycles. In modern systems (e.g., PCIe bus), buses can be serial (faster, point-to-point) instead of parallel.

Easy way to remember: How buses work = "Delivery process" — Step 1: Check address (postcode), Step 2: Send command (open mailbox), Step 3: Grab package (data), Step 4: Confirm receipt. Clocks keep it rhythmic!

1.4 Computer Instructions

These are the actual commands that the CPU can understand and run. In the Basic Computer (the one in your syllabus), every instruction is 16 bits long, and they are divided into 3 clear types:

| Type | How to identify it | What it does (simple words) | Number of instructions |
| --- | --- | --- | --- |
| Memory Reference | Opcode = 000 to 110 (bits 14-12) | Works with memory (read data, add, store, jump etc.) | 7 |
| Register Reference | Opcode = 111 and I = 0 | Works only inside CPU registers (clear AC, increment, etc.) | 12 |
| Input/Output | Opcode = 111 and I = 1 | Takes input from keyboard or sends output to screen | 6 |

Most important - Memory Reference Instructions (you must remember these 7)

| Symbol | Name | Simple Meaning |
| --- | --- | --- |
| AND | Logical AND | AC = AC AND Memory[AR] |
| ADD | Add | AC = AC + Memory[AR] |
| LDA | Load to AC | AC = Memory[AR] |
| STA | Store AC | Memory[AR] = AC |
| BUN | Branch Unconditionally | PC = AR (jump to address) |
| BSA | Branch and Save Return Address | Save PC to memory, then jump |
| ISZ | Increment and Skip if Zero | Memory[AR]++, skip next if zero |

Easy way to remember: Memory Reference → talks to RAM. Register Reference → only inside CPU (no memory). I/O → keyboard or monitor.

1.5 Instruction Formats

This is the structure (layout) of the 16-bit instruction.

Main Format (used by Memory Reference Instructions)

`
Bit: 15 14 13 12 11 10 9 8 7 6 5 4 3 2 1 0
     I  |  Opcode  |       Address (12 bits)
`

• I (Indirect bit): 0 = Direct address, 1 = Indirect address
• Opcode (3 bits): Tells WHAT to do (000=AND, 001=ADD, ... 110=ISZ, 111=special)
• Address (12 bits): Memory location (0 to 4095)

Special Formats when Opcode = 111

Register Reference Format (I=0)

`
1 1 1 0 | 12-bit code (each bit does one micro-operation)
`

Example: 1110 0000 0000 0001 → CLA (Clear Accumulator)

Input/Output Format (I=1)

`
1 1 1 1 | 12-bit code for I/O operation
`

Example: 1111 0000 0000 0001 → INP (Input data)

Why different formats? Because when Opcode=111, the 12 address bits are not used as address - they are used as operation codes instead.

1.6 Instruction Cycle

This is the complete process the CPU follows to execute one single instruction. It repeats again and again until the program finishes.

4 main steps (very easy to remember):
Fetch → Bring the instruction from memory into CPU
Decode → Understand what the instruction says
Execute → Actually do the work (add, load, jump etc.)
Store (sometimes) → Save the result back if needed

In your Basic Computer (with timing):
• The whole cycle uses timing signals T0, T1, T2, ... T6
• Fetch usually takes T0 + T1
• Decode at T2
• Execute from T3 onwards
• If indirect addressing is used → one extra step (Indirect cycle)

Simple Flow (like a cycle):

`
Start → Fetch instruction (PC → AR → IR, PC++) → Decode the opcode →
If Memory Reference → check I bit → Indirect? → Execute →
If Register or I/O → Execute directly →
Go to next instruction (repeat)
`

This cycle runs millions of times per second!

1.7 Fetch and Decode

These are the first two steps of the Instruction Cycle. The CPU does them automatically for every instruction using timing signals (T0, T1, T2, ...). SC (Sequence Counter) starts at 0 and increases with every clock pulse.

Step-by-Step (very simple):

| Timing | What happens (Micro-operations) | Simple Meaning |
| --- | --- | --- |
| T0 | AR ← PC | Put the address of next instruction into Address Register (like opening the correct page in a book) |
| T1 | IR ← M[AR], PC ← PC + 1 | Bring the instruction from memory into Instruction Register + increase PC so it points to the next instruction |
| T2 | Decode the opcode (bits 14-12 of IR) + check I bit (bit 15) | Understand WHAT the instruction is (ADD? LDA? CLA?) and whether it is direct or indirect |

After T2, the control unit knows exactly which instruction to execute.

1.8 Flowchart for Instruction Cycle

This is the complete road map the CPU follows for every instruction. It is drawn using the timing signals T0 to T6 and SC (Sequence Counter).

Main Flowchart (in simple steps):
Start → SC ← 0
T0: AR ← PC
T1: IR ← M[AR], PC ← PC + 1
T2: Decode opcode in IR

If opcode = 111:
• If I = 0 → Register Reference Instruction
• If I = 1 → Input/Output Instruction

If opcode ≠ 111 → Memory Reference Instruction

For Memory Reference:
   - T3: If I = 1 → AR ← M[AR] (Indirect cycle)
   - Then Execute (T4, T5, T6 depending on instruction)

After execution → SC ← 0 (go back to fetch next instruction)

Important points in the flowchart:
• Indirect addressing adds one extra step at T3
• Register and I/O instructions finish quickly (no memory access)
• After any instruction finishes, SC is cleared to 0 and the cycle repeats

1.9 Register Reference Instructions

These are special instructions that work only inside the CPU registers (no memory access). They are identified by:

• Opcode = 111 (bits 14-12)
• I bit = 0 (bit 15)
• The 12 address bits become control signals (each bit does one job)

There are exactly 12 such instructions. All start with binary: 0111 followed by 12 bits.

| Hex Code | Symbol | Name | Simple Meaning (what it does) |
| --- | --- | --- | --- |
| 7800 | CLA | Clear Accumulator | AC ← 0 |
| 7400 | CLE | Clear Extend (E) | E ← 0 |
| 7200 | CMA | Complement Accumulator | AC ← AC' (flip all bits) |
| 7100 | CME | Complement Extend | E ← E' |
| 7080 | CIR | Circulate Right | Shift AC + E right (circular) |
| 7040 | CIL | Circulate Left | Shift AC + E left (circular) |
| 7020 | INC | Increment Accumulator | AC ← AC + 1 |
| 7010 | SPA | Skip if Positive | If AC ≥ 0 then PC ← PC + 1 (skip next instruction) |
| 7008 | SNA | Skip if Negative | If AC < 0 then PC ← PC + 1 |
| 7004 | SZA | Skip if Zero | If AC = 0 then PC ← PC + 1 |
| 7002 | SZE | Skip if E is Zero | If E = 0 then PC ← PC + 1 |
| 7001 | HLT | Halt | Stop the computer (SC ← 0 and stop clock) |

How they are executed: All these instructions are executed in one step at T3 (very fast because no memory is involved).

Example: If IR = 0111 1000 0000 0000 → CLA → Clear AC

Unit-II
Register Transfer and Micro-operation

2.1 Register Transfer Language  
2.2 Register Transfer  
2.3 Bus and Memory Transfer  
2.4 Three state bus buffers  
2.5 Memory Transfer  
2.6 Arithmetic Micro operations  
2.7 Logic Micro operations

2.1 Register Transfer Language (RTL)

Register Transfer Language (RTL) is a special symbolic way to write what happens inside the CPU during one clock pulse. It is like a "short-hand language" used only for computer design and micro-operations. We use RTL to describe how data moves from one register to another or how operations are performed.

Basic Symbols of RTL (must remember these 5)

| Symbol | Meaning | Simple Example |
| --- | --- | --- |
| Letters | Name of a register | AC, DR, PC, AR, R1 |
| ( ) Parentheses | Part of a register (bits) | AC(7:0), PC(L) = lower 8 bits |
| ← Arrow | Data is transferred / copied | DR ← AC (DR gets copy of AC) |
| , Comma | Two or more things happen at the same time | AC ← DR, PC ← PC + 1 |
| : Colon | Conditional (only if condition is true) | P: AC ← DR (if P=1 then do it) |

Easy examples in RTL:
• AC ← DR → Copy data from DR to AC
• R1 ← R2, R3 ← R1 → Swap R1 and R2 at the same time
• P: DR ← M[AR] → If P=1, load data from memory address AR into DR

Why we use RTL? It helps designers write the exact steps the hardware must do - very useful for drawing circuits later.

2.2 Register Transfer

Register Transfer means moving data from one register to another register inside the CPU. This is the most basic micro-operation. It always happens in one clock cycle.

How Register Transfer actually works
Source register puts its data on the bus
Destination register loads (accepts) that data

Common Register Transfers in Basic Computer:
• DR ← AC (Data Register gets value from Accumulator)
• AC ← DR (Accumulator gets value from Data Register)
• PC ← AR (Program Counter gets address from Address Register)
• AR ← PC (Address Register gets next instruction address)

Important Rule:
• Only one register can put data on the common bus at a time.
• Multiple registers can load data at the same time (using comma in RTL).

Easy way to remember: Think of registers as buckets. Register Transfer = pouring water from one bucket to another using a single pipe (the bus).

2.3 Bus and Memory Transfer

Bus Transfer = Moving data between registers using the common bus.  
Memory Transfer = Moving data between a register and the main memory (RAM).

Why Common Bus?
• Connecting every register to every other register directly = too many wires!
• So we use one shared 16-bit common bus (like a single highway).

How Bus Transfer works
• 3 select lines (S2 S1 S0) choose which register puts data on the bus.
• Every register has LD (Load) signal → to take data from the bus.

Memory Transfer (two types):

Read (Memory to Register)

RTL: DR ← M[AR]

Meaning: Put address in AR → Read memory → Load into DR

Write (Register to Memory)

RTL: M[AR] ← DR

Meaning: Put address in AR → Write data from DR into memory

Three-State Buffers (very important for bus):
• Normal gates cannot share a wire (they fight).
• Three-state buffers have 3 states: 0, 1, or High Impedance (Z) = disconnected.
• Only the selected register's buffer is enabled (E=1), others stay in Z state.

Easy example: To move data from AC to DR using bus:
Select AC (S2 S1 S0 = 100)
AC puts data on bus
DR gives LD=1 → DR loads the data

2.4 Three state bus buffers

Three-state bus buffers are special electronic gates that solve a big problem in the common bus system.

Problem with normal gates: If two registers try to put data on the same bus wire at the same time (one puts 0, another puts 1), it causes a short circuit → damage or wrong data.

Solution: Three-state buffer (also called Tri-state buffer). It has 3 possible output states instead of only 0 or 1.

| Enable (E) | Input | Output | Meaning |
| --- | --- | --- | --- |
| 0 | 0 or 1 | Z (High Impedance) | Like the wire is disconnected (floating) |
| 1 | 0 | 0 | Normal logic 0 |
| 1 | 1 | 1 | Normal logic 1 |

In the basic computer:
• Every register output is connected to the bus through its own three-state buffer.
• A decoder (usually 3×8 or 2×4) uses the 3 select lines S2 S1 S0 to send Enable=1 to only one buffer at a time.
• All other buffers stay in Z state → they do not affect the bus.

This way, only the selected register "drives" the bus. Others are safely disconnected.

Easy way to remember: Think of three-state buffers as "smart switches" on a single road (bus). Only one car (register) is allowed to enter the road at a time; others wait with their engine off (Z state).

2.5 Memory Transfer

Memory Transfer means moving data between the CPU registers and the main memory (RAM) using the common bus.

There are exactly two types:

| Type | RTL Notation | Simple Meaning | Direction |
| --- | --- | --- | --- |
| Memory Read | DR ← M[AR] | Copy data from memory location (given by AR) into Data Register | Memory → CPU |
| Memory Write | M[AR] ← DR | Copy data from Data Register into memory location (given by AR) | CPU → Memory |

How Memory Read works (step by step)
Address is already in AR
Memory unit gets "Read" signal
Memory puts the 16-bit data on the common bus
DR gives LD = 1 → DR loads the data from the bus

How Memory Write works (step by step)
Address is already in AR
DR puts its data on the common bus (select DR using S2 S1 S0)
Memory unit gets "Write" signal
Memory stores the data present on the bus at the address in AR

Summary of Register Transfer Microoperations

| Notation | Description |
| --- | --- |
| A ← B | Transfer content of reg. B into reg. A |
| AR ← DR(AD) | Transfer content of AD portion of reg. DR into reg. AR |
| A ← constant | Transfer a binary constant into reg. A |
| ABUS ← R1, R2 ← ABUS | Transfer content of R1 into bus A and, at the same time, transfer content of bus A into R2 |
| AR | Address register |
| DR | Data register |
| M[R] | Memory word specified by reg. R |
| M | Equivalent to M[AR] |
| DR ← M | Memory read operation: transfers content of memory word specified by AR into DR |
| M ← DR | Memory write operation: transfers content of DR into memory word specified by AR |

Important points:
• AR always holds the memory address (12 bits).
• DR is the data bridge between bus and memory.
• These transfers happen during the Execute phase of memory-reference instructions (LDA, STA, ADD, etc.).
• In the timing diagram, Read/Write signals are active only for one clock cycle.

Easy way to remember: Read = "Memory gives data to DR" (like taking a book from shelf). Write = "DR gives data to Memory" (like putting a book back on shelf).

2.6 Arithmetic Micro operations

Arithmetic Micro-operations are the mathematical operations performed by the ALU (Arithmetic Logic Unit) inside the CPU. These operations work on numbers stored in registers (usually AC and DR in the basic computer).

They are done in one clock cycle and always produce a result + a carry (in E flip-flop).

Most Important Arithmetic Micro-operations

| Micro-operation | RTL Notation | Simple Meaning | How it is done (in hardware) |
| --- | --- | --- | --- |
| Add | AC ← AC + DR | Add content of DR to AC | Normal addition |
| Subtract | AC ← AC + DR' + 1 | Subtract DR from AC (using 2's complement) | Invert DR + add 1 + add to AC |
| Increment | AC ← AC + 1 | Increase AC by 1 | Add 1 to AC |
| Decrement | AC ← AC - 1 | Decrease AC by 1 | Add all 1's (or special logic) |
| Transfer | AC ← DR or AC ← AC | Just copy value (no change) | No addition, direct transfer |

Arithmetic Circuit Function Table

| S1 | S0 | Cin | Y | Output | Microoperation |
| --- | --- | --- | --- | --- | --- |
| 0 | 0 | 0 | B | D = A + B | Add |
| 0 | 0 | 1 | B | D = A + B + 1 | Add with carry |
| 0 | 1 | 0 | B' | D = A + B' | Subtract with borrow |
| 0 | 1 | 1 | B' | D = A + B' + 1 | Subtract |
| 1 | 0 | 0 | 0 | D = A | Transfer A |
| 1 | 0 | 1 | 0 | D = A + 1 | Increment A |
| 1 | 1 | 0 | 1 | D = A - 1 | Decrement A |
| 1 | 1 | 1 | 1 | D = A | Transfer A |

Hardware used:
• A 4-bit (or 16-bit) binary adder-subtractor made of full-adders.
• 4×1 MUX selects what to add (B, B', 0, 1).
• One XOR gate before each full-adder flips bits when subtracting (M=1 for subtract).
• Carry-out goes to E flip-flop.

Easy way to remember: Arithmetic = "Math on numbers" → always uses the adder circuit. Subtract = Add the 2's complement (invert + add 1).

2.7 Logic Micro operations

Logic Micro-operations are bit-by-bit operations performed on the bits of two registers (AC and DR). These do not use the adder - they use simple logic gates (AND, OR, XOR, NOT).

They are very useful for masking, setting, clearing, or comparing bits.

Most Important Logic Micro-operations (used in Basic Computer)

| Micro-operation | RTL Notation | Simple Meaning (bit by bit) | Symbol used |
| --- | --- | --- | --- |
| AND | AC ← AC ∧ DR | Bitwise AND (1 only if both bits are 1) | ∧ |
| OR | AC ← AC ∨ DR | Bitwise OR (1 if any bit is 1) | ∨ |
| XOR | AC ← AC ⊕ DR | Bitwise Exclusive-OR (1 if bits are different) | ⊕ |
| Complement | AC ← AC' | Flip all bits of AC (0→1, 1→0) | ' |

Logic Circuit Function Table

| S1 | S0 | Output | Operation |
| --- | --- | --- | --- |
| 0 | 0 | E = A ∧ B | AND |
| 0 | 1 | E = A ∨ B | OR |
| 1 | 0 | E = A ⊕ B | XOR |
| 1 | 1 | E = A' | Complement |

Hardware used:
• A 4×1 MUX for each bit of the register.
• Inputs to MUX:
  1. AC AND DR
  2. AC OR DR
  3. AC XOR DR
  4. AC' (complement)
• Two select lines S1 S0 choose which logic operation to perform.

Easy way to remember: Logic = "Bitwise decisions" → no addition, just gates + MUX. AND = "Both must be true", OR = "Any one true", XOR = "Different", Complement = "Flip".

Unit-III
Micro programmed Control Unit & Central Processing Unit

3.1 Design of Control Unit  
3.2 Introduction to Central Processing Unit  
3.3 General Register Organization  
3.4 Stack Organization  
3.5 Register stack  
3.6 Memory stack  
3.7 Instruction Formats  
3.8 Addressing Modes

3.1 Design of Control Unit

The Control Unit (CU) is like the "traffic cop" of the CPU. It reads instructions, figures out what to do, and sends signals to other parts (like ALU or registers) to make everything happen in the right order. There are two main types of Control Unit designs: Hardwired (fixed like a machine) and Microprogrammed (flexible like software).

Types of Control Unit Designs

| Type | Simple Meaning | Pros & Cons (easy words) |
| --- | --- | --- |
| Hardwired | Built with fixed wires and logic gates (AND, OR, etc.). No changes possible. | Fast (direct signals), but rigid - hard to fix or add new instructions. |
| Microprogrammed | Uses a special ROM (Control Memory) to store tiny "micro-instructions" (like a mini-program). CU reads these step-by-step. | Flexible (easy to update ROM), but slightly slower (needs to fetch from memory). |

How Microprogrammed CU Works:
IR (Instruction Register) sends opcode to a decoder → picks starting address in Control Memory (ROM).
CAR (Control Address Register) loads that address → ROM outputs micro-instruction to CDR (Control Data Register).
CDR activates signals (e.g., "Load AC" or "Add").
CDR also has "next address" → CAR updates for the next step. Repeat until instruction ends.

Easy way to remember: Hardwired = "Baked-in recipe" (quick but unchangeable). Microprogrammed = "Editable cookbook" (slower fetch but fixable).

3.2 Introduction to Central Processing Unit

The Central Processing Unit (CPU) is the "heart and brain" of the computer. It's a small chip (like Intel Core i7) that runs programs by fetching instructions from memory, decoding them, and executing operations. In simple words: CPU takes your commands (like "add two numbers") and makes them happen super fast (billions of times per second).

Main Functions of CPU (must know these 4)
Fetch: Grabs next instruction from memory (using PC).
Decode: Understands what the instruction means (using CU).
Execute: Does the work (using ALU for math/logic).
Store: Saves results if needed (back to memory or registers).

Basic CPU Architecture (Block Diagram View)

CPU has 3 core parts connected by internal buses (address for locations, data for info, control for signals).

| Part | Simple Job | Key Components Inside |
| --- | --- | --- |
| ALU | Does math (add/subtract) and logic (AND/OR) | Adders, logic gates |
| Control Unit (CU) | Boss - decodes and sends signals | Decoder, sequencer, microprogram ROM (if microprogrammed) |
| Registers | Fast temporary storage (faster than RAM) | PC, IR, AC, etc. |

Clock Signal: Everything syncs to the CPU clock (e.g., 3 GHz = 3 billion ticks/second).

Easy way to remember: CPU = "Kitchen": CU = chef (plans), ALU = stove (cooks), Registers = counters (hold ingredients).

3.3 General Register Organization

General Register Organization is how the CPU arranges its "work registers" (small, fast storage inside CPU) for quick data handling. These are like "scratch pads" for temporary data during calculations. In basic CPUs, there are 8-16 general registers; modern ones have 32+. They connect via a common bus for easy transfers.

Types of Registers in Organization

| Type | Simple Meaning | Examples (in Basic Computer) |
| --- | --- | --- |
| General-Purpose Registers (GPRs) | Multi-use for data or addresses (most flexible) | AC (for results), R0-R7 (extra temps) |
| Dedicated Registers | Fixed job (not general) | PC (next instruction address), IR (current instruction) |
| Special-Purpose | For status or flags (like carry bit) | E (extend/carry flag), MAR (memory address) |

How Organization Works:
• Registers are grouped (e.g., 8 GPRs in a bank).
• Use MUX (multiplexer) to select which one connects to ALU/bus.
• Decoder lines (e.g., 3 lines for 8 registers) choose the right one.
• In "Register File" design: Dual-port (read/write two at once) for speed.

Easy way to remember: Registers = "Quick drawers in a desk". GPRs = any drawer for anything; organization = labels so you find fast.

3.4 Stack Organization

Stack Organization is a special way to store and manage data in the CPU or memory, following LIFO (Last In, First Out) rule — like a stack of books where you add or remove only from the top. It's great for handling function calls, saving addresses during jumps, or managing temporary data in programs.

Types of Stack Organization

| Type | Simple Meaning | Pros & Cons (easy words) |
| --- | --- | --- |
| Register Stack | Uses CPU registers as stack levels (fast but small) | Super quick access; limited to few items (e.g., 8-64 levels). |
| Memory Stack | Uses RAM locations as stack (slow but huge) | Holds thousands of items; slower due to memory access. |

How Stack Organization Works (Step-by-Step)
Initialize: Set Stack Pointer (SP) to top (e.g., empty stack starts at base address).
Push Operation: Add data to top → SP moves up/down (depending on growth direction).
Pop Operation: Remove from top → SP moves back.
Check Overflow/Underflow: Push on full stack or pop on empty = error.

Easy way to remember: Stack = "Plate dispenser" in a kitchen — grab the top plate (pop), add new on top (push). No middle access!

3.5 Register Stack

Register Stack is a compact stack made entirely of CPU registers (no memory involved). It's the fastest type, ideal for quick operations like arithmetic in the ALU. SP (Stack Pointer) is a special register that tracks the current top level. Size is fixed (e.g., 64 words or levels).

Working of Register Stack (Step-by-Step Example with 4 Levels)

Assume registers: R0 (bottom, empty), R1, R2, R3 (top possible). SP starts at 0.

| Step | Operation | SP Before | Action (RTL) | SP After | Stack Content (Top to Bottom) |
| --- | --- | --- | --- | --- | --- |
| 1 | Push 10 | 0 | SP ← SP + 1, R1 ← 10 | 1 | R1=10 (top) |
| 2 | Push 20 | 1 | SP ← SP + 1, R2 ← 20 | 2 | R2=20, R1=10 |
| 3 | Pop | 2 | Data ← R2, SP ← SP - 1 | 1 | R1=10 (new top) |
| 4 | Push 30 | 1 | SP ← SP + 1, R2 ← 30 | 2 | R2=30, R1=10 |

Full/Empty Flags: Hardware bits signal when SP hits max (full) or 0 (empty).

Easy way to remember: Register Stack = "Handheld card stack" — flip top card fast, but you can't hold too many.

3.6 Memory Stack

Memory Stack uses main memory (RAM) as the stack area, pointed by SP (which holds a memory address). It grows downward (high to low addresses) for efficiency. Used for large data like recursion or OS tasks. Slower than register stack but unlimited size.

Working of Memory Stack (Step-by-Step Example)

Assume stack starts at address 100 (top), grows down to 0. SP=100 (empty).

| Step | Operation | SP Before | Action (RTL) | SP After | Memory Content (Top Location) |
| --- | --- | --- | --- | --- | --- |
| 1 | Push 10 | 100 | SP ← SP - 1, M[99] ← 10 | 99 | M[99]=10 (top) |
| 2 | Push 20 | 99 | SP ← SP - 1, M[98] ← 20 | 98 | M[98]=20, M[99]=10 |
| 3 | Pop | 98 | Data ← M[98], SP ← SP + 1 | 99 | M[99]=10 (new top) |
| 4 | Push 30 | 99 | SP ← SP - 1, M[98] ← 30 | 98 | M[98]=30, M[99]=10 |

Integration with CPU: PC (instructions), AR (data access), SP (stack) all point to memory sections.

Easy way to remember: Memory Stack = "Warehouse shelf" — huge space, but you need a ladder (SP) to reach the top shelf.

3.7 Instruction Formats

Instruction Formats refer to the layout or structure of a machine instruction in binary bits (e.g., 16-bit or 32-bit word). It's like a "form" that packs the opcode (what to do) and operands (data or addresses needed). Different formats balance speed, complexity, and number of operands. In basic computers, formats vary by instruction type (e.g., memory-reference vs. register).

Types of Instruction Formats (Based on Number of Addresses/Operands)

| Type | Simple Meaning | Example (ADD Operation) | Pros & Cons (easy words) |
| --- | --- | --- | --- |
| Zero-Address | No explicit addresses; uses stack (push/pop implied) | PUSH A, PUSH B, ADD (pops two, pushes result) | Simple hardware; limited flexibility (stack only). |
| One-Address | One address (accumulator implied as source/dest) | ADD X (AC = AC + Memory[X]) | Compact; assumes one register (AC). |
| Two-Address | Two addresses (source and dest; one can be register) | ADD X, Y (X = X + Y) | Balanced; needs more bits. |
| Three-Address | Three addresses (dest, source1, source2) | ADD X, Y, Z (X = Y + Z) | Flexible; uses more bits/space. |

How Instruction Format Works (Step-by-Step in a 16-Bit Example)
Bits Allocation: Total 16 bits → e.g., 4-bit opcode + 12-bit address (for one-address).
Decode: CPU reads opcode first → decides format and action.
Execute: Fetches operands based on addresses → performs op.
Variations: Some bits for mode (direct/indirect) or flags.

Easy way to remember: Formats = "Recipe cards" — zero-address (just "mix top two"), three-address (full details: "put Y+Z in X"). More addresses = more flexible but longer instructions.

3.8 Addressing Modes

Addressing Modes are the ways the CPU finds the operand (data or address) in an instruction. Instead of hard-coding data, the instruction specifies "how to get it" (e.g., direct from memory or calculate via register). This makes programs efficient and flexible. Common in RISC/CISC architectures.

Types of Addressing Modes

| Type | Simple Meaning | Example (Load Instruction) | Pros & Cons (easy words) |
| --- | --- | --- | --- |
| Immediate | Data is in the instruction itself (no memory fetch) | LOAD #5 (load constant 5 directly) | Fast (no fetch); limited to small constants. |
| Direct | Address in instruction points straight to memory | LOAD 100 (load from memory[100]) | Simple; fixed addresses only. |
| Indirect | Address in instruction points to another address | LOAD @100 (load from memory[memory[100]]) | Flexible (pointers); extra fetch cycle. |
| Register | Operand in a CPU register (fastest) | LOAD R1 (load from register R1) | Super quick; no memory access. |
| Indexed | Address = base register + offset in instruction | LOAD R1 + 10 (load from memory[R1 + 10]) | Good for arrays/loops. |
| Relative/PC-Relative | Address = PC + offset (for branches/jumps) | JUMP +5 (jump to PC + 5 instructions) | Position-independent code. |

How Addressing Modes Work (Step-by-Step Example for Indexed Mode)
Instruction Fetch: Get opcode + register (R1) + offset (10).
Calculate Effective Address (EA): EA = R1 content + 10.
Fetch Operand: Go to memory[EA] → load data.
Execute: Use the data (e.g., add to AC).

Easy way to remember: Modes = "Treasure hunt clues" — immediate (treasure in hand), direct (go to map spot), indirect (spot leads to another spot). Choose mode to save time/space.

Unit-IV
Input Output Organization

4.1 Peripheral devices  
4.2 Input Output interface  
4.3 Modes of Data Transfer  
4.4 Priority Interrupt  
4.5 Direct Memory Access

4.1 Peripheral Devices

Peripheral devices (or I/O devices) are hardware components attached to the computer system to perform input (data to CPU), output (data from CPU), or secondary storage functions. They operate at much slower speeds than the CPU (e.g., CPU at GHz, keyboard at characters/sec), hence need special handling.

Classifications:

Peripherals are classified based on function, mode of I/O, data representation, and access method.

| Classification Basis | Types/Subtypes | Examples | Key Characteristics |
| --- | --- | --- | --- |
| By Function | Input | Keyboard, Mouse, Joystick, Scanner, Microphone | Human or machine input; unidirectional data flow to computer |
|  | Output | Monitor (CRT/LCD), Printer (Dot-matrix/Inkjet/Laser), Plotter, Speaker | Display/print results; unidirectional from computer |
|  | Storage | HDD, SSD, Floppy Disk, Magnetic Tape, Optical Disk (CD/DVD) | Bidirectional; persistent data storage |
| By Data Representation | Human-Readable | Printer, Monitor | ASCII/text for humans |
|  | Machine-Readable | Magnetic Disk/Tape, Paper Tape | Binary for machines |
| By Usage | Interactive | Keyboard, Mouse | Real-time user interaction |
|  | Batch | Tape Drives, Card Readers | Sequential processing |
| By Transfer Mode | Serial (bit-by-bit) | USB, RS-232 | Single wire pair; long distance |
|  | Parallel (byte/word) | Printer Port (Centronics), SCSI | Multiple wires; short distance, faster |
| By Synchronization | Synchronous | Disk Drives | Clock signal shared; fixed timing |
|  | Asynchronous | Keyboard, Mouse | Handshaking (start/stop bits); variable timing |

Interface Characteristics:
• Device Speed: Low (keyboard: 10-100 chars/sec), Medium (printer: 100-1000 pages/hr), High (disk: MB/sec).
• Unit of Transfer: Character (keyboard), Block (disk), Pixel (display).
• Data Representation: Binary, BCD, Gray Code.
• Access Method: Sequential (tape), Direct/Random (disk), Indexed (some disks).

Advantages:
• Extend computer capabilities (e.g., printing, storage).
• Modular - easy to upgrade.

Disadvantages:
• Speed mismatch causes bottlenecks.
• Need drivers/software for control.

Example: A hard disk as storage peripheral – transfers data in blocks (512 bytes/sector) via parallel interface (SATA/AHCI).

Concept Summary: Peripherals are "arms and eyes" of the computer; their diversity requires flexible I/O organization.

4.2 Input-Output Interface

The I/O Interface (or I/O Module/Controller) is the hardware circuitry that connects slow peripherals to the fast CPU/bus. It isolates the CPU from device details, handling synchronization, buffering, and protocol conversion.

Key Components:

| Component | Description | Function |
| --- | --- | --- |
| I/O Ports | Addressable registers (8/16/32-bit) | Entry/exit points; e.g., Port 0x3F8 for COM1 |
| Data Register (DR) | Holds actual data byte/word | Buffer for transfer |
| Status Register (SR) | Bits for flags (e.g., R/W, Ready, Error) | CPU polls/checks status |
| Control Register (CR) | Configures mode (e.g., enable interrupt) | Mode selection |
| Latches/Buffers | Temporary storage | Match speeds |
| Address Decoder | Selects specific device/port | From bus address lines |
| Handshaking Logic | READY/ACK signals | Asynchronous sync |
| DMA/Interrupt Logic | For advanced modes | Offloads CPU |

Types of I/O Addressing:

Isolated I/O (I/O Mapped):
• Separate address space (e.g., IN/OUT instructions).
• Ports: 0 to 64K-1.
• Adv: No confusion with memory.
• Disadvantage: Extra instructions (IN/OUT vs LOAD/STORE).

Memory Mapped I/O:
• Peripherals share memory address space.
• Use LOAD/STORE instructions.
• Adv: Simpler, flexible (e.g., x86).
• Disadvantage: Reduces available memory addresses.

Functions in Detail:
Interface Electronics: Voltage level matching (TTL to RS-232).
Buffering: FIFO queues for speed mismatch.
Signal Conditioning: Noise filtering, encoding (parallel to serial).
Device Selection: Chip select lines.
Data Transfer Synchronization: Polling, interrupts, DMA.
Error Handling: Parity, CRC checks.

Working Example (Keyboard Interface):
• CPU writes "enable" to CR.
• Keyboard sends char → DR fills, SR sets "ready".
• CPU reads SR, then DR.

Advantages:
• CPU independence from device specifics.
• Standardized communication.

Disadvantages:
• Additional cost/hardware.

Concept Summary: I/O Interface is the "middleman" ensuring smooth, error-free communication.

4.3 Modes of Data Transfer

Data transfer modes define how data moves from/to peripherals. CPU involvement reduces progressively for efficiency. Three modes: Programmed I/O, Interrupt-Initiated I/O, DMA.

Programmed I/O (PIO)
• Detail: CPU fully controls; actively polls (checks) device status in a loop.
• Types:

| Subtype | Polling Type | Efficiency |
| --- | --- | --- |
| Non-Blocking | Continuous loop | Very low (CPU 100% busy) |
| Blocking | Wait on status | Low |

• Steps:
  1. CPU issues command to CR.
  2. Loop: Poll SR until "ready".
  3. Read/Write DR.
  4. Verify.

• Assembly Example (8085-like):

`assembly
MVI A, CMD      ; Load command
OUT PORTCR     ; Send to control
LOOP: IN PORTSR
ANI 01H         ; Check ready bit
JZ LOOP         ; Poll if not
IN PORTDR      ; Get data
`

• Adv: Simple, no extra hardware.
• Disadv: CPU wasted (95% idle time); only 1 device.

Interrupt-Driven I/O
• Detail: Device interrupts CPU when ready (via INTR line). CPU saves context, services via ISR.
• Steps:
  1. CPU enables interrupt, starts I/O.
  2. Device finishes → Sends interrupt.
  3. CPU acknowledges (INTA), gets vector if vectored.
  4. ISR: Transfer data, restore CPU.
• Hardware: Interrupt Controller (e.g., 8259 PIC).
• Adv: CPU multitasking; efficient for sporadic devices.
• Disadv: ISR overhead; interrupt latency.

Direct Memory Access (DMA)
• DMAC takes bus control; direct memory-peripheral transfer.

Comparison Table:

| Parameter | Programmed I/O | Interrupt-Driven | DMA |
| --- | --- | --- | --- |
| CPU Involvement | High (polling) | Medium (ISR) | Low (setup only) |
| Hardware Needed | Minimal | Interrupt Controller | DMAC |
| Efficiency | Poor (CPU busy-wait) | Good | Excellent (bulk data) |
| Devices Suited | Slow/low-volume | Interactive (mouse) | High-speed (disk) |
| Overhead | 100% CPU time | Context switch | Bus arbitration |

Concept Summary: Choose mode by device speed/volume – PIO for simple, Interrupt for responsive, DMA for heavy loads.

4.4 Priority Interrupt

Priority Interrupt is a mechanism to handle multiple interrupts from devices simultaneously. Not all can be serviced at once, so priorities decide the order (highest first). Used when CPU is busy but devices need urgent service. Handled by Interrupt Controller (e.g., 8259A PIC in x86).

Classifications of Priority Interrupt Schemes:

| Scheme | Description | Hardware Requirement | Speed | Scalability |
| --- | --- | --- | --- | --- |
| Parallel Priority | Each device has independent request (IR0-IR7) and acknowledge lines. Highest active bit wins. | Many wires (one per device) | Very Fast | Poor (fixed lines) |
| Daisy Chaining | Devices chained serially. Interrupt passes through chain; first enabled device grabs it. | Single request/ack line + chain | Medium | Good (expandable) |
| Matrix | Combines parallel + daisy; fixed priorities via matrix decoder. | Moderate | Fast | Medium |
| Serial | Time-sharing; devices poll in sequence. | Low | Slow | Good |

Types of Interrupts:
• Hardware (devices), Software (traps), Exception (errors).
• Vectored (device supplies ISR address), Non-Vectored (fixed ISR).

Working of Daisy Chaining (Most Common):
Device raises INTR (shared line).
CPU checks if interrupts enabled (IF flag).
CPU sends INTA pulses:
   - 1st INTA: Enables chain.
   - 2nd INTA: Device puts vector on bus.
ISR executed; low priority waits.

Priority Assignment: Fixed (IR0 highest) or Programmable (8259 allows rotation).

Assembly Example (8085/8086):

`assembly
; ISR Entry (Hardware pushes PC)
POP H           ; Save return
PUSH PSW        ; Save flags
; Handle device
POP PSW
POP H
EI              ; Re-enable interrupts
RET             ; Return
`

8259A PIC Features:
• 8 interrupt levels; cascadable to 64.
• Modes: Edge/Level triggered, Auto/manual EOI.

Advantages:
• Efficient multi-device handling.
• Prevents low-priority blocking high (e.g., emergency vs mouse).

Disadvantages:
• Daisy chain delay (propagation).
• Fixed priorities inflexible.

Concept Summary: Priority ensures critical devices (e.g., disk error > keyboard) get serviced first; daisy chaining is cost-effective for 4-8 devices.

4.5 Direct Memory Access (DMA)

DMA enables high-speed peripherals (e.g., disks, networks) to transfer large data blocks directly to/from memory, bypassing CPU. DMA Controller (DMAC) (e.g., 8237 in x86) arbitrates bus access. Ideal for bulk transfers where CPU polling/interrupts are inefficient.

Classifications/Types of DMA:

| Type/Mode | Description | CPU Status During Transfer | Use Case |
| --- | --- | --- | --- |
| Burst Mode | DMAC takes full bus control; transfers entire block continuously. | Halted | High-speed, infrequent |
| Cycle Stealing | DMAC steals one bus cycle between CPU cycles (transparent to CPU). | Runs normally | Continuous low-volume |
| Block/Transparent | Full block, but CPU can run if priority given. | Partially active | Balanced |
| Single/Multiple | Single: One word/transfer; Multiple: Block. | Varies | Flexible |

Additional Features:
• Channels: 4-8 independent (e.g., one for HDD, one for FDD).
• Transfer Directions: Memory-to-Device, Device-to-Memory, Memory-to-Memory.
• Addressing: Fixed (one address), Incrementing, Flying (current address).

Detailed Working (Cycle Stealing Example):

Initialization (CPU):
• Write to DMAC registers: Start Addr, Count, Mode (e.g., channel 0).
• Assert HRQ (Hold Request).

Bus Acquisition:
• CPU grants HLDA (Hold Acknowledge); tri-states its lines.

Transfer:
• DMAC asserts MEMR/MEMW or IOR/IOW.
• Data flows directly (Device ↔ Memory).
• Auto-increment address/decrement count.

Completion:
• Count=0 → Interrupt to CPU.
• CPU regains bus.

8237 DMAC Registers:

| Register | Purpose |
| --- | --- |
| Mode | Transfer type/mode |
| Address | Starting memory/port addr |
| Count | Bytes to transfer (16-bit) |

Pseudocode Example:

`
DMACWRITE(MODEREG, AUTOINC | DEVICETOMEM);
DMACWRITE(ADDRREG, 0x1000);
DMACWRITE(COUNTREG, 1024);
CPUHRQ();          // Request bus
// DMAC transfers 1024 bytes from device to 0x1000
DMACINT();         // Signals done
`

Advantages:
• CPU 100% free (up to 80% speedup for I/O).
• High throughput (e.g., 100 MB/s disks).

Disadvantages:
• Expensive hardware.
• Bus contention (CPU waits).
• Complex arbitration.

Concept Summary: DMA is "CPU vacation mode" for I/O; essential for modern systems with gigabytes of data movement.

Unit-V
Memory Organization

5.1 Memory Hierarchy  
5.2 Main Memory  
5.3 Auxiliary Memory  
5.4 Associative Memory  
5.5 Cache Memory  
5.6 Virtual Memory

5.1 Memory Hierarchy

Memory hierarchy is a crucial concept in computer architecture, designed to optimize the performance and efficiency of memory usage. It categorizes different types of memory based on three primary criteria: speed, cost, and capacity.

Key Concepts
Speed: Memory types closer to the CPU are typically faster, facilitating quicker data access.
Cost: Faster memory is generally more expensive per unit of storage.
Capacity: Slower memory types can store larger amounts of data.

Levels of Memory Hierarchy

The memory hierarchy can be visualized as a pyramid, with the fastest and most expensive memory at the top and the slowest and cheapest at the bottom.

| Level | Type | Speed | Size | Cost |
| --- | --- | --- | --- | --- |
| Level 1 | Registers | Very Fast | Very Small | Very Expensive |
| Level 2 | Cache Memory | Fast | Small | Moderately Expensive |
| Level 3 | Main Memory | Moderate | Medium | Moderate |
| Level 4 | Auxiliary Memory | Slow | Large | Cheap |

Detailed Explanation of Each Level

Level 1: Registers
• Description: Small storage locations within the CPU.
• Speed: Access time is in the range of nanoseconds.
• Use: Store immediate values needed for calculations.

Level 2: Cache Memory
• Description: A smaller, faster type of volatile memory located close to the CPU.
• Speed: Faster than main memory, with access times in nanoseconds.
• Use: Temporarily stores frequently accessed data and instructions to speed up processing.

Level 3: Main Memory (RAM)
• Description: Primary working memory of the computer.
• Speed: Slower than cache, typically in nanoseconds to microseconds.
• Use: Stores data and programs currently in use.

Level 4: Auxiliary Memory
• Description: Non-volatile storage that retains data when powered off.
• Speed: Slower, with access times in milliseconds.
• Use: Long-term storage for data, applications, and the operating system.

Importance of Memory Hierarchy
• Performance Optimization: By utilizing a hierarchy, the system can provide fast access to frequently used data while maintaining a larger pool of slower storage.
• Cost Efficiency: It balances the cost of high-speed memory with the need for larger storage capacity.
• Data Management: Efficiently manages how data is stored, accessed, and retrieved.

5.2 Main Memory

Main memory, often referred to as RAM (Random Access Memory), plays a critical role in a computer's performance. It is the primary storage area that the CPU accesses to read and write data during operation.

Key Characteristics
Volatile: Data is lost when the power is turned off.
Directly Accessible: The CPU can access data directly without any intermediary steps.
Types: Common types include:
   - DRAM (Dynamic RAM): Requires periodic refreshing to maintain data.
   - SRAM (Static RAM): Faster and does not require refreshing, but is more expensive.

Functions of Main Memory
• Stores Data: Holds data that the CPU is currently processing.
• Holds Instructions: Keeps the instructions for programs that are currently running.
• Temporary Storage: Acts as a buffer for data being processed by the CPU.

Structure of Main Memory
• Memory Cells: Each cell can store a binary value (0 or 1).
• Addressing: Each memory location has a unique address, allowing the CPU to access specific data quickly.

Performance Factors
• Capacity: Typically measured in gigabytes (GB).
• Speed: Measured in nanoseconds; faster speeds reduce the time the CPU waits for data.

| Feature | Description |
| --- | --- |
| Capacity | Typically 4GB to 64GB in modern systems. |
| Speed | Access time ranges from 10ns to 100ns. |
| Power Consumption | Generally consumes more power when active. |

5.3 Auxiliary Memory

Auxiliary memory, also known as secondary storage, is a crucial component of a computer's memory organization. It is used for long-term data retention and provides a larger storage capacity compared to main memory (RAM).

Key Characteristics
Non-volatile: Data remains intact even when the power is turned off.
Higher Capacity: Typically offers much more storage space compared to main memory.
Slower Access Speed: Access times are generally longer than those for main memory.

Types of Auxiliary Memory

Hard Disk Drives (HDD)
• Description: Magnetic storage device, widely used for general storage.
• Speed: Slower access times (typically in milliseconds).
• Capacity: Ranges from hundreds of GB to several TB.

Solid State Drives (SSD)
• Description: Uses flash memory to provide faster data access.
• Speed: Much faster than HDDs, with access times often below 1 millisecond.
• Capacity: Ranges from hundreds of GB to several TB.

Optical Discs
• Description: Includes CDs, DVDs, and Blu-rays, used primarily for media storage.
• Speed: Slower compared to HDDs and SSDs.
• Capacity: Varies from 700 MB for CDs to 100 GB for Blu-rays.

Flash Drives
• Description: Portable storage devices used for data transfer.
• Speed: Comparable to SSDs, but can vary widely by brand.
• Capacity: Ranges from a few GB to several TB.

Functions of Auxiliary Memory
• Long-term Data Storage: Provides a place to store operating systems, applications, and user data.
• Backup: Often used for backing up important files to prevent data loss.
• Data Transfer: Facilitates data transfer between different systems.

Performance Factors
• Access Speed: Measured in milliseconds for HDDs and microseconds for SSDs.
• Durability: SSDs are generally more durable than HDDs since they have no moving parts.

| Feature | Hard Disk Drive (HDD) | Solid State Drive (SSD) | Optical Discs | Flash Drives |
| --- | --- | --- | --- | --- |
| Capacity | Up to several TB | Up to several TB | Varies (700MB - 100GB) | Up to several TB |
| Access Speed | 10-20 ms | <1 ms | 100-300 ms | <1 ms |
| Durability | Moderate | High | Moderate | High |
| Cost per GB | Low | Moderate to High | Very Low | Moderate |

5.4 Associative Memory

Associative memory, also known as content-addressable memory (CAM), is a type of memory that allows data retrieval based on content rather than specific addresses. This unique feature makes it particularly useful for applications where quick data access is critical.

Key Characteristics
Content Addressability: Allows search and retrieval of data by content, not by address.
Parallel Search: Capable of searching multiple memory locations simultaneously, leading to faster access.
Volatile: Typically, associative memory is volatile, meaning it loses its contents when power is turned off.

How Associative Memory Works
• Data Storage: Data is stored in a way that each entry can be accessed by its content.
• Search Mechanism: When a search query is made, the memory compares the input against all stored entries in parallel, returning matches quickly.

Hardware organization of associative memory:
• Argument register (A): Holds the search key.
• Key Register (K): Specifies which bits to compare.
• Associative memory array logic: Performs parallel comparison.
• Match Register (M): Indicates which entries matched.

Applications of Associative Memory
• Cache Memory: Used in CPU caches to quickly locate data.
• Database Management: Facilitates fast data retrieval in databases.
• Networking: Used in routers for packet forwarding based on content.

Advantages and Disadvantages

| Feature | Advantages | Disadvantages |
| --- | --- | --- |
| Speed | Extremely fast data retrieval | More complex design compared to RAM |
| Efficiency | Reduces the time for search operations | Generally more expensive per bit |
| Flexibility | Allows for dynamic data lookup | Limited capacity compared to traditional RAM |

5.5 Cache Memory

Cache memory is a small-sized type of volatile computer memory that provides high-speed access to frequently accessed data and instructions. It acts as a buffer between the CPU and main memory, optimizing performance by reducing data access times.

Key Characteristics
Speed: Cache memory is significantly faster than main memory (RAM).
Volatile: Data is lost when power is turned off.
Limited Size: Typically smaller in capacity compared to main memory.

Levels of Cache Memory

Cache memory is usually organized into different levels, primarily:

L1 Cache:
• Location: Integrated directly into the CPU.
• Size: Usually between 16KB to 128KB.
• Speed: Fastest access time (1-2 cycles).

L2 Cache:
• Location: Can be on-chip or on a separate chip close to the CPU.
• Size: Typically 256KB to 8MB.
• Speed: Slower than L1 but faster than main memory (3-10 cycles).

L3 Cache:
• Location: Shared among multiple cores in multi-core processors.
• Size: Can range from 2MB to 20MB.
• Speed: Slower than L1 and L2 but faster than main memory.

Functions of Cache Memory
• Data Storage: Temporarily holds frequently accessed data and instructions.
• Speed Enhancement: Reduces latency by providing faster access to data compared to main memory.
• Prefetching: Anticipates the data needed based on the CPU's processing patterns.

Cache Memory Operation
Cache Hit: When the CPU finds the requested data in the cache, resulting in a fast data retrieval.
Cache Miss: When the data is not found in the cache, requiring a fetch from main memory, which is slower.

Advantages and Disadvantages

| Feature | Advantages | Disadvantages |
| --- | --- | --- |
| Performance | Significantly improves CPU performance | Higher cost per bit compared to RAM |
| Efficiency | Reduces access time for data | Limited storage capacity |
| Power Consumption | Consumes less power than accessing main memory | Complexity in cache management |

5.6 Virtual Memory

Virtual memory is a memory management capability of an operating system (OS) that uses hardware and software to allow a computer to compensate for physical memory shortages by temporarily transferring data from random access memory (RAM) to disk storage. This technique enables systems to run larger applications with less physical memory and enhances multitasking capabilities.

Key Concepts of Virtual Memory

Abstraction of Memory:
• Virtual memory provides an abstraction of the physical memory, allowing applications to use more memory than what is physically available. Each process operates in its own virtual address space.

Paging:
• Memory is divided into fixed-size units called pages (typically 4KB). The physical memory is divided into page frames of the same size. When a program accesses a page not currently in memory, a page fault occurs, prompting the OS to load the required page from secondary storage.

Page Table:
• Each process has a page table that maps virtual addresses to physical addresses. The page table contains entries for each page, indicating whether it is in physical memory and its corresponding frame number.

Swapping:
• When physical memory is full, the OS may choose to swap out pages that are not currently being used to disk (swap space or page file). This process allows more processes to run simultaneously but can introduce latency due to disk I/O.

Benefits of Virtual Memory
• Increased Memory Capacity: Allows systems to run applications that require more memory than physically available.
• Isolation and Security: Each process operates in its own address space, reducing the risk of one process affecting another.
• Efficient Memory Usage: Pages that are not frequently accessed can be swapped out, keeping the most active data in RAM.

Drawbacks of Virtual Memory
• Performance Overhead: Accessing data from disk is significantly slower than accessing RAM, which can lead to performance issues if excessive paging (thrashing) occurs.
• Complexity: The management of virtual memory requires sophisticated algorithms to track pages, page tables, and swapping.

Summary Table

| Feature | Description |
| --- | --- |
| Abstraction | Allows applications to use more memory than physically available. |
| Paging | Memory management technique that divides memory into pages. |
| Page Table | Maps virtual addresses to physical addresses for each process. |
| Swapping | Moves pages between RAM and disk to free up memory. |
| Benefits | Increases capacity, provides isolation, and optimizes usage. |
| Drawbacks | Performance overhead due to disk access and added complexity. |

Happy Learning

Love from Aakash
``
