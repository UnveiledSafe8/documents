---
title: 03_Hardware-Description-Langauges
description: 
published: true
date: 2025-07-20T03:32:33.027Z
tags: 
editor: markdown
dateCreated: 2025-07-20T03:32:33.027Z
---

# Chapter 3: Hardware Description Languages
---
## Summary
---
> ""


## 3.0 Introduction
---
### Key Concepts
- **Hardware Description Language (HDL)**:
  - Specifications given to CAD tools for optimized gates.
  - Leading languages is VHDL and SystemVerilog.
### Definitions
- **Module**
  - Block of hardware with inputs and outputs.
  - Functionality described using behavioural or strutural techniques.
- **Netlist**
  - Produced by a synthesis tool describing the hardware.
- **Idiom**
  - Specific ways to describe a class of logic in a HDL.
### Code Snippets
**Combinational Logic SystemVerilog**
Describe a module's behaviour where $y=\left(\neg a \wedge \neg b \wedge \neg c \right) \lor \left(a \wedge \neg b \wedge \neg c \right) \lor \left(a \wedge \neg b \wedge c \right)$.
```systemverilog
module sillyfunction(input logic a, b, c,
											output logic y);
	assign y = ~a & ~b & ~c |
  						a & ~b & ~c |
              a & ~b & c;
endmodule
```
### Visual Aids
#### Simulation WaveForms Using VHDL
![simulation-waves_hdl.png](/simulation-waves_hdl.png)

### Notable Quotes
> “However, the vast majority of commercial systems are now built using HDLs rather than schematics."
### References
- *Digital Design and Computer Architecture* — Chapter 4, Pages 171–175


## 3.1 Combinational Logic
---
### Key Concepts
- **Concept Name**:
  - Subpoint or clarification.
### Definitions
- **Bitwise Operator**
  - Acts on single single-bit signals or multibit busses.
- **Little-Endian Order**
  - Least singificant bit has smallest bit number.
- **Big-Endian Order**
  - Most singificant bit has smallest bit number.
- **Big Swizzling**
  - Operate on a subset of bus or concatenate signals to form busses.
### Code Snippets
**Inverter**
Inverts a 4-bit bus.
```systemverilog
module inv(input logic [3:0] a,
						output logic [3:0] y);
	assign y = ~a;
endmodule
```
**Logic Gates**
Performs multiple logic gate functions on two inputs.
```systemverilog
module gates(input logic [3:0] a, b,
							output logic [3:0] y1, y2,
																	y3, y4, y5);
	/* five different two-input logic 
	gates acting on 4-bit busses */
	assign y1 = a & b; // AND
	assign y2 = a | b; // OR
	assign y3 = a ^ b; // XOR
	assign y4 = ~(a & b); // NAND
	assign y5 = ~(a | b); // NOR
endmodule
```
**Eight-Input AND**
Perform reduced operation of multi-input AND.
```systmeverilog
module and8(input logic [7:0] a,
						output logic y);
	assign y =&a;
	// &a is much easier to write than
	// assign y = a[7] & a[6] & a[5] & a[4] &
	// a[3] & a[2] & a[1] & a[0];
endmodule
```
**2:1 Multiplexer**
Create a 2:1 multiplexer operating on 4 bits of data.
```systmeverilog
module mux2(input logic [3:0] d0, d1,
						input logic s,
						output logic [3:0] y);
	assign y = s ? d1 : d0;
endmodule
```
**4:1 Multiplexer**
Create a 4:1 multiplexer operating on 4 bits of data.
```systemverilog
module mux4(input logic [3:0] d0, d1, d2, d3,
						input logic [1:0] s,
						output logic [3:0] y);
	assign y = s[1] ? (s[0] ? d3 : d2)
									: (s[0] ? d1 : d0);
endmodule
```
**Full Adder**
Create a full adder using internal variables.
```systemverilog
module fulladder(input logic a, b, cin,
									output logic s, cout);
	logic p, g;
	assign p = a ^ b;
	assign g = a & b;
  
  assign s = p ^ cin;
	assign cout = g | (p & cin);
endmodule
```
**Tristate Buffer**
Create a tristate buffer using a floating number.
```systemverilog
module tristate(input logic [3:0] a,
								input logic en,
								output tri [3:0] y);
	assign y = en ? a : 4'bz;
endmodule
```
**Bus Concatenation**
Create a bus.
```systemverilog
assign y = {c[2:1], {3{d[0]}}, c[0], 3'b101};
```
**Logic Gates With Delays**
Create logic gates again but with delays for debugging purposes.
```systemverilog
'timescale 1ns/1ps
module example(input logic a, b, c,
								output logic y);
	logic ab, bb, cb, n1, n2, n3;
	assign #1 {ab, bb, cb} = ~{a, b, c};
	assign #2 n1 = ab & bb & cb;
	assign #2 n2 = a & bb & cb;
	assign #2 n3 = a & bb & c;
	assign #4 y = n1 | n2 | n3;
endmodule
```
### Visual Aids
![systemverilog_operators.png](/systemverilog_operators.png)

![systemverilog_numbers.png](/systemverilog_numbers.png)

![systemverilog_input-resolve.png](/systemverilog_input-resolve.png)

### References
- *Digital Design and Computer Architecture* — Chapter 4, Pages 175–188


## 3.2 Structural Modeling
---
### Definitions
- **Instance**
  - Copy of a module.
### Code Snippets
**Structural Model 4:1 Multiplexer**
Create a 4:1 multiplexer using instances of mux2 2:1 multiplexer.
```systemverilog
module mux4(input logic [3:0] d0, d1, d2, d3,
						input logic [1:0] s,
						output logic [3:0] y);
	logic [3:0] low, high;
	mux2 lowmux(d0, d1, s[0], low);
	mux2 highmux(d2, d3, s[0], high);
	mux2 finalmux(low, high, s[1], y);
endmodule
```
**Structural Model of 2:1 Multiplexer**
Create a 2:1 multiplexer from tristate buffers.
```systemverilog
module mux2(input logic [3:0] d0, d1,
						input logic s,
						output tri [3:0] y);
	tristate t0(d0, ~s, y);
	tristate t1(d1, s, y);
endmodule
```
**8-bit Wide 2:1 Multiplexer**
Create 2:1 multiplexer from two 4-bit 2:1 multiplexers.
```systemverilog
module mux2_8(input logic [7:0] d0, d1,
							input logic s,
							output logic [7:0] y);
	mux2 lsbmux (d0[3:0], d1[3:0], s, y[3:0]);
	mux2 msbmux(d0[7:4], d1[7:4], s, y[7:4]);
endmodule
```
### References
- *Digital Design and Computer Architecture* — Chapter 4, Pages 188–191


## 3.3 Sequential Logic
---
### Code Snippets
**Flip-Flop**
Description.
```systemverilog
module flop(input logic clk,
						input logic [3:0] d,
						output logic [3:0] q);
	always_ff @(posedge clk)
		q <= d;
endmodule
```
**Resetabble-Register**
Create a resetabble register for both async and sync use.
```systemverilog
module flopr(input logic clk,
							input logic reset,
							input logic [3:0] d,
							output logic [3:0] q);
	// asynchronous reset
	always_ff @(posedge clk, posedge reset)
		if (reset) q <= 4'b0;
		else q <= d;
endmodule
module flopr(input logic clk,
							input logic reset,
							input logic [3:0] d,
							output logic [3:0] q);
	// synchronous reset
	always_ff @(posedge clk)
		if (reset) q <= 4'b0;
		else q <= d;
endmodule
```
**Resettable Enabled Register**
Create a resettable enabled async register.
```systemverilog
module flopenr(input logic clk,
								input logic reset,
								input logic en,
								input logic [3:0] d,
								output logic [3:0] q);
	// asynchronous reset
	always_ff @(posedge clk, posedge reset)
		if (reset) q <= 4'b0;
		else if (en) q <= d;
endmodule
```
**Synchronizer**
Create a synchronizer.
```systemverilog
module sync(input logic clk,
						input logic d,
						output logic q);
	logic n1;
	always_ff @(posedge clk)
		begin
			n1 <= d; // nonblocking
			q <= n1; // nonblocking
		end
endmodule
```
**D-Latch**
Create a d-latch.
```systemverilog
module latch(input logic clk,
							input logic [3:0] d,
							output logic [3:0] q);
	always_latch
		if (clk) q <= d;
endmodule
```
### References
- *Digital Design and Computer Architecture* — Chapter 4, Pages 191–196


## 3.4 More Combinational Logic
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