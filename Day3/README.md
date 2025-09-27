# Day 3: Combinational and Sequential Optimization

Welcome to **Day 3** of the RTL Workshop!  
Today we focus on **optimization techniques** for both **combinational** and **sequential circuits**, learning how synthesis tools simplify logic, reduce area, improve timing, and save power.

---

## 📑 Table of Contents

- [1. Constant Propagation](#1-constant-propagation)
- [2. State Optimization](#2-state-optimization)
- [3. Cloning](#3-cloning)
- [4. Retiming](#4-retiming)
- [5. Labs on Optimization](#5-labs-on-optimization)

---

## 1. Constant Propagation

Constant propagation is an optimization technique where **variables with constant values are replaced directly in the logic**.  

**Benefits:**
- ✅ Reduced logic complexity  
- ✅ Smaller circuit area  
- ✅ Improved performance due to fewer gates  
- ✅ Less power consumption  

---

## 2. State Optimization

State optimization targets **Finite State Machines (FSMs)**.  
It reduces the number of states or optimizes their encoding to save hardware.

**Steps:**
1. **State Reduction:** Merge equivalent states.  
2. **State Encoding:** Choose optimal binary/Gray/one-hot encoding.  
3. **Logic Minimization:** Use Boolean simplification or CAD tools.  
4. **Power Optimization:** Apply techniques like clock gating.  

---

## 3. Cloning

**Cloning** is the duplication of logic cells to **balance fan-out load** and **improve timing**.  

**Why clone?**
- High fan-out nets can cause long delays.  
- Duplicating the driver cell splits the load.  

---

## 4. Retiming

Retiming is the process of **moving registers across combinational logic** to improve performance.  

**Steps:**
1. Represent circuit as a graph.  
2. Move registers (flip-flops) across nodes.  
3. Ensure functionality remains identical.  
4. Optimize clock period and power.  

👉 Used heavily in **pipelined designs** (e.g., CPUs, DSPs).  

---

## 5. Labs on Optimization

**Lab 1**

```verilog
module opt_check (input a , input b , output y);
  assign y = a ? b : 0;
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/8f415154-4c79-4a1f-acfd-f8f48522aaf0" />

---

**Lab 2**

```verilog
module opt_check2 (input a , input b , output y);
  assign y = a ? 1 : b;
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/c396ba6f-121f-4c75-9e40-4080e2cefba6" />


---

**Lab 3**

```verilog
module opt_check3 (input a , input b , output y);
  assign y = a ? 1 : b;
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/86a2ea64-d084-4e43-9702-6017dbcd1aad" />

**Lab 4**

```verilog
module opt_check4 (input a , input b , input c , output y);
  assign y = a ? (b ? (a & c) : c) : (!c);
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/9866c34d-dc09-419a-9317-87123598bae4" />

---

**Lab 5**

```verilog
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset) begin
  if (reset)
    q <= 1'b0;
  else
    q <= 1'b1;
end
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/90e1676e-f43d-4b2d-83ec-30b30e1f752b" />

---

**Lab 6**

```verilog
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset) begin
  if (reset)
    q <= 1'b1;
  else
    q <= 1'b1;
end
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/4c82382a-a967-4ea3-a399-9421b3267ef2" />

---

**Lab 7**

```verilog
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset) begin
  if (reset) begin
    q  <= 1'b1;
    q1 <= 1'b0;
  end
  else begin
    q1 <= 1'b1;
    q  <= q1;
  end
end
endmodule
```

<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/5e861d2e-130c-4377-8f83-07a230d53085" />


---

**Lab 8**

```verilog
module dff_const4(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset) begin
  if (reset) begin
    q  <= 1'b1;
    q1 <= 1'b1;
  end
  else begin
    q1 <= 1'b1;
    q  <= q1;
  end
end
endmodule
```
<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/9e971861-eeaf-4b43-9a0e-62a63ca4dbe8" />

---

**Lab 9**

```verilog
module dff_const5(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset) begin
  if (reset) begin
    q  <= 1'b0;
    q1 <= 1'b0;
  end
  else begin
    q1 <= 1'b1;
    q  <= q1;
  end
end
endmodule
```

<img width="1280" height="800" alt="Image" src="https://github.com/user-attachments/assets/7d3ab413-687f-416e-a04c-d2b28a129d98" />


---


## ✅ Summary

* **Constant Propagation:** Simplifies design by replacing signals with constants.
* **State Optimization:** Reduces redundant states and minimizes FSM logic.
* **Cloning:** Duplicates cells to balance load and improve timing.
* **Retiming:** Relocates registers for better clock performance.
