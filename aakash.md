## Computer Architecture

##### **Aakash**


##### **Computer Architecture**

**Syllabus**


**Unit-I: Basic Computer Organization and Design**


1.1 Instruction Codes


1.2 Computer Registers


1.3 Common bus system


1.4 Computer Instructions


1.5 Instruction formats


1.6 Instruction Cycle


1.7 Fetch and Decode


1.8 Flowchart for Instruction cycle


1.9 Register reference instructions


**Unit-II: Register Transfer and Micro-operation**


2.1 Register Transfer Language


2.2 Register Transfer


2.3 Bus and Memory Transfer


2.4 Three state bus buffers


2.5 Memory Transfer


2.6 Arithmetic Micro operations


2.7 Logic Micro operations


**Computer Architecture** **AAKASH**
### **2**


**Unit-III: Micro programmed Control Unit & Central Processing Unit**


3.1 Design of Control Unit


3.2 Introduction to Central Processing Unit


.3 General Register Organization


3.4 Stack Organization


3.5 Register stack


3.6 Memory stack


3.7 Instruction Formats


3.8 Addressing Modes


**Unit-IV: Input Output Organization**


4.1 Peripheral devices


4.2 Input Output interface


4.3 Modes of Data Transfer


4.4 Priority Interrupt


4.5 Direct Memory Access


**Unit-V: Memory Organization**


5.1 Memory Hierarchy


5.2 Main Memory


5.3 Auxiliary Memory


5.4 Associative Memory


5.5 Cache Memory


5.6 Virtual Memory


**Computer Architecture** **AAKASH**
### **3**


#### **Unit-I** **Basic Computer Organization and Design**

1.1 Instruction Codes


1.2 Computer Registers


1.3 Common bus system


1.4 Computer Instructions


1.5 Instruction formats


1.6 Instruction Cycle


1.7 Fetch and Decode


1.8 Flowchart for Instruction cycle


1.9 Register reference instructions


[Aakash](https://github.com/aakashsinghrajawat75)


**Computer Architecture** **AAKASH**
### **4**


**1.1 Instruction Codes**


An **instruction code** is the “command” given to the computer in binary form (only 0s and

1s). It tells the CPU exactly **what to do** (like add, load, store, jump, etc.).


**How an Instruction Code looks**


In the basic computer (the one you are studying), one instruction is **16 bits** long.


It is divided into 3 parts:
















|Part Number of What it does Example<br>Bits|Col2|Col3|Col4|
|---|---|---|---|
|**I (Indirect bit)**|1 bit (bit 15)|Tells whether address is<br>direct or indirect|0 = direct, 1 = indirect|
|**Opcode**<br>**(Operation Code)**|3 bits (bits<br>14-12)|Tells WHAT operation to<br>perform (ADD, LOAD, etc.)|000 = AND, 001 = ADD,<br>etc.|
|**Address (or**<br>**Operand)**|12 bits (bits<br>11-0)|Tells WHERE the data is<br>(memory location)|000000001010 =<br>memory address 10|



**Simple example** : Suppose the instruction code is: 0 001 000000001010 → I=0 (direct),

Opcode=001 (ADD), Address=10 Meaning: “Add the number present at memory location 10 to

the accumulator.”


**Computer Architecture** **AAKASH**
### **5**


**Types of Instructions (based on opcode)**


1. **Memory-Reference Instructions**   - Work with memory (ADD, LDA, STA, etc.)


2. **Register-Reference Instructions**   - Work only inside CPU registers (CLA, CLE, INC,

etc.)


3. **Input/Output Instructions**   - For taking input or giving output (INP, OUT)


**1.2 Computer Registers**


Registers are **super-fast, small storage places inside the CPU** . They are much faster than

main memory (RAM). The CPU uses them to hold data, addresses, and instructions while

working.











|Register Size Full Name Simple Function (in easy words)|Col2|Col3|Col4|
|---|---|---|---|
|**AC**|16<br>bits|Accumulator|Main working register. All calculations (add, subtract)<br>happen here.|
|**DR**|16<br>bits|Data Register|Temporary storage for data coming from or going to<br>memory.|
|**PC**|12<br>bits|Program Counter|Holds the address of the**next** instruction to be<br>executed.|
|**AR**|12<br>bits|Address Register|Holds the memory address when we want to read or<br>write.|
|**IR**|16<br>bits|Instruction<br>Register|Holds the current instruction that is being executed.|
|**TR**|16<br>bits|Temporary<br>Register|Extra temporary storage.|
|**INPR**|8 bits|Input Register|Holds data coming from keyboard/input device.|
|**OUTR**|8 bits|Output Register|Holds data to be sent to screen/printer.|


**Computer Architecture** **AAKASH**
### **6**


**Easy way to remember** : Think of registers as the **CPU’s pockets** . AC is the biggest pocket

where most work happens. PC is like a bookmark that says “next page to read”.


**1.3 Common Bus System**


If we connect every register to every other register with separate wires, we need **hundreds**

**of wires** → very costly and messy.


So, we use a **Common Bus** - like a **single shared road** (highway) inside the CPU.


  - Only **one register** can put data on the bus at a time.


  - Other registers can take (read) that data when needed.


**How it works (very simple)**


  - There is a **16-bit common bus** .


**Computer Architecture** **AAKASH**
### **7**


  - Each register has:


`o` **LD** (Load) → to

take data FROM

the bus


`o` **INR** (Increment)

→ to increase

value by 1


`o` **CLR** (Clear) → to

make it zero


  - Three select lines **S2, S1, S0** decide **which register** will put its data on the bus (like

choosing which car enters the highway).


**Computer Architecture** **AAKASH**
### **8**


**Example** : If we want to move data from DR to AC:


1. DR puts data on the bus (S2 S1 S0 select DR).


2. AC gives LD=1 → AC loads the data from the bus.


This common bus system saves a lot of wires and makes the design simple and clean.


**Bus Types**


**Bus Types** are the **shared pathways (wires)** that connect the CPU to memory,

input/output devices, and other parts of the computer. They carry information in parallel

(multiple bits at once) like a multi-lane highway. There are **three main types**, and together

they form the **system bus** . Buses are bidirectional where needed and synced by the clock

signal to avoid chaos.


**Types of Bus Types**














|Bus Simple Meaning Width (Bits) Direction What It<br>Type Example (Unidirectional/ Carries<br>Bidirectional)|Col2|Col3|Col4|Col5|
|---|---|---|---|---|
|**Address**<br>**Bus**|Specifies**locations** <br>(like house numbers)<br>for where to<br>read/write data.|32-bit (accesses 4GB<br>addresses)|Unidirectional<br>(CPU → devices)|"Go to<br>memory<br>spot 100"|
|**Data**<br>**Bus**|Transfers**actual**<br>**information** <br>(numbers,<br>instructions)<br>between parts.|64-bit (handles big<br>data fast)|Bidirectional (both<br>ways)|"Send the<br>number 50<br>here"|
|**Control**<br>**Bus**|Sends**commands**<br>**and status signals** <br>(like traffic lights) to<br>manage operations.|8-16 lines<br>(signals/flags)|Bidirectional<br>(commands/status<br>both ways)|"Read now"<br>or<br>"Interrupt!"|



**Computer Architecture** **AAKASH**
### **9**


**Easy way to remember** : Buses = "Mail system" — Address Bus = envelope address, Data

Bus = letter inside, Control Bus = stamps/instructions. Without them, CPU can't "talk" to RAM

or keyboard!


**How Buses Work (Step-by-Step)**


Buses operate in **cycles** (e.g., one clock tick = one transfer). They use **buffers/drivers** to

boost signals over long distances and **arbitration** (priority system) if multiple devices

compete. Here's a **memory read cycle** example (CPU fetching data from RAM at address

100):


1. **Prepare Address** : CPU loads address 100 into its Address Register (AR).


2. **Address Bus Transmits** : Address 100 (in binary, e.g., 00000000000001100100) is

placed on Address Bus → RAM decodes it and selects the right spot.


3. **Control Bus Commands** : Control Bus sends "Read Enable" signal (high voltage = 1)

→ RAM knows to output data; "Write Disable" is low (0).


**Computer Architecture** **AAKASH**
### **10**


4. **Data Bus Fetches** : RAM puts data (e.g., instruction "ADD 5") on Data Bus → CPU's

Data Register (DR) loads it.


5. **Control Bus Confirms** : Control Bus sends "Ready" status back → Cycle ends; buses

clear for next use (e.g., write cycle reverses data flow).


This takes **1-3 clock cycles** . In modern systems (e.g., PCIe bus), buses can be serial (faster,

point-to-point) instead of parallel.


**Easy way to remember** : How buses work = "Delivery process" — Step 1: Check address

(postcode), Step 2: Send command (open mailbox), Step 3: Grab package (data), Step 4:

Confirm receipt. Clocks keep it rhythmic!


**1.4 Computer Instructions**


These are the **actual commands** that the CPU can understand and run. In the Basic

Computer (the one in your syllabus), every instruction is 16 bits long, and they are divided into

**3 clear types** :


**Computer Architecture** **AAKASH**
### **11**


|Type How to identify What it does (simple Number of<br>it words) instructions|Col2|Col3|Col4|
|---|---|---|---|
|**Memory**<br>**Reference**|Opcode = 000 to<br>110 (bits 14-12)|Works with memory (read<br>data, add, store, jump etc.)|7|
|**Register**<br>**Reference**|Opcode = 111 and<br>I = 0|Works only inside CPU<br>registers (clear AC, increment,<br>etc.)|12|
|**Input/Output**|Opcode = 111 and<br>I = 1|Takes input from keyboard or<br>sends output to screen|6|



**Most important - Memory Reference Instructions (you must remember these 7)**

|Symbol Name Simple Meaning|Col2|Col3|
|---|---|---|
|**AND**|Logical AND|AC = AC AND Memory[AR]|
|**ADD**|Add|AC = AC + Memory[AR]|
|**LDA**|Load to AC|AC = Memory[AR]|



**Computer Architecture** **AAKASH**
### **12**


|STA|Store AC|Memory[AR] = AC|
|---|---|---|
|**BUN**|Branch Unconditional|Jump to address AR (PC = AR)|
|**BSA**|Branch and Save Return|Save current PC and jump (subroutine call)|
|**ISZ**|Increment and Skip if Zero|Memory[AR]++, if result=0 then skip next instruction|


**Easy way to remember** : Memory Reference → talks to RAM Register Reference → only

inside CPU (no memory) I/O → keyboard or monitor


**1.5 Instruction Formats**


This is the **structure** (layout) of the 16-bit instruction.


**Main Format (used by Memory Reference Instructions)**


Bit: 15 14 13 12  11 10 9 8 7 6 5 4 3 2 1 0


I   Opcode   Address (12 bits)


  - **I (Indirect bit)** : 0 = Direct address, 1 = Indirect address


**Computer Architecture** **AAKASH**
### **13**


  - **Opcode (3 bits)** : Tells WHAT to do (000=AND, 001=ADD, … 110=ISZ, 111=special)


  - **Address (12 bits)** : Memory location (0 to 4095)


PPT - CS/IT 12 COMPUTER ORGANIZATION &amp; ARCHITECTURE PowerPoint Presentation 
ID:6126740


**Special Formats when Opcode = 111**


1. **Register Reference Format** (I=0)


text


1 1 1 0  12-bit code (each bit does one micro-operation)


Example: 1110 0000 0000 0001 → CLA (Clear Accumulator)


**Computer Architecture** **AAKASH**
### **14**


2. **Input/Output Format** (I=1)


text


1 1 1 1  12-bit code for I/O operation


Example: 1111 0000 0000 0001 → INP (Input data)


**Why different formats?** Because when Opcode=111, the 12 address bits are not used as

address - they are used as operation codes instead.


**1.6 Instruction Cycle**


This is the **complete process** the CPU follows to execute **one single instruction** . It repeats

again and again until the program finishes.


**4 main steps** (very easy to remember):


1. **Fetch** → Bring the instruction from memory into CPU


2. **Decode** → Understand what the instruction says


3. **Execute** → Actually do the work (add, load, jump etc.)


4. **Store** (sometimes) → Save the result back if needed


**Computer Architecture** **AAKASH**
### **15**


**In your Basic Computer (with timing):**


  - The whole cycle uses **timing signals** T0, T1, T2, … T6


  - Fetch usually takes T0 + T1


  - Decode at T2


  - Execute from T3 onwards


  - If indirect addressing is used → one extra step (Indirect cycle)


**Computer Architecture** **AAKASH**
### **16**


**Simple Flow (like a cycle):**


Start


↓


Fetch instruction (PC → AR → IR, PC++)


↓


Decode the opcode


↓


If Memory Reference → check I bit → Indirect? → Execute


If Register or I/O → Execute directly


↓


Go to next instruction (repeat)


This cycle runs millions of times per second!


**1.7 Fetch and Decode**


These are the **first two steps** of the Instruction Cycle. The CPU does them **automatically**

for every instruction using **timing signals** (T0, T1, T2, …). SC (Sequence Counter) starts at 0

and increases with every clock pulse.


**Step-by-Step (very simple):**







|Timing What happens (Micro- Simple Meaning<br>operations)|Col2|Col3|
|---|---|---|
|**T0**|AR ← PC|Put the address of next instruction into Address<br>Register (like opening the correct page in a book)|


**Computer Architecture** **AAKASH**
### **17**


|T1|IR ← M[AR], PC ← PC + 1|Bring the instruction from memory into<br>Instruction Register + increase PC so it points to<br>the next instruction|
|---|---|---|
|**T2**|Decode the opcode (bits 14-12<br>of IR) + check I bit (bit 15)|Understand WHAT the instruction is (ADD? LDA?<br>CLA?) and whether it is direct or indirect|



After T2, the control unit knows exactly which instruction to execute.


**1.8 Flowchart for Instruction Cycle**


This is the **complete road map** the CPU follows for every instruction. It is drawn using the

timing signals T0 to T6 and SC (Sequence Counter).


**Main Flowchart (in simple steps):**


1. Start → SC ← 0


2. T0: AR ← PC


3. T1: IR ← M[AR], PC ← PC + 1


4. T2: Decode opcode in IR


**Computer Architecture** **AAKASH**
### **18**


`o` If opcode = 111


§ If I = 0 → Register Reference Instruction


§ If I = 1 → Input/Output Instruction


`o` If opcode ≠ 111 → Memory Reference Instruction


5. For Memory Reference:


`o` T3: If I = 1 → AR ← M[AR] (Indirect cycle)


`o` Then Execute (T4, T5, T6 depending on instruction)


6. After execution → SC ← 0 (go back to fetch next instruction)


**Important points in the flowchart** :


**Computer Architecture** **AAKASH**
### **19**


  - Indirect addressing adds one extra step at T3


  - Register and I/O instructions finish quickly (no memory access)


  - After any instruction finishes, SC is cleared to 0 and the cycle repeats


**1.9 Register Reference Instructions**


These are **special instructions** that work **only inside the CPU registers** (no memory

access). They are identified by:


  - Opcode = 111 (bits 14-12)


  - I bit = 0 (bit 15)


  - The 12 address bits become control signals (each bit does one job)


There are exactly **12** such instructions. All start with binary: **1110** followed by 12 bits.













|Hex Symbol Name Simple Meaning (what it does)<br>Code|Col2|Col3|Col4|
|---|---|---|---|
|**7800**|CLA|Clear Accumulator|AC ← 0|
|**7400**|CLE|Clear Extend (E)|E ← 0|
|**7200**|CMA|Complement<br>Accumulator|AC ← AC’ (flip all bits)|
|**7100**|CME|Complement Extend|E ← E’|
|**7080**|CIR|Circulate Right|Shift AC + E right (circular)|
|**7040**|CIL|Circulate Left|Shift AC + E left (circular)|
|**7020**|INC|Increment Accumulator|AC ← AC + 1|
|**7010**|SPA|Skip if Positive|If AC ≥ 0 then PC ← PC + 1 (skip next<br>instruction)|


**Computer Architecture** **AAKASH**
### **20**


|7008|SNA|Skip if Negative|If AC < 0 then PC ← PC + 1|
|---|---|---|---|
|**7004**|SZA|Skip if Zero|If AC = 0 then PC ← PC + 1|
|**7002**|SZE|Skip if E is Zero|If E = 0 then PC ← PC + 1|
|**7001**|HLT|Halt|Stop the computer (SC ← 0 and stop clock)|


**How they are executed** : All these instructions are executed in **one step** at T3 (very fast

because no memory is involved). Example: If IR = 1110 1000 0000 0000 → CLA → Clear AC


**Computer Architecture** **AAKASH**
### **21**


##### **Unit-II** **Register Transfer and Micro-operation**

2.1 Register Transfer Language


2.2 Register Transfer


2.3 Bus and Memory Transfer


2.4 Three state bus buffers


2.5 Memory Transfer


2.6 Arithmetic Micro operations


2.7 Logic Micro operations


[Aakash](https://github.com/aakashsinghrajawat75)


**Computer Architecture** **AAKASH**
### **22**


**2.1 Register Transfer Language (RTL)**


**Register Transfer Language (RTL)** is a **special symbolic way** to write what happens

inside the CPU during one clock pulse. It is like a “short-hand language” used only for

computer design and micro-operations. We use RTL to describe **how data moves** from one

register to another or how operations are performed.


**Basic Symbols of RTL (must remember these 5)**













|Symbol Meaning Simple Example|Col2|Col3|
|---|---|---|
|**Letters**|Name of a register|AC, DR, PC, AR, R1|
|**( )**<br>**Parentheses**|Part of a register (bits)|AC(7:0), PC(L) = lower 8 bits|
|**← Arrow**|Data is transferred / copied|DR ← AC (DR gets copy of<br>AC)|
|**, Comma**|Two or more things happen at the same<br>time|AC ← DR, PC ← PC + 1|
|**: Colon**|Conditional (only if condition is true)|P: AC ← DR (if P=1 then do<br>it)|


**Easy examples in RTL** :


  - AC ← DR → Copy data from DR to AC


  - R1 ← R2, R3 ← R1 → Swap R1 and R2 at the same time


  - P: DR ← M[AR] → If P=1, load data from memory address AR into DR


**Why we use RTL?** It helps designers write the exact steps the hardware must do - very

useful for drawing circuits later.


**2.2 Register Transfer**


**Computer Architecture** **AAKASH**
### **23**


**Register Transfer** means **moving data from one register to another register** inside the

CPU. This is the most basic micro-operation. It always happens in **one clock cycle** .


**How Register Transfer actually works**


1. Source register puts its data on the bus


2. Destination register loads (accepts) that data


**Simple block diagram view** :


**Computer Architecture** **AAKASH**
### **24**


**Common Register Transfers in Basic Computer** :


  - DR ← AC (Data Register gets value from Accumulator)


  - AC ← DR (Accumulator gets value from Data Register)


  - PC ← AR (Program Counter gets address from Address Register)


  - AR ← PC (Address Register gets next instruction address)


**Important Rule** :


  - Only **one** register can put data on the common bus at a time.


  - Multiple registers can load data at the same time (using comma in RTL).


**Easy way to remember** : Think of registers as buckets. Register Transfer = pouring water

from one bucket to another using a single pipe (the bus).


**2.3 Bus and Memory Transfer**


**Bus Transfer** = Moving data between registers using the **common bus** . **Memory Transfer**

= Moving data between a register and the main memory (RAM).


**Why Common Bus?**


  - Connecting every register to every other register directly = too many wires!


  - So we use **one shared 16-bit common bus** (like a single highway).


**How Bus Transfer works**


  - 3 select lines (S2 S1 S0) choose **which register** puts data on the bus.


  - Every register has LD (Load) signal → to take data from the bus.


**Diagram of Common Bus System** (this is the heart of the basic computer):


**Computer Architecture** **AAKASH**
### **25**


**Memory Transfer (two types)** :


1. **Read (Memory to Register)** RTL: DR ← M[AR] Meaning: Put address in AR → Read

memory → Load into DR


2. **Write (Register to Memory)** RTL: M[AR] ← DR Meaning: Put address in AR → Write

data from DR into memory


**Three-State Buffers** (very important for bus):


  - Normal gates cannot share a wire (they fight).


  - Three-state buffers have 3 states: 0, 1, or **High Impedance (Z)** = disconnected.


  - Only the selected register’s buffer is enabled (E=1), others stay in Z state.


**Computer Architecture** **AAKASH**
### **26**


**Easy example** : To move data from AC to DR using bus:


1. Select AC (S2 S1 S0 = 100)


2. AC puts data on bus


3. DR gives LD=1 → DR loads the data


**2.4 Three state bus buffers**


**Three-state bus buffers** are special electronic gates that solve a big problem in the common

bus system.


**Problem with normal gates** : If two registers try to put data on the same bus wire at the

same time (one puts 0, another puts 1), it causes a **short circuit** → damage or wrong data.


**Solution** : Three-state buffer (also called Tri-state buffer) It has **3 possible output states**

instead of only 0 or 1.

|Enable (E)|Input|Output|Meaning|
|---|---|---|---|
|0|0 or 1|**Z** (High Impedance)|Like the wire is**disconnected** (floating)|
|1|0|0|Normal logic 0|
|1|1|1|Normal logic 1|



**Symbol of one three-state buffer** (looks like a normal buffer with extra enable line).


In the basic computer:


  - Every register output is connected to the bus **through its own three-state buffer** .


  - A **decoder** (usually 3×8 or 2×4) uses the 3 select lines **S2 S1 S0** to send Enable=1 to

**only one buffer** at a time.


  - All other buffers stay in **Z state** → they do not affect the bus.


**Computer Architecture** **AAKASH**
### **27**


This way, only the selected register “drives” the bus. Others are safely disconnected.


**Easy way to remember** : Think of three-state buffers as “smart switches” on a single road

(bus). Only one car (register) is allowed to enter the road at a time; others wait with their

engine off (Z state).


**2.5 Memory Transfer**


**Memory Transfer** means moving data **between the CPU registers and the main**

**memory (RAM)** using the common bus.


There are exactly **two types** :


**Computer Architecture** **AAKASH**
### **28**


|Type|RTL<br>Notation|Simple Meaning|Direction|
|---|---|---|---|
|**Memory**<br>**Read**|DR ← M[AR]|Copy data from memory location (given by<br>AR) into Data Register|Memory →<br>CPU|
|**Memory**<br>**Write**|M[AR] ← DR|Copy data from Data Register into memory<br>location (given by AR)|CPU →<br>Memory|



**How Memory Read works (step by step)**


1. Address is already in AR


2. Memory unit gets “Read” signal


3. Memory puts the 16-bit data on the common bus


4. DR gives LD = 1 → DR loads the data from the bus


**How Memory Write works (step by step)**


1. Address is already in AR


2. DR puts its data on the common bus (select DR using S2 S1 S0)


3. Memory unit gets “Write” signal


4. Memory stores the data present on the bus at the address in AR


**Computer Architecture** **AAKASH**
### **29**


**Computer Architecture** **AAKASH**
### **30**


**Important points** :


  - AR always holds the **memory address** (12 bits).


  - DR is the **data bridge** between bus and memory.


  - These transfers happen during the **Execute phase** of memory-reference instructions

(LDA, STA, ADD, etc.).


  - In the timing diagram, Read/Write signals are active only for one clock cycle.


**Easy way to remember** : Read = “Memory gives data to DR” (like taking a book from shelf)

Write = “DR gives data to Memory” (like putting a book back on shelf)


**Computer Architecture** **AAKASH**
### **31**


**2.6 Arithmetic Micro operations**


**Arithmetic Micro-operations** are the mathematical operations performed by the **ALU**

**(Arithmetic Logic Unit)** inside the CPU. These operations work on numbers stored in

registers (usually AC and DR in the basic computer).


They are done in **one clock cycle** and always produce a result + a carry (in E flip-flop).


**Most Important Arithmetic Micro-operations**




















|Micro-<br>operation|RTL Notation|Simple Meaning|How it is done (in<br>hardware)|
|---|---|---|---|
|**Add**|AC ← AC + DR|Add content of DR to AC|Normal addition|
|**Subtract**|AC ← AC + DR’<br>+ 1|Subtract DR from AC (using<br>2’s complement)|Invert DR + add 1 +<br>add to AC|
|**Increment**|AC ← AC + 1|Increase AC by 1|Add 1 to AC|
|**Decrement**|AC ← AC - 1|Decrease AC by 1|Add all 1’s (or special<br>logic)|
|**Transfer**|AC ← DR or AC<br>← AC|Just copy value (no change)|No addition, direct<br>transfer|



**Computer Architecture** **AAKASH**
### **32**


**Hardware used** :


  - A **4-bit (or 16-bit) binary adder-subtractor** made of full-adders.


  - 4×1 MUX selects what to add (B, B’, 0, 1).


  - One XOR gate before each full-adder flips bits when subtracting (M=1 for subtract).


  - Carry-out goes to E flip-flop.


**Easy way to remember** : Arithmetic = “Math on numbers” → always uses the adder circuit.

Subtract = Add the 2’s complement (invert + add 1).


**2.7 Logic Micro operations**


**Computer Architecture** **AAKASH**
### **33**


**Logic Micro-operations** are **bit-by-bit** operations performed on the bits of two registers

(AC and DR). These do **not** use the adder - they use simple logic gates (AND, OR, XOR, NOT).


They are very useful for masking, setting, clearing, or comparing bits.


**Most Important Logic Micro-operations (used in Basic Computer)**















|Micro-<br>operation|RTL Notation|Simple Meaning (bit by bit)|Symbol<br>used|
|---|---|---|---|
|**AND**|AC ← AC∧ DR|Bitwise AND (1 only if both bits are 1)|∧ <br>|
|**OR**|AC ← AC∨ DR|Bitwise OR (1 if any bit is 1)|∨ <br>|
|**XOR**|AC ← AC⊕ <br>DR|Bitwise Exclusive-OR (1 if bits are<br>different)|⊕|
|**Complement**|AC ← AC’|Flip all bits of AC (0→1, 1→0)|’|


**Hardware used** :


**Computer Architecture** **AAKASH**
### **34**


  - A **4×1 MUX** for each bit of the register.


  - Inputs to MUX:


1. AC AND DR


2. AC OR DR


3. AC XOR DR


4. AC’ (complement)


  - Two select lines **S1 S0** choose which logic operation to perform.


**Easy way to remember** : Logic = “Bitwise decisions” → no addition, just gates + MUX. AND

= “Both must be true”, OR = “Any one true”, XOR = “Different”, Complement = “Flip”.


**Computer Architecture** **AAKASH**
### **35**


##### **Unit-III** **Micro programmed Control Unit & Central Processing** **Unit**

3.1 Design of Control Unit


3.2 Introduction to Central Processing Unit


3.3 General Register Organization


3.4 Stack Organization


3.5 Register stack


3.6 Memory stack


3.7 Instruction Formats


3.8 Addressing Modes


[Aakash](https://github.com/aakashsinghrajawat75)


**Computer Architecture** **AAKASH**
### **36**


###### **3.1 Design of Control Unit**

The **Control Unit (CU)** is like the "traffic cop" of the CPU. It reads instructions, figures out

what to do, and sends signals to other parts (like ALU or registers) to make everything happen

in the right order. There are **two main types** of Control Unit designs: **Hardwired** (fixed like

a machine) and **Microprogrammed** (flexible like software).


**Types of Control Unit Designs**



|Type Simple Meaning Pros & Cons (easy<br>words)|Col2|Col3|
|---|---|---|
|**Hardwired**|Built with fixed wires and logic gates<br>(AND, OR, etc.). No changes possible.|Fast (direct signals), but<br>rigid - hard to fix or add<br>new instructions.|
|**Microprogrammed**|Uses a special ROM (Control Memory)<br>to store tiny "micro-instructions" (like<br>a mini-program). CU reads these step-<br>by-step.|Flexible (easy to update<br>ROM), but slightly slower<br>(needs to fetch from<br>memory).|


**How Microprogrammed CU Works** :





1. IR (Instruction Register) sends opcode to a decoder → picks starting address in Control

Memory (ROM).


2. CAR (Control Address Register) loads that address → ROM outputs micro-instruction to

CDR (Control Data Register).


3. CDR activates signals (e.g., "Load AC" or "Add").


4. CDR also has "next address" → CAR updates for the next step. Repeat until instruction

ends.


**Easy way to remember** : Hardwired = "Baked-in recipe" (quick but unchangeable).

Microprogrammed = "Editable cookbook" (slower fetch but fixable).


**Computer Architecture** **AAKASH**
### **37**


###### **3.2 Introduction to Central Processing Unit**

The **Central Processing Unit (CPU)** is the "heart and brain" of the computer. It's a small

chip (like Intel Core i7) that runs programs by fetching instructions from memory, decoding

them, and executing operations. In simple words: CPU takes your commands (like "add two

numbers") and makes them happen super fast (billions of times per second).


**Main Functions of CPU (must know these 4)**


1. **Fetch** : Grabs next instruction from memory (using PC).


2. **Decode** : Understands what the instruction means (using CU).


3. **Execute** : Does the work (using ALU for math/logic).


4. **Store** : Saves results if needed (back to memory or registers).


**Basic CPU Architecture (Block Diagram View)**


**Computer Architecture** **AAKASH**
### **38**


CPU has 3 core parts connected by internal buses (address for locations, data for info, control

for signals).












|Part Simple Job Key Components Inside|Col2|Col3|
|---|---|---|
|**ALU**|Does math (add/subtract) and<br>logic (AND/OR)|Adders, logic gates|
|**Control Unit**<br>**(CU)**|Boss - decodes and sends<br>signals|Decoder, sequencer, microprogram ROM<br>(if microprogrammed)|
|**Registers**|Fast temporary storage (faster<br>than RAM)|PC, IR, AC, etc.|



**Clock Signal** : Everything syncs to the CPU clock (e.g., 3 GHz = 3 billion ticks/second). **Easy**

**way to remember** : CPU = "Kitchen": CU = chef (plans), ALU = stove (cooks), Registers =

counters (hold ingredients).


**Computer Architecture** **AAKASH**
### **39**


Block Diagram of a CPU: Detailed Analysis of All Components

###### **3.3 General Register Organization**


**General Register Organization** is how the CPU arranges its "work registers" (small, fast

storage inside CPU) for quick data handling. These are like "scratch pads" for temporary data

during calculations. In basic CPUs, there are 8-16 general registers; modern ones have 32+.

They connect via a common bus for easy transfers.


**Types of Registers in Organization**











|Type Simple Meaning Examples (in Basic Computer)|Col2|Col3|
|---|---|---|
|**General-Purpose**<br>**Registers (GPRs)**|Multi-use for data or<br>addresses (most flexible)|AC (for results), R0-R7 (extra<br>temps)|
|**Dedicated Registers**|Fixed job (not general)|PC (next instruction address), IR<br>(current instruction)|
|**Special-Purpose**|For status or flags (like carry<br>bit)|E (extend/carry flag), MAR<br>(memory address)|


**How Organization Works** :


  - Registers are grouped (e.g., 8 GPRs in a bank).






  - Use MUX (multiplexer) to select which one connects to ALU/bus.


  - Decoder lines (e.g., 3 lines for 8 registers) choose the right one.


  - In "Register File" design: Dual-port (read/write two at once) for speed.


**Easy way to remember** : Registers = "Quick drawers in a desk". GPRs = any drawer for

anything; organization = labels so you find fast.


**Computer Architecture** **AAKASH**
### **40**


###### **3.4 Stack Organization**

**Stack Organization** is a special way to store and manage data in the CPU or memory,

following **LIFO (Last In, First Out)** rule-like a stack of books where you add or remove only

from the top. It's great for handling function calls, saving addresses during jumps, or

managing temporary data in programs.


**Types of Stack Organization**








|Type Simple Meaning Pros & Cons (easy words)|Col2|Col3|
|---|---|---|
|**Register**<br>**Stack**|Uses CPU registers as stack levels<br>(fast but small)|Super quick access; limited to few items<br>(e.g., 8-64 levels).|



**Computer Architecture** **AAKASH**
### **41**


**How Stack Organization Works (Step-by-Step)**


1. **Initialize** : Set Stack Pointer (SP) to top (e.g., empty stack starts at base address).


2. **Push Operation** : Add data to top → SP moves up/down (depending on growth

direction).


3. **Pop Operation** : Remove from top → SP moves back.


4. **Check Overflow/Underflow** : Push on full stack or pop on empty = error.


**Easy way to remember** : Stack = "Plate dispenser" in a kitchen-grab the top plate (pop),

add new on top (push). No middle access!

###### **3.5 Register Stack**


**Computer Architecture** **AAKASH**
### **42**


**Register Stack** is a **compact stack made entirely of CPU registers** (no memory

involved). It's the fastest type, ideal for quick operations like arithmetic in the ALU. SP (Stack

Pointer) is a special register that tracks the current top level. Size is fixed (e.g., 64 words or

levels).


**Working of Register Stack (Step-by-Step Example with 4 Levels)**


Assume registers: R0 (bottom, empty), R1, R2, R3 (top possible). SP starts at 0.












|Step Operation SP Action (RTL) SP Stack Content (Top to<br>Before After Bottom)|Col2|Col3|Col4|Col5|Col6|
|---|---|---|---|---|---|
|**1 **|Push 10|0|SP ← SP + 1, R1<br>← 10|1|R1=10 (top)|
|**2 **|Push 20|1|SP ← SP + 1, R2<br>← 20|2|R2=20, R1=10|
|**3 **|Pop|2|Data ← R2, SP ←<br>SP - 1|1|R1=10 (new top)|
|**4 **|Push 30|1|SP ← SP + 1, R2<br>← 30|2|R2=30, R1=10|



**Full/Empty Flags** : Hardware bits signal when SP hits max (full) or 0 (empty). **Easy way to**

**remember** : Register Stack = "Handheld card stack"-flip top card fast, but you can't hold too

many.


**Computer Architecture** **AAKASH**
### **43**


###### **3.6 Memory Stack**

**Memory Stack** uses **main memory (RAM)** as the stack area, pointed by SP (which holds a

memory address). It grows downward (high to low addresses) for efficiency. Used for large

data like recursion or OS tasks. Slower than register stack but unlimited size.


**Working of Memory Stack (Step-by-Step Example)**


Assume stack starts at address 100 (top), grows down to 0. SP=100 (empty).












|Step Operation SP Action (RTL) SP Memory Content (Top<br>Before After Location)|Col2|Col3|Col4|Col5|Col6|
|---|---|---|---|---|---|
|**1 **|Push 10|100|SP ← SP - 1, M[99]<br>← 10|99|M[99]=10 (top)|
|**2 **|Push 20|99|SP ← SP - 1, M[98]<br>← 20|98|M[98]=20, M[99]=10|



**Computer Architecture** **AAKASH**
### **44**


|3|Pop|98|Data ← M[98], SP<br>← SP + 1|99|M[99]=10 (new top)|
|---|---|---|---|---|---|
|**4 **|Push 30|99|SP ← SP - 1, M[98]<br>← 30|98|M[98]=30, M[99]=10|



**Integration with CPU** : PC (instructions), AR (data access), SP (stack) all point to memory

sections. **Easy way to remember** : Memory Stack = "Warehouse shelf"-huge space, but you

need a ladder (SP) to reach the top shelf.


**Computer Architecture** **AAKASH**
### **45**


###### **3.7 Instruction Formats**

**Instruction Formats** refer to the **layout or structure** of a machine instruction in binary

bits (e.g., 16-bit or 32-bit word). It's like a "form" that packs the opcode (what to do) and

operands (data or addresses needed). Different formats balance speed, complexity, and

number of operands. In basic computers, formats vary by instruction type (e.g., memory
reference vs. register).


**Types of Instruction Formats (Based on Number of**

**Addresses/Operands)**














|Type Simple Meaning Example (ADD Pros & Cons (easy<br>Operation) words)|Col2|Col3|Col4|
|---|---|---|---|
|**Zero-**<br>**Address**|No explicit addresses; uses<br>stack (push/pop implied)|PUSH A, PUSH B, ADD<br>(pops two, pushes<br>result)|Simple hardware;<br>limited flexibility (stack<br>only).|
|**One-**<br>**Address**|One address (accumulator<br>implied as source/dest)|ADD X (AC = AC +<br>Memory[X])|Compact; assumes one<br>register (AC).|
|**Two-**<br>**Address**|Two addresses (source<br>and dest; one can be<br>register)|ADD X, Y (X = X + Y)|Balanced; needs more<br>bits.|
|**Three-**<br>**Address**|Three addresses (dest,<br>source1, source2)|ADD X, Y, Z (X = Y + Z)|Flexible; uses more<br>bits/space.|



**How Instruction Format Works (Step-by-Step in a 16-Bit Example)**


1. **Bits Allocation** : Total 16 bits → e.g., 4-bit opcode + 12-bit address (for one-address).


2. **Decode** : CPU reads opcode first → decides format and action.


**Computer Architecture** **AAKASH**
### **46**


3. **Execute** : Fetches operands based on addresses → performs op.


4. **Variations** : Some bits for mode (direct/indirect) or flags.


**Easy way to remember** : Formats = "Recipe cards" - zero-address (just "mix top two"),

three-address (full details: "put Y+Z in X"). More addresses = more flexible but longer

instructions.

###### **3.8 Addressing Modes**


**Addressing Modes** are the **ways the CPU finds the operand** (data or address) in an

instruction. Instead of hard-coding data, the instruction specifies "how to get it" (e.g., direct


from memory or calculate via register). This makes programs efficient and flexible. Common in

RISC/CISC architectures.


**Computer Architecture** **AAKASH**
### **47**


**Types of Addressing Modes**












|Type Simple Meaning Example (Load Pros & Cons<br>Instruction) (easy words)|Col2|Col3|Col4|
|---|---|---|---|
|**Immediate**|Data is in the<br>instruction itself (no<br>memory fetch)|LOAD #5 (load constant 5<br>directly)|Fast (no fetch);<br>limited to small<br>constants.|
|**Direct**|Address in instruction<br>points straight to<br>memory|LOAD 100 (load from<br>memory[100])|Simple; fixed<br>addresses only.|
|**Indirect**|Address in instruction<br>points to another<br>address|LOAD @100 (load from<br>memory[memory[100]])|Flexible<br>(pointers); extra<br>fetch cycle.|
|**Register**|Operand in a CPU<br>register (fastest)|LOAD R1 (load from register<br>R1)|Super quick; no<br>memory access.|
|**Indexed**|Address = base<br>register + offset in<br>instruction|LOAD R1 + 10 (load from<br>memory[R1 + 10])|Good for<br>arrays/loops.|
|**Relative/PC-**<br>**Relative**|Address = PC + offset<br>(for branches/jumps)|JUMP +5 (jump to PC + 5<br>instructions)|Position-<br>independent code.|



**How Addressing Modes Work (Step-by-Step Example for Indexed**

**Mode)**


1. **Instruction Fetch** : Get opcode + register (R1) + offset (10).


**Computer Architecture** **AAKASH**
### **48**


2. **Calculate Effective Address (EA)** : EA = R1 content + 10.


3. **Fetch Operand** : Go to memory[EA] → load data.


4. **Execute** : Use the data (e.g., add to AC).


**Easy way to remember** : Modes = "Treasure hunt clues" - immediate (treasure in hand),

direct (go to map spot), indirect (spot leads to another spot). Choose mode to save

time/space.


**Computer Architecture** **AAKASH**
### **49**


#### **Unit-IV** **Input Output Organization**

4.1 Peripheral devices


4.2 Input Output interface


4.3 Modes of Data Transfer


4.4 Priority Interrupt


4.5 Direct Memory Access


[Aakash](https://github.com/aakashsinghrajawat75)


**Computer Architecture** **AAKASH**
### **50**


###### **4.1 Peripheral Devices**

Peripheral devices (or I/O devices) are hardware components attached to the computer

system to perform input (data to CPU), output (data from CPU), or secondary storage

functions. They operate at much slower speeds than the CPU (e.g., CPU at GHz, keyboard at

characters/sec), hence need special handling.


**Classifications:**


Peripherals are classified based on **function**, **mode of I/O**, **data representation**, and

**access method** .



















|Classification Types/Subtypes Examples Key Characteristics<br>Basis|Col2|Col3|Col4|
|---|---|---|---|
|**By Function**<br>|Input|Keyboard, Mouse, Joystick,<br>Scanner, Microphone|Human or machine<br>input; unidirectional<br>data flow to computer|
|<br>|Output|Monitor (CRT/LCD), Printer<br>(Dot-matrix/Inkjet/Laser),<br>Plotter, Speaker|Display/print results;<br>unidirectional from<br>computer|
||Storage|HDD, SSD, Floppy Disk,<br>Magnetic Tape, Optical<br>Disk (CD/DVD)|Bidirectional; persistent<br>data storage|
|**By Data**<br>**Representati**<br>**on**|Human-Readable|Printer, Monitor|ASCII/text for humans|
||Machine-Readable|Magnetic Disk/Tape, Paper<br>Tape|Binary for machines|
|**By Usage**|Interactive|Keyboard, Mouse|Real-time user<br>interaction|


**Computer Architecture** **AAKASH**
### **51**


|Col1|Batch|Tape Drives, Card Readers|Sequential processing|
|---|---|---|---|
|**By Transfer**<br>**Mode**<br>|Serial (bit-by-bit)|USB, RS-232|Single wire pair; long<br>distance|
||Parallel<br>(byte/word)|Printer Port (Centronics),<br>SCSI|Multiple wires; short<br>distance, faster|
|**By**<br>**Synchronizat**<br>**ion**<br>|Synchronous|Disk Drives|Clock signal shared;<br>fixed timing|
||Asynchronous|Keyboard, Mouse|Handshaking (start/stop<br>bits); variable timing|



**Interface Characteristics:**


  - **Device Speed** : Low (keyboard: 10-100 chars/sec), Medium (printer: 100-1000

pages/hr), High (disk: MB/sec).


  - **Unit of Transfer** : Character (keyboard), Block (disk), Pixel (display).


  - **Data Representation** : Binary, BCD, Gray Code.


  - **Access Method** : Sequential (tape), Direct/Random (disk), Indexed (some disks).


**Advantages** :


  - Extend computer capabilities (e.g., printing, storage).


  - Modular – easy to upgrade.


**Disadvantages** :


  - Speed mismatch causes bottlenecks.


  - Need drivers/software for control.


**Computer Architecture** **AAKASH**
### **52**


**Example** : A hard disk as storage peripheral – transfers data in blocks (512 bytes/sector) via

parallel interface (SATA/AHCI).


**Concept Summary** : Peripherals are "arms and eyes" of the computer; their diversity

requires flexible I/O organization.

###### **4.2 Input-Output Interface**


The I/O Interface (or I/O Module/Controller) is the **hardware circuitry** that connects slow

peripherals to the fast CPU/bus. It isolates the CPU from device details, handling

synchronization, buffering, and protocol conversion.


**Computer Architecture** **AAKASH**
### **53**


**Key Components:**




















|Component Description Function|Col2|Col3|
|---|---|---|
|**I/O Ports**|Addressable registers (8/16/32-<br>bit)|Entry/exit points; e.g., Port 0x3F8<br>for COM1|
|**Data Register (DR)**|Holds actual data byte/word|Buffer for transfer|
|**Status Register**<br>**(SR)**|Bits for flags (e.g., R/W, Ready,<br>Error)|CPU polls/checks status|
|**Control Register**<br>**(CR)**|Configures mode (e.g., enable<br>interrupt)|Mode selection|
|**Latches/Buffers**|Temporary storage|Match speeds|
|**Address Decoder**|Selects specific device/port|From bus address lines|
|**Handshaking Logic**|READY/ACK signals|Asynchronous sync|
|**DMA/Interrupt**<br>**Logic**|For advanced modes|Offloads CPU|



**Types of I/O Addressing:**


1. **Isolated I/O (I/O Mapped)** :


`o` Separate address space (e.g., IN/OUT instructions).


`o` Ports: 0 to 64K-1.


`o` **Adv** : No confusion with memory.


`o` **Disadvantage** : Extra instructions (IN/OUT vs LOAD/STORE).


2. **Memory Mapped I/O** :


`o` Peripherals share memory address space.


**Computer Architecture** **AAKASH**
### **54**


`o` Use LOAD/STORE instructions.


`o` **Adv** : Simpler, flexible (e.g., x86).


`o` **Disadvantage** : Reduces available memory addresses.


**Functions in Detail:**


1. **Interface Electronics** : Voltage level matching (TTL to RS-232).


2. **Buffering** : FIFO queues for speed mismatch.


3. **Signal Conditioning** : Noise filtering, encoding (parallel to serial).


4. **Device Selection** : Chip select lines.


5. **Data Transfer Synchronization** : Polling, interrupts, DMA.


6. **Error Handling** : Parity, CRC checks.


**Working Example (Keyboard Interface)** :


  - CPU writes "enable" to CR.


  - Keyboard sends char → DR fills, SR sets "ready".


  - CPU reads SR, then DR.


**Advantages** :


  - CPU independence from device specifics.


  - Standardized communication.


**Disadvantages** :


  - Additional cost/hardware.


**Computer Architecture** **AAKASH**
### **55**


**Computer Architecture** **AAKASH**
### **56**


**Concept Summary** : I/O Interface is the "middleman" ensuring smooth, error-free

communication.

###### **4.3 Modes of Data Transfer**


Data transfer modes define **how** data moves from/to peripherals. CPU involvement reduces

progressively for efficiency. Three modes: Programmed I/O, Interrupt-Initiated I/O, DMA.


**1. Programmed I/O (PIO)**


  - **Detail** : CPU fully controls; actively polls (checks) device status in a loop.


  - **Types** :

|Subtype Polling Type Efficiency|Col2|Col3|
|---|---|---|
|**Non-Blocking**|Continuous loop|Very low (CPU 100% busy)|
|**Blocking**|Wait on status|Low|



  - **Steps** :


1. CPU issues command to CR.


2. Loop: Poll SR until "ready".


3. Read/Write DR.


4. Verify.


  - **Assembly Example** (8085-like):


MVI A, CMD  ; Load command


OUT PORT_CR  ; Send to control


LOOP: IN PORT_SR


ANI 01H  ; Check ready bit


**Computer Architecture** **AAKASH**
### **57**


JZ LOOP  ; Poll if not


IN PORT_DR  ; Get data


  - **Adv** : Simple, no extra hardware.


  - **Disadv** : CPU wasted (95% idle time); only 1 device.


**2. Interrupt-Driven I/O**


  - **Detail** : Device interrupts CPU when ready (via INTR line). CPU saves context, services

via ISR.


  - **Steps** :


1. CPU enables interrupt, starts I/O.


2. Device finishes → Sends interrupt.


3. CPU acknowledges (INTA), gets vector if vectored.


4. ISR: Transfer data, restore CPU.


  - **Hardware** : Interrupt Controller (e.g., 8259 PIC).


  - **Adv** : CPU multitasking; efficient for sporadic devices.


  - **Disadv** : ISR overhead; interrupt latency.


**3. Direct Memory Access (DMA)**


  - DMAC takes bus control; direct memory-peripheral transfer.


**Comparison Table** :

|Parameter Programmed I/O Interrupt-Driven DMA|Col2|Col3|Col4|
|---|---|---|---|
|**CPU Involvement**|High (polling)|Medium (ISR)|Low (setup only)|
|**Hardware Needed**|Minimal|Interrupt Controller|DMAC|



**Computer Architecture** **AAKASH**
### **58**


|Efficiency|Poor (CPU busy-wait)|Good|Excellent (bulk data)|
|---|---|---|---|
|**Devices Suited**|Slow/low-volume|Interactive (mouse)|High-speed (disk)|
|**Overhead**|100% CPU time|Context switch|Bus arbitration|
|||||
|||||


**Concept Summary** : Choose mode by device speed/volume – PIO for simple, Interrupt for

responsive, DMA for heavy loads.


**Computer Architecture** **AAKASH**
### **59**


###### **4.4 Priority Interrupt**

Priority Interrupt is a mechanism to handle **multiple interrupts** from devices simultaneously.

Not all can be serviced at once, so **priorities** decide the order (highest first). Used when CPU

is busy but devices need urgent service. Handled by **Interrupt Controller** (e.g., 8259A PIC

in x86).


**Classifications of Priority Interrupt Schemes:**



















|Scheme Description Hardware Speed Scalability<br>Requirement|Col2|Col3|Col4|Col5|
|---|---|---|---|---|
|**Parallel**<br>**Priority**|Each device has independent<br>request (IR0-IR7) and<br>acknowledge lines. Highest<br>active bit wins.|Many wires (one<br>per device)|Very<br>Fast|Poor (fixed<br>lines)|
|**Daisy**<br>**Chaining**|Devices chained serially.<br>Interrupt passes through chain;<br>first enabled device grabs it.|Single request/ack<br>line + chain|Medium|Good<br>(expandable)|
|**Matrix**|Combines parallel + daisy;<br>fixed priorities via matrix<br>decoder.|Moderate|Fast|Medium|
|**Serial**|Time-sharing; devices poll in<br>sequence.|Low|Slow|Good|


**Types of Interrupts:**






  - **Hardware** (devices), **Software** (traps), **Exception** (errors).


  - **Vectored** (device supplies ISR address), **Non-Vectored** (fixed ISR).


**Working of Daisy Chaining (Most Common):**


**Computer Architecture** **AAKASH**
### **60**


1. Device raises **INTR** (shared line).


2. CPU checks if interrupts enabled (IF flag).


3. CPU sends **INTA** pulses:


`o` 1st INTA: Enables chain.


`o` 2nd INTA: Device puts vector on bus.


4. ISR executed; low priority waits.


**Priority Assignment** : Fixed (IR0 highest) or Programmable (8259 allows rotation).


**Assembly Example (8085/8086)** :


; ISR Entry (Hardware pushes PC)


POP H   ; Save return


PUSH PSW ; Save flags;


Handle device


POP PSW


POP H


EI    ; Re-enable interrupts


RET    ; Return


**8259A PIC Features** :


  - 8 interrupt levels; cascadable to 64.


  - Modes: Edge/Level triggered, Auto/manual EOI.


**Computer Architecture** **AAKASH**
### **61**


**Advantages** :


  - Efficient multi-device handling.


  - Prevents low-priority blocking high (e.g., emergency vs mouse).


**Disadvantages** :


  - Daisy chain delay (propagation).


  - Fixed priorities inflexible.


**Concept Summary** : Priority ensures critical devices (e.g., disk error > keyboard) get

serviced first; daisy chaining is cost-effective for 4-8 devices.


**Computer Architecture** **AAKASH**
### **62**


###### **4.5 Direct Memory Access (DMA)**

DMA enables **high-speed peripherals** (e.g., disks, networks) to transfer **large data blocks**

**directly to/from memory**, bypassing CPU. **DMA Controller (DMAC)** (e.g., 8237 in x86)

arbitrates bus access. Ideal for bulk transfers where CPU polling/interrupts are inefficient.


**Classifications/Types of DMA:**







|Type/Mode Description CPU Status Use Case<br>During<br>Transfer|Col2|Col3|Col4|
|---|---|---|---|
|**Burst Mode**|DMAC takes full bus control;<br>transfers entire block<br>continuously.|Halted|High-speed,<br>infrequent|
|**Cycle Stealing**|DMAC steals one bus cycle<br>between CPU cycles (transparent<br>to CPU).|Runs normally|Continuous<br>low-volume|
|**Block/Transparent**|Full block, but CPU can run if<br>priority given.|Partially active|Balanced|
|**Single/Multiple**|Single: One word/transfer;<br>Multiple: Block.|Varies|Flexible|


**Additional Features:**






  - **Channels** : 4-8 independent (e.g., one for HDD, one for FDD).


  - **Transfer Directions** : Memory-to-Device, Device-to-Memory, Memory-to-Memory.


  - **Addressing** : Fixed (one address), Incrementing, Flying (current address).


**Detailed Working (Cycle Stealing Example):**


**Computer Architecture** **AAKASH**
### **63**


1. **Initialization** (CPU):


`o` Write to DMAC registers: Start Addr, Count, Mode (e.g., channel 0).


`o` Assert **HRQ** (Hold Request).


2. **Bus Acquisition** :


`o` CPU grants **HLDA** (Hold Acknowledge); tri-states its lines.


3. **Transfer** :


`o` DMAC asserts **MEMR/MEMW** or **IOR/IOW** .


`o` Data flows directly (Device ↔ Memory).


`o` Auto-increment address/decrement count.


4. **Completion** :


`o` Count=0 → Interrupt to CPU.


`o` CPU regains bus.


**8237 DMAC Registers** :

|Register Purpose|Col2|
|---|---|
|**Mode**|Transfer type/mode|
|**Address**|Starting memory/port addr|
|**Count**|Bytes to transfer (16-bit)|



**Pseudocode Example** :


DMAC_WRITE(MODE_REG, AUTO_INC | DEVICE_TO_MEM);


DMAC_WRITE(ADDR_REG, 0x1000);


**Computer Architecture** **AAKASH**
### **64**


DMAC_WRITE(COUNT_REG, 1024);


CPU_HRQ(); // Request bus


// DMAC transfers 1024 bytes from device to 0x1000D


MAC_INT(); // Signals done


**Advantages** :


  - CPU 100% free (up to 80% speedup for I/O).


  - High throughput (e.g., 100 MB/s disks).


**Disadvantages** :


  - Expensive hardware.


  - Bus contention (CPU waits).


  - Complex arbitration.


**Computer Architecture** **AAKASH**
### **65**


**Computer Architecture** **AAKASH**
### **66**


**Concept Summary** : DMA is "CPU vacation mode" for I/O; essential for modern systems

with gigabytes of data movement.


**Computer Architecture** **AAKASH**
### **67**


#### **Unit-V** **Memory Organization**

5.1 Memory Hierarchy


5.2 Main Memory


5.3 Auxiliary Memory


5.4 Associative Memory


5.5 Cache Memory


5.6 Virtual Memory


[Aakash](https://github.com/aakashsinghrajawat75)


**Computer Architecture** **AAKASH**
### **68**


##### **Unit-V** **Memory Organization**

###### **5.1 Memory Hierarchy**

Memory hierarchy is a crucial concept in computer architecture, designed to optimize the

performance and efficiency of memory usage. It categorizes different types of memory based

on three primary criteria: speed, cost, and capacity.


**Key Concepts**


1. **Speed** : Memory types closer to the CPU are typically faster, facilitating quicker data

access.


2. **Cost** : Faster memory is generally more expensive per unit of storage.


3. **Capacity** : Slower memory types can store larger amounts of data.


**Levels of Memory Hierarchy**


The memory hierarchy can be visualized as a pyramid, with the fastest and most expensive

memory at the top and the slowest and cheapest at the bottom.

|Level Type Speed Size Cost|Col2|Col3|Col4|Col5|
|---|---|---|---|---|
|**Level 1**|Registers|Very Fast|Very Small|Very Expensive|
|**Level 2**|Cache Memory|Fast|Small|Moderately<br>Expensive|
|**Level 3**|Main Memory|Moderate|Medium|Moderate|
|**Level 4**|Auxiliary Memory|Slow|Large|Cheap|



**Detailed Explanation of Each Level**


**Computer Architecture** **AAKASH**
### **69**


  - **Level 1: Registers**


      - **Description** : Small storage locations within the CPU.


      - **Speed** : Access time is in the range of nanoseconds.


      - **Use** : Store immediate values needed for calculations.


  - **Level 2: Cache Memory**


      - **Description** : A smaller, faster type of volatile memory located close to the CPU.


      - **Speed** : Faster than main memory, with access times in nanoseconds.


      - **Use** : Temporarily stores frequently accessed data and instructions to speed up

processing.


  - **Level 3: Main Memory (RAM)**


      - **Description** : Primary working memory of the computer.


      - **Speed** : Slower than cache, typically in nanoseconds to microseconds.


      - **Use** : Stores data and programs currently in use.


  - **Level 4: Auxiliary Memory**


      - **Description** : Non-volatile storage that retains data when powered off.


      - **Speed** : Slower, with access times in milliseconds.


      - **Use** : Long-term storage for data, applications, and the operating system.


**Computer Architecture** **AAKASH**
### **70**


**Importance of Memory Hierarchy**


  - **Performance Optimization** : By utilizing a hierarchy, the system can provide fast

access to frequently used data while maintaining a larger pool of slower storage.


  - **Cost Efficiency** : It balances the cost of high-speed memory with the need for larger

storage capacity.


  - **Data Management** : Efficiently manages how data is stored, accessed, and retrieved.

###### **5.2 Main Memory**


Main memory, often referred to as **RAM (Random Access Memory)**, plays a critical role in a

computer's performance. It is the primary storage area that the CPU accesses to read and

write data during operation.


**Key Characteristics**


1. **Volatile** : Data is lost when the power is turned off.


2. **Directly Accessible** : The CPU can access data directly without any intermediary steps.


**Computer Architecture** **AAKASH**
### **71**


3. **Types** : Common types include:


      - **DRAM (Dynamic RAM)** : Requires periodic refreshing to maintain data.


      - **SRAM (Static RAM)** : Faster and does not require refreshing, but is more

expensive.


**Functions of Main Memory**


  - **Stores Data** : Holds data that the CPU is currently processing.


  - **Holds Instructions** : Keeps the instructions for programs that are currently running.


  - **Temporary Storage** : Acts as a buffer for data being processed by the CPU.


**Structure of Main Memory**


  - **Memory Cells** : Each cell can store a binary value (0 or 1).


**Computer Architecture** **AAKASH**
### **72**


  - **Addressing** : Each memory location has a unique address, allowing the CPU to access

specific data quickly.


**Performance Factors**


  - **Capacity** : Typically measured in gigabytes (GB).


  - **Speed** : Measured in nanoseconds; faster speeds reduce the time the CPU waits for

data.



|Feature Description|Col2|
|---|---|
|**Capacity**|Typically 4GB to 64GB in<br>modern systems.|
|**Speed**|Access time ranges from 10ns<br>to 100ns.|
|**Power**<br>**Consumption**|Generally consumes more<br>power when active.|

###### **5.3 Auxiliary Memory**





Auxiliary memory, also known as **secondary storage**, is a crucial component of a computer's

memory organization. It is used for long-term data retention and provides a larger storage

capacity compared to main memory (RAM).


**Key Characteristics**


1. **Non-volatile** : Data remains intact even when the power is turned off.


2. **Higher Capacity** : Typically offers much more storage space compared to main

memory.


**Computer Architecture** **AAKASH**
### **73**


3. **Slower Access Speed** : Access times are generally longer than those for main

memory.


**Types of Auxiliary Memory**


  - **Hard Disk Drives (HDD)**


      - **Description** : Magnetic storage device, widely used for general storage.


      - **Speed** : Slower access times (typically in milliseconds).


      - **Capacity** : Ranges from hundreds of GB to several TB.


  - **Solid State Drives (SSD)**


      - **Description** : Uses flash memory to provide faster data access.


      - **Speed** : Much faster than HDDs, with access times often below 1 millisecond.


      - **Capacity** : Ranges from hundreds of GB to several TB.


  - **Optical Discs**


      - **Description** : Includes CDs, DVDs, and Blu-rays, used primarily for media

storage.


      - **Speed** : Slower compared to HDDs and SSDs.


      - **Capacity** : Varies from 700 MB for CDs to 100 GB for Blu-rays.


  - **Flash Drives**


      - **Description** : Portable storage devices used for data transfer.


      - **Speed** : Comparable to SSDs, but can vary widely by brand.


      - **Capacity** : Ranges from a few GB to several TB.


      

**Computer Architecture** **AAKASH**
### **74**


**Functions of Auxiliary Memory**


  - **Long-term Data Storage** : Provides a place to store operating systems, applications,

and user data.


  - **Backup** : Often used for backing up important files to prevent data loss.


  - **Data Transfer** : Facilitates data transfer between different systems.


**Performance Factors**


  - **Access Speed** : Measured in milliseconds for HDDs and microseconds for SSDs.


  - **Durability** : SSDs are generally more durable than HDDs since they have no moving

parts.


**Computer Architecture** **AAKASH**
### **75**


|Feature Hard Disk Solid State Optical Flash<br>Drive Drive (SSD) Discs Drives<br>(HDD)|Col2|Col3|Col4|Col5|
|---|---|---|---|---|
|**Capacity**|Up to several<br>TB|Up to several<br>TB|Varies<br>(700MB -<br>100GB)|Up to<br>several TB|
|**Access**<br>**Speed**|10-20 ms|<1 ms|100-300 ms|<1 ms|
|**Durability**|Moderate|High|Moderate|High|
|**Cost per**<br>**GB**|Low|Moderate to<br>High|Very Low|Moderate|


###### **5.4 Associative Memory**

Associative memory, also known as **content-addressable memory (CAM)**, is a type of

memory that allows data retrieval based on content rather than specific addresses. This

unique feature makes it particularly useful for applications where quick data access is critical.


**Key Characteristics**


1. **Content Addressability** : Allows search and retrieval of data by content, not by

address.


2. **Parallel Search** : Capable of searching multiple memory locations simultaneously,

leading to faster access.


3. **Volatile** : Typically, associative memory is volatile, meaning it loses its contents when

power is turned off.


**How Associative Memory Works**


**Computer Architecture** **AAKASH**
### **76**


  - **Data Storage** : Data is stored in a way that each entry can be accessed by its content.


  - **Search Mechanism** : When a search query is made, the memory compares the input

against all stored entries in parallel, returning matches quickly.


**Applications of Associative Memory**


  - **Cache Memory** : Used in CPU caches to quickly locate data.


  - **Database Management** : Facilitates fast data retrieval in databases.


  - **Networking** : Used in routers for packet forwarding based on content.


**Advantages and Disadvantages**


**Computer Architecture** **AAKASH**
### **77**


|Feature Advantages Disadvantages|Col2|Col3|
|---|---|---|
|**Speed**|Extremely fast data<br>retrieval|More complex design<br>compared to RAM|
|**Efficiency**|Reduces the time for<br>search operations|Generally more expensive per<br>bit|
|**Flexibility**|Allows for dynamic data<br>lookup|Limited capacity compared to<br>traditional RAM|

###### **5.5 Cache Memory**





Cache memory is a small-sized type of volatile computer memory that provides high-speed

access to frequently accessed data and instructions. It acts as a buffer between the CPU and

main memory, optimizing performance by reducing data access times.


**Key Characteristics**


1. **Speed** : Cache memory is significantly faster than main memory (RAM).


2. **Volatile** : Data is lost when power is turned off.


3. **Limited Size** : Typically smaller in capacity compared to main memory.


**Levels of Cache Memory**


Cache memory is usually organized into different levels, primarily:


  - **L1 Cache** :


      - **Location** : Integrated directly into the CPU.


      - **Size** : Usually between 16KB to 128KB.


      - **Speed** : Fastest access time (1-2 cycles).


**Computer Architecture** **AAKASH**
### **78**


  - **L2 Cache** :


      - **Location** : Can be on-chip or on a separate chip close to the CPU.


      - **Size** : Typically 256KB to 8MB.


      - **Speed** : Slower than L1 but faster than main memory (3-10 cycles).


  - **L3 Cache** :


      - **Location** : Shared among multiple cores in multi-core processors.


      - **Size** : Can range from 2MB to 20MB.


      - **Speed** : Slower than L1 and L2 but faster than main memory.


**Functions of Cache Memory**


  - **Data Storage** : Temporarily holds frequently accessed data and instructions.


  - **Speed Enhancement** : Reduces latency by providing faster access to data compared

to main memory.


  - **Prefetching** : Anticipates the data needed based on the CPU's processing patterns.


**Cache Memory Operation**


**Computer Architecture** **AAKASH**
### **79**


1. **Cache Hit** : When the CPU finds the requested data in the cache, resulting in a fast

data retrieval.


2. **Cache Miss** : When the data is not found in the cache, requiring a fetch from main

memory, which is slower.


**Advantages and Disadvantages**







|Feature Advantages Disadvantages|Col2|Col3|
|---|---|---|
|**Performance**|Significantly improves CPU<br>performance|Higher cost per bit<br>compared to RAM|
|**Efficiency**|Reduces access time for<br>data|Limited storage<br>capacity|
|**Power**<br>**Consumption**|Consumes less power<br>than accessing main<br>memory|Complexity in cache<br>management|

###### **5.6 Virtual Memory**





Virtual memory is a memory management capability of an operating system (OS that uses

hardware and software to allow a computer to compensate for physical memory shortages by

temporarily transferring data from random access memory (RAM) to disk storage. This

technique enables systems to run larger applications with less physical memory and enhances

multitasking capabilities.


**Key Concepts of Virtual Memory**


1. **Abstraction of Memory** :


**Computer Architecture** **AAKASH**
### **80**


      - Virtual memory provides an abstraction of the physical memory, allowing

applications to use more memory than what is physically available. Each process

operates in its own virtual address space.


2. **Paging** :


      - Memory is divided into fixed-size units called **pages** (typically 4KB). The physical

memory is divided into **page frames** of the same size. When a program

accesses a page not currently in memory, a **page fault** occurs, prompting the

OS to load the required page from secondary storage.


3. **Page Table** :


      - Each process has a **page table** that maps virtual addresses to physical

addresses. The page table contains entries for each page, indicating whether it is

in physical memory and its corresponding frame number.


4. **Swapping** :


      - When physical memory is full, the OS may choose to swap out pages that are

not currently being used to disk (swap space or page file). This process allows

more processes to run simultaneously but can introduce latency due to disk I/O.


**Computer Architecture** **AAKASH**
### **81**


**Benefits of Virtual Memory**


  - **Increased Memory Capacity** : Allows systems to run applications that require more

memory than physically available.


  - **Isolation and Security** : Each process operates in its own address space, reducing the

risk of one process affecting another.


  - **Efficient Memory Usage** : Pages that are not frequently accessed can be swapped

out, keeping the most active data in RAM.


**Drawbacks of Virtual Memory**


  - **Performance Overhead** : Accessing data from disk is significantly slower than

accessing RAM, which can lead to performance issues if excessive paging (thrashing)

occurs.


**Computer Architecture** **AAKASH**
### **82**


  - **Complexity** : The management of virtual memory requires sophisticated algorithms to

track pages, page tables, and swapping.


**Summary Table**

|Feature Description|Col2|
|---|---|
|**Abstraction**|Allows applications to use more memory than physically available.|
|**Paging**|Memory management technique that divides memory into pages.|
|**Page Table**|Maps virtual addresses to physical addresses for each process.|
|**Swapping**|Moves pages between RAM and disk to free up memory.|
|**Benefits**|Increases capacity, provides isolation, and optimizes usage.|
|**Drawbacks**|Performance overhead due to disk access and added complexity.|



**Computer Architecture** **AAKASH**
### **83**


# **Happy learning** **Love form Aakash**

**Computer Architecture** **AAKASH**
### **84**


---

## 👨‍💻 Author

> **Aakash**

> **GitHub: [aakashsinghrajawat75](https://github.com/aakashsinghrajawat75)**

---
