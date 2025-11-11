# Inception of open-source EDA,OPENLANE and sky130 PDK
## Overview from Application to Hardware
-   **Apps**: Application software, often referred to as "apps," performs specific tasks or functions for end-users.
    
-   **System Software**: This category acts as an intermediary between hardware components and user-facing applications. It provides essential services, manages resources, and enables application execution.
    
-   **Operating System**: The fundamental software managing hardware resources and offering services for users and applications. It controls memory, processes, files, and interfaces (e.g., Windows, macOS, Linux, Android).
    
-   **Compiler**: Translates high-level programming code( C ,C++ , java etc... ) into assembly-level language.
    
-   **Assembler**: Converts assembly language code into machine code ( 10101011100 ) for direct processor execution.
    
-   **RTL (Register Transfer Level)**: Represents digital circuit behavior using registers and data transfer operations.
    
-   **Hardware**: Physical components of a computer system or electronic device enabling various tasks.
## Why do we need a Chip?
Consider the Arduino Uno, a versatile development board used for various projects. At its core lies the ATmega328P microcontroller, a crucial component.

Here's why we need this chip: The Arduino Uno is powered by the ATmega328P microcontroller. This chip serves as the brain of the board and is responsible for executing user-programmed code. It contains program memory (Flash), RAM, EEPROM, and various hardware peripherals. The microcontroller handles input, output, and data processing, making it the central processing unit (CPU) of the Arduino Uno. It operates at a clock speed of 16 MHz, ensuring precise timing for program execution.
## Components of a Chip:
A chip comprises several key components:
-   **Macros**: Predefined, reusable digital circuit blocks, like standard cells, simplifying complex chip design.
    
-   **Foundry IPs (Intellectual Property)**: Pre-designed, verified circuit elements (e.g., analog blocks, memory cores) licensed from semiconductor foundries for custom chip integration.
    
-   **IO Pads and Pins**: IO pads are physical interfaces connecting the chip to the external world. IO pins facilitate electrical connections between these pads and the internal circuitry for input and output communication.
## Overview of RTL to GDS Flow:
The RTL to GDS (Register-Transfer Level to Graphic Data System) flow is a complex process that transforms a high-level chip design into a physical layout ready for manufacturing. Here are the key steps involved:

1.  RTL Design

-   Creation of a high-level chip functionality description using HDL (Hardware Description Language) like VHDL or Verilog.
-   Captures the behavior and logic of the design.

1.  Functional Verification

-   Subject the RTL design to functional verification to ensure it adheres to specifications.
-   Use simulation and test benches to validate functionality and performance.

1.  RTL Synthesis

-   Transform RTL code into a gate-level representation using a synthesis tool.
-   Maps RTL onto a library of standard cells, optimizing for area, power, and timing.

1.  Technology Mapping

-   Map the synthesized gate-level netlist to the target technology library.
-   Replace generic gates with technology-specific counterparts (e.g., NAND, NOR, XOR).

1.  Physical Design

-   Transform the gate-level netlist into a manufacturable physical layout.

-   a. **Floorplanning**: Determine the chip's area and organize the placement of major components.
-   b. **Placement**: Assign specific gate and flip-flop locations, optimizing for metrics like wire length and performance.
-   c. **Clock Tree Synthesis (CTS)**: Create a clock distribution network to ensure uniform clock signals with minimal skew.
-   d. **Routing**: Establish physical interconnections using metal and polysilicon layers. Includes global and detailed routing.
-   e. **Physical Verification**: Check layout against design rules, including timing, power, signal, and rule violations.

1.  GDS Generation

-   Generate the GDS (Graphic Data System) file.
-   This binary file format represents the complete chip layout, including geometric details and interconnections.

1.  Signoff

-   Encompasses verification and validation steps.

The RTL to GDS flow is a critical process in chip design, ensuring the translation of high-level design into a manufacturable physical layout.
### Key Components Needed for ASIC Development
To develop an ASIC efficiently, you need three key components:

1.  **RTL IPs**: Source from platforms like GitHub, OpenCores, and LibreCores for pre-designed RTL blocks.
    
2.  **PDK Data**: Process Design Kit (PDK) data is needed to get the Design Fabricated.
    
3.  **EDA Tools**: Use Electronic Design Automation (EDA) tools for RTL synthesis, layout design, and verification.
# DAY 1: OpenLane and SKYWATER-130
The Skywater PDK files we are working with are described under `pdks`

1.  **SKYWATER-PDK**: This directory contains essential PDK files provided by the foundry, serving as the foundation for ASIC development.
    
2.  **Open\_pdks**: In this directory, you'll find scripts that bridge closed-source and open-source PDKs, ensuring compatibility with various Electronic Design Automation (EDA) tools. These scripts facilitate seamless integration.
    
3.  **Sky130A**: Specifically tailored for Skywater, this directory houses open-source-compatible PDK files. They are designed to work harmoniously with open-source EDA tools, empowering users to develop ASICs without reliance on proprietary software.

## Hands-on OpenLane Flow :
1.  Navigate to the OpenLane directory in your terminal.
    
2.  Type the following command: OpenLane provides the flexibility to run the entire flow in one go or to use an interactive mode for a more detailed step-by-step process
```
make mount
./flow.tcl -interactive
```
3.  Software Dependencies for OpenLane

To ensure that OpenLane functions correctly, you need to manage software dependencies. You can import these dependencies into the OpenLane tool by using the following command:
```
package require openlane
```
![openlane](images/1.png)
4.  Preparing the Design in OpenLane

In OpenLane, the "prep" step is crucial for setting up the file structure and merging essential technology and cell information.

-   **File Structure Setup**: Create a structured directory in your project's design folder.
    
-   **Configurations**: The "config.tcl" file generated in this folder contains critical parameters used by OpenLane for your specific run. These configurations tailor the OpenLane flow to your design.
    
-   **Merging Technology and Cell Data**: The command merges essential technology LEF data, which includes layer definitions and design rules needed for Place-and-Route (PnR). Additionally, it combines cell LEF data, reducing Design Rule Check (DRC) errors during the PnR process.
![openlane](images/2.png)
Prepare design command :

```
prep -design <design_name> -tag <tag>

```

After running the `prep` command, you'll find a well-structured project directory with all the necessary information and configurations, ready for the OpenLane flow.
![openlane](images/3.png)
## Synthesis 
run synthesis using this command 
```
run_synthesis
```
![openlane](images/4.png)
the result of synthesis is
![openlane](images/5.png)
![openlane](images/6.png)
