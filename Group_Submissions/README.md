# Digital System Design – Group Project

> Complete every mandatory section. Do not delete headings. Replace bracketed prompts. If a section is not applicable, explain why.

## 1. Team Details
| Role | Student name | Roll number | GitHub username |
|---|---|---|---|
| Group leader | Vaibhavi Bhamare | D9B 3 | https://github.com/2025vaibhavibhamare-dev |
| Member 2 |Tanvish Patil |D9A 41 | (https://github.com/9dtanvishpatil-art) |
| Member 3 | Sumit Tithe   |D9B 63 | (https://github.com/SumitThite) |
| Member 4 | Vikrant Kharatmol |D9B  71 | (https://github.com/8511kharatmolvikrantsvhs-bit) |

**Class:** [D9A/D9B]  
**Group ID:** [ D9A_Group32]  
**Repository URL:** (https://github.com/2025vaibhavibhamare-dev/DSD-2026-D9B-Group32) 
**Final Pull Request URL:**

## 2. Assigned Problem Statement
- **Number/title:** Age Group Detector using Moore Finite State Machine (FSM) with Four-Category Classification.5
- **Problem summary:** The project involves designing a digital system that classifies a person's age into four categories: Child (0–12), Teen (13–19), Adult (20–25), and Senior (26–31). A 5-bit binary input is used to represent the age, which is stored in an input register and processed by a range decoder. A Moore Finite State Machine (FSM) determines the corresponding age category and activates the respective LED indicator. The original three-category age detector is modified by introducing an additional Senior category.
- **Objective:** To design and implement a 5-bit age input system using Verilog HDL.

To develop a range decoder for classifying ages into four distinct categories.

To design a Moore FSM with separate states for IDLE, CHILD, TEEN, ADULT, and SENIOR, along with an intermediate CHECK state.

To implement START, ACK, and RESET control operations.

To display the detected age category using four individual LED indicators.

To simulate and verify all 32 possible age input combinations (0–31) using a Verilog testbench.

To implement the design on a Spartan-7 FPGA using Xilinx Vivado.
- **Inputs and outputs:**
- |---|---|---|---|
- Signal Width Description
clk |1bit |Clock signal for synchronous operation
reset |1 bit| Active-high reset to initialise the FSM
start| 1 bit| Initiates age capture and classification
ack| 1 bit| Returns the FSM to IDLE state2
age_switches[4:0]| 5 bits| Binary age input through five switches (0–31)

Outputs:
Signal  Width Description
child_led | 1 bit|  Indicates Child category (0–12)
teen_led  | 1 bit| Indicates Teen category (13–19)
adult_led |1 bit | Indicates Adult category (20–25)
senior_led| 1bit| Indicates Senior category (26–31)

Age Classification:

Age Range Category LED Output
0–12 | Child|Green
13–19| Teen | Yellow
20–25|Adult | Red
26–31  |Senior| Blue
- **Constraints and assumptions:** Input Range: The system accepts only 5-bit unsigned binary inputs, representing ages from 0 to 31.

Age Classification: Each age value belongs to exactly one of the four predefined categories, with no overlapping ranges.

Input Registration: The age entered through the switches is captured in the input register when START is activated while the FSM is in IDLE.

Moore FSM Operation: The output LEDs depend only on the current FSM state and not directly on the input age.

Reset Operation: An active-high synchronous reset initialises the FSM to the IDLE state, with all LEDs turned OFF.

Acknowledgement: The ACK signal returns the FSM from any classification state to IDLE, switching OFF all category LEDs.

Clock Dependency: All state transitions and input registration operations are synchronised with the rising edge of the clock.

Single Category Output: Only one category LED is activated at a time. All LEDs remain OFF in the IDLE and CHECK states.

Hardware Interface: Five slide switches are used for age input, three push buttons for START, ACK and RESET, and four LEDs for category indication on the Spartan-7 FPGA board.

## 3. Problem Analysis and Proposed Solution
## 3. Problem Analysis and Proposed Solution

### 3.1 Requirements Analysis

The Age Group Detector requires a digital system capable of accepting a 5-bit binary age input and classifying it into four predefined categories: Child, Teen, Adult and Senior. The system must store the input age, decode its range and use a Moore Finite State Machine (FSM) to generate the corresponding output.

The major requirements are:

- Accept a 5-bit age input representing values from 0 to 31.
- Store the input using a 5-bit register when the START signal is activated.
- Classify the age into one of four categories using range-based combinational logic.
- Implement a Moore FSM with IDLE, CHECK, CHILD, TEEN, ADULT and SENIOR states.
- Use RESET to initialise the system and ACK to return it to the IDLE state.
- Activate the appropriate LED for the detected category while keeping the remaining LEDs OFF.
- Verify all 32 possible input combinations through Verilog simulation and implement the design on a Spartan-7 FPGA.

### 3.2 Edge Cases and Challenges

The design must correctly handle boundary values to ensure accurate classification. Particular attention is given to ages at the transition points between categories.

- **Lower and upper limits:** Ages 0 and 31 must be correctly classified as Child and Senior respectively.
- **Category boundaries:** Ages 12, 13, 19, 20, 25 and 26 must activate the correct category LED.
- **Reset condition:** When RESET is activated, the FSM must return to IDLE and all LEDs must turn OFF.
- **Input stability:** Once START is activated, the entered age must be stored so that subsequent changes in switch positions do not affect the current classification.
- **Acknowledgement:** ACK must return the system from any classification state to IDLE.
- **Invalid state handling:** Any undefined FSM state must return to IDLE through the default state condition.

### 3.3 Proposed Solution

The proposed solution uses a combination of sequential and combinational logic implemented in Verilog HDL.

Initially, the age is entered through five switches and captured by a 5-bit input register when START is activated. The registered age is then processed by a combinational range decoder, which identifies the corresponding category based on predefined age intervals.

The decoded result is used by a Moore FSM to determine the system state. The FSM consists of six states: IDLE, CHECK, CHILD, TEEN, ADULT and SENIOR. The CHECK state evaluates the registered age and transfers the FSM to the appropriate classification state.

Based on the current state, the output logic activates one of the four LEDs. The RESET signal initialises the system, while ACK returns the FSM to IDLE after classification.

The design is developed and simulated using Xilinx Vivado and subsequently programmed onto a Spartan-7 FPGA board for hardware verification.

### 3.4 Distinctive Features

- **Four-category classification:** Extends the original three-category age detector by introducing a Senior category (26–31).
- **Moore FSM architecture:** Ensures that LED outputs depend only on the current state, providing stable and predictable outputs.
- **Registered input:** Stores the entered age to maintain input stability during classification.
- **Independent LED indicators:** Uses four separate LEDs to represent the four age categories.
- **Control operations:** Incorporates START, ACK and RESET signals for controlled system operation.
- **Complete input verification:** Tests all 32 possible age combinations using an automated Verilog testbench.
- **FPGA implementation:** Demonstrates the practical implementation of digital logic using a Spartan-7 FPGA and Vivado.

### 3.5 Feasibility of the Design

The proposed design is feasible because it uses basic digital design concepts such as registers, combinational logic, comparators and finite state machines. These components can be efficiently described using Verilog HDL and implemented using the FPGA resources available on the Spartan-7 board.

The design requires only five input switches, three push buttons, four LED indicators and an onboard clock. Vivado provides the necessary environment for RTL design, behavioural simulation, synthesis, implementation and bitstream generation.

Furthermore, the classification logic is straightforward, requires minimal hardware resources and can be verified exhaustively for all 32 possible input values. Therefore, the project is technically achievable, cost-effective and suitable for demonstrating the practical application of FSM-based digital system design.
## 4. Architecture

flowchart LR
    A["5-bit Age Input<br/>SW0–SW4"] --> B["5-bit Input Register<br/>Age_Reg"]
    B --> C["Range Decoder<br/>0–12: Child<br/>13–19: Teen<br/>20–25: Adult<br/>26–31: Senior"]
    C --> D["Moore FSM Controller<br/>IDLE, CHECK,<br/>CHILD, TEEN,<br/>ADULT, SENIOR"]
    D --> E["Output Logic"]
    E --> F["Child LED<br/>Green"]
    E --> G["Teen LED<br/>Yellow"]
    E --> H["Adult LED<br/>Red"]
    E --> I["Senior LED<br/>Blue"]

    J["START"] --> B
    J --> D
    K["ACK"] --> D
    L["RESET"] --> D
    L --> B
    M["Clock"] --> B
    M --> D


## 5. FSM Design
State whether the design uses an FSM. If yes, specify Moore/Mealy, states/encoding, state diagram, state table, transition conditions and reset behaviour. If not, justify the alternative.

**Diagram:** [Path/link]  
**State table:** [Path/link]

## 6. Logisim Implementation
- Logisim version: [Version]
- Circuit file: [Path to `.circ`]
- Test cases and expected/observed behaviour: [Details]
- Issues and corrections: [Details]
- Screenshot/evidence: [Path/link]

## 7. Verilog HDL Implementation
- Tool/version: [Details]
- Top module and submodules: [Names]
- Architecture/coding decisions: [Details]
- Synthesizability considerations: [Details]
- RTL: `03_Verilog_Implementation/RTL/`
- Testbench: `03_Verilog_Implementation/Testbench/`

## 8. Verification and Simulation Results
| Test ID | Inputs/conditions | Expected output | Observed output | Pass/Fail |
|---|---|---|---|---|
| T01 | [ ] | [ ] | [ ] | [ ] |
| T02 | [ ] | [ ] | [ ] | [ ] |
| T03 | [ ] | [ ] | [ ] | [ ] |

Tool/version: [Details]  
Number passed/failed: [Details]  
Waveform/log path: [Path]

## 9. FPGA Hardware Implementation
- FPGA board/device: [Details]
- Tool/version: [Details]
- Clock/constraints: [Details]
- Synthesis/implementation summary: [Details]
- Programming and hardware test result: [Details]
- Evidence path: `04_FPGA_Hardware/`

Explain differences between simulation and hardware results, if any.

## 10. Challenges, Debugging and Improvements
| Issue | Root cause | Correction | Outcome |
|---|---|---|---|
| [ ] | [ ] | [ ] | [ ] |

Future improvements: [Details]

## 11. Task Allocation and Individual Contribution
| Student | Assigned responsibility | Actual contribution/evidence |
|---|---|---|
| Group leader | [ ] | [ ] |
| Member 2 | [ ] | [ ] |
| Member 3 | [ ] | [ ] |
| Member 4 | [ ] | [ ] |

Every student must be ready to explain the complete design.

## 12. Progress Log
Maintain time-wise updates in `STATUS.md`.

## 13. Final Results and Conclusion
Summarise requirements met, correctness of simulation/hardware results, measured results, limitations and conclusion.

[Write here]

## 14. Team Reflection
What did the team learn? What would you improve?

[Write here]

## 15. Final Submission Checklist
- [ ] Team details and problem analysis complete.
- [ ] Architecture/block diagram included.
- [ ] FSM diagram/table or justified alternative included.
- [ ] Logisim source and simulation evidence uploaded.
- [ ] Verilog RTL and testbench uploaded.
- [ ] Simulation results and test cases documented.
- [ ] FPGA implementation and hardware evidence uploaded.
- [ ] Results, challenges and conclusion documented.
- [ ] Presentation and final report uploaded.
- [ ] STATUS.md is up to date.
- [ ] Final Pull Request created and URL recorded.
