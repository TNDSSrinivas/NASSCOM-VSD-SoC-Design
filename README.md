# NASSCOM-VSD-Soc-Design
This repository describes the overall flow from RTL to GDSII.
## Table of Contents
1. [DAY1 - Introduction to open-source](#Day1---Introduction-to-open-source)
    1. [How to talk to Computers](#how-to-talk-to-Computers)
    2. [Soc design and OpenLANE](#Soc-design-and-OpenLANE)
    3. [Open-source EDA tools](#Open-source-EDA-tools)
2. [DAY2 - Floorplan and introduction to library cells](#Day2)
    1. [1.Chip Floor planning](#1.Floorplan)
    2. [2.Library Binding and Placement](#2.Placement)
    3. [3.Cell design and characterization flows](#3.Cell_design)
    4. [4.General timing Characterization parameters](#4.Timing)
3. [DAY3 - Design library cell using Magic layout and ngspice characterization](#Day3)
    1. [1.Labs for CMOS inverter](#1.CMOS_Inverter)
    2. [2.Inception of Layout](#2.Layout)
    3. [3.Sky130 Tech File Labs](#3.Sky130_tech_file)
4. [DAY4 - Pre-layout timing analysis](#Day4)
    1. [1.Timing modelling](#1.Modelling)
    2. [2.Timing analysis with ideal clocks](#2.Ideal_clocks)
    3. [3.Clock tree synthesis](#3.Clock_tree)
    4. [4.Timing analysis with real clocks](#4.Real_clocks)
5. [DAY5 - Final steps for RTL2GDS](#Day5)
    1. [1.Routing and Design rule check (DRC)](#1.Routing_&_DRC)
    2. [2.Power Distribution Network and routing](#2.Power)
    3. [3.TritonRoute Features](#3.TritonRoute)

## <a name="Day1---Introduction-to-open-source"></a>DAY1 - Introduction to open-source
### <a name="how-to-talk-to-Computers"></a>How to talk to Computers
- From the figure below, this board is an Arduino Uno. The yellow circle on the board indicates the area whhere the VLSI industry is working.
![Screenshot (256)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/6598798d-36c9-4804-a612-db4133f2f84d)

- This is the architecture of the Ardunio Uno board.
![Screenshot (257)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/547af97f-07f0-48e0-8a15-0b62fa95b0b9)

- This chip is known as Package.We have different types of packages, below image refer to package qfn-48 (Quard Flat No-Leads) where this 48 indicates the number of pins the package had.
- This is the way that wires are connected to the boundaries of the chip like this
![Screenshot (260)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/6262cd8d-57aa-43e5-b6bf-ab466e5a5b2b)

- Inside the chip it has various components
    1. Pads:
        - It is the external connection points where the chip makes contact with the outside world. It acts like a door to allow the signal from inside to outside world and vise versa.
    2. Core:
        - In the core where all the logic circuitry and functional components are located. It includes mux, gates and other elements this all placed in this area.
        - In core we have two types:
            1. Foundry IP's:
                - Basically this foundry IP's are provided by foundry where IP is known as Intellectual Properities.
            2. Macros:
                - It is purley on digital logic.
    3. Die:
        - It is the size of the entire chip, and it is manufactured on a silicon wafer.
    
 ![Screenshot (264)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/c66e16ea-2d25-442d-b8dc-c1d5ef0613bf)
 ![Screenshot (266)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/53a720df-f1d2-4d07-9f29-2b93d6f4803c)

- This describes how a program communicates with hardware. For implementing the hardware, Register Transfer Level (RTL) comes into the picture. 
![Screenshot (270)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/0ec5e2a4-4299-4520-84d1-0f9c62ff5265)

- When an application opens, it communicates with hardware using binary information. This communication involves different layers.
- There are three layers
    1. Operating System:
        - Generally Operating System operates different handles
        - The other part of handling is to take a particular application and convert it into respective assembly language, and finally into a binary language program so that can be understood by the hardware. This is the main purpose of an operating system.
    2. Compiler:
        - If a program is written in C or C++, it is taken by respective compiler and converted into instructions. These instructions depend on hardware being used.
        - If the hardware belongs to ARM architecture, then these instructions will be in ARM format.
    3. Assemble:
        - Assemble language is used to convert instructions into binary numbers that are understood by the machine.

![Screenshot (272)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/866b6a98-8262-4440-9aa0-d3a0e95eff0d)

- An instruction acts as an abstract interface between a C program and hardware. This abstract interface, which an instruction represents, is called an Instruction Set Architecture (ISA). ISA defines the architecture of a laptop or computer, it is how humans or users communicate with computers.
- To generate binary numbers, we need to use a hardware describtion language (HDL).
- This RTL (Register Transfer Level) description is synthesized into a netlist, which is a description of the logic gates and flip-flops in the design. This netlist is then used for physical design implementation.
![Screenshot (282)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/99693ef6-a765-42f6-8523-8ad0edb2911d)

### <a name="Soc-design-and-OpenLANE"></a>Soc design and OpenLANE

- Designing an Application-Specific Integrated Cricuit (ASIC) design in an automated way requires several elements, all of which must be present.
- They are:
    1. RTL IP's
    2. EDA Tools
    3. PDK Data
![Screenshot (285)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/e1754838-921e-46c8-81f2-4d2616184679)
![Screenshot (291)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/227c3fa5-3292-49a2-ba8b-d81cb1474dad)
![Screenshot (293)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/0ac4c974-b6c0-4467-8934-e40c09ead728)

- From RTL to GDSII (Graphic Data System II), the process involves several steps.
- They are:
    1. Synthesis:
        - Converts RTL to a circuit out of components from the standard cell library (SCL)
    2. Floor/Power Planning:
        - In Floor Planning they are two types
            1. Chip Floor-Planning - Partition the chip die between different system building blocks and place the I/O pads
            2. Macro Floor-Planning - Define the dimensions, pin locations and rows.
        - Power Planning - It includes power straps, pads and rings.
    3. Placement:
        - Place the cells on the floor plan rows, aligning them with the sites
        - It done in two steps Global and Detailed
    4. Clock Tree Synthesis:
        - It create clock distribution network to deliver the clock to all sequential elements with minimum skew and in good shap like a H-Tree, X-Tree, etc..
        - Clock skew defines the arrival of the clock at different components at different times
    5. Routing:
        - Implements the interconnect using the available metal layer that are pitch and tracks
        - They are two routing
            1. Global routing: Generates routing details
            2. Detailed Routing: Uses the routing guides to implement the actual wiring.
    6. Sign Off:
        - In signing off they are two types
            1. Physical Verifications: In physical verification the Design Rule Checking (DRC) and Layout vs Schematic (LVS) is verified
            2. Timing Verification: It verifies Static Timing Analysis (STA)

    ![Screenshot (293)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/02baae3f-afd0-4699-a353-6be24df9a0db)

- The main goal is to produce a clean GSDII with no human intervention.
![Screenshot (319)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/eb48cc8c-0dab-429c-bfa3-0b7f47d2bd11)
![Screenshot (320)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/88ea9c68-5d73-422d-82c8-fa99ccaad3a8)

- Below figure shows the flow from RTL to GDSII flow. Generally this flow operates in two modes Autonomous or Interactive
![Screenshot (329)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/b064e4c2-fae6-4173-9686-4e8821b7458a)

### <a name="Open-source-EDA-tools"></a>Open-source EDA tools

![Screenshot (344)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/e355f298-fbe0-4bde-91a6-dd4440f8feab)
![Screenshot (345)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/604da9ea-a1c1-4f0a-b519-26608cd6a3cc)

- OpenLANE runs in two modes
    1. Autonomous - To run in Autonomous mode, use the command './flow.tcl -design spm'.
    2. Interactive - To run in Interactive mode, use the command './flow.tcl -interactive'.
- In Interactive mode it involves various steps
    - package require openlane 0.9
    1. prep -design <design_name>
    2. run_synthesis
    3. run_floorplan
    4. run_placement
    5. run_cts
    6. run_routing
    7. run_magic
    8. run_magic_spice_exports
    9. run_magic_drc
    10. run_netgen
    11. run_magic_antenna_check

![Screenshot (346)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/d529ce3a-5a88-4011-a0df-e3a5a9345954)

- prep -design picorv32a
![Screenshot (347)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/9c37cd40-350f-432a-ba1f-bca8822be5c4)

- run_synthesis
![Screenshot (357)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/5a196414-7c99-4560-b938-9c89e4680cd6)

- The flop ratio for the image below can be calculated using the formula: Flop Ratio = Number of D Flip-Flops/Total Number of Cells.
- Flop Ratio = 1613/14876 = 0.108.
- Flop Ratio in percentage is 10.8%.
![Screenshot (359)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/124aac0f-7f9f-480e-9d8e-a07321533984)

