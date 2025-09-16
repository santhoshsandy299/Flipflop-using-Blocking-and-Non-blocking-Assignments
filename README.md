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

***Input/Output Signal Diagram:***

***D Flip Flop***

***SR Flip Flop***

***JK Flip Flop***

***T Flip Flop***


***RTL Code:***

***D Flip flop***
```
module dff ( clk, rst,d, q);
input clk,rst,d;
output reg q;
    always @(posedge clk) begin
        if (rst)   
            q <= 1'b0;
        else
            q <= d;  
    end
endmodule
```

***SR Flip Flop***
```
module sr_ff (input clk,input S,input R,output reg Q);
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
```

***JK Flip Flop***
```
module jk_ff(input clk,J,K, output reg Q);
always @(posedge clk) begin
case({J,K})
2'b00: Q<=Q;
2'b01: Q<=0;
2'b10: Q<=1;
2'b11: Q<=~Q;
endcase
end
endmodule
```

***T Flip Flop***
```
module t_ff(clk,rst,Tout,T);
    input clk,rst,T;
    output reg Tout;
    always@ (posedge clk)
     begin
     if(rst)
        Tout = 1'b0;
     else if(T)
        Tout = ~Tout;
     else
        Tout = Tout;
     end
endmodule
```

***TestBench:***

***D Flip flop***
```
module dff_tb;
    reg clk_t, rst_t, d_t;
    wire q_t;
    dff dut (.clk(clk_t),.rst(rst_t),.d(d_t),.q(q_t) );
    initial begin
        clk_t = 1'b0;
        rst_t = 1'b1;  
        d_t   = 1'b0;
        #100 rst_t = 1'b0; 
        #100 d_t = 1'b1;
        #100 d_t = 1'b0;
        #100 d_t = 1'b1;
end
     always #10 clk_t = ~clk_t;
endmodule
```
***SR Flip Flop***
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

***JK Flip Flop***
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

***T Flip Flop***
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

***Output waveform:***

***D Flip flop***

<img width="1268" height="754" alt="Screenshot 2025-09-16 200255" src="https://github.com/user-attachments/assets/e5ba3aca-929e-4f5a-a4d7-c572ebe94daf" />


***SR Flip Flop***

<img width="1646" height="978" alt="Screenshot 2025-09-16 200520" src="https://github.com/user-attachments/assets/781dea5e-7096-4e30-81f6-83db0c77751d" />


***JK Flip Flop***

<img width="1645" height="977" alt="Screenshot 2025-09-16 200543" src="https://github.com/user-attachments/assets/954d5db9-e1ad-4e9a-9ecb-6b0593aff4c6" />


***T Flip Flop***

<img width="1644" height="976" alt="Screenshot 2025-09-16 200607" src="https://github.com/user-attachments/assets/88dc7b4b-761e-4b7b-ae6e-9c52c1ead4ed" />


***Conclusion:***


