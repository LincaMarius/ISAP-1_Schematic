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
The final structure of the SAP-1 computer and implicitly the ISAP-1 computer is:

![ Figure 1 ](/Pictures/Figure1.png)

The original block diagram of the Central Processing Unit of the SAP-1 computer and implicitly of the ISAP-1 computer is:

![ Figure 2 ](/Pictures/Figure2.png)

Initially, I used Altium Designer to design the Schematic and PCB.

But so that they can be viewed and possibly edited by anyone, I put the KiCAD-edited version on GitHub because this program is free and can be used freely by anyone.

The implemented scheme will be almost identical to the original one of the SAP-1 Computer.

### Program Counter Schematic
In the original schematic, the authors used 4 Flip-Flops connected in such a way that they form a Binary Counter. For implementation, two 74LS107 were used for this purpose.

Counting is done when the CP control signal is active and the falling edge of the clock signal appears.

The Program Counter has its output connected to the Bus, therefore it must be Tri-State. A 74LS126 chip is used for this purpose

The output from the circuit to the bus is done using four three-state drivers, using a 74LS126 integrated circuit.

The Schematic Diagram does has no changes from the original one.

![ Figure 3 ](/Pictures/Figure3.png)

### Address Register Schematic
In the original scheme, the authors used a 4-bit register using the 74LS173 integrated circuit which has a permanently active output.

Note that the connection of the inputs to the data bus is in reverse order in the original SAP-1 computer schematic, D0 is connected to pin 11, D1 is connected to pin 12, D2 is connected to pin 13 and D4 is connected to pin 14.

The outputs are also connected in the reverse order. The operation of the SAP-1 computer is not affected by this order because the correspondence between inputs and outputs is maintained.

I modified the pin connections to the bus according to the catalog data for the 74LS173.

Because the correspondence between inputs and outputs is maintained in both implementations, the operation of the computer is not influenced.

The Schematic Diagram does has no changes from the original one.

![ Figure 4 ](/Pictures/Figure4.png)

### Memory Subsystem
In the SAP-1 Computer, the Memory is represented in the middle of the System. Separation from the Central Processing Unit part is not possible.

In the ISAP-1 implementation, I separated the Memory Subsystem from the CPU and the I/O Subsystem.

The Block Diagram of the Memory Subsystem of the ISAP-1 computer which is identical to that of the SAP-1 computer is shown in the following figure

![ Figure 5 ](/Pictures/Figure5.png)

Although the Memory subsystem is treated as a separate block, the scheme does not show any changes from the original one in SAP-1.

I also highlighted the components that are part of the Control Panel

![ Figure 6 ](/Pictures/Figure6.png)

The integrated circuit marked in the diagram C5 in the SAP-1 schematic and U5 in the ISAP-1 schematic of the 74LS157 type which consists of 4 2-to-1 multiplexers is used to select the address.

If switch SW2 is in the “Program” position, the address given by the Address Register via the Address Bus is selected, otherwise if switch SW2 is in the “Run” position, the value set by switch group SW1 is selected as the address.

From the catalog data of the 74LS189 chip we find that when the #CE input is low, this chip outputs the Data stored at the selected Address, this happens when the DM (CE) control signal is activated or when the SW2 switch is moved to the “Programming” position.

### Instruction Register
The Instruction Register is made using two integrated circuits of the 74LS173 type which is a 4-bit register.

The first chip marked U8 in the diagram stores the upper nibble which represents the binary code of the instruction being executed.

The second chip marked in the diagram U9 stores the lower nibble which represents the parameter for the instruction being executed.

According to the catalog data for the 74LS173 integrated circuit, pin 14 is D0 and the corresponding output Q0 is pin 3, pin 13 is D1 and the corresponding output Q1 is pin 4, pin 12 is D2 and the corresponding output Q2 is pin 4, and pin 11 is D3 and the corresponding output Q3 is pin 6.

But in the SAP-1 computer schematic, pin 14 which is D0 and pin 3 which is Q0 are connected to bit 3 of the W Bus, pin 13 which is D1 and pin 4 which is Q1 are connected to bit 2 of the W Bus, pin 12 which is D2 and pin 5 which is Q2 are connected to bit 1 of the W Bus and pin 11 which is D3 and pin 6 which is Q3 are connected to bit 0 of the W Bus.

So, the order of inputs and outputs is reversed. Since the inputs and outputs are also reversed accordingly, the operation of the SAP-1 computer is normal.

I connected the chip pins to the bus in the order given in the catalog sheets

The Schematic does not present any other changes compared to the original one.

![ Figure 7 ](/Pictures/Figure7.png)

### Accumulator Register
The Accumulator register is made using two 4-bit 74LS173 type registers marked U10 and U11 in the diagram (in the original diagram they are marked C10 and C11).

Pin 1 and pin 2 are connected to ground which causes the outputs to be permanently active. Thus, the contents of the Accumulator Register are permanently transmitted to the ALU via signals AC0 to AC7.

The contents of the Accumulator Register are put on the bus when the EA control signal is active, which activates the 8 Tri-State drivers. The Tri-State drivers are implemented using two 74LS126 chips, each containing 4 Tri-State drivers.

As in the previous cases, the order of inputs and outputs is reversed from the order of the bits on the W bus. Since the inputs and outputs are also reversed accordingly, the operation of the SAP-1 computer is normal.

I connected the chip pins to the bus in the order given in the catalog sheets

The schematic does not present any other changes compared to the original one.

I added decoupling capacitors with a value of 100nF for each integrated circuit used

![ Figure 11 ](/Pictures/Figure11.png)

### Arithmetic and Logic Unit
The SAP-1 computer has no Logic Unit, it can only perform the Addition and Subtraction operations.

The main element of the Arithmetic Unit is the 74LS83 integrated circuit which is a 4-bit Full Adder, so two such chips are used.

The Subtract Operation is performed by 2's Complementing the operand B. For this purpose, 8 x XOR Gates are used. Each 74LS86 chip has 4 gates, so 2 chips are used.

The result is transmitted on the Bus via 8 three-state buffers when the EU control signal is active. These buffers are of the 74LS126 type. Each chip has 4 buffers, so 2 chips are required.

The schematic does not present any other changes compared to the original one.

I added decoupling capacitors with a value of 100nF for each integrated circuit used

![ Figure 12 ](/Pictures/Figure12.png)

### Register B
Register B acts as a temporary storage register, where the operand B required by the Adder to perform the Addition operation is loaded.

In the original schematic, two 4-bit 74LS173 registers are used, denoted C20 and C21.

When the LB control signal is low and the rising edge of the clock signal appears, the data present on the Bus is loaded into the registers.

The output is connected to input B of the Adder and is permanently enabled by connecting pins 1 and 2 to ground.

The schematic does not present any other changes compared to the original one.

I added decoupling capacitors with a value of 100nF for each integrated circuit used

![ Figure 13 ](/Pictures/Figure13.png)

### Output Device – Binary Display
In the SAP-1 computer the output device is called the Output Register and is present in the Block Diagram at the bottom right of the drawing.

The Binary Display is made with 8 LEDs connected directly to the output of the Output Register.

![ Figure 14 ](/Pictures/Figure14.png)

### Output Device
In the original schematic, two 4-bit 74LS173 registers are used, denoted C22 and C23.

When the LO control signal is low and the rising edge of the clock signal appears, the data present on the Bus is loaded into the registers.

The output is permanently active because pins 1 and 2 are connected to ground. The outputs are labeled O0 to O7.

![ Figure 15 ](/Pictures/Figure15.png)

### Binary Display
The Binary Display consists of eight LEDs connected to eight current limiting resistors of 1k ohm each.

The current is limited by resistors for a red LED to the value of (Voh – Vled) / (R + Rint) = (2.4V – 1.8V) / (1000 + 100) = 0.5 / 1100 = 0.5mA (theoretical)

The schematic does not present any other changes compared to the original one.

![ Figure 16 ](/Pictures/Figure16.png)

### Control Panel
The control panel provides the user interface.

The control panel provides the user interface. Contains the Reset circuit, Manual/Automatic mode selector, Step button, main clock.

The schematic does not present any other changes compared to the original one.

I added decoupling capacitors with a value of 100nF for each integrated circuit used

![ Figure 17 ](/Pictures/Figure17.png)

### Control Unit
The Control Unit's role is to direct the flow of data between the various Component Blocks of the Computer to ensure its operation and achieve the expected results.

It consists of three elements: the Instruction Decoder, the Ring Counter, and the Control Matrix.

The schematic does not present any other changes compared to the original one.

I added decoupling capacitors with a value of 100nF for each integrated circuit used

![ Figure 18 ](/Pictures/Figure18.png)

### ISAP-1 computer assembly
The Hierarchical Structure Diagram of the ISAP-1 Computer is as follows

![ Figure 19 ](/Pictures/Figure19.png)

To power the computer with 5 volts, we included a Barrel Jack plug and a USB - A connector.

An overview of the PCB is shown in the following figure

![ Figure 20 ](/Pictures/Figure20.png)