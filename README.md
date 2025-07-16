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

## 📂 File Structure

├── Top.v[Main_Block].docx # Top-level DSP pipeline
├── variables.v[Main_Block].docx # 3-tap delay input register
├── shifting.v[Main_Block].docx # Coefficient log2 detector
├── multi.v[Main_Block].docx # Shift-based multiplier controller
├── barrelshifter.v[Main_Block].docx # Performs left shift operations
├── setting.v[Main_Block].docx # Arithmetic operation selector
├── repple_carry_adder.v[Main_Block].docx # 8-bit ripple carry adder
├── carry_look_ahead.v[Main_Block].docx # 8-bit carry look-ahead adder
├── regi.v[Main_Block].docx # Output selector and register
├── alu.v[Main_Block].docx # ALU control unit
├── cond.v[Main_Block].docx # Overflow and zero flag generator
├── tb_top.v[Main_Block].docx # Testbench with input sequence
├── FULL WORKING.docx # Complete design document
└── README.md # Project overview

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
