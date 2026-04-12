# iMX6 Bare Bones

An open source development board using the NXP i.MX 6ULL application processor. This design was completed using KiCad version 9.0.6.

## Project Status, April 11th, 2026: 

This is the first revision of the completed PCBA design. It has not been fabricated or assembled yet. I am quoting the bare PCB with both JLCPCB and PCBWay, and sourcing the components.

I have not yet created a linux build for this design, but will doing so using the Yocto project.

## Objectives

The iMX6 Bare Bones project was created with the following objectives:
- Create an open source PCBA for learning digital hardware and embedded linux design
- Implement minimum peripherals and interfaces to prioritize simplicity
- Specified impedance control using a standard PCB stackup published by a low-cost fabricator
- Power management using buck converters and LDOs, with no complex PMICs
- Expose interfaces such as GPIO, SPI, I2C and CAN over standard 0.1 inch / 2.54 mm headers. Users can create their own daughter PCBAs.
- Can be powered from a widely available power adapter (USB C, 15W selected)

## Architecture

System Block Diagram:

<img width="1641" height="820" alt="block_diagram" src="Design Files\Images\block_diagram.png" />

<br>The i.MX 6ULL processor was selected mainly for it's simple and forgiving boot sequence requirements.

## PCB Design and Layout

PCBA, Top 3D View

<img width="1786" height="1213" alt="pcba_top" src="Design Files\Images\pcba_top.png" />

<br>PCBA, Bottom 3D View

<img width="1808" height="1176" alt="pcba_bottom" src="Design Files\Images\pcba_bottom.png" /><br>

### Placement
- All I/O connectors are placed along a single board edge. This enables easy cable insertion from the front of a system with an enclosure design.
- The power input is a USB C connector on the opposite board edge. A 15W wall adapter can be plugged into the back of a system.
- The 0.1 inch vertical headers allow daughter boards to be installed on top of the system. 
- Most components are placed on the top side of the PCB. The bottom was reserved mostly for passives and smaller SMD components. The largest component on the bottom is the QSPI flash U3, with a height of 63 mils / 1.6 mm.

### Stackup
- The PCB thickness was selected to be 1.6 mm. The design intent was to use a standard stackup listed online from a low-cost PCBA manufacturer.
- The selection was made while considering several factors to enable impedance control and DDR routing:
  - DDR3 requires 50 ohm impedance for single ended, and 100 ohm impedance for differential signals
  - Routing a x16 DDR interface while maintaining sufficient clearance between traces requires relatively thin traces. The i.MX 6ULL HDG recommends a trace width of 4.5 mils, which is used on their SODIMM reference design.
  - The thinnest outer-layer prepreg I coud find in a 1.6 mm stackup was JLC061611_3313D from JLCPCB. The prepreg thickness is 3.62 mils / 0.092 mm in this stackup.
  - Using JLC PCB's online [impdedance calculator](https://jlcpcb.com/impedance), this requires a trace width of 5.62 mm for 50 ohm single ended signals. 





