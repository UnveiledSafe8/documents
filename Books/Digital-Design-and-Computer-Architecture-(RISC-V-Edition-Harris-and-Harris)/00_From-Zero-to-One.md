---
title: 00_From-Zero-to-One
description: First chapter
published: true
date: 2025-07-14T04:02:45.524Z
tags: 
editor: markdown
dateCreated: 2025-07-10T01:49:10.799Z
---

# Chapter 0: From Zero To One
---


## Summary
---
> 


## 0.0 The Game Plan
---
### Key Concepts
- **The book’s educational journey**:
  - Starts with logic gates → builds to modules → explores assembly language → culminates in building a microprocessor.
- **Managing Complexity**
  - Key to digital design is handling systems too complex to fully visualize at once.
### Definitions
- **Digital System**
  - A system that processes discrete values (typically binary) rather than continuous signals.
- **Logic Gate**
  - A basic building block of digital circuits that performs a logical operation on one or more binary inputs.
- **Assembly Language**
  - A low-level programming language that is closely tied to a processor’s instruction set.
### Visual Aids
| Levels of Abstraction |
| - |
| Application Software |
| Operating Systems |
| Architecture |
| Micro-architecture |
| Logic |
| Digital Circuits |
| Analog Circuits |
| Devices |
| Physics |
### Notable Quotes
> "A microprocessor may be the first system that you build that is too complex to fit in your head all at once."
### Common Pitfalls
- Underestimating the importance of abstraction in digital system design.
- Assuming deep physics or math knowledge is required to design microprocessors.
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 1–2


## 0.1 The Art of Managing Complexity
---
### Key Concepts
- **Abstraction**
  - Hiding irrelevant details by viewing a system at different levels, so complexity becomes manageable.
- **Discipline**
  - Intentionally restricting design choices to work effectively at a higher abstraction level.
- **Hierarchy**
  - Breaking a system into nested modules or layers that are easier to understand and manage.
- **Modularity**
  - Designing components with well-defined functions and interfaces, allowing independent development and replacement without unintended side effects.
- **Regularity**
  - Promoting uniformity and reuse of modules to reduce unique components, simplifying design and manufacturing.
### Definitions
- **Abstraction**
  - The process of simplifying a complex system by focusing on important details while hiding the underlying complexity that is not immediately relevant.
- **Electrical Devices**
  - Basic components such as transistors and vacuum tubes that form the building blocks of circuits. They have defined connection points called terminals.
- **Terminals**
  - Physical connection points on an electrical device where voltages and currents are measured and applied.
- **Analog Circuits**
  - Circuits that process continuous voltage levels, representing a range of values rather than discrete states.
- **Digital Circuits**
  - Circuits that operate on discrete voltage levels (typically representing binary 0 and 1).
- **Micro-Architecture**
  - The implementation of a processor’s architecture via specific logic circuits and organization, determining performance and efficiency.
- **Architecture**
  - The abstract, programmer-visible structure and behavior of a computer system, including instruction sets and registers.
- **Discipline**
  - The practice of limiting design choices to standardize components and simplify complex system design and production.
- **Hierarchy**
  - A layered organization where a complex system is decomposed into subsystems, which are further subdivided recursively.
- **Modularity**
  - The design principle of creating components with clear, stable interfaces and well-defined functionality.
- **Regularity**
  - The principle of designing similar or identical components to be reused throughout a system, facilitating mass production and maintainability.
### Examples
**Political Abstraction Levels**
**Problem:**
How to understand voting patterns across a country with many regions and cities?
**Solution:**
Use abstraction levels — politicians focus on states rather than individual counties or cities to simplify decisions.

**Automobile Manufacturing and Managing Complexity**
**Problem:**
Building millions of cars quickly with interchangeable parts.
**Solution:**
Use hierarchy (breaking cars into subsystems), modularity (standardized parts with well-defined interfaces), and regularity (mass-produced identical components like nuts and bolts).
### Notable Quotes
> “No human being could understand modern digital systems by tracking individual electrons. The key is managing complexity.”

> “Discipline restricts design choices to enable building large, reliable systems.”
### Common Pitfalls
- Ignoring the importance of discipline, leading to chaotic, unmaintainable designs.
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 2–5


## 0.2 The Digital Abstraction
---
### Key Concepts
- **Digital Systems**:
  - Systems that process information using discrete values.
- **Digital Logic**
  - Logic on binary variables.
  - 1=TRUE=HIGH.
  - 0=FALSE=LOW.
### Definitions
- **Continous Variables**
  - Variables with infinite values.
- **Discrete Variables**
  - Variables with discrete values.
- **Bit**
  - Binary digit.
- **Boolean Logic**
  - Logic on binary variables.
- **Digital Abstraction**
  - Abstracting from hardware implementation to underlying digital logic.
### Formulas
**Amount of Information in Discrete Variable**
N states lead to D bits of information.
$$
D = \log_{2}\left(N\right) {bits}
$$
### Examples
**The Analytical Engine**
**Problem:**
How to perform logic using mechnical operations.
**Solution:**
Use rows of gears with discrete values (0–9) to represent individual digits, allowing mechanical logic.
### Notable Quotes
> “The beauty of the digital abstraction is that digital designers can
focus on 1’s and 0’s, ignoring whether the Boolean variables are physically
represented with specific voltages, rotating gears, or even hydraulic fluid
levels."
### Common Pitfalls
- While continuous variables theoretically carry infinite information, real-world limitations like measurement error mean they effectively carry only ~16 bits of usable information.
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 5–7


## 0.3 Numer Systems
---
### Key Concepts
- **Sign/Magnitude Binary**:
  - The most significant bit indicates sign; magnitude remains unchanged.
  - Addition of binary breaks down
- **Two's Complement Binary**:
  - Significant bit maintains its weight but is negative.
  - Addition of binary holds.
  - Subtraction is possible by inverting subtracted number.
- **Reverting Sign Method**
  - Method to reverse the sign of a Two's complement binary number.
  - Inversion is slightly more complex than Sign/Magnitude, invert all bits and add $1_2$.
- **One's Complement**
  - Inverting all digits in binary
### Definitions
- **Number System Base**
  - Number of unique digits
- **Decimal Number**
  - Base 10 number system (0-9)
- **Binary Number**
  - Base 2 number system (0, 1)
- **Hexadecimal Number**
  - Base 16 number system (0-9, A-F)
- **Range**
  - Total unique numbers representable by amount of digits in some number system
- **Weight**
  - Implied value of a digit by position such as $11_{10} = 1 \times 10^1 + 1 \times 10^0$.
- **Byte**
  - 8-bit group
- **Nibble**
  - 4-bit group
- **Word**
  - Varied bit size data chunk handled by microprocessor e.g. 64-bit
- **Least Significant Bit**
  - First digit bit
- **Most Significant Bit**
  - Last digit bit
- **Least Significant Byte**
  - First byte in a group
- **Most Significant Byte**
  - Last byte in a group
- **Overflow**
  - Summation of numbers higher than available digits
- **Signed Binary**
  - Binary system inclusive of negative numbers
- **Counterpart**
  - Same magnitude opposite sign binary number
- **Weird Number**
  - Highest magnitude negative number of two's complement binary number which has no counterpart.
- **Sign Extension**
  - Expanding Two's complement binary number's digits without changing the value by simply copying the sign bit
### Formulas
**Range**
Unique numbers representable by base, b, of a number system and N digits.
$$
b^N
$$
### Visual Aids
| 1-Bit | 2-Bit | 3-Bit | 4-Bit | Decimal |
| - | - | - | - | - |
| 0 | 00 | 000 | 0000 | 0 |
| 1 | 01 | 001 | 0001 | 1 |
|  | 10 | 010 | 0010 | 2 |
|  | 11 | 011 | 0011 | 3 |
|  |  | 100 | 0100 | 4 |
|  |  | 101 | 0101 | 5 |
|  |  | 110 | 0110 | 6 |
|  |  | 111 | 0111 | 7 |
|  |  |  | 1000 | 8 |
|  |  |  | 1001 | 9 |
|  |  |  | 1010 | 10 |
|  |  |  | 1011 | 11 |
|  |  |  | 1100 | 12 |
|  |  |  | 1101 | 13 |
|  |  |  | 1110 | 14 |
|  |  |  | 1111 | 15 |


| Hexadecimal Digit | Decimal | Binary |
| - | - | - |
| 0 | 0 | 0000 |
| 1 | 1 | 0001 |
| 2 | 2 | 0010 |
| 3 | 3 | 0011 |
| 4 | 4 | 0100 |
| 5 | 5 | 0101 |
| 6 | 6 | 0110 |
| 7 | 7 | 0111 |
| 8 | 8 | 1000 |
| 9 | 9 | 1001 |
| A | 10 | 1010 |
| B | 11 | 1011 |
| C | 12 | 1100 |
| D | 13 | 1101 |
| E | 14 | 1110 |
| F | 15 | 1111 |


| Symbol | Name | Amount |
| - | - | - |
| KB OR KiB | Kilobyte OR Kibibyte | $2^{10}$ bytes |
| Kb OR Kbit | Kilobit OR Kibibit | $2^{10}$ bits |
| MB OR MiB | Megabyte OR Mibibyte | $2^{20}$ bytes |
| Mb OR Mbit | Megabit OR Mibibit | $2^{20}$ bits |
| GB OR GiB | Gigabyte OR Gibibyte | $2^{30}$ bytes |
| Gb OR Gbit | Gigabit OR Gibibit | $2^{30}$ bits |


| System | Range |
| - | - |
| Unsigned | \[0, $2^{N}-1$\]
| Two's Complement | \[$-2^{N-1}$, $2^{N-1}-1$\] |
| Sign/Magnitude | \[$-2^{N-1} + 1$, $2^{N-1}-1$\] |
### Examples
**Convert binary to decimal**
**Problem:**
Convert $10110_2$ to decimal.
**Solution:**
$$
10110_2 = 1 * 2^4 + 0 * 2^3 + 1 * 2^2 + 1 * 2^1 + 0 * 2^0 = 22_{10}
$$
**Convert decimal to binary**
**Problem:**
Convert $84_{10}$ to binary.
**Solution:**
$$
84_{10} = 1 * 2^6 + 0 * 2^5 + 1 * 2^4 + 0 * 2^3 + 1 * 2^2 + 0 * 2^1 + 0 * 2^0 = 1010100_2
$$
**Convert hexadecimal to binary and decimal**
**Problem:**
Convert $2ED_{16}$ to binary and decimal.
**Solution:**
$$
2ED_{16} = 1 * 2^9 + 0 * 2^8 + 1 * 2^7 + 1 * 2^6 + 1 * 2^5 + 1 * 2^4 + 1 * 2^3 + 1 * 2^2 + 0 * 2^1 + 1 * 2^0
$$
$$
= 1011111101_2 = 749_{10}
$$
**Binary addition**
**Problem:**
Add $1011_2$ and $0101_2$.
**Solution:**
$$
1011_2 + 0101_2 = 1110_2
$$
**Binary overflow**
**Problem:**
Add $1101_2$ and $0101_2$ with four reserved digits.
**Solution:**
$$
1101_2 + 0101_2 = 0010_2
$$
**Sign/Magnitude Binary**
**Problem:**
Represent $-5_{10}$ and $5_{10}$ using Sign/Magnitude Binary.
**Solution:**
$$
-5_{10} = 1101_2
$$
$$
5_{10} = 0101_2
$$
**Revert Sign of Two's Complement Binary Number**
**Problem:**
Flip the sign of $2_{10} = 0010_2$.
**Solution:**
$$
0010_2 \Rightarrow 1110_2
$$
**Sign Extension Two's Complement**
**Problem:**
Extend $1101_2$.
**Solution:**
$$
1101_2 = 1111101_2
$$
### Notable Quotes
> “You are accustomed to working with decimal numbers. In digital systems consisting of 1’s and 0’s, binary or hexadecimal numbers are often more convenient. "
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 7–17


## 0.4 Logic Gates
---
### Key Concepts
- **Logic Gates**:
  - Digital circuits that take binary input and produce a binary output.
  - Input is typically represented on the left or top of gate symbol.
  - Output is typically represented on the right or bottom of gate symbol.
- **Truth Table**
  - Relationship table of rows for each possible truthy combination of inputs to output.
- **Boolean Expression**
  - Mathamatical expression with boolean variables.
- **Boolean Variable**
  - Represents True or False
  - If representing input, the letter is usually at the beggining of the alphabet
  - If representing output, the letter is usually Y.
### Definitions
- **Bubble**
  - Inversion symbol, a circle, added to the output of inverted gates.
- **Parity Gate**
  - N-input XOR gate.
  - True whenever an odd number of inputs are true.
- **N-input AND gate**
  - True when all N inputs are true.
- **N-input OR Gate**
  - True when some input is true.
### Visual Aids
#### NOT Gate / Inverter
![not_gate.drawio.svg](/not_gate.drawio.svg)


| A | Y |
| - | - |
| 0 | 1 |
| 1 | 0 |


$$
Y = \neg A
$$
#### BUF Gate / Buffer
![buf_gate.drawio.svg](/buf_gate.drawio.svg)


| A | Y |
| - | - |
| 0 | 0 |
| 1 | 1 |


$$
Y = A
$$
#### AND Gate
![and_gate.drawio.svg](/and_gate.drawio.svg)


| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |


$$
Y = A \wedge B
$$
#### OR Gate
![or_gate.drawio.svg](/or_gate.drawio.svg)


| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |


$$
Y = A \vee B
$$
#### XOR Gate
![xor_gate.drawio.svg](/xor_gate.drawio.svg)


| A | B | Y |
| - | - | - |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |


$$
Y = A \oplus B
$$
#### NAND Gate
![nand_gate.drawio.svg](/nand_gate.drawio.svg)


| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |


$$
Y = \neg\left(A \wedge B \right)
$$
#### NOR Gate
![nor_gate.drawio.svg](/nor_gate.drawio.svg)


| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 0 |


$$
Y = \neg\left(A \vee B \right)
$$
#### XNOR Gate
![xnor_gate.drawio.svg](/xnor_gate.drawio.svg)


| A | B | Y |
| - | - | - |
| 0 | 0 | 1 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |


$$
Y = \neg\left(A \oplus B \right)
$$
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 17–20


## 0.5 Beneath The Digital Abstraction
---
### Key Concepts
- **Logic Levels**:
  - Maps continous variables to discrete.
  - Driver sends to a receiver
- **DC Transfer Characteristics**
  - Graph of gate output voltage as a function of input voltage.
- **Static Discipline**
  - Given logically valid inputs, the gate produces logically valid outputs.
- **Logic Family**
  - All gates in a group that obey static discipline with other members.
  - Consistent logic levels and $V_{DD}$.
### Definitions
- **Ground**
  - Abbreivated as GND
  - Usually 0V in DC circuits
- **Supply Voltage**
  - Abbreivated as $V_{DD}$
  - Maximum voltage applied to circuit.
- **Noise Margin**
  - Abbreivated as $NM_L$ for low voltage noise margin or $NM_H$ for high voltage noise margin.
  - Amount of noise that can be added to a worst-case output with the signal still being capable of being interpreted as valid input.
- **Logic High Output Range**
  - The difference between $V_{DD}$ and high voltage level of driver, $V_{OH}$.
- **Logic Low Output Range**
  - The difference between GND and low voltage level of driver, $V_{OL}$.
- **Logic High Input Range**
  - The difference between $V_{DD}$ and high voltage level of receiver, $V_{IH}$.
- **Logic Low Input Range**
  - The difference between GND and low voltage level of receiver, $V_{IL}$.
- **Forbidden Zone**
  - Values between $V_{IH}$ and $V_{IL}$ that exceed noise margin.
  - Usually leads to unexpected results.
- **Unity Gain Pointer**
  - Points where slope of transfer characteristics is -1.
  - Usually maximizes noise margins.
### Formulas
**High Voltage Noise Margin**
High voltage noise margin between driver and receiver.
$$
NM_H = V_{OH} - V_{IH}
$$
**Low Voltage Noise Margin**
Low voltage noise margin between driver and receiver.
$$
NM_L = V_{OL} - V_{IL}
$$
### Visual Aids
![noise_margins.png](/noise_margins.png)
![dc_transfer_characteristics_and_logic_levels.jpg](/dc_transfer_characteristics_and_logic_levels.jpg)
| Logic Family | $V_{DD}$ | $V_{IL}$ | $V_{IH}$ | $V_{OL}$ | $V_{OH}$ |
| - | - | - | - | - | - |
| TTL | 5V | 0.8V | 2V | 0.4V | 2.4V |
| CMOS | 5V | 1.35V | 3.15V | 0.33V | 3.84V |
| LVTTL | 3.3V | 0.8V | 2V | 0.4V | 2.4V |
| LVCMOS | 3.3V | 0.9V | 1.8V | 0.36V | 2.7V |
### Notable Quotes
> “A digital system uses discrete-valued variables. However, the variables
are represented by continuous physical quantities, such as the voltage on
a wire, the position of a gear, or the level of fluid in a cylinder."
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 20–24


## 0.6 CMOS Transistors
---
### Key Concepts
- **Semiconductor**:
  - Conductivity largely dependent on dopant concentration.
  - Silicon is the primary semiconductor used, forming a crystalline lattice with covalent bonds.
  - Pure silicon is a poor conductor because electrons are bound in bonds.
  - Conductivity improved by doping with impurity atoms.
- **Dopant**
  - An impurity atom added to semiconductor to modify its electrical properties.
  - n-type dopants (e.g., arsenic): add extra electrons that increase negative charge carriers.
  - p-type dopants (e.g., boron): create "holes" (missing electrons) that act as positive charge carriers.
### Definitions
- **Transistor**
  - Electrically controlled switches that turn ON or OFF when a voltage or
current is applied to a control terminal.
- **Bipolar Junction Transistor (BJT)**
- **Metal-Oxide-Semiconductor Field Effect Transistor (MOSFETS)**
- **Diode**
  - Junction between p-type and n-type silicon.
  - Has an anode (p-type) and cathode (n-type).
  - Allows current flow only when forward biased (anode voltage > cathode voltage).
  - Blocks current when reverse biased.
- **Capacitor**
  - Two conductors separated by an insulator.
  - Stores charge
  - Larger conductor area and smaller separation increase capacitance.
  - Important for timing and energy considerations in circuits.
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
> “MOSFETs are now the building blocks of almost all digital systems."
### Common Pitfalls
- Pitfall 1.
### Related Links
- [Link]()
### References
- *Digital Design and Computer Architecture* — Chapter 1, Pages 24–32


## 0.7 Subsection Title
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