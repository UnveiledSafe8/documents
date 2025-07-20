---
title: 02_Sequential-Logic-Design
description: 
published: true
date: 2025-07-19T20:17:32.844Z
tags: 
editor: markdown
dateCreated: 2025-07-16T17:29:35.991Z
---

# Chapter 2: Sequential Logic Design
---
## Summary
---
> "Describes the analysis and design of sequential logic."


## 2.0 Introduction
---
### Key Concepts
- **Sequential Logic**:
  - Explicitly remebers previous inputs or store in the state of the system.
  - Simplify design by building a synchronous circuit with only combintaional logic and banks of flip flops.
### Definitions
- **State Variables**
  - Set of bits.
  - Contain information about the past necessary to explain future behaviour.
- **State**
  - Store state variables.
### References
- *Digital Design and Computer Architecture* — Chapter 3, Pages 107–107


## 2.1 Latches And Flip-Flops
---
### Key Concepts
- **Bistable**:
  - Element with two stable states.
- **Cross-Coupled**
  - Two loigc gates feed into each others inputs.
  - Allows circuit to hold stable state.
- **Sync Resettable**
  - Bit only reset on clock edge.
- **Async Resettable**
  - Bit reset immediately.
### Definitions
- **Set**
  - Turn bit to True.
- **Reset**
  - Turn bit to False.
- **Transparent**
  - Data input flows to output as if passing through buffer.
  - Latch usually reaches this when CLK is HIGH.
- **Opaque**
  - Data input does not flows to output as if circuit is open.
  - Latch usually reaches this when CLK is LOW.
- **Transparent Latch (Level-Sensitive)**
  - Latch defined by the transparent and opaque properties.
- **Positive Edge-Triggered Flip-Flop**
  - Flip-FLop that stores data on falling edge until rising edge but does not output the change until rising edge.
- **Active Low**
  - Input produces function at value 0.
- **Active High**
  - Input produces function at value 1.
### Formulas
**Information In Latch**
The amount of information in bits stored in a N-stable states latch.
$$
\log_{2}N
$$
### Visual Aids
#### Bistable Cross-Coupled Inverters
![cross-coupled_inverters.png](/cross-coupled_inverters.png)

#### SR Latch
![sr-latch.png](/sr-latch.png)

![sr-latch_chip.png](/sr-latch_chip.png)

| $S$ | $R$ | $Q$ | $\neg Q$ |
| - | - | - | - |
| 0 | 0 | $Q_{PREV}$ | $Q_{PREV}$ |
| 0 | 1 | 0 | 1 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |


#### D Latch
![d-latch.png](/d-latch.png)

![d-latch_chip.png](/d-latch_chip.png)

| $CLK$ | $D$ | $\neg D$ | $S$ | $R$ | $Q$ | $\neg Q$ |
| - | - | - | - | - | - | - |
| 0 | $X$ | $\neg X$ | 0 | 0 | $Q_{PREV}$ | $Q_{PREV}$ |
| 1 | 0 | 1 | 0 | 1 | 0 | 1 |
| 1 | 1 | 0 | 1 | 0 | 1 | 0 |


#### D Flip-Flop
![d-flip-flop.png](/d-flip-flop.png)

![d-flip-flop_chip.png](/d-flip-flop_chip.png)

![d-flip-flop_chip_small.png](/d-flip-flop_chip_small.png)

#### Register
![4-bit_register.png](/4-bit_register.png)

![4-bit_regsiter_chip.png](/4-bit_regsiter_chip.png)

#### Enabled D Flip-Flop
![enabled-d-flip-flop_0.png](/enabled-d-flip-flop_0.png)

Glitch prone, avoid this specific design if possible.
![enabled-d-flip-flop_1.png](/enabled-d-flip-flop_1.png)

![enabled-d-flip-flop_chip.png](/enabled-d-flip-flop_chip.png)

#### Resettable D Flip-Flop
![reset-d-flip-flop.png](/reset-d-flip-flop.png)

![reset-d-flip-flop_chip.png](/reset-d-flip-flop_chip.png)

![reset-d-flip-flop_chip_small.png](/reset-d-flip-flop_chip_small.png)

### Examples
**Example Title**
**Problem:**
Apply the D and CLK inputs shown in the figure to a D latch and a D flip-flop. Determine the output Q for both devices.
![3_2_example_problem.png](/3_2_example_problem.png)

**Solution:**
![3_2_example_solution.png](/3_2_example_solution.png)

### Notable Quotes
> “Latches and flip-flops are the fundamental building blocks of sequential circuits."
### References
- *Digital Design and Computer Architecture* — Chapter 3, Pages 107–116


## 2.2 Synchronous Logic Design
---
### Key Concepts
- **Synchronous Sequential Circuit**
  - Contains discrete states.
  - Propogation delay from clock edge to output notated as $t_{pcq}$.
  - Contamination delay from clock edge to output notated as $t_{ccq}$.
  - $t_{setup}$ and $t_{hold}$ specify time durations inputs must be held stable.
- **Synchronous Sequential Circuit Composition**:
  - Every element is a combinational circuit or register.
  - There exists at least one register.
  - All registers synced to the same clock signal.
  - Every cyclic path contains at least one register.
### Definitions
- **Unstable**
  - Circuit with no stable states.
- **Ring Oscillator**
  - Oscillates between high and low output every certain period.
- **Race Condition**
  - Circuit failure or success dependent on gate delays.
- **Current State (State)**
  - Current system state usually notated as S.
- **Next State**
  - Next system state after clock cycle notated usually as S'.
### Visual Aids
#### Ring Oscillator
![ring-oscillator-circuit.png](/ring-oscillator-circuit.png)

![ring-oscillator_time-graph.png](/ring-oscillator_time-graph.png)

#### Race Conditions
![race-conditions_circuit.png](/race-conditions_circuit.png)

![race-condition_time-graph.png](/race-condition_time-graph.png)

#### States
![flip-flop_states.png](/flip-flop_states.png)

### Examples
**Synchronous Sequential Circuits**
**Problem:**
Determine if each circuit is a synchronous sequential circuit.
![syncvasync.png](/syncvasync.png)

**Solution:**
Circuit (a) is combinational, not sequential, because it has no registers. (b) is a simple sequential circuit with no feedback. (c) is neither a combinational circuit nor a synchronous sequential circuit because it has a latch that is neither a register nor a combinational circuit. (d) and (e) are synchronous sequential logic; they are two forms of finite state machines. (f) is neither combinational nor synchronous sequential because it has a cyclic path from the output of the combinational logic back to the input of the same logic but no register in the path. (g) is synchronous sequential logic in the form of a pipeline. (h) is not, strictly speaking, a synchronous sequential circuit, because the second register receives a different clock signal than the first, delayed by two inverter delays.
### Notable Quotes
> “By disciplining ourselves to synchronous sequential circuits, we can develop easy, systematic ways to analyze and design sequential systems."

> "Asynchronous design in theory is more general than synchronous design because the timing of the system is not limited by clocked registers. Just as analog circuits are more general than digital circuits because analog circuits can use any voltage, asynchronous circuits are more general than synchronous circuits because they can use any kind of feedback."
### References
- *Digital Design and Computer Architecture* — Chapter 3, Pages 117–121


## 2.3 Finite State Machines
---
### Key Concepts
- **Finite State Machine (FSM)**:
  - Form of synchronous sequential circuit with $2^k$ states for k registers.
  - Systematic approach to sequential circuit design with general flow from input logic to registers to output logic.
  - Synced to clock with optional reset.
- **Moore Machine**
  - Output loigc utilizes only current state.
- **Mealy Machine**
  - Output logic utilizes current state and current input.
- **Factoring**
  - Designing complex FSMs by reducing to multiple interacting FSMs.
- **Deriving FSM From Schematic**
  - Examine circuit, stating inputs, outputs, and state bits.
  - Write next state and output equations.
  - Create next state and output tables.
  - Reduce the next state table to eliminate unreachable states.
  - Assign each valid state bit combination a name.
  - Rewrite next state and output tables with state names.
  - Draw state transition diagram.
  - State in words what the FSM does.
- **FSM Design Procedure**
  - Identify the inputs and outputs.
  - Sketch a state transition diagram.
  - Write a state transition table and output table.
  - Select state encodings—your selection affects the hardware design.
  - Write Boolean equations for the next state and output logic.
  - Sketch the circuit schematic.
### Definitions
- **State**
  - A stable value capabale of being held.
  - Represented by usually $Sk$ for kth state or $S'k$ when referencing next state, not to be confused with $S_k$ which usually represents a state bit in the encoding.
- **State Transition Diagram**
  - Abstract flow model of FSM states.
- **State Transition Table**
  - Table relationship between next state output and inputs with current state.
- **Output Table**
  - Table relationship between current state with input depending on FSM type and output.
- **Binary Encoding**
  - Representing states in binary numbers.
- **One-Hot Encoding**
  - Representing states with respective digits in a binary number.
- **One-Cold Encoding**
  - Similar to One-hot except bits are inversed.
### Visual Aids
#### Moore Machine
![moore-machine.png](/moore-machine.png)

#### Mealy Machine
![mealy-machine.png](/mealy-machine.png)

### Examples
**Traffic Control**
**Problem:**
Invent a traffic light controller for intersection on a campus. You will have access to traffic sensors $T_A$ and $T_B$ corresponding to the respective lights in the intersection diagram.
![intersection_example.png](/intersection_example.png)

**Solution:**
![traffic-controller_black-box.png](/traffic-controller_black-box.png)

![transition_diagram_traffic.png](/transition_diagram_traffic.png)

| $S$ | $T_A$ | $T_B$ | $S'$ |
| - | - | - | - |
| S0 | 0 | X | S1 |
| S0 | 1 | X | S0 |
| S1 | X | X | S2 |
| S2 | X | 0 | S3 |
| S2 | X | 1 | S2 |
| S3 | X | X | S0 |


| State | Encoding |
| - | - |
| S0 | 00 |
| S1 | 01 |
| S2 | 10 |
| S3 | 11 |


| $S_{1:0}$ | $T_A$ | $T_B$ | $S'_{1:0}$ |
| - | - | - | - |
| 00 | 0 | X | 01 |
| 00 | 1 | X | 00 |
| 01 | X | X | 10 |
| 10 | X | 0 | 11 |
| 10 | X | 1 | 10 |
| 11 | X | X | 00 |


$$
S'1 = S_1 \oplus S_2
$$
$$
S'0 = \left(\neg S_1 \wedge \neg S_0 \wedge \neg T_A \right) \lor \left(S_1 \wedge \neg S_0 \wedge \neg T_B \right)
$$
| Output | Encoding |
| - | - |
| green | 00 |
| yellow | 01 |
| red | 10 |


| $S_{1:0}$ | $L_{A_{1:0}}$ | $L_{B_{1:0}}$ |
| - | - | - |
| 00 | 00 | 10 |
| 01 | 01 | 10 |
| 10 | 10 | 00 |
| 11 | 10 | 01 |


$$
L_{A_1} = S_1
$$
$$
L_{A_0} = \neg S_1 \wedge S_0
$$
$$
L_{B_1} = \neg S_1
$$
$$
L_{B_0} = S_1 \wedge S_0
$$
![traffic-control_state-register.png](/traffic-control_state-register.png)

![traffic-control_input-logic.png](/traffic-control_input-logic.png)

![traffic-control_output-logic.png](/traffic-control_output-logic.png)

![traffic-control_timing-diagram.png](/traffic-control_timing-diagram.png)

**Divide-By-N Counter**
**Problem:**
A divide-by-N counter has one output and no inputs. The output Y is HIGH for one clock cycle out of every N. In other words, the output divides the frequency of the clock by N. Sketch circuit designs for such a counter using binary and one-hot state encodings. The waveform and state transitions are provided.
![divide-by-3_waveform.png](/divide-by-3_waveform.png)

![divider-by-3_transitions.png](/divider-by-3_transitions.png)

**Solution:**
| State | One-Hot | Binary | Y |
| - | - | - | - |
| S0 | 001 | 00 | 1 |
| S1 | 010 | 01 | 0 |
| S2 | 100 | 10 | 0 |


| Binary $S_{1:0}$ | $S'_{1:0}$ |
| - | - |
| 00 | 01 |
| 01 | 10 |
| 10 | 00 |


$$
S'_1 = \neg S_1 \wedge S_0
$$
$$
S'_0 = \neg S_1 \wedge \neg S_0
$$
$$
Y = \neg S_1 \wedge \neg S_0
$$
![divide-by-3_binary-encoding_circuit.png](/divide-by-3_binary-encoding_circuit.png)

| One-Hot $S_{2:0}$ | $S'_{2:0}$ |
| - | - |
| 001 | 010 |
| 010 | 100 |
| 100 | 001 |


$$
S'_2 = S_1
$$
$$
S'_1 = S_0
$$
$$
S'_0 = S_2
$$
$$
Y = S_0
$$
![divide-by-3_hot-encoding_circuit.png](/divide-by-3_hot-encoding_circuit.png)

**Moore Vs Mealy**
**Problem:**
Alyssa P. Hacker owns a pet robotic snail with an FSM brain. The snail crawls from left to right along a paper tape containing a sequence of 1’s and 0’s. On each clock cycle, the snail crawls to the next bit. The snail smiles when the last two bits that it has crawled over are 01. Design the FSM to compute when the snail should smile. The input A is the bit underneath the snail’s antennae. The output Y is TRUE when the snail smiles. Compare Moore and Mealy state machine designs. Sketch a timing diagram for each machine showing the input, states, and output as Alyssa’s snail crawls along the sequence 0100110111.
**Solution:**
#### Moore
![moore_transition_example.png](/moore_transition_example.png)

| $S_{1:0}$ | $A$ | $S'_{1:0}$ |
| - | - | - |
| 00 | 0 | 01 |
| 00 | 1 | 00 |
| 01 | 0 | 01 |
| 01 | 1 | 10 |
| 10 | 0 | 01 |
| 10 | 1 | 00 |


| $S_{1:0}$ | Y |
| - | - |
| 00 | 0 |
| 01 | 0 |
| 10 | 1 |


![moore_diagram_example.png](/moore_diagram_example.png)

#### Mealy
![screenshot_2025-07-19_at_10.27.18.png](/screenshot_2025-07-19_at_10.27.18.png)

| $S_{0}$ | $A$ | $S'_{0}$ | Y |
| - | - | - | - |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 1 |


![mealy_diagram_example.png](/mealy_diagram_example.png)

![moorevmealy_timing-graph.png](/moorevmealy_timing-graph.png)

**Factoring**
**Problem:**
Modify the traffic light controller to have a parade mode, which keeps the Bravado Boulevard light green while spectators and the band march to football games in scattered groups. The controller receives two more inputs: P and R. Asserting P for at least one cycle enters parade mode. Asserting R for at least one cycle leaves parade mode. When in parade mode, the controller proceeds through its usual sequence until $L_B$ turns green, then remains in that
state with $L_B$ green until parade mode ends.
First, sketch a state transition diagram for a single FSM. Then, sketch the state transition diagrams for two interacting FSMs. The Mode FSM asserts the output M when it is in parade mode. The Lights FSM controls the lights based on M and the traffic sensors.

![unfactored_traffic-control_black-box.png](/unfactored_traffic-control_black-box.png)

![factored_traffic-control_black-box.png](/factored_traffic-control_black-box.png)

**Solution:**
![unfactored_transition-diagram_traffic-light.png](/unfactored_transition-diagram_traffic-light.png)

![factored_transition-diagram_traffi-light0.png](/factored_transition-diagram_traffi-light0.png)

![factored_transition-diagram_traffic-light1.png](/factored_transition-diagram_traffic-light1.png)

**Deriving FSM From Circuit**
**Problem:**
Derive FSM from provided circuit.
![circuit2fsm_example.png](/circuit2fsm_example.png)

**Solution:**
$$
Unlock = S_1
$$
$$
S'_1 = S_0 \wedge \neg A_1 \wedge A_0
$$
$$
S'_0 = \neg S_1 \wedge \neg S_0 \wedge A_1 \wedge A_0
$$
| $S_{1:0}$ | $A_{1:0}$ | $S'_{1:0}$ |
| - | - | - |
| 00 | 00 | 00 |
| 00 | 01 | 00 |
| 00 | 10 | 00 |
| 00 | 11 | 01 |
| 01 | 00 | 00 |
| 01 | 01 | 10 |
| 01 | 10 | 00 |
| 01 | 11 | 00 |
| 10 | 00 | 00 |
| 10 | 01 | 00 |
| 10 | 10 | 00 |
| 10 | 11 | 00 |
| 11 | 00 | 00 |
| 11 | 01 | 10 |
| 11 | 10 | 00 |
| 11 | 11 | 00 |


| $S_{1:0}$ | Unlock |
| - | - |
| 00 | 0 |
| 01 | 0 |
| 10 | 1 |
| 11 | 1 |


| S | A | S' |
| - | - | - |
| S0 | 0 | S0 |
| S0 | 1 | S0 |
| S0 | 2 | S0 |
| S0 | 3 | S1 |
| S1 | 0 | S0 |
| S1 | 1 | S2 |
| S1 | 2 | S0 |
| S1 | 3 | S0 |
| S2 | X | S0 |


| S | Unlock |
| - | - |
| S0 | 0 |
| S1 | 0 |
| S2 | 1 |


![circuit2fsm_transition-diagram.png](/circuit2fsm_transition-diagram.png)

### References
- *Digital Design and Computer Architecture* — Chapter 3, Pages 121–139


## 2.4 Timing Of Sequential Logic
---
### Key Concepts
- **Dynamic Discipline**:
  - Only changing signals outside aperture time.
- **Metastability**
  - Flip-Flop captures value between 0 and 1 resulting in infinite time to resolve.
  - Usually happens when input from a user happens during aperture time.
  - Can be prevented with a synchronizer.
- **Sequential Overhead**
  - Time in clock cycle needed for flip-flop propogation.
  - Constrains combinational logic delay or clock frequency.
- **Clock Skew**
  - Variation in clock edges from delays.
  - Notated as $t_{skew}$.
- **Synchronizer**
  - Recieves an asynchronous input and clock, then outputs within a bounded time.
  - Prevents output from being in a metastable position.
### Definitions
- **Sampling**
  - Flip-Flop fully copying input value to output.
- **Aperture Time**
  - $t_{setup} + t_{hold}$ time needed for input stability
- **Value At Clock Cycle**
  - Value of a signal at a certain clock cycle notated as A\[n\].
- **Clock Period**
  - Time between clock edges - $T_c$.
- **Clock Frequency**
  - $\frac{1}{T_c}$ - determined by clock period.
- **Metastable**
  - Holds value in forbidden zone.
  - Unbounded resolution time.
- **Resolution Time**
  - $t_{res}$, time needed for flip-flop to reach stable state.
  - If input change is outside aperture, $t_{res} = t_{pcq}$.
### Formulas
**Setup Time Constraint**
Must be met in sequential circuits, usually a limit either to clock period or combinational logic delay.
$$
T_c \ge t_{pcq} + t_{pd} + t_{setup} + t_{skew}
$$
**Hold Time Constraint**
Must be met in sequential circuits, usually a limit to short path contamination delay in combinational logic.
$$
t_{cd} \ge t_{hold} + t_{skew} - t_{ccq}
$$
**Resolve Time Probability**
Probability that resoluion time exceeds some abritrary time.
$$
P(t_{res} > t) = \frac{T_0}{T_c}e^{-\frac{t}{\tau}}
$$
**Synchronizer Failure**
Probability that resoluion time exceeds $T_c - t_{setup}$ on a synchronizer.
$$
P(failure)/sec = N * \frac{T_0}{T_c}e^{-\frac{T_c - t_{setup}}{\tau}}
$$
**Mean Time Between Failures**
Average time between metastable failure.
$$
MTBF = \frac{1}{P(failure)/sec}
$$
### Visual Aids
#### Sequential Circuit Timing Diagram
![sequential-circuit_timing-diagram.png](/sequential-circuit_timing-diagram.png)

#### Setup Time Constraint
![setup-time-constraint_example.png](/setup-time-constraint_example.png)

![setup-constraint-with-skew_example.png](/setup-constraint-with-skew_example.png)

#### Hold Time Constraint
![hold-time-constraint_example.png](/hold-time-constraint_example.png)

![hold-time-constraint-with-skew_example.png](/hold-time-constraint-with-skew_example.png)

#### Clock Skew
![clock-skew_example.png](/clock-skew_example.png)

#### Synchronizer
![synchronizer_black-box.png](/synchronizer_black-box.png)

![synchronizer_circuit_example.png](/synchronizer_circuit_example.png)

### Examples
**Timing Analysis**
**Problem:**
Flip-flops have a clock-to-Q contamination delay of 30 ps and a propagation delay of 80 ps. They have a setup time of 50ps and a hold time of 60 ps. Each logic gate has a propagation delay of 40 ps and a contamination delay of 25 ps. Determine the maximum clock frequency and whether any hold time violations could occur.
![timing-analysis_circuit.png](/timing-analysis_circuit.png)

**Solution:**
![timing-analysis_timing-diagram.png](/timing-analysis_timing-diagram.png)

Notice that the critical path occurs when B=1, C=0, D=0, and A rises from 0 to 1. Thus,
$$
T_c \ge 80 + 3*40 + 50 = 250ps
$$
Then, the maximum clock frequency is $\frac{1}{250ps}$ = 4GHz.
Notice the short path occurs when A=0 and C rises. Then,
$$
t_{ccq} + t_{cd} = 30 + 25 = 55ps
$$
But the flip-flop hold time is 60ps which is a hold time violation.
**Fixing Hold Time Violations**
**Problem:**
Fix the previous hold time violation.
**Solution:**
![fix_hold-time_circuit.png](/fix_hold-time_circuit.png)

![fix_hold-time_time-diagram.png](/fix_hold-time_time-diagram.png)

### Notable Quotes
> “Modern flip-flops are usually designed so that the minimum delay through the combinational logic can be 0—that is, flip-flops can be placed back-to-back."
### References
- *Digital Design and Computer Architecture* — Chapter 3, Pages 139–155


## 2.5 Parallelism
---
### Key Concepts
- **Token**:
  - Group of inputs processed to produce a group of outputs.
- **Latency**
  - Time for one token to pass through the system from start to end.
- **Throughput**
  - Number of tokens that can be produced per unit time.
- **Parallelism**
  - Processing several tokens at a time.
- **Spatial Parallelism**
  - Uses multiple hardware copies.
- **Temporal Parallelism (Pipelining)**
  - Task broken into stages with multiple tasks dispersed accross each stage.
### Definitions
- **Dependencies**
  - Current task dependent on the result of prior task, roadblock to parallelism.
### Formulas
**Throughput**
Throughput using latency L for no, spatial, and temporal parallelism. $L_1$ is the latency of the longest step.
None:
$$
\frac{1}{L}
$$
Spatial
$$
\frac{N}{L}
$$
Temporal
$$
\frac{1}{L_1}
$$
### Examples
**Pipelining**
**Problem:**
Continue to speed up the throughput of this circuit. Let $t_{pcq} = 03ns$ and $t_{setup} = 0.2ns$. Notice that $T_c = 0.3 + 3 + 2 + 0.2 = 9.5ns$. Then latency is 9.5ns and throughput at 105MHz.
![no-parallelism_circuit.png](/no-parallelism_circuit.png)

**Solution:**
![two-stage-parallelism_circuit.png](/two-stage-parallelism_circuit.png)

![three-stage-paralleism_circuit.png](/three-stage-paralleism_circuit.png)

### References
- *Digital Design and Computer Architecture* — Chapter 3, Pages 155–159