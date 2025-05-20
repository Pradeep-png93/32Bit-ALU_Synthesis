# 32Bit-ALU_Synthesis

## Aim:

Synthesize 32 Bit ALU design using Constraints and analyse area and Power reports.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,
![Screenshot 2025-05-20 105429](https://github.com/user-attachments/assets/fac15f58-4e03-49f8-97ce-83a935242b11)

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

# Design Code
```
module ALU ( input [3:0] A, B,
input [2:0] ALU_Sel,
output reg [3:0] ALU_Out,
output reg CarryOut );
always @(*) begin
    case (ALU_Sel)
        3'b000: {CarryOut, ALU_Out} = A + B;
        3'b001: {CarryOut, ALU_Out} = A - B;
        3'b010: ALU_Out = A & B;
        3'b011: ALU_Out = A | B;
        3'b100: ALU_Out = A ^ B;
        3'b101: ALU_Out = ~A;
        3'b110: ALU_Out = A << 1;
        3'b111: ALU_Out = A >> 1;
        default: ALU_Out = 4'b0000;
    endcase
end
endmodule
```

# TestBench:
```
module ALU_tb;
reg [3:0] A, B;
reg [2:0] ALU_Sel;
wire [3:0] ALU_Out;
wire CarryOut;

ALU uut (
    .A(A),
    .B(B),
    .ALU_Sel(ALU_Sel),
    .ALU_Out(ALU_Out),
    .CarryOut(CarryOut)
);

initial begin
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b000; #10;
    A = 4'b0101; B = 4'b0011; ALU_Sel = 3'b001; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b010; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b011; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b100; #10;
    A = 4'b1100; B = 4'b1010; ALU_Sel = 3'b101; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b110; #10;
    A = 4'b0011; B = 4'b0000; ALU_Sel = 3'b111; #10;
    $finish;
end
endmodule
```

### Step 2 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh
![Screenshot 2025-05-20 105446](https://github.com/user-attachments/assets/71debf33-ee15-4b9d-a72c-165fd560e402)

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.
![Screenshot 2025-05-20 110751](https://github.com/user-attachments/assets/b807ac56-a0d2-431a-a1ab-b04ffa658e38)

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.

#### Synthesis RTL Schematic :
![image](https://github.com/user-attachments/assets/27e58ac3-fef4-45ec-84da-796612a65553)

#### Area report:
![Screenshot 2025-05-20 111321](https://github.com/user-attachments/assets/66906af0-7b55-4f45-8a56-dfde93287148)

#### Power Report:
![Screenshot 2025-05-20 111503](https://github.com/user-attachments/assets/1dad72fb-6354-47d2-a834-7bbd51c7994b)

#### Result: 
![Screenshot 2025-05-20 111022](https://github.com/user-attachments/assets/681055ad-a98e-432f-9d68-3e9ada5c186b)

The generic netlist of 32 bit ALU  has been created, and area, power reports have been tabulated and generated using Genus.
