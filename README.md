# VLSI-LAB-EXP-4
# SIMULATION AND IMPLEMENTATION OF SEQUENTIAL LOGIC CIRCUITS

AIM: 
 To simulate and synthesis SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Xilinx ISE.

APPARATUS REQUIRED:

Xilinx 14.7
Spartan6 FPGA

**LOGIC DIAGRAM**

SR FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/77fb7f38-5649-4778-a987-8468df9ea3c3)


JK FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/1510e030-4ddc-42b1-88ce-d00f6f0dc7e6)

T FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/7a020379-efb1-4104-85ee-439d660baa08)


D FLIPFLOP

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/dda843c5-f0a0-4b51-93a2-eaa4b7fa8aa0)


COUNTER

![image](https://github.com/navaneethans/VLSI-LAB-EXP-4/assets/6987778/a1fc5f68-aafb-49a1-93d2-779529f525fa)


  
PROCEDURE:
STEP:1  Start  the Xilinx navigator, Select and Name the New project.
STEP:2  Select the device family, device, package and speed.       
STEP:3  Select new source in the New Project and select Verilog Module as the Source type.                       
STEP:4  Type the File Name and Click Next and then finish button. Type the code and save it.
STEP:5  Select the Behavioral Simulation in the Source Window and click the check syntax.                       
STEP:6  Click the simulation to simulate the program and  give the inputs and verify the outputs as per the truth table.               
STEP:7  Select the Implementation in the Sources Window and select the required file in the Processes Window.
STEP:8  Select Check Syntax from the Synthesize  XST Process. Double Click in the  FloorplanArea/IO/Logic-Post Synthesis process in the User Constraints process group. UCF(User constraint File) is obtained. 
STEP:9  In the Design Object List Window, enter the pin location for each pin in the Loc column Select save from the File menu.
STEP:10 Double click on the Implement Design and double click on the Generate Programming File to create a bitstream of the design.(.v) file is converted into .bit file here.
STEP:11  On the board, by giving required input, the LEDs starts to glow light, indicating the output.

# D-FLIP FLOP

VERILOG CODE
~~~
module Dflipflop(D,clk,reset,Q);
input D;
input clk;
input reset;
output reg Q;
always @(posedge clk)
begin
 if(reset==1'b1)
  Q <= 1'b0;
 else
  Q <= D;
end
endmodule
~~~

OUTPUT:

<img width="962" alt="2024-04-08 (1)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/14d28510-670f-4285-8b8b-2eb32b192557">
<img width="962" alt="2024-04-08 (2)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/8662d8bf-2960-4624-adc8-6df6b2b29437">

# JK FLIP FLOP

VERILOG CODE:
~~~
module JK_flipflop (q, q_bar, j,k, clk,reset);
input j,k,clk, reset;
output reg q;
output q_bar;
always@(posedge clk)
begin
  if(!reset)        
    q <= 0;
  else 
  begin
      case({j,k})
        2'b00: q <= q;    // No change
        2'b01: q <= 1'b0; // reset
        2'b10: q <= 1'b1; // set
        2'b11: q <= ~q; // Toggle
      endcase
  end
end
assign q_bar = ~q;
endmodule
~~~

OUTPUT:

<img width="962" alt="2024-04-08 (13)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/ae673382-8af3-43d2-b5fd-0065ae2ad318">
<img width="962" alt="2024-04-08 (14)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/5b3ec235-00fc-4f84-b61e-0c457642569d">

# MOD-10 COUNTER

VERILOG CODE:
~~~
module mod10(clk,rst,out);
input clk,rst;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1 | out==4'b1001)
out=4'b0000;
else
out=out+1;
end
endmodule
~~~

OUTPUT:

<img width="962" alt="2024-04-08 (3)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/c71dd581-83a7-4c0a-8486-49c17fde037f">
<img width="962" alt="2024-04-08 (4)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/7dd5026a-585c-40d0-9bff-53ba0834976f">

# RIPPLE CARRY COUNTER

VERILOG CODE:
~~~
module tff(q,clk,rst);
input clk,rst;
output q;
wire d;
dff df1(q,d,clk,rst);
not n1(d,q);
endmodule
module dff(q,d,clk,rst);
input d,clk,rst;
output q;
reg q;
always @(posedge clk or posedge rst)
begin
if (rst)
q=1'b0;
else 
q=d;
end
endmodule
module ripplecounter(clk,rst,q);
input clk,rst;
output [3:0]q;
tff tf0(q[0],clk,rst);
tff tf1(q[1],q[0],rst);
tff tf2(q[2],q[1],rst);
tff tf3(q[3],q[2],rst);
endmodule
~~~

OUTPUT:

<img width="962" alt="2024-04-08 (5)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/c6c79543-f800-467a-81d7-eb7e67d14cbc">
<img width="962" alt="2024-04-08 (6)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/01c95bee-1816-4bb8-bd36-42e3c49ceea4">

# SR FLIP FLOP

VERILOG CODE:
~~~
module sr_flipflop(s,r,clk,rst,q);
input s,r,clk,rst;
output reg q;
always@(posedge clk)
begin
if(rst==1)
q=0;
else
begin
case({s,r})
2'b00:q=q;
2'b01:q=0;
2'b10:q=1;
2'b11:q=1'bX;
endcase
end
end
endmodule
~~~

OUTPUT:

<img width="962" alt="2024-04-08 (7)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/95924674-55f0-408b-b91d-5c0abe5a7f7d">
<img width="962" alt="2024-04-08 (8)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/5c626c90-315c-48e0-9de3-fe3c4f87bc06">

# T FLIP FLOP

VERILOG CODE:
~~~
module T_flipflop(clk,rst,t,q);
input clk,rst,t;
output reg q;
always @(posedge clk)
begin
if (rst==1)
q=1'b0;
else if (t==0)
q=q;
else
q=~q;
end
endmodule
~~~

OUTPUT:

<img width="962" alt="2024-04-08 (9)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/1cc68048-1013-4a9a-831f-53c09e85a9f2">
<img width="962" alt="2024-04-08 (10)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/19d226fa-5bfd-4fe0-9726-3cdfe7d0aa5b">

# UP-DOWN COUNTER

VERILOG CODE:
~~~
module updown_counter(clk,rst,updown,out);
input clk,rst,updown;
output reg [3:0]out;
always@(posedge clk)
begin
if (rst==1)
out=4'b0000;
else if(updown==1)
out=out+1;
else
out=out-1;
end
endmodule
~~~

OUTPUT:

<img width="617" alt="2024-04-08 (11)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/eaf2a2ee-935c-457b-92e3-aa92be0c017c">
<img width="962" alt="2024-04-08 (12)" src="https://github.com/21004601/VLSI-LAB-EXP-4/assets/146088220/f2772b2a-196d-4b24-871c-5f153ef91116">


RESULT:
 Hence The simulation and synthesis  of SR, JK, T, D - FLIPFLOP, COUNTER DESIGN using Vivado 2023 is done and output verified successfully.
















