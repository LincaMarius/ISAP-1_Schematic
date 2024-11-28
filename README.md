# ISAP-1 Computer Schematic
The ISAP-1 computer is the improved version of the SAP-1 computer made by me.

ISAP Computer stands for Improved Simple as Possible Computer

This is the stage of choosing the electronic components used to make the ISAP-1 computer and designing the electronic schematic.

By: Lincă Marius Gheorghe.

Pitești, Argeș, România, Europe.

https://github.com/LincaMarius

## About the project, brief description
The goal of this project is to create a more efficient version of the SAP (Simple As Possible) computer, but with minimal changes so that the instruction format remains the same.

This project is part of a project made by me:
https://github.com/LincaMarius/ISAP-Computer


where I optimized the SAP-1 computer

## ISAP-1 version 1
The Structure of the SAP-1 computer is:

![ Figure 1 ](/Pictures/Figure1.png)

The Block Diagram of the Central Processing Unit of the ISAP-1 computer is:

![ Figure 2 ](/Pictures/Figure2.png)

The Output Device Block Diagram representing the original Output Register in the SAP-1 computer is as follows

![ Figure 3 ](/Pictures/Figure3.png)

The Block Diagram of the Memory Subsystem of the ISAP-1 computer which is identical to that of the SAP-1 computer is shown in the following figure

![ Figure 4 ](/Pictures/Figure4.png)

To design the Schematic, I used the KiCAD program

The implemented scheme will be almost identical to the original one of the SAP-1 Computer

### Program Counter Schematic
In the original scheme, the authors used 4 flip-flops connected in such a way that they form a binary counter with 16. For implementation, two 74LS107 integrated circuits were used.

The output from the circuit to the bus is done using four three-state drivers, using a 74LS126 integrated circuit.

The scheme does not show any changes from the original one.

I added decoupling capacitors with a value of 100nF for each integrated circuit used

![ Figure 5 ](/Pictures/Figure5.png)

### Address Register Schematic
In the original scheme, the authors used a 4-bit register using the 74LS173 integrated circuit which has a permanently active output.

Note that the connection of the inputs to the data bus is in reverse order in the original SAP-1 computer schematic, D0 is connected to pin 11, D1 is connected to pin 12, D2 is connected to pin 13 and D4 is connected to pin 14.

The outputs are also connected according to the inputs. The operation of the SAP-1 computer is not affected by this order.

![ Figure 6 ](/Pictures/Figure6.png)

I modified the pin connections to the bus according to the catalog data for the 74LS173.

Because the correspondence between inputs and outputs is maintained in both implementations, the operation of the computer is not influenced.

### Memory Subsystem
In the SAP-1 Computer, the Memory is represented in the middle of the System. Separation from the Central Processing Unit part is not possible.

In the ISAP-1 implementation, I separated the Memory Subsystem from the CPU and the I/O Subsystem.

Although the Memory subsystem is treated as a separate block, the scheme does not show any changes from the original one in SAP-1.

![ Figure 7 ](/Pictures/Figure7.png)

I also highlighted the components that are part of the Control Panel

The integrated circuit marked U4 in the diagram, type 74LS157, which consists of 4 2-to-1 multiplexers, is used to select the address.

If switch SW2 is in the “Program” position, the address given by the Address Register via the Address Bus is selected, otherwise if switch SW2 is in the “Run” position, the value set by switch group SW1 is selected as the address.

