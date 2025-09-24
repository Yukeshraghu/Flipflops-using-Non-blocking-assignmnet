# EXPERIMENT 3B: Simulation of All Flip-Flops using Non Blocking Statement

## AIM
To design and simulate basic flip-flops (SR, D, JK, and T) using **Non blocking statements** in Verilog HDL, and verify their functionality through simulation in Vivado 2023.1.

## APPARATUS REQUIRED
- Vivado 2023.1
- Computer with HDL Simulator

## DESCRIPTION
Flip-flops are the basic memory elements in sequential circuits.  
In this experiment, different types of flip-flops (SR, D, JK, T) are modeled using **behavioral modeling** with **Non blocking assignment (`<=`)** inside the `always` block.  
Non Blocking assignments execute sequentially in the given order, which makes it easier to describe simple synchronous circuits.

## PROCEDURE
1. Open **Vivado 2023.1**.  
2. Create a **New RTL Project** (e.g., `FlipFlop_Simulation`).  
3. Add Verilog source files for each flip-flop (SR, D, JK, T).  
4. Add a testbench file to verify all flip-flops.  
5. Run **Behavioral Simulation**.  
6. Observe waveforms of inputs and outputs for each flip-flop.  
7. Verify that outputs match the truth table.  
8. Save results and capture simulation screenshots.

---

## VERILOG CODE

### SR Flip-Flop (Non Blocking)
```
`timescale 1ns / 1ps

module srff(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;

always @ (posedge clk) begin
if (rst==1)
q <= 0;
else if(s==0 && r==0)
q <= q;
else if(s==0 && r==1)
q <= 1'b0;
else if(s==1 && r==0)
q <= 1'b1;
else
q <= 1'bx;
end
endmodule

```
### SR Flip-Flop Test bench 
```
module srff_tb;
reg s,r,clk,rst;
wire q;

srff uut(s,r,clk,rst,q);

always #5 clk=~clk;

initial begin
clk=0;
s=0; r=0;
rst=1;
#10 rst=0;
#10 s=1; r=0; // set
#10 s=0; r=0; // hold
#10 s=0; r=1; // reset
#10 s=1; r=1; // invalid condition
#10 s=1; r=0; // hold
#20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT
![WhatsApp Image 2025-09-24 at 13 12 23_006aba81](https://github.com/user-attachments/assets/b294d25b-7f1c-4f81-b95f-ba63053a8475)

---

### JK Flip-Flop (Non Blocking)
```
`timescale 1ns / 1ps

module jkflipflop(j,k,clk,rst,q);
input j,k,clk,rst;
output reg q;

always @ (posedge clk) 
begin
if (rst==1)
q <= 0;
else if(j==0 && k==0)
q <= q;
else if(j==0 && k==1)
q <= 1'b0;
else if(j==1 && k==0)
q <= 1'b1;
else
q <= ~q;
end
endmodule

```
### JK Flip-Flop Test bench 
```

module jkflipflop_tb;
reg j,k,clk,rst;
wire q;

jkflipflop uut(j,k,clk,rst,q);

always #5 clk = ~clk;

initial begin
clk = 0;
j = 0; k = 0;
rst = 1;
#10 rst = 0;
#10 j = 1; k = 0; // set
#10 j = 0; k = 0; // hold
#10 j = 0; k = 1; // reset
#10 j = 1; k = 1; // toggle
#10 j = 1; k = 0; // hold
#20 $finish;
end
endmodule

```
#### SIMULATION OUTPUT
![WhatsApp Image 2025-09-24 at 13 15 20_cb397c13](https://github.com/user-attachments/assets/1e509f26-f1af-4638-9d73-89d4aff16fc8)

---
### D Flip-Flop (Non Blocking)
```
`timescale 1ns / 1ps

module dflipflop(d,clk,rst,q);
input d,clk,rst;
output reg q;

always @ (posedge clk) begin
if (rst==1)
q <= 0;
else if(d==0)
q <= 0;
else
q <= 1;
end
endmodule
```
### D Flip-Flop Test bench 
```
module dflipflop_tb;
reg d,clk,rst;
wire q;

dflipflop uut(d,clk,rst,q);

always #5 clk = ~clk;

initial begin
clk = 0;
d = 0;
rst = 1;
#10 rst = 0; d = 0;
#10 d = 1;
#20 $finish;
end
endmodule

```

#### SIMULATION OUTPUT

![WhatsApp Image 2025-09-24 at 13 18 04_34371bdb](https://github.com/user-attachments/assets/9fb35895-0436-4019-813d-5143ae04dd6f)

---
### T Flip-Flop (Non Blocking)
```
module tflipflop_tb;
reg t,clk,rst;
wire q;

tflipflop uut(t,clk,rst,q);

always #5 clk = ~clk;

initial begin
clk = 0;
t = 0;
rst = 1;
#10 rst = 0; t = 0;
#10 t = 1;
#20 $finish;
end
endmodule

```
### T Flip-Flop Test bench 
```


module tflipflop_tb;
reg t,clk,rst;
wire q;

tflipflop uut(t,clk,rst,q);

always #5 clk = ~clk;

initial begin
clk = 0;
t = 0;
rst = 1;
#10 rst = 0; t = 0;
#10 t = 1;
#20 $finish;
end
endmodule

```

#### SIMULATION OUTPUT

![WhatsApp Image 2025-09-24 at 13 20 43_f609f6d8](https://github.com/user-attachments/assets/d9eacd32-61ed-4b81-afe4-5a313fcf02fd)


---

### RESULT

All flip-flops (SR, D, JK, T) were successfully simulated using Non blocking statements in Verilog HDL.
The outputs matched the expected truth table values, demonstrating correct sequential behavior.
