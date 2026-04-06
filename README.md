# 🔷 APB Slave Design and UVM Verification

## 📌 Overview

This project implements and verifies an APB (Advanced Peripheral Bus) slave using SystemVerilog and UVM.

The design supports:

* Read and Write operations
* Wait-state insertion
* Error generation (PSLVERR)
* Memory-mapped transactions

A complete UVM testbench is developed for functional verification.

---

## 🧠 APB Protocol

APB is part of AMBA architecture used for low-power peripherals.

### Transfer Phases:

1. Setup Phase → `PSEL=1, PENABLE=0`
2. Enable Phase → `PENABLE=1`
3. Completion → `PREADY=1`

---

## 🏗️ RTL Design

### Features:

* 8-bit address & data
* 8-depth memory
* Configurable wait states (`N = 4`)
* Error for invalid address

### Key Logic:

* Wait-state generator
* Transaction control
* Memory read/write
* Error detection

---

## 🔌 Interface

SystemVerilog interface connects DUT with UVM environment.

Includes:

* Driver clocking block
* Monitor clocking block
* Virtual interface usage

---

## 🧪 UVM Verification Architecture

### Components:

* Transaction (APB_TRANS)
* Sequence (APB_SEQUENCE)
* Sequencer
* Driver
* Monitor
* Agent
* Reference Model
* Scoreboard
* Environment
* Test

---

## 🔄 Verification Flow

Sequence → Sequencer → Driver → DUT
↓
Monitor
↓     ↓
Reference   Scoreboard
↓
Comparison

---

## ⚙️ Simulation

### Tools:

* Cadence Xcelium
* Synopsys VCS
* EDA Playground

### Run Command:

```
run_test("APB_TEST");
```

---

## 📊 Features

✔ Protocol-compliant APB slave
✔ Wait-state handling
✔ Error detection
✔ Random stimulus generation
✔ Self-checking testbench
✔ Reusable UVM components

---

## 📁 Project Structure

```
rtl/ → RTL Design  
tb/  → UVM Testbench  
sim/ → Simulation scripts  
docs/ → Waveforms & diagrams  
```

---

## 📌 Results

* Successful read/write verification
* Scoreboard PASS results
* Correct wait-state behavior
<img width="2396" height="914" alt="Screenshot 2026-04-06 190339" src="https://github.com/user-attachments/assets/db00eead-4b2a-47d6-b4c5-12986ee0da75" />

## 📊 Simulation Results

- UVM test executed successfully
- Driver performed APB read/write operations
- Monitor captured DUT transactions
- Reference model generated expected outputs
- Scoreboard verified correctness

### Example Result:
ADDR = 0x0  
Expected = 0x0  
Actual = 0x0  
Result = PASS
<img width="2227" height="740" alt="Screenshot 2026-04-06 190534" src="https://github.com/user-attachments/assets/caa7c0e2-67d2-4b81-8da6-0acb6123dd9c" />
## 🔁 Multiple Write Verification

The design correctly supports multiple writes to the same address.

### Example:
1st Write → ADDR = 0x1, DATA = 0x69  
2nd Write → ADDR = 0x1, DATA = 0x0E  

### Observation:
- Memory value is updated on each write
- Previous data is overwritten correctly
- No stale or incorrect data observed

### Conclusion:
The APB slave correctly handles consecutive write operations.

<img width="2408" height="934" alt="Screenshot 2026-04-06 190546" src="https://github.com/user-attachments/assets/aab6b836-b828-4272-9974-f7b33b5e606e" />
## ✍️ Write Transaction Verification

The APB slave correctly performs write operations.

### Example:
ADDR = 0x1  
DATA = 0x69  

### Observations:
- Driver successfully executed write transaction
- Monitor captured correct address and data
- Reference model updated memory correctly
- Scoreboard received transaction without mismatch

### Conclusion:
Write functionality of APB slave is verified successfully.



<img width="2854" height="620" alt="Screenshot 2026-04-06 192038" src="https://github.com/user-attachments/assets/0f613eb2-4522-41ff-9977-bf7454c4f778" />
## 📈 Waveform Analysis

The waveform confirms correct APB protocol behavior.

### Key Observations:
- PSEL remains high during active transactions
- PENABLE toggles between setup and enable phases
- PREADY is asserted after 4 wait cycles
- wait_counter increments from 0 to 3
- transaction_active signal controls transfer execution

### Data Flow:
- Write data (PWDATA) is correctly stored in memory
- Read data (PRDATA) matches expected values

### Conclusion:
The waveform validates correct implementation of APB protocol, wait-state insertion, and data transactions.


The system correctly handles APB protocol transactions with wait states.
<img width="2463" height="1092" alt="Screenshot 2026-04-06 190617" src="https://github.com/user-attachments/assets/76549741-dcba-431c-8857-8d38a7b7656a" />
## 📊 UVM Verification Summary

The simulation completed successfully with no errors.

### Report Summary:
- UVM_INFO    : 71  
- UVM_WARNING : 0  
- UVM_ERROR   : 0  
- UVM_FATAL   : 0  

### Results:
- All transactions passed scoreboard checks
- DUT output matched reference model
- No functional mismatches observed

### Performance:
- Simulation Time: 525 ns
- Clean execution with zero errors

The APB slave design and UVM verification environment are validated successfully.


---

## 🔮 Future Work

* Functional coverage
* SystemVerilog Assertions (SVA)
* APB4 support
* SoC-level integration

---

## 👨‍💻 Author

chitrachedu shareefvali
