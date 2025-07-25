---
title: 04_Digital-Building-Blocks
description: 
published: true
date: 2025-07-25T17:01:47.727Z
tags: 
editor: markdown
dateCreated: 2025-07-22T17:33:24.596Z
---

# Chapter 4: Digital Building Blocks
---
## Summary
---
> ""


## 4.1 Arithmetic Circuits
---
### Key Concepts
- **Carry-Lookahead Adder (CLA)**:
  - Carry propogate adder that divides adder into blocks that determine carry out independent of computation.
  - Generate signal, G, produced if carry out is independent of carry in.
  - Propogation signal, P, produced if a carry in would lead to a carry out.
### Definitions
- **Prefix**
  - Propogation and generation signals from -1:-1 to N-2:-1.
- **Set if less than (SLT)**
  - Set result to 1 if less than is achieved otherwise 0.
  - Typically treats input as signed.
  - A SLTU treats input as unsigned.
- **Logical Shifter**
  - Shifts number to left or right and fills empty spots with 0s - << # or >> #.
- **Arithmetic Shifter**
  - Same as logical shifter execept on right shifts the msb is preserved by duplication - >>> #.
- **Rotator**
  - Rotates a number either left, ROL #, or right, ROR #, such that bits shift to the other end.
- **Multiply Accumulate**
  - Multiplies two numbers and adds them to a third number, often used in DSP.
### Algorithms
**Binary Division**
Perform binary division with such that $\frac{A}{B} = Q + \frac{R}{B}$ for N-bit unsigned number.
```pseudo
1. R′ = 0
2. for i = N−1 to 0
3. 	R = {R′ << 1, Ai}
4. 	D = R − B
5. 	if D < 0 then Qi = 0, R′ = R // R < B
6. 	else Qi = 1, R′ = D // R ≥ B
7. R = R′
```
### Code Snippets
**CPA**
Configure a CPA
```systemverilog
module adder #(parameter N = 8)
							(input logic [N–1:0] a, b,
              input logic cin,
              output logic [N–1:0] s,
              output logic cout);
	assign {cout, s} = a + b + cin;
endmodule
```
**Subtractor**
Configure a subtraction module.
```systemverilog
module subtractor #(parameter N = 8)
                    (input logic [N–1:0] a, b,
                    output logic [N–1:0] y);
	assign y = a – b;
endmodule
```
**Comparators**
Using various comparisons for unsigned binary.
```systemverilog
module comparators #(parameter N = 8)
                      (input logic [N–1:0] a, b,
                      output logic eq, neq, lt, lte, gt, gte);
  assign eq = (a == b);
  assign neq = (a != b);
  assign lt = (a < b);
  assign lte = (a <= b);
  assign gt = (a > b);
  assign gte = (a >= b);
endmodule
```
### Formulas
**Ripple Adder Delay**
With N digit binary numbers to add and $t_{FA}$ gate delay between each full adder, the total ripple adder delay would be,
$$
Nt_{FA}
$$
**CLA Delay**
Find the propogation delay for a N-bit adder with k-bit blocks where $t_{pg}$ is the delay of the column propogate and generate gates, $t_{pg\_block}$ is the delay of the block propogate and generate signals, and $t_{AND_OR}$ is the delay from $C_{in}$ to $C_{out}$.
$$
t_{CLA} = t_{pg} + t_{pg\_block} + \left(\frac{N}{k} - 1 \right)\times t_{AND\_OR} + k \times t_{FA}
$$
**Prefix Adder Delay**
With $t_{pg_prefix}$ being the delay of a prefix cell, the propogation delay for this adder is,
$$
t_{PA} = t_{pg} + \log_{2}N \times \left(t_{pg\_prefix}\right) + t_{XOR}
$$
### Visual Aids
#### Half Adder
![half-adder_black-box.png](/half-adder_black-box.png)

| $A$ | $B$ | $C_{out}$ | $S$ |
| - | - | - | - |
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 1 | 1 | 0 |


#### Full Adder
![full-adder_black-box.png](/full-adder_black-box.png)

| $C_{in}$ | $A$ | $B$ | $C_{out}$ | Y |
| - | - | - | - | - |
| 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 0 | 1 |
| 0 | 1 | 0 | 0 | 1 |
| 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 | 1 |
| 1 | 0 | 1 | 1 | 0 |
| 1 | 1 | 0 | 1 | 0 |
| 1 | 1 | 1 | 1 | 1 |


#### Carry Propogate Adder
![carry-propogate-adder_black-box.png](/carry-propogate-adder_black-box.png)

#### Ripple Carry Adder
![ripple-carry-adder_black-box.png](/ripple-carry-adder_black-box.png)

#### Carry Lookahead Adder (CLA)
![carry-lookahead-adder_black-box.png](/carry-lookahead-adder_black-box.png)

![cla_circuit.png](/cla_circuit.png)

$$
G_i = A_i \wedge B_i
$$
$$
P_i = A_i \lor B_i
$$
$$
C_i = A_i \wedge B_i \lor \left(A_i \lor B_i \right) \wedge C_{i-1} = G_i \lor P_i\wedge C_{i-1}
$$
$$
G_{3:0} = G_3 \lor P_3 \wedge\left(G_2 \lor P_2 \wedge\left(G_1 \lor P_1 \wedge G_0\right)\right)
$$
$$
P_{3:0} = P_3 \wedge P_2 \wedge P_1 \wedge P_0
$$
$$
C_i = G_{i:j} \lor P_{i:j} \wedge C_{j-1}
$$
#### Prefix Adder
$$
S_i = \left(A_i \oplus B_i \right) \oplus C_{i-1}
$$
$$
G_{-1} = C_{in}
$$
$$
P_{-1} = 0
$$
Then,
$$
C_{i-1} = G_{i-1:-1}
$$
$$
S_i = \left(A_i \oplus B_i \right) \oplus G_{i-1:-1}
$$
$$
G_{i:j} = G_{i:k} \lor P_{i:k} \wedge G_{k-1:j}
$$
$$
P_{i:j} = P_{i:k} \wedge P_{k-1:j}
$$
![prefix-adder_circuit.png](/prefix-adder_circuit.png)

#### Subtractor
![subtractor_black-box.png](/subtractor_black-box.png)

![subtractor_circuit.png](/subtractor_circuit.png)

#### Equality Comparator
![equality-comparator_black-box.png](/equality-comparator_black-box.png)

![equality-comparator_circuit.png](/equality-comparator_circuit.png)

#### Magnitude Comparator
![magnitude-comparator_circuit.png](/magnitude-comparator_circuit.png)

#### Arithmetic Logic Unit (ALU)
![alu_black-box.png](/alu_black-box.png)

| $ALUControl_{1:0}$ | $Function$ |
| - | - |
| 00 | Add |
| 01 | Subtract |
| 10 | AND |
| 11 | OR |


![alu_circuit.png](/alu_circuit.png)

![alu-flags_black-box.png](/alu-flags_black-box.png)

![alu-flags_circuit.png](/alu-flags_circuit.png)

| Comparison | Signed | Unsigned |
| - | - | - |
| = | Z | Z |
| $\neq$ | $\neg$ Z | $\neg$ Z |
| < | N $\oplus$ V | $\neg$ C |
| $\leq$ | Z $\lor$ N $\oplus$ V | Z $\lor\neg$ C |
| > | $\neg$ Z $\wedge\neg$(N$\oplus$P) | $\neg$ Z $\wedge$ C |
| $\geq$ | $\neg$(N$\oplus$P) | C |


#### Shifters
![logical-shift-left_black-box.png](/logical-shift-left_black-box.png)

![logical-shift-left_circuit.png](/logical-shift-left_circuit.png)

![logical-shift-right_black-box.png](/logical-shift-right_black-box.png)

![logical-shift-right_circuit.png](/logical-shift-right_circuit.png)

![arithmetic-shift-right_black-box.png](/arithmetic-shift-right_black-box.png)

![arithmetic-shift-right_circuit.png](/arithmetic-shift-right_circuit.png)

#### Multiplier
![multiplier_black-box.png](/multiplier_black-box.png)

![multiplier_function.png](/multiplier_function.png)

![multiplier_circuit.png](/multiplier_circuit.png)

#### Divider
![division_circuit.png](/division_circuit.png)

### Examples
**Carry Propogation Adder Delay**
**Problem:**
Compare the delays of a 32-bit ripple-carry adder and a 32-bit carry-lookahead adder with 4-bit blocks. Assume that each two-input gate delay is 100 ps and that a full adder delay is 300 ps.
**Solution:**
For the ripple carry adder,
$$
32 * 300ps = 9.6ns
$$
For the CLA,
$$
100ps + 6 \times 100ps + \left(\frac{32}{4} -1 \right)\times 2 \times 100ps + \left(4 \times 300ps \right) = 3.3ns
$$
**Binary Multiplication**
**Problem**
Multiply the unsigned binary numbers 0101 and 0111.
**Solution**
$$
0101 \times 0111 = 0101 + 01010 + 010100 + 0000000 = 0100011
$$
### Notable Quotes
> “Arithmetic circuits are the central building blocks of computers."
### References
- *Digital Design and Computer Architecture* — Chapter 5, Pages 237–256


## 4.2 Number Systems
---
### Key Concepts
- **Fixed-Point Binary**:
  - Analogous to decimals; some of the bits represent the integer part, and the rest represent the fraction.
  - Implied binary point between the integer and fraction bits.
  - Can use two's complement or sign/magnitude representation.
  - Denoted by Ua.b for unsigned or Qa.b for two's complement with a integer bits and b fraction bits.
- **Floating-Point Binary**
  - Analogous to scientific notation, with a mantissa and an exponent.
  - Contains sign, mantissa, and exponent bits.
### Definitions
- **Underflow**
  - Number too small to be represented.
- **Floating-Point Unit (FPU)**
  - Responsible for floating-point arithmetic.
### Algorithms
**Floating-Point Addition**
Process for adding floating-point binary.
```pseudo
1. Extract exponent and fraction bits.
2. Prepend leading 1 to form the mantissa.
3. Compare exponents.
4. Shift smaller mantissa if necessary.
5. Add mantissas.
6. Normalize mantissa and adjust exponent if necessary.
7. Round result.
8. Assemble exponent and fraction back into floating-point number.
```
### Visual Aids
| Number | Sign | Exponent | Fraction |
| - | - | - | - |
| 0 | X | 00000000 | 00000000000000000000000 |
| $\infty$ | 0 | 11111111 | 00000000000000000000000 |
| -$\infty$ | 1 | 00000000 | 00000000000000000000000 |
| Nan | X | 11111111 | Non-Zero |


| Format | Total Bits | Sign Bits | Exponent Bits | Fraction Bits | Bias |
| - | - | - | - | - | - |
| Single | 32 | 1 | 8 | 23 | 127 |
| Double | 64 | 1 | 11 | 52 | 1023 |
| Quad | 128 | 1 | 15 | 112 | 16363 |


![floating-point_addition_example.png](/floating-point_addition_example.png)

### Examples
**Fixed-Point To Decimal**
**Problem:**
Convert 01101100 to decimal where 4 integer bits exist.
**Solution:**
$$
01101100_2 = 0110.1100_2
$$
$$
0110.1100_2 = 2 + 4 + \frac{1}{2} + \frac{1}{4} = 6.75_{10}
$$
**Add Fixed-Point**
**Problem**
Add 00001100 with 11110110 such that both ar Q4.4.
**Solution**
$$
00001100_2 + 11110110_2 = 00000010_2
$$
**Decimal To Floating-Point**
**Problem**
Represent 228_{10} as a floating-point number using a basic 32 bit encoding and then single-precision efficient encoding.
**Solution**
$$
228_{10} = 11100100_2 = 1.11001_2 \times 2^7 = sign[0]exponent[00000111]mantissa[11100100000000000000000]
$$
Notice that the leading 1 of the mantissa is implicit, thus,
$$
1.11001_2 \times 2^7 = sign[0]exponent[00000111]mantissa[11001000000000000000000]
$$
We can then represent negative exponents by adding a bias to the exponent, $127_{10}$ for single-precision.
$$
1.11001_2 \times 2^7 = sign[0]exponent[10000110]mantissa[11001000000000000000000]
$$
### References
- *Digital Design and Computer Architecture* — Chapter 5, Pages 256–261


## 4.3 Sequential Building Blocks
---
### Definitions
- **Digitally Controlled Oscillator (DCO)**
  - N-bit counter that adds p on each cycle rather than 1.
  - $f_{out} = f_{clk} \times \frac{p}{2^N}$
### Code Snippets
**Counter**
Create a N-bit counter.
```systemverilog
module counter #(parameter N = 8)
                  (input logic clk,
                  input logic reset,
                  output logic [N–1:0] q);
	always_ff @(posedge clk, posedge reset)
		if (reset) q <= 0;
		else q <= q + 1;
endmodule
```
**Shift Register With Parralel Load**
Construct a shift register with parralel load.
```systemverilog
module shiftreg #(parameter N = 8)
                  (input logic clk,
                  input logic reset, load,
                  input logic sin,
                  input logic [N–1:0] d,
                  output logic [N–1:0] q,
                  output logic sout);
	always_ff @(posedge clk, posedge reset)
    if (reset) q <= 0;
    else if (load) q <= d;
    else q <= {q[N–2:0], sin};
	assign sout = q[N–1];
endmodule
```
### Visual Aids
#### N-bit Counter (Divide-By-$2^N$-Counter)
![n-bit-counter_black-box.png](/n-bit-counter_black-box.png)

![n-bit-counter_circuit.png](/n-bit-counter_circuit.png)

#### Shift Register
![shift-register_black-box.png](/shift-register_black-box.png)

Serial-To-Parralel Converter,
![shift-register_serial-to-parralel_circuit.png](/shift-register_serial-to-parralel_circuit.png)

Parralel-To-Serial Converter,
![shift-register_parallel-to-serial_circuit.png](/shift-register_parallel-to-serial_circuit.png)

### References
- *Digital Design and Computer Architecture* — Chapter 5, Pages 261–265


## 4.4 Memory Arrays
---
### Key Concepts
- **Memory Array**:
  - An efficient storage for large amounts of data.
  - Size given as depth x width.
- **Random Access Memory (RAM)**
  - Volatile.
- **Dynamic RAM (DRAM)**
  - Stores data as a charge on a capacitor.
- **Static RAM (SRAM)**
  - Stores data using a pair of cross-coupled inverters.
- **SDRAM**
  - Uses clock to pipeline memory access.
- **DDR SDRAM**
  - Uses both rising and falling edges of clock effectively doubling throughput.
- **Read Only Memory (ROM)**
  - Nonvolatile.
- **Programmable ROM (PROM)**
  - Allows connections or disconnections of transistors to effectively controll stored data.
- **Register File**
  - Group of registers to store temporary variables.
  - Usually built as a small multiported SRAM array.
### Definitions
- **Address**
  - Row in a memory array.
- **Data**
  - Value read or written to in memory array.
- **Word**
  - Row of data in memory array.
- **Bit Cell**
  - Connected to wordline and bitline, essentially a single digit of data.
- **Wordline**
  - Connection shared with a word in a memory array.
 - **Bitline**
   - Connection shared with a column in memory array.
 - **Port**
   - Gives read/write access to one memory address.
### Algorithms
**Algorithm Name**
Description.
```pseudo
1. Step 1
2. Step 2
3. Step 3
```
### Code Snippets
**Snippet Name**
Description.
```program
// code
```
### Theorems & Proofs
**Theorem Name**
Proof.
### Formulas
**Formula Name**
Description.
$$
Equation
$$
### Visual Aids
#### Memory Array
![memory-array_black-box.png](/memory-array_black-box.png)

![memory-array-4x3_black-box.png](/memory-array-4x3_black-box.png)

![memory-array-4x3_representation_example.png](/memory-array-4x3_representation_example.png)

![memory-array-4x3_high-level-overview.png](/memory-array-4x3_high-level-overview.png)

![memory-array-1024x32_black-box.png](/memory-array-1024x32_black-box.png)

#### Multiported Memory Array
![multiported-memory-array_black-box.png](/multiported-memory-array_black-box.png)

#### DRAM
![dram_circuit.png](/dram_circuit.png)

#### SRAM
![sram_circuit.png](/sram_circuit.png)

| Memory Type | Transistors Per Bit Cell | Latency |
| - | - | - |
| Flip-Flop | 20 | Fast |
| SRAM | 6 | Medium |
| DRAM | 1 | Slow |


#### Register File
![register-file-32x32_black-box.png](/register-file-32x32_black-box.png)

#### ROM
![rom_circuit.png](/rom_circuit.png)

![rom-dot_representation.png](/rom-dot_representation.png)

#### Fuse-PROM
![fuse-programmable-rom_circuit.png](/fuse-programmable-rom_circuit.png)

### Examples
**Example Title**
**Problem:**
Problem Statement.
**Solution:**
Solution Statement.
### Notable Quotes
> “Notable quote."
### Common Pitfalls
- Pitfall 1.

### References
- *Book Title* — Chapter X, Pages Y–Z














## #.# Subsection Title
---
### Key Concepts
- **Concept Name**:
  - Subpoint or clarification.
### Definitions
- **Term 1**
  - Concise explanation of the term.
### Algorithms
**Algorithm Name**
Description.
```pseudo
1. Step 1
2. Step 2
3. Step 3
```
### Code Snippets
**Snippet Name**
Description.
```program
// code
```
### Theorems & Proofs
**Theorem Name**
Proof.
### Formulas
**Formula Name**
Description.
$$
Equation
$$
### Visual Aids
| Header | Header |
| - | - |
| Content | Content |
![Diagram]()
### Examples
**Example Title**
**Problem:**
Problem Statement.
**Solution:**
Solution Statement.
### Notable Quotes
> “Notable quote."
### Common Pitfalls
- Pitfall 1.
### Related Links
- [Link]()
### References
- *Book Title* — Chapter X, Pages Y–Z

- [Author(s), "Paper or Article Title," Journal or Conference Name, Year]() 

- [Related Chapter in This Wiki]()  

- [Official Specification or Standard Document (PDF/URL)]()  

- Class Lecture ([Link]())