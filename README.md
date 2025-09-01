# Exp-No: 02 - SEVEN SEGMENT DISPLAY USING VERILOG HDL 

## **Aim:** <br>
<br>
&emsp;&emsp;To design and simulate a Seven-Segment Display Decoder using Verilog HDL and to verify its functionality through a testbench using the Vivado 2023.1 simulation environment. The experiment aims to understand how different abstraction levels in Verilog can be used to describe the same digital circuit and analyze their performance..<br>
<br>

## **Apparatus Required:** <br>
<br>
&emsp;&emsp;Vivado 2023.1<br>
<br>

## **Procedure:** <br>
<br>
1. Launch Vivado Open Vivado 2023.1 by double-clicking the Vivado icon or searching for it in the Start menu.<br>
2. Create a New Project Click on "Create Project" from the Vivado Quick Start window. In the New Project Wizard: Project Name: Enter a name for the project (e.g., Mux4_to_1). Project Location: Select the folder where the project will be saved. Click Next. Project Type: Select RTL Project, then click Next. Add Sources: Click on "Add Files" to add the Verilog files (e.g., mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.). Make sure to check the box "Copy sources into project" to avoid any external file dependencies. Click Next. Add Constraints: Skip this step by clicking Next (since no constraints are needed for simulation).
Default Part Selection: You can choose a part based on the FPGA board you are using (if any). If no board is used, you can choose any part, for example, xc7a35ticsg324-1L (Artix-7). Click Next, then Finish.<br>
3. Add Verilog Source Files In the "Sources" window, right-click on "Design Sources" and select Add Sources if you didn't add all files earlier. Add the Verilog files (mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.) and the testbench (mux4_to_1_tb.v).<br>
4. Check Syntax Expand the "Flow Navigator" on the left side of the Vivado interface. Under "Synthesis", click "Run Synthesis". Vivado will check your design for syntax errors. If any errors or warnings appear, correct them in the respective Verilog files and re-run the synthesis.<br>
5. Simulate the Design In the Flow Navigator, under "Simulation", click on "Run Simulation" → "Run Behavioral Simulation". Vivado will open the Simulations Window, and the waveform window will show the signals defined in the testbench.<br>
6. View and Analyze Simulation Results The simulation waveform window will display the signals (S1, S0, A, B, C, D, Y_gate, Y_dataflow, Y_behavioral, Y_structural). Use the time markers to verify the correctness of the 4:1 MUX output for each set of inputs. You can zoom in/out or scroll through the simulation time using the waveform viewer controls.<br>
7. Adjust Simulation Time To run a longer simulation or adjust timing, go to the Simulation Settings by clicking "Simulation" → "Simulation Settings".
Under "Simulation", modify the Run Time (e.g., set to 1000ns).<br>
8. Generate Simulation Report Once the simulation is complete, you can generate a simulation report by right-clicking on the simulation results window and selecting "Export Simulation Results". Save the report for reference in your lab records.<br>
9. Save and Document Results Save your project by clicking File → Save Project. Take screenshots of the waveform window and include them in your lab report to document your results. You can include the timing diagram from the simulation window showing the correct functionality of the 4:1 MUX across different select inputs and data inputs.<br>
10. Close the Simulation Once done, by going to Simulation → "Close Simulation<br>
<br>

## **Logic Diagram:** <br>
<br>
<img width="589" height="587" alt="image" src="https://github.com/user-attachments/assets/f7dc1a6b-016e-4fe0-9855-f46af48e912d" />
<br>

## **Truth Table:** <br>
<br>
<img width="750" height="351" alt="image" src="https://github.com/user-attachments/assets/4c575d61-dd52-4d13-970d-cc69ce23c5dd" />
<br>

## **Verilog Code:** <br>
**Seven Segment Behavioral Implementation:**
```
module sevenseg(bcd,seg);
input [3:0] bcd;
output reg[6:0] seg;
always@(bcd)
begin
case(bcd)
    4'b0000 : seg = 7'b0111111;
    4'b0001 : seg = 7'b0000110;
    4'b0010 : seg = 7'b1110011;
    4'b0011 : seg = 7'b1001111;
    4'b0100 : seg = 7'b1100110;
    4'b0101 : seg = 7'b1101101;
    4'b0110 : seg = 7'b1111101;
    4'b0111 : seg = 7'b0000111;
    4'b1000 : seg = 7'b1111111;
    4'b1001 : seg = 7'b1101111;
      default : seg = 7'b0;
    endcase
  end
endmodule
```
## **Testbench Implementation:**
**Seven Segment Behavioral Implementation:**
```
module sevenseg_tb;
    reg [3:0] bcd_t;
    wire [6:0] seg_t;
    sevenseg dut(.bcd(bcd_t),.seg(seg_t));
    initial
    begin
    bcd_t = 4'b0000;
    #100
    bcd_t = 4'b0001;
    #100
    bcd_t = 4'b0010;
    #100
    bcd_t = 4'b0011;
    #100
    bcd_t = 4'b0100;
    #100
    bcd_t = 4'b0101;
    #100
    bcd_t = 4'b0110;
    #100
    bcd_t = 4'b0111;
    #100
    bcd_t = 4'b1000;
    #100
    bcd_t = 4'b1001;
    end
 endmodule
```
## **Sample Output:**
```

Time=00 | s[1]=0 s[0]=0 | Inputs: a[0]=0 a[1]=0 a[2]=0 a[3]=0
        | out_gate=0 | out_dataflow=0 | out_behavioral=0 | out_structural=0
Time=04 | s[1]=0 s[0]=0 | Inputs: a[0]=1 a[1]=0 a[2]=0 a[3]=0
        | out_gate=1 | out_dataflow=1 | out_behavioral=1 | out_structural=1
Time=06 | s[1]=0 s[0]=1 | Inputs: a[0]=0 a[1]=1 a[2]=0 a[3]=0
        | out_gate=1 | out_dataflow=1 | out_behavioral=1 | out_structural=1
Time=08 | s[1]=1 s[0]=0 | Inputs: a[0]=0 a[1]=0 a[2]=1 a[3]=0
        | out_gate=1 | out_dataflow=1 | out_behavioral=1 | out_structural=1
Time=10 | s[1]=1 s[0]=1 | Inputs: a[0]=0 a[1]=0 a[2]=0 a[3]=1
        | out_gate=1 | out_dataflow=1 | out_behavioral=1 | out_structural=1
Time=12 | s[1]=0 s[0]=1 | Inputs: a[0]=0 a[1]=0 a[2]=1 a[3]=1
        | out_gate=0 | out_dataflow=0 | out_behavioral=0 | out_structural=0
Time=14 | s[1]=1 s[0]=0 | Inputs: a[0]=0 a[1]=1 a[2]=0 a[3]=1
        | out_gate=0 | out_dataflow=0 | out_behavioral=0 | out_structural=0
Time=16 | s[1]=1 s[0]=1 | Inputs: a[0]=0 a[1]=1 a[2]=1 a[3]=0
        | out_gate=0 | out_dataflow=0 | out_behavioral=0 | out_structural=0
Time=18 | s[1]=0 s[0]=0 | Inputs: a[0]=1 a[1]=1 a[2]=1 a[3]=1
        | out_gate=1 | out_dataflow=1 | out_behavioral=1 | out_structural=1
```

## **Output waveform** <br>
**Behavioral Level:**
<br>
<img width="1916" height="1199" alt="Screenshot 2025-08-26 163445" src="https://github.com/user-attachments/assets/f13f0a43-096c-4916-a2af-34b368d5a309" />
<br>

## **Conclusion:** <br>
<br>
&emsp;&emsp;In this experiment, a seven segment display was successfully designed and simulated using Verilog HDL . The simulation results verified the correct functionality of the Seven Segement display, with all implementations producing identical outputs for the given input conditions.



  
