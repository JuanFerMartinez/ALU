# Arithmetic and Logic Unit (ALU) for FPGA Implementation

This project implements an **Arithmetic and Logic Unit (ALU)** designed for an FPGA using VHDL. The system supports multiple arithmetic and logic operations, allowing real-time execution and visualization of results using LEDs and seven-segment displays.

## Features

- **Arithmetic Operations**: Supports signed arithmetic operations, including:  
  - `-A + 3`  
  - `-A - 3`  
  - `-B - 4`  
  - `-B - 3`  

- **Logical Operations**: Implements fundamental logic operations:  
  - `A AND B`  
  - `A OR B`  
  - `A XOR B`  
  - `NOT A`  

- **Multiplexed Selection**: A **2-to-1 multiplexer** selects between arithmetic and logic results based on the mode input (`S2`).  
- **FPGA Implementation**: Designed for a **Cyclone III FPGA** using Quartus, with pre-defined pin assignments for easy integration.  
- **Visual Output**:  
  - **Logical results** are displayed using **LEDs**.  
  - **Arithmetic results** are displayed using **two 7-segment displays**, supporting both positive and negative numbers.  
- **User Input**: The system takes two **4-bit operands (A and B)** and a **3-bit selector (S2, S1, S0)** for operation selection.  

## Components  

- **FPGA (Cyclone III - DE0 Board)**  
- **4-bit Inputs (A and B) from DIP Switches**  
- **3-bit Selection Input (`S2, S1, S0`) from Switches**  
- **Logic LEDs**: Displays logical results  
- **7-Segment Displays**: Shows arithmetic results  
- **Push Button for Mode Selection**  

## Project Structure  

- `GAluMain.vhd`: Top-level design integrating arithmetic and logic units with a multiplexer.  
- `ALU_Logica.vhd`: Implements bitwise logical operations.  
- `ALU_Aritmetica.vhd`: Implements arithmetic operations with signed representation.  
- `GMUX2T.vhd`: 2-to-1 multiplexer selecting between arithmetic and logic results.  
- `BCD_To_7Segment.vhd`: Converts 4-bit BCD values to seven-segment display output.  
- `DE0_pin_assignments.qsf`: Pin assignments for FPGA implementation.  

## How to Use  

1. **Select Inputs**:  
   - Use DIP switches for **A (SW[3:0])** and **B (SW[7:4])**.  
   - Use **SW[9:8]** for operation selection (`S1`, `S0`).  
   - Use a push button for switching between arithmetic and logic operations (`S2`).  

2. **Operations**:  
   - **Logic operations** will be shown on **LEDs**.  
   - **Arithmetic operations** will be shown on **7-segment displays**.  

3. **Interpret Output**:  
   - **Logic Mode (`S2 = 0`)** → LED lights display the logical result.  
   - **Arithmetic Mode (`S2 = 1`)** → The result appears in **HEX0 and HEX1**.  

## Pin Assignments (DE0 FPGA)  

- `A[3:0]` → `SW[3:0]` (First 4-bit input)  
- `B[3:0]` → `SW[7:4]` (Second 4-bit input)  
- `S1, S0` → `SW[9:8]` (Operation selection)  
- `S2` → `BUTTON[0]` (Mode selection: Arithmetic/Logic)  
- `Y[3:0]` → `LEDG[3:0]` (Logical output)  
- `HEX0` → `HEX0[6:0]` (7-segment display: Arithmetic Result)  
- `HEX1` → `HEX1[6:0]` (7-segment sign indicator)  

## Project Implementation Steps  

1. **Synthesize the VHDL code** in Quartus II.  
2. **Assign FPGA pins** using `DE0_pin_assignments.qsf`.  
3. **Compile and generate the programming file (`.sof`).**  
4. **Upload the bitstream to the FPGA** using the **USB Blaster**.  
5. **Interact with the switches and buttons** to verify operation execution.  

## Expected Behavior  

| `S2` | `S1 S0` | Operation | Logic Output (LEDs) | Arithmetic Output (HEX0, HEX1) |
|------|--------|------------|------------------|------------------|
| `0`  | `00`   | A AND B | LEDs show result | (N/A) |
| `0`  | `01`   | A OR B | LEDs show result | (N/A) |
| `0`  | `10`   | A XOR B | LEDs show result | (N/A) |
| `0`  | `11`   | NOT A | LEDs show result | (N/A) |
| `1`  | `00`   | `-A + 3` | (N/A) | HEX Displays show result |
| `1`  | `01`   | `-A - 3` | (N/A) | HEX Displays show result |
| `1`  | `10`   | `-B - 4` | (N/A) | HEX Displays show result |
| `1`  | `11`   | `-B - 3` | (N/A) | HEX Displays show result |

## Final Notes  

- Ensure **correct pin assignments** before programming the FPGA.  
- The **seven-segment displays are active-low**, meaning `0` turns on a segment.  
- The **LEDs should match logical operations**, while **arithmetic operations must be converted to BCD** for display.  
- If the **arithmetic result is negative**, `HEX1` should display a **"-"** symbol.  

🚀 **Now the ALU is fully implemented and functional on the FPGA!** 🚀
