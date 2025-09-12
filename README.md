# Exp-No: 01 - Write and simulate 4:1 Multiplexer using Verilog HDL and verify with testbench 


**Aim:** <br>
<br>
&emsp;&emsp;To design and simulate a 4:1 Mux using Verilog HDL and verify its functionality through a testbench using the Vivado 2023.1 simulation environment. 
<br>
**Apparatus Required:** <br>
<br>
&emsp;&emsp;Vivado 2023.1<br>
<br>
**Procedure:** <br>
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

Input/Output Signal Diagram:


RTL Code:

module mux_4_to_1(
    input wire a,
    input wire b,
    input wire c,
    input wire d,
    input wire [1:0] s,
    output reg y
    );

    always @(*)
    begin
        case(s)
            2'b00: y = a;
            2'b01: y = b;
            2'b10: y = c;
            2'b11: y = d;
            default: y = 1'bx;
        endcase
    end

endmodule


TestBench:

module mux_4_to_1_tb;

    reg tb_a;
    reg tb_b;
    reg tb_c;
    reg tb_d;
    reg [1:0] tb_s;
    wire tb_y;

    mux_4_to_1 dut (
        .a(tb_a),
        .b(tb_b),
        .c(tb_c),
        .d(tb_d),
        .s(tb_s),
        .y(tb_y)
    );

    initial begin
        // Test Case 1
        tb_a = 1'b1; tb_b = 1'b0; tb_c = 1'b1; tb_d = 1'b0;
        
        tb_s = 2'b00; #10;
        tb_s = 2'b01; #10;
        tb_s = 2'b10; #10;
        tb_s = 2'b11; #10;

        // Test Case 2
        tb_a = 1'b0; tb_b = 1'b1; tb_c = 1'b0; tb_d = 1'b1;

        tb_s = 2'b00; #10;
        tb_s = 2'b01; #10;
        tb_s = 2'b10; #10;
        tb_s = 2'b11; #10;
        
        #20;
        $finish;
    end

endmodule


Output waveform:
<img width="1519" height="796" alt="Screenshot 2025-09-10 112102" src="https://github.com/user-attachments/assets/b40b4cbf-3641-42fe-b2d8-aca02e562433" />



Conclusion:






  
