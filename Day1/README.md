# Day 1: Introduction to Verilog RTL Design & Synthesis

Welcome to **Day 1** of the RTL Design Workshop! 🎉  
Today marks the beginning of your journey into digital hardware design using Verilog. We'll cover simulation using **Icarus Verilog (iverilog)** and introduce **logic synthesis** using **Yosys**, an open-source tool. By the end of the day, you'll simulate and synthesize a simple digital circuit — a 2-to-1 multiplexer.

---

## 📚 Table of Contents

1. [Understanding Simulator, Design, and Testbench](#1-understanding-simulator-design-and-testbench)  
2. [Getting Started with Icarus Verilog (iverilog)](#2-getting-started-with-icarus-verilog-iverilog)  
3. [Lab: Simulating a 2-to-1 Multiplexer](#3-lab-simulating-a-2-to-1-multiplexer)  
4. [Verilog Code Walkthrough](#4-verilog-code-walkthrough)  
5. [Introduction to Yosys & Gate Libraries](#5-introduction-to-yosys--gate-libraries)  
6. [Lab: Synthesizing with Yosys](#6-lab-synthesizing-with-yosys)  
7. [Summary](#7-summary)  

---

## 1. Understanding Simulator, Design, and Testbench

### 🔧 Simulator
A **simulator** is a software tool used to verify the logic behavior of your hardware design. It allows you to apply inputs and observe outputs without physically building the circuit.

### 📐 Design
The **design** is your Verilog module that describes the digital logic you want to implement.

### 🧪 Testbench
A **testbench** is a Verilog file that tests your design. It provides stimulus (input signals) and monitors the output to verify correct functionality.

---

## 2. Getting Started with Icarus Verilog (iverilog)

**iverilog** is an open-source Verilog simulation tool. You'll also use **GTKWave** to visualize signal transitions.

### 🔧 Installation

Run the following commands to install required tools (Ubuntu/Debian):

```bash
sudo apt update
sudo apt install iverilog gtkwave
````

---

## 3. Lab: Simulating a 2-to-1 Multiplexer

### ✅ Step 1: Clone the Workshop Repository

```bash
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
cd sky130RTLDesignAndSynthesisWorkshop/verilog_files
```

### ✅ Step 2: Compile the Design and Testbench

```bash
iverilog good_mux.v tb_good_mux.v
```

### ✅ Step 3: Run the Simulation

```bash
./a.out
```

### ✅ Step 4: View the Waveform in GTKWave

```bash
gtkwave tb_good_mux.vcd
```

<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/860ce07f-5798-4c95-9931-3eb44a75a53c" />

---

## 4. Verilog Code Walkthrough

### 📄 `good_mux.v`

```verilog
module good_mux (input i0, input i1, input sel, output reg y);
    always @ (*)
    begin
        if(sel)
            y <= i1;
        else 
            y <= i0;
    end
endmodule
```

### 🔍 How It Works

* **Inputs**: `i0`, `i1` (data inputs), `sel` (select line)
* **Output**: `y` (selected output)
* **Behavior**: If `sel` is `1`, `y` takes the value of `i1`. If `sel` is `0`, `y` takes the value of `i0`.

---

## 5. Introduction to Yosys & Gate Libraries

### 🛠 What is Yosys?

**Yosys** is an open-source tool used for **logic synthesis**. It translates your Verilog code into a **gate-level netlist**, which is a structural representation suitable for chip fabrication.

### 🧠 Key Features

* Logic synthesis and optimization
* Gate-level technology mapping
* Support for multiple standard cell libraries
* Visualization of the synthesized design

### 📦 Gate Libraries (.lib)

A `.lib` file contains multiple versions of basic gates (AND, OR, NOT, etc.) with different characteristics:

* **Performance**: High-speed vs. low-power gates
* **Power**: Some consume less power
* **Area**: Smaller versions save space
* **Drive Strength**: Stronger gates for higher load
* **Signal Integrity**: Specialized gates for noise-sensitive paths

---

## 6. Lab: Synthesizing with Yosys

Let’s synthesize the `good_mux` design using Yosys.

### ✅ Step-by-Step Instructions

1. **Launch Yosys**:

   ```bash
   yosys
   ```

2. **Read the Liberty File**:

   ```tcl
   read_liberty -lib /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```

3. **Read Your Verilog Design**:

   ```tcl
   read_verilog /home/vsduser/VLSI/sky130RTLDesignAndSynthesisWorkshop/verilog_files/good_mux.v
   ```

4. **Synthesize the Design**:

   ```tcl
   synth -top good_mux
   ```

5. **Technology Mapping**:

   ```tcl
   abc -liberty /path/to/sky130_fd_sc_hd__tt_025C_1v80.lib
   ```

6. **Visualize the Netlist**:

   ```tcl
   show
   ```


<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/ed941aa4-e12c-4fe5-bb31-a0282070f270" />

---

## 7. Summary

🎯 Today you achieved the following:

* Understood the roles of a **design**, **simulator**, and **testbench**.
* Installed and used **iverilog** to simulate a Verilog design.
* Visualized waveforms using **GTKWave**.
* Explored how a **2-to-1 multiplexer** works.
* Learned the basics of **logic synthesis** with **Yosys**.
* Understood the purpose of **gate libraries** in synthesis.
* Successfully synthesized and visualized a gate-level schematic of your design.

