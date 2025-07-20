---
title: 01_Combinational-Logic-Design
description: 
published: true
date: 2025-07-15T22:17:14.560Z
tags: 
editor: markdown
dateCreated: 2025-07-14T04:04:55.779Z
---

# Chapter 1: Combinational Logic Design
---
## Summary
---
> "A digital circuit is a module with discrete-valued inputs and outputs and a specification describing the function and timing of the module. This chapter has focused on combinational circuits, whose outputs depend only on the current values of the inputs."
## 1.0 Introduction
---
### Key Concepts
- **Circuit**:
  - Network that processes discrete-valued variables.
- **Combinational Circuit**
  - Depends only on current input values.
  - Memoryless.
- **Sequential Circuit**
  - Dependent on input sequence.
  - Memory.
### Definitions
- **Element**
  - Essentially a black box.
- **Node**
  - Wire whose voltage conveys discrete-valued variables
- **Black Box**
  - Discrete input and output terminals.
  - Functional specification of relationship between inputs and outputs, usually boolean functions or truth table).
  - Timing specification describing delay between input to output change.
  - Contains elements and nodes (internal, input, output).
- **Impementation**
  - Logically equivalent circuits.
- **Bus**
  - Bundle of multiple signals usually indicated by a forward slash through a wire and optionally a number specifying number of lines.
- **Combinational Composition**
  - All elements combinational.
  - No cyclic paths.
  - Every node is input or connects to one output terminal.
### Visual Aids
#### Combinational Logic Circuit
![clc_example.png](/clc_example.png)

### Related Links
- [00_From-Zero-to-One](/Books/Digital-Design-and-Computer-Architecture-(RISC-V-Edition-Harris-and-Harris)/00_From-Zero-to-One#h-01-the-art-of-managing-complexity)
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 53–56


## 1.1 Boolean Equations
---
### Key Concepts
- **Sum of Products Canoical Form (SOP)**:
  - Sum of every minterm.
- **Product of Sums Canoical Form (POS)**:
  - Product of every maxterm.
### Definitions
- **Compliment**
  - Inverse of a variable.
- **Literal**
  - A variable and its complement.
- **True Form**
  - Variable.
- **Complement Form**
  - Compliment of a variable.
- **Product**
  - AND of 2+ literals.
- **Sum**
  - OR of 2+ literals.
- **Minterm**
  - Product involving all function inputs.
- **Maxterm**
  - Sum involving all function inputs.
- **Precedence**
  - Order of operations for boolean logic.
  - NOT > AND > OR
### Formulas
**Truth Table Row Count**
The number of rows to represent every combination of input in a truth table is a function of N input variables.
$$
2^N
$$
### Visual Aids
#### SOP
| A | B | Y | Minterm | Minterm Name |
| - | - | - | - | - |
| 0 | 0 | 0 | $\neg A \wedge \neg B$ | $m_0$ |
| 0 | 1 | 1 | $\neg A \wedge B$ | $m_1$ |
| 1 | 0 | 0 | $A \wedge \neg B$ | $m_2$ |
| 1 | 1 | 1 | $A \wedge B$ | $m_3$ |


$$
F(A,B) = \left(\neg A \wedge B \right) \lor \left(A \wedge B \right) = \sum\left(m_1, m_3 \right)
$$


#### POS
| A | B | Y | Maxterm | Maxterm Name |
| - | - | - | - | - |
| 0 | 0 | 0 | $A \lor B$ | $M_0$ |
| 0 | 1 | 1 | $A \lor \neg B$ | $M_1$ |
| 1 | 0 | 0 | $\neg A \lor B$ | $M_2$ |
| 1 | 1 | 1 | $\neg A \lor \neg B$ | $M_3$ |


$$
F(A,B) = \left(A \lor B \right) \wedge \left(\neg A \lor B \right) = \prod\left(M_0, M_3 \right)
$$
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 56–58


## 1.2 Boolean Algebra
---
### Key Concepts
- **Boolean Algebra**:
  - Algebra on boolean variables.
- **Duality**
  - If a theorem exists, interchanging the symbols 0 and 1 and operators $\wedge$ and $\lor$ still holds true.
- **Dual**
  - The theorem that forms by applying the concept of duality to a theorem usually notated by '.
- **Minimized**
  - Reducing SOP to have the fewer products or fewer literals in an equivalent expression.
### Definitions
- **Perfect Induction**
  - Proving a equivalence through bi-implication.
- **Prime Implicant**
  - Implicant that can not be combined with other implicants for a reduced expression.
- **Expanding**
  - Adding literals to an expression that is still equivalent to the original expression.
  - Can lead to better minimization when reduced after.
### Theorems & Proofs
#### Axioms
| Axiom | Dual | Name |
| - | - | - |
| $B=0$ if $B\neq 1$ | $B=1$ if $B\neq 0$ | Binary Field |
| $\neg 0 = 1$ | $\neg 1 = 0$ | NOT |
| $0 \wedge 0 = 0$ | $1 \lor 1 = 1$ | AND/OR |
| $1 \wedge 1 = 1$ | $0 \lor 0 = 0$ | AND/OR |
| $0 \wedge 1 = 1 \wedge 0 = 0$ | $1 \lor 0 = 0 \lor 1 = 1$ |AND/OR |


#### Single Variable
| Theorem | Dual | Name |
| - | - | - |
| $B \wedge 1 = B$ | $B \lor 0 = B$ | Identity |
| $B \wedge 0 = 0$ | $B \lor 1 = 1$ | Null Element |
| $B \wedge B = B$ | $B \lor B = B$ | Idempotency |
| $\neg \neg B + B$ | $\neg \neg B = B$ | Involution |
| $B \wedge \neg B = 0$ | $B \lor \neg B = 1$ | Complements |


#### Multiple Variables
| Theorem | Dual | Name |
| - | - | - |
| $B \wedge C = C \wedge B$ | $B \lor C = C \lor B$ | Commutavity |
| $\left(B\wedge C \right) \wedge D = B \wedge \left(C \wedge D \right)$ | $\left(B \lor C \right) \lor D = B \lor \left(C \lor D \right)$ | Associativity |
| $\left(B \wedge C \right) \lor \left(B \wedge D \right) = B \wedge \left(C \lor D \right)$ | $\left(B \lor C \right) \wedge \left(B \lor D \right) = B \lor \left(C \wedge D \right)$ | Distributivity |
| $B \wedge \left(B \lor C \right) = B$ | $B \lor \left(B \wedge C \right) = B$ | Covering |
| $\left(B \wedge C \right) \lor \left(B \wedge \neg C \right) = B$ | $\left(B \lor C \right) \wedge \left(B \lor \neg C \right) = B$ | Combining |
| $\left(B \wedge C \right) \lor \left(\neg B \wedge D \right) \lor \left(C \wedge D \right) = \left(B \wedge C \right) \lor \left(\neg B \wedge D \right)$ | $\left(B \lor C \right) \wedge \left(\neg B \lor D \right) \wedge \left(C \lor D \right) = \left(B \lor C \right) \wedge \left(\neg B \lor D \right)$ | Consensus |
| $\neg\left(\prod_{k=0}^{n}B_k \right) = \sum_{k=0}^{n}\neg B_k$ | $\neg\left(\sum_{k=0}^{n}B_k \right) = \prod_{k=0}^{n}\neg B_k$ | De Morgan |
### Examples
**Prove Commutavity**
**Problem:**
Prove the commutavity theorem.
**Solution:**
| $B$ | $C$ | $B \wedge C$ | $C \wedge B$ |
| - | - | - | - |
| 0 | 0 | 0 | 0 |
| 0 | 1 | 0 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 |
$$
B \wedge C \iff C \wedge B
$$
### Notable Quotes
> “Just as you use algebra to simplify mathematical
equations, you can use Boolean algebra to simplify Boolean equations."
### Common Pitfalls
- Not understanding the usefulness of expansion in minimization.
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 58–64


## 1.3 From Logic To Gates
---
### Key Concepts
- **Schematic**:
  - Diagram of a digital circuit.
- **Don't Cares**
  - Notated with an X in a truth table.
  - Signifies the irrelevance of an input in determining output for a specific sequence.
### Definitions
- **Schematic Guidelines**
  - Inputs should be placed on left or top.
  - Outputs should be placed on right or bottom.
  - Use straight wires rather than wires with many corners when possible.
  - Wires should connect at a T-junction.
  - When wires cross, a dot indicates that both wires should share a connection.
  - When wires cross, the absence of a dot indicates that both wires should not share a connection.
### Examples
**Minimize and Create a Schematic**
**Problem:**
The dean, the department chair, the teaching assistant, and the dorm social chair each use the auditorium from time to time. Unfortunately, they occasionally conflict, leading to disasters such as the one that occurred when the dean’s fundraising meeting with crusty trustees happened at the same time as the dorm’s BTB1 party. Alyssa P. Hacker has been called in to design a room reservation system.

The system has four inputs, A3, …, A0, and four outputs, Y3, …, Y0. These signals can also be written as A3:0 and Y3:0. Each user asserts her input when she requests the auditorium for the next day. The system asserts at most one output, granting the auditorium to the highest priority user. The dean, who is paying for the system, demands highest priority (3). The department chair, teaching assistant, and dorm social chair have decreasing priority.

Write a truth table and Boolean equations for the system. Sketch a circuit that performs this function.
**Solution:**
| $A_3$ | $A_2$ | $A_1$ | $A_0$ | $Y_3$ | $Y_2$ | $Y_1$ | $Y_0$ |
| - | - | - | - | - | - |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 | 0 | 0 | 1 | 0 |
| 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 0 | 1 | 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 | 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 | 0 | 1 | 0 | 0 |
| 1 | 0 | 0 | 0 | 1 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 1 | 1 | 0 | 0 | 0 |
| 1 | 1 | 0 | 0 | 1 | 0 | 0 | 0 |
| 1 | 1 | 0 | 1 | 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 0 | 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 | 1 | 0 | 0 | 0 |


| $A_3$ | $A_2$ | $A_1$ | $A_0$ | $Y_3$ | $Y_2$ | $Y_1$ | $Y_0$ |
| - | - | - | - | - | - |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 1 | 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | X | 0 | 0 | 1 | 0 |
| 0 | 1 | X | X | 0 | 1 | 0 | 0 |
| 1 | X | X | X | 1 | 0 | 0 | 0 |


$$
Y_3 = A_3
$$
$$
Y_2 = \neg A_3 \wedge A_2
$$
$$
Y_1 = \neg A_3 \wedge \neg A_2 \wedge A_1
$$
$$
Y_0 = \neg A_3 \wedge \neg A_2 \wedge \neg A_1 \wedge A_0
$$


![priority_circuit_schematic.png](/priority_circuit_schematic.png)
### Notable Quotes
> “Depending on the implementation technology, it may be cheaper to use
the fewest gates or to use certain types of gates in preference to others."
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 64–67


## 1.4 Multilevel Combinational Logic
---
### Key Concepts
- **Two-level Logic**:
  - Literals connected to a level of AND gates connected to a level of OR gates.
- **Multilevel Logic**
  - Literals connected via multiple levels.
- **Bubble Pushing**
  - Method for understanding circuits by inspection, especially those minimized.
### Definitions
- **Bubble Pushing Guidelines**
  - Begin at the output of the circuit and work toward the inputs.
  - Push any bubbles on the final output back toward the inputs so that you can read an equation in terms of the output instead of the complement of the output.
  - Working backward, draw each gate in a form so that bubbles cancel. If the current gate has an input bubble, draw the preceding gate with an output bubble. If the current gate does not have an input bubble, draw the preceding gate without an output bubble.
### Visual Aids
![three-input_xor.png](/three-input_xor.png)
![3-input_xor.png](/3-input_xor.png)
### Notable Quotes
> “Selecting the best multilevel implementation of a specific logic function is not a simple process. Moreover, 'best' has many meanings: fewest gates, fastest, shortest design time, least cost, least power consumption."
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 67–71


## 1.5 X's And Z's, Oh My
---
### Key Concepts
- **X**:
  - Unknown or illegal value in a circuit.
  - Indicates error.
- **Z**
  - Driving neither HIGH or LOW.
  - Not neccessarily an error.
  - Node is said to be floating/high impedance/high Z.
### Definitions
- **Contention**
  - Driving both 0 and 1 on the same node.
- **Active High Enable**
  - Input of 1 to enable enables tristate buffer as a standard buffer.
- **Active Low Enable**
  - Input of 0 to enable enables tristate buffer as a standard buffer.
- **Bus**
  - Node that carries signals from multiple sources.
  - Implicitly usually includes tristate buffers in configuration.
- **Point To Point Links**
  - Chips connected directly for communication.
  - Modern replacement over busses.
### Visual Aids
![contention.drawio.svg](/contention.drawio.svg)
#### Tristate Buffer
![tristate_buffer_high.drawio.svg](/tristate_buffer_high.drawio.svg)
| E | A | Y |
| - | - | - |
| 0 | 0 | Z |
| 0 | 1 | Z |
| 1 | 0 | 0 |
| 1 | 1 | 1 |
![tristate_buffer_low.drawio.svg](/tristate_buffer_low.drawio.svg)
| E | A | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | Z |
| 1 | 1 | Z |
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 71–73


## 1.6 Karnaugh Maps
---
### Key Concepts
- **Karnaugh Maps (K-maps)**:
  - Graphical representation of boolean equations for easy minimization.
  - Usually not used for more than four variables.
  - Utilizes gray code such that each adjacent square differs only by one variable value.
  - "Wraps" such that the table could be spherical and squares would still hold their adjacent properties.
- **Gray Code**
  - Adjusted binary order such that each adjacent number differs only by one digit.
  - For two digit number, the order follows: 00, 01, 11, 10.
### Definitions
- **K-Map Guide**
  - Use fewest circles necessary to cover all 1s.
  - All squares in each circle must contain 1s or Xs.
  - Each circle must span a rectangular block with dimensions of power 2 in each direction.
  - Each circle should be as large as possible.
  - A circle can wrap around edges.
  - A 1 in the map can be recircled if it leads to fewer or larger circles.
- **Don't Cares**
  - When applied to outputs, signfies that the outputs are unimportant or unreachable.
- **Logic Synthesizer**
  - Produce simplified circuits from description of basic function.
### Visual Aids
![seven-segment_display_decoder.png](/seven-segment_display_decoder.png)
### Examples
**Build a K-map**
**Problem:**
Turn this truth table into a k-map:
| A | B | C | Y |
| - | - | - | - |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |


**Solution:**
![k-map_example.drawio.svg](/k-map_example.drawio.svg)
![k-map_example_sop.drawio.svg](/k-map_example_sop.drawio.svg)

**Solve a K-map**
**Problem:**
Given this K-map, solve for the minimal equation:
![k-map_solver_example.drawio.svg](/k-map_solver_example.drawio.svg)

**Solution:**
![k-map_solved_circled_example.drawio.svg](/k-map_solved_circled_example.drawio.svg)

$$
Y = \neg B \lor \left(\neg C \wedge A \right)
$$
**Seven-Segment Display Decoder**
**Problem:**
A seven-segment display decoder takes a 4-bit data input $D_{3:0}$ and produces seven outputs to control light-emitting diodes to display a digit from 0 to 9. The seven outputs are often called segments a through g, or $S_a$–$S_g$.
Write a truth table for the outputs, and use K-maps to find Boolean equations for outputs $S_a$. Assume that illegal input values (10–15) produce a blank readout.
**Solution:**
| $V_{3:0}$ | $S_{g:a}$ |
| - | - |
| 0000 | 0111111 |
| 0001 | 0000110 |
| 0010 | 1011011 |
| 0011 | 1001111 |
| 0100 | 1100110 |
| 0101 | 1101101 |
| 0110 | 1111101 |
| 0111 | 0000111 |
| 1000 | 1111111 |
| 1001 | 1100111 |
| others | 0000000 |


![seven_decoder_k-map_solved.drawio.svg](/seven_decoder_k-map_solved.drawio.svg)

$$
S_a = \left(\neg V_1 \wedge V_3 \wedge \neg V_2 \right) \lor \left(\neg V_0 \wedge \neg V_1 \wedge \neg V_2 \right) \lor \left(V_0 \wedge V_2 \wedge \neg V_3 \right) \lor \left(V_1 \wedge \neg V_3 \right)
$$
**Seven-Segment Display Decoder With Don't Cares**
**Problem:**
A seven-segment display decoder takes a 4-bit data input $D_{3:0}$ and produces seven outputs to control light-emitting diodes to display a digit from 0 to 9. The seven outputs are often called segments a through g, or $S_a$–$S_g$.
Write a truth table for the outputs, and use K-maps to find Boolean equations for outputs $S_a$. Assume that illegal input values (10–15) produce a blank readout and use don't care values when possible.
**Solution:**
| $V_{3:0}$ | $S_{g:a}$ |
| - | - |
| 0000 | 0111111 |
| 0001 | 0000110 |
| 0010 | 1011011 |
| 0011 | 1001111 |
| 0100 | 1100110 |
| 0101 | 1101101 |
| 0110 | 1111101 |
| 0111 | 0000111 |
| 1000 | 1111111 |
| 1001 | 1100111 |
| others | xxxxxxx |


![seven-segement_k-map_solved_dont-cares.drawio.svg](/seven-segement_k-map_solved_dont-cares.drawio.svg)

$$
S_a = \left(\neg V_0 \wedge \neg V_2 \right) \lor \left(V_1 \right) \lor \left(V_3 \right) \lor \left(V_0 \wedge V_2 \right)
$$
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 73–81


## 1.7 Combinational Building Blocks
---
### Key Concepts
- **Multiplexer/MUX**:
  - Selects output from serveral inputs from select signal.
- **Lookup Table**
  - Stores predefined outputs for pre-programmed input combinations.
  - Can be built with MUX.
  - MUX lookup table size can be reduced by using one literal in input feed rather than just 1s and 0s. This reduces input size from $2^N$ to $2^{N-1}$.
  - Can also be built from decoders by combining with OR gates.
- **Decoder**
  - Takes N inputs and produces $2^N$ outputs for each possible bit combination from input.
  - Can be constructed from $2^N$ N-input AND gates for $N:2^N$ decoder.
### Definitions
- **Select Signal (Control Signal)**
  - Signal used to choose between multiple output sources.
- **Hot Output**
  - Current output from decoder input.
  - Only one output able to be "hot" at a time.
### Visual Aids
#### 2:1 Multiplexer
| $S$ | $B_1$ | $B_0$ | $Y$ |
| - | - | - | - |
| 0 | 0 | 0 | 0 |
| 0 | 0 | 1 | 1 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 1 |


![2-1-multiplexer_diagram.drawio.svg](/2-1-multiplexer_diagram.drawio.svg)

![2-1-multiplexer_k-map.drawio.svg](/2-1-multiplexer_k-map.drawio.svg)

$$
Y = \left(\neg S \wedge D_0 \right) \lor \left(S \wedge D_1 \right)
$$
![two-level-logic_2-1-multiplexer.drawio.svg](/two-level-logic_2-1-multiplexer.drawio.svg)

![tristate-buffer_2-1-multiplexer.drawio.svg](/tristate-buffer_2-1-multiplexer.drawio.svg)

#### 4:1 Multiplexer
![4-1-multiplexer_diagram.drawio.svg](/4-1-multiplexer_diagram.drawio.svg)

![4-1-multiplexer_2-1-multiplexers_diagram.drawio.svg](/4-1-multiplexer_2-1-multiplexers_diagram.drawio.svg)

#### 4:1 Multiplexer Representation Of AND
| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |


![4-1-multiplexer_and_diagram.drawio.svg](/4-1-multiplexer_and_diagram.drawio.svg)

| A | Y |
| - | - |
| 0 | 0 |
| 1 | B |


![24-1-multiplexer_reduced-and_diagram.drawio.svg](/24-1-multiplexer_reduced-and_diagram.drawio.svg)

#### 2:4 Decoder
| $A_{1:0}$ | $Y_{3:0}$ |
| - | - |
| 00 | 0001 |
| 01 | 0010 |
| 10 | 0100 |
| 11 | 1000 |


![2-4-decoder.drawio.svg](/2-4-decoder.drawio.svg)

#### 2:4 Decoder Representation Of XNOR
$$
Y = \neg\left(A \oplus B \right)
$$
![xnor_2-4-decoder.drawio.svg](/xnor_2-4-decoder.drawio.svg)

### Examples
**Create Lookup Table**
**Problem:**
Create a lookup table for $Y = \left(A \wedge \neg B \right) \lor \left(\neg B \wedge \neg C \right) \lor \left(\neg A \wedge B \wedge C \right)$.
First create the lookup using a 8:1 multiplexer, then reduce the circuit to a 4:1 multiplexer and an inverter.
**Solution:**
| A | B | C | Y |
| - | - | - | - |
| 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 1 |
| 1 | 0 | 1 | 1 |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | 0 |


![8-1-multiplexer_example_diagram.drawio.svg](/8-1-multiplexer_example_diagram.drawio.svg)

| A | B | Y |
| - | - | - |
| 0 | 0 | $\neg C$ |
| 0 | 1 | $C$ |
| 1 | 0 | 1 |
| 1 | 1 | 0 |


![8-1-multiplexer_example-reduced_diagram.drawio.svg](/8-1-multiplexer_example-reduced_diagram.drawio.svg)
### Notable Quotes
> “Combinational logic is often grouped into larger building blocks to build more complex systems."
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 81–86


## 1.8 Timing
---
### Key Concepts
- **Timing**:
  - Concerned with circuit runtime.
- **Timing Diagram**
  - Portrays transient response from input change.
- **Delay**
  - Usually a reference to propogation delay.
- **Reasons Why $t_{cd}$ Usually Is Not Equal To $t_{pd}$**
  - Some inputs or outputs have faster response times than others.
  - Speed influences from chip temperature.
  - Different rising and falling delays.
- **Combinational Circuit Time Properties**
  - Total propogation delay is the sum of propogation delays on critical path.
  - Total conamination delay is the sum of contamination delays on short path.
- **Glitch (Hazard)**
  - Single input transition causes several output transitions.
  - Typically not an issue if output is not needed while glitch is happening.
  - Usually happens when change in input results in different prime implication.
### Definitions
- **Rising Edge**
  - Signal change from LOW to HIGH.
- **Falling Edge**
  - Signal change from HIGH to LOW.
- **Propogation Delay**
  - Denoted by $t_{pd}$.
  - Maximum time for outputs to fully propogate from any input change.
- **Contamination Delay**
  - Denoted by $t_{cd}$.
  - Minimum time for any output to start transitioning from any input change.
- **Path**
  - Sequences of nodes passed through from input to output.
  - The critical path is the path with most cummulative propogation delay.
  - The short path is the path with least cummulative contamination delay.
- **Control Critical**
  - Critical path is from control signal.
- **Data Critical**
  - Critical path is from data signal.
### Visual Aids
#### Buffer Timing Diagram
![timing_diagram_simple.png](/timing_diagram_simple.png)

![timing_diagram_full.png](/timing_diagram_full.png)

#### Circuit Timing Diagram
![digital_circuit_example.png](/digital_circuit_example.png)

![digital_circuit_example_prop-delay.png](/digital_circuit_example_prop-delay.png)

![digital_circuit_example_cont-delay.png](/digital_circuit_example_cont-delay.png)

#### Glitch In Circuit
![glitch_digital_circuit_example.png](/glitch_digital_circuit_example.png)

![glitch_timing_diagram_example.png](/glitch_timing_diagram_example.png)

#### Fixing Glitch For Single Input Variable Change
![fixed_glitch_k-map.png](/fixed_glitch_k-map.png)

![new_digital_circuit_fixed_glitch.png](/new_digital_circuit_fixed_glitch.png)

### Notable Quotes
> “The best choice depends not only on the critical path through the circuit and the
input arrival times but also on the power, cost, and availability of parts."

> "However, simultaneous transitions on multiple inputs can also cause glitches. These glitches cannot be fixed by adding hardware. Because the vast majority of interesting systems have simultaneous (or near-simultaneous) transitions on multiple inputs, glitches are a fact of life in most circuits."
### References
- *Digital Design and Computer Architecture* — Chapter 2, Pages 86–93