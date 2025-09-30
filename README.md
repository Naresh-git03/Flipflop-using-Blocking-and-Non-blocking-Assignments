# Flipflop-using-Blocking-and-Non-blocking-Assignments
Exp 3 -Write and simulate D, SR, JK, T Flipflops using Blocking and Non blocking Assignments
   Aim: To design and simulate D, SR, JK, T Flipflops using Blocking and Non blocking Assignments in Verilog HDL and verify its functionality through a testbench using the Vivado 2023.1 simulation environment.
   
  Apparatus Required:
  Vivado 2023.1
Procedure:

Launch Vivado Open Vivado 2023.1 by double-clicking the Vivado icon or searching for it in the Start menu. 
Create a New Project Click on "Create Project" from the Vivado Quick Start window. In the New Project Wizard: Project Name: Enter a name for the project (e.g., Mux4_to_1). 
Project Location: Select the folder where the project will be saved. Click Next. 
Project Type: Select RTL Project, then click Next. Add Sources: Click on "Add Files" to add the Verilog files (e.g., mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.). 
Make sure to check the box "Copy sources into project" to avoid any external file dependencies. 
Click Next.
Add Constraints: Skip this step by clicking Next (since no constraints are needed for simulation). 
Default Part Selection: You can choose a part based on the FPGA board you are using (if any). 
If no board is used, you can choose any part, for example, xc7a35ticsg324-1L (Artix-7). 
Click Next, then Finish.
Add Verilog Source Files In the "Sources" window, right-click on "Design Sources" and select Add Sources if you didn't add all files earlier.
Add the Verilog files and the testbench. 
Check Syntax Expand the "Flow Navigator" on the left side of the Vivado interface. 
Simulate the Design In the Flow Navigator, under "Simulation", click on "Run Simulation" → "Run Behavioral Simulation". 
Vivado will open the Simulations Window, and the waveform window will show the signals defined in the testbench. 
View and Analyze Simulation Results Adjust Simulation Time To run a longer simulation or adjust timing, go to the Simulation Settings by clicking "Simulation" → "Simulation Settings". Under "Simulation", modify the Run Time (e.g., set to 1000ns).
Generate Simulation Report Once the simulation is complete, you can generate a simulation report by right-clicking on the simulation results window and selecting "Export Simulation Results".
Save the report for reference in your lab records. Save and Document Results Save your project by clicking File → Save Project.
Take screenshots of the waveform window and include them in your lab report to document your results. 
You can include the timing diagram from the simulation window showing the correct functionality of the Seven Segment across different select inputs and data inputs. 
Close the Simulation Once done, by going to Simulation → "Close Simulation

Input/Output Signal Diagram:

D FF

SR FF

JK FF

T FF


RTL Code:
D Flip Flop
```
  module dff (clk, rst,d, q); 
  input clk, rst,d;
  output reg q;
         always @(posedge clk) begin
            if (rst)
                q <= 1'b0;
              else
                   q <= d;
      end
   endmodule
```
SR Flip Flop
```
  module sr_ff (input clk, input S, input R,output reg Q); 
  always @(posedge clk) 
  begin
  case ({S,R})
  2'b00: Q <= Q;
  2'b01: Q <= 0;
   2'b10: Q <= 1;
  2'b11: Q <= 1'bx;
 endcase
 end
endmodule

JK Flip Flop
module jk_ff(input clk,J,K, output reg Q);
always @(posedge clk) 
begin
case({J,K})
2'b00: Q<=Q;
2'b01: 0<=0;
2'b10: Q<=1;
2'b11: Q<=~Q;
endcase
end
endmodule
```
T FLIP FLOP
```
module t_ff(clk, rst, Tout, T);
input clk, rst, T;
output reg Tout;
always@ (posedge clk)
begin
if(rst)
  Tout=1'b0;
else if(T) 
  Tout = ~Tout;
else
Tout = Tout
end
endmodule
```
TestBench:
```
D Flip flop

module dff_tb;
reg clk_t, rst_t, d_t;
wire q_t;
dff dut (.clk(clk_t),.rst(rst_t),.d(d_t),.q(q_t) );
initial begin
clk_t = 1'b0;
rst_t = 1'b1;
d_t = 1'b0;
#100 rst t = 1'b0;
#100 d t = 1'b1;
#100 d t = 1'b0;
#100 d_t = 1'b1;
end
always #10 clk t = ~clk t;
endmodule
```
SR Flip Flop 
```
module sr_ff_tb;
reg clk, S, R;
wire Q;
sr_ff uut (.clk(clk),.S(S),.R(R),.Q(Q));
initial begin
clk = 0;
forever #10 clk = ~clk;
end
initial begin
S = 0; R = 0;
#100 S = 1; R = 0;
#100 S = 0; R = 0;
#100 S = 0; R = 1;
#100 S = 1; R = 1;
#100 S = 0; R = 0;
end
endmodule
```
JK Flip Flop 
```
module tb_jk_ff;
reg clk;
reg J, K;
wire Q;
jk_ff uut (.clk(clk),.J(J),.K(K),.Q(Q));
initial begin
clk=0;
forever #20 clk=~clk;
end
initial begin
J = 0; K = 0;
#100 J=0; K=0;
#100 J=0; K=1;
#100 J=1; K=0;
#100 J=1; K=1;
#100 J=0; K=1;
#100 J=1; K=0;
#100 J=1; K=1;
end
endmodule
```
T Flip Flop
```
module t_ff_tb;
reg clk, rst, T;
wire Tout;
t_ff uut (.clk(clk),.rst(rst),.T(T),.Tout(Tout));
initial begin
clk = 0;
forever #10 clk = ~clk;
end
initial begin
rst = 1; T = 0;
#20 rst = 0;
#20 T = 1;
#20 T = 0;
#20 T = 1;
#20 T = 1;
#20 T = 0;
end
endmodule
```
Output waveform:

D Flip Flop//

![WhatsApp Image 2025-09-16 at 21 11 38_f8996400](https://github.com/user-attachments/assets/ccb83a3c-9320-46c4-a3e2-5d800a292902)

SR Flip Flop//

![WhatsApp Image 2025-09-16 at 21 13 00_5be1b69b](https://github.com/user-attachments/assets/cc3205df-fc9f-4f9c-8a8b-bff834dde41e)

JK Flip Flop//

![WhatsApp Image 2025-09-16 at 21 13 25_0b864ca5](https://github.com/user-attachments/assets/6d51b316-9d2b-488f-ac55-adb6150f2a42)

Conclusion:

This project demonstrates flip-flop design using both blocking (=) and non-blocking (<=) assignments in Verilog. While blocking assignments are sequential and can lead to race conditions in clocked logic, non-blocking assignments correctly model parallel hardware behavior. Hence, non-blocking assignments are recommended for reliable flip-flop and synchronous circuit design.


