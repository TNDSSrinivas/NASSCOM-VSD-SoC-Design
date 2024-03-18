# NASSCOM-VSD-Soc-Design
This repository describes the overall flow from RTL to GDSII.
## Table of Contents
- [DAY1 - Introduction to open-source](#Day1---Introduction-to-open-source)
    - [How to talk to Computers](#how-to-talk-to-Computers)
    - [Soc design and OpenLANE](#Soc-design-and-OpenLANE)
    - [Open-source EDA tools](#Open-source-EDA-tools)
- [DAY2 - Floorplan and introduction to library cells](#Day2)
    - [1.Chip Floor planning](#1.Floorplan)
    - [2.Library Binding and Placement](#2.Placement)
    - [3.Cell design and characterization flows](#3.Cell_design)
    - [4.General timing Characterization parameters](#4.Timing)
- [DAY3 - Design library cell using Magic layout and ngspice characterization](#Day3)
    - [1.Labs for CMOS inverter](#1.CMOS_Inverter)
    - [2.Inception of Layout](#2.Layout)
    - [3.Sky130 Tech File Labs](#3.Sky130_tech_file)
- [DAY4 - Pre-layout timing analysis](#Day4)
    - [1.Timing modelling](#1.Modelling)
    - [2.Timing analysis with ideal clocks](#2.Ideal_clocks)
    - [3.Clock tree synthesis](#3.Clock_tree)
    - [4.Timing analysis with real clocks](#4.Real_clocks)
- [DAY5 - Final steps for RTL2GDS](#Day5)
    - [1.Routing and Design rule check (DRC)](#1.Routing_&_DRC)
    - [2.Power Distribution Network and routing](#2.Power)
    - [3.TritonRoute Features](#3.TritonRoute)

## <a name="Day1---Introduction-to-open-source"></a>DAY1 - Introduction to open-source
### <a name="how-to-talk-to-Computers"></a>How to talk to Computers
From the figure below, this board is an Arduino Uno. The yellow circle on the board indicates the area whhere the VLSI industry is working.
![Screenshot (256)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/6598798d-36c9-4804-a612-db4133f2f84d)
<br></br>
This is the architecture of the Ardunio Uno board.
![Screenshot (257)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/547af97f-07f0-48e0-8a15-0b62fa95b0b9)
<br></br>
This chip is known as Package.We have different types of packages, below image refer to package qfn-48 (Quard Flat No-Leads) where this 48 indicates the number of pins the package had.
<br>This is the way that wires are connected to the boundaries of the chip like this.</br>
![Screenshot (260)](https://github.com/TNDSSrinivas/NASSCOM-VSD-SoC-Design/assets/145267199/6262cd8d-57aa-43e5-b6bf-ab466e5a5b2b)
<br></br>
### <a name="Soc-design-and-OpenLANE"></a>Soc design and OpenLANE

### <a name="Open-source-EDA-tools"></a>Open-source EDA tools
