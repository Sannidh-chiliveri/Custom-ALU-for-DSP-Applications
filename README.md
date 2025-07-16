# 🧠 Custom ALU for DSP Applications

A Verilog-based hardware implementation of a 3-tap digital signal processing (DSP) filter, designed with a custom Arithmetic Logic Unit (ALU) that replaces traditional multipliers with power-efficient barrel shifters and optimized adders.

---

## 🚀 Project Overview

This design computes the following DSP equation using purely hardware logic:**Y[n] = A·X[n] + B·X[n−1] + C·X[n−2]**
Where `A`, `B`, and `C` are power-of-two constants. The implementation avoids using multipliers and instead uses barrel shifters to perform fast, low-power coefficient multiplication. Accumulation is done through a pipelined adder structure using both Ripple Carry Adder (RCA) and Carry Look-Ahead Adder (CLA).

---

## 🔧 Features

- ✅ **Barrel Shifter-Based Multiplication** — Efficient shift operations for power-of-2 coefficients.
- ✅ **Modular Design** — Parameterized and easily extensible architecture.
- ✅ **Dual Adder Pipeline** — Uses both RCA and CLA for reduced latency.
- ✅ **Overflow & Zero Detection** — Generates `en_ov` and `en_zero` flags.
- ✅ **Fully Testbenched** — Verified in simulation with timing and functional correctness.

---

## 📁 File Descriptions

Each `.v[........].txt` file contains the **Verilog code**  for respective module in the DSP-based custom ALU design.

- **Top.v[Main_Block].txt**  
  Describes the top-level module integrating all DSP blocks to implement the equation:  
  `Y[n] = A·X[n] + B·X[n−1] + C·X[n−2]`.

- **variables.v[Sub_Block].txt**  
  Details the register block implementing a 3-tap delay line to store input values X[n], X[n−1], and X[n−2].

- **shifting.v[Sub_Block].txt**  
  Contains the logic for detecting shift values based on coefficients A, B, and C using log₂ encoding.

- **multi.v[Sub_Block].txt**  
  Implements shift-based multiplication control logic, replacing power-hungry multipliers with efficient barrel shifters.

- **barrelshifter.v[Sub_Block].txt**  
  Defines the barrel shifter used to perform fast left-shift operations for multiplication by powers of two.

- **setting.v[Sub_Block].txt**  
  Describes the arithmetic operation selector that routes inputs to the appropriate adder module.

- **repple_carry_adder.v[Sub_Block].txt**  
  Details the 8-bit ripple carry adder module for basic addition operations.

- **carry_look_ahead.v[Sub_Block].txt**  
  Explains the 8-bit carry look-ahead adder for faster addition with reduced propagation delay.

- **regi.v[Sub_Block].txt**  
  Manages output selection and final register storage of computed Y[n].

- **alu.v[Sub_Block].txt**  
  Defines the control unit that coordinates arithmetic operations across the DSP datapath.

- **cond.v[Sub_Block].txt**  
  Generates status flags such as overflow and zero, useful for further control or branching.

- **tb_top.v[Testbench Block].txt**  
  Provides the testbench structure with input stimulus and expected output checks for validating the entire design.

- **FULL WORKING**  
  A consolidated document compiling working of all Verilog modules  and their interconnections for a complete RTL design.

- **README.md**  
  Project overview, explanation of architecture, usage, simulation details, and contribution guidelines.

---

## 📊 Functional Workflow

1. **Input Capture:**
   - Samples are delayed using a 3-tap register to get `X[n]`, `X[n−1]`, `X[n−2]`.

2. **Shift-Based Multiplication:**
   - Barrel shifters multiply each input by coefficient using left-shift (since A, B, C are powers of 2).

3. **Pipelined Addition:**
   - Intermediate values are summed using `setting.v` via RCA and CLA units.

4. **Result & Flags:**
   - Final result `Y[n]` is output along with status flags:
     - `en_ov`: Overflow flag
     - `en_zero`: Zero-result flag

---

## 🧪 Testbench Summary

- **Input Sequence:** `X[n]=5`, `X[n-1]=2`, `X[n-2]=1`
- **Coefficients:** `A=4`, `B=8`, `C=16`
- **Computation:**
`-->A·X[n] = 5 << 2 = 20`
`-->B·X[n-1] = 2 << 3 = 16`
`-->C·X[n-2] = 1 << 4 = 16`
`-->Y[n] = 20 + 16 + 64 = 100`
- **Expected Output:**
`Y[n] = 100`
`en_ov = 0`, `en_zero = 0`

---
