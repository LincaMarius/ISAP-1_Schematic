# ISAP-1 Computer Schematic
The ISAP-1 computer is the improved version of the SAP-1 computer made by me.

ISAP Computer stands for Improved Simple as Possible Computer

This is the stage of choosing the electronic components used to make the ISAP-1 computer and designing the electronic schematic.

By: Lincă Marius Gheorghe.

Pitești, Argeș, Romania, Europe.

https://github.com/LincaMarius

## About the project, brief description
The goal of this project is to create a more efficient version of the SAP (Simple As Possible) computer, but with minimal changes so that the instruction format remains the same.

This project is part of a project made by me:
https://github.com/LincaMarius/ISAP-Computer


where I optimized the SAP-1 computer

## ISAP-1 Model A Version 1
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
In the original schematic, the authors used a 4-bit register using the 74LS173 chip which has a permanently active output.

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

Although the Memory subsystem is treated as a separate block, the schematic does not show any changes from the original one in SAP-1.

I also highlighted the components that are part of the Front Panel

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

![ Figure 8 ](/Pictures/Figure8.png)

### Arithmetic Unit
The SAP-1 computer has no Logic Unit, it can only perform the Addition and Subtraction operations.

The main element of the Arithmetic Unit is the 74LS83 chip which is a 4-bit Full Adder, so two such chips are used.

The Subtract Operation is performed by 2's Complementing the operand B. For this purpose, 8 x XOR Gates are used. Each 74LS86 chip has 4 gates, so 2 chips are used.

The result is transmitted on the Bus via 8 three-state buffers when the EU control signal is active. These buffers are of the 74LS126 type. Each chip has 4 buffers, so 2 chips are required.

The schematic does not present any other changes compared to the original one.

![ Figure 9 ](/Pictures/Figure9.png)

### Register B
Register B acts as a temporary storage register, where the operand B required by the Adder to perform the Addition operation is loaded.

In the original schematic, two 4-bit 74LS173 registers are used, denoted C20 and C21.

When the LB control signal is low and the rising edge of the clock signal occurs, the data present on the Bus is loaded into the registers.

The output is connected to input B of the Adder and is permanently enabled by connecting pins 1 and 2 to ground.

The schematic does not present any other changes compared to the original one.

![ Figure 10 ](/Pictures/Figure10.png)

### Output Device – Binary Display
In the SAP-1 computer the output device is called the Output Register and is present in the Block Diagram at the bottom right of the drawing.

The Binary Display is made with 8 LEDs connected directly to the output of the Output Register.

![ Figure 11 ](/Pictures/Figure11.png)

### Output Device
In the original schematic, two 4-bit 74LS173 registers are used, denoted C22 and C23.

When the LO control signal is low and the rising edge of the clock signal appears, the data present on the Bus is loaded into the registers.

The output is permanently active because pins 1 and 2 are connected to ground. The outputs are labeled O0 to O7.

The schematic does not present any other changes compared to the original one.

![ Figure 12 ](/Pictures/Figure12.png)

### Binary Display
The Binary Display consists of eight LEDs connected to eight current limiting resistors of 1k ohm each.

The current is limited by resistors for a red LED to the value of (Voh – Vled) / (R + Rint) = (2.4V – 1.8V) / (1000 + 100) = 0.5 / 1100 = 0.5mA (theoretical)

The schematic does not present any other changes compared to the original one.

![ Figure 13 ](/Pictures/Figure13.png)

### Front Panel
The control panel provides the user interface. Contains the Reset circuit, Manual/Automatic mode selector, Step button, main clock.

The schematic does not present any other changes compared to the original one.

![ Figure 14 ](/Pictures/Figure14.png)

### Control Unit
The Control Unit's role is to direct the flow of data between the various Component Blocks of the Computer to ensure its operation and achieve the expected results.

It consists of three elements: the Instruction Decoder, the Ring Counter, and the Control Matrix.

The schematic does not present any other changes compared to the original one.

![ Figure 15 ](/Pictures/Figure15.png)

### Power supply
The power supply's role is to provide the 5 Volt supply voltage and support the computer's power consumption.

This power supply is powered directly from the Mains and consists of a step-down transformer followed by a full bridge rectifier and an integrated regulator of 5 Volts.

The transformer according to the Bill of Materials is of the F-25X type and has a primary voltage of 115 Volts, but in Europe a transformer with a primary voltage of 240 Volts is required.

The secondary voltage according to the Materials List on page 502 in the original book is 12.6 Volts. Nowadays we can buy standard transformers with a secondary voltage of 12 Volts.

The nominal power of the transformer for a current consumption of maximum 1.5 Amps is 12V x 1.5A = 18 VA.

The maximum voltage on capacitor C3 is: Vmax = Vsec * 1.41 – 2 * Vd = 12 * 1.414 – 2 * 0.8 = 16.97 – 1.6 = 15.37 Volts

The voltage ripple on the filter capacitor C3 is: dU = (Iout * T) / (2 * C3)

For a mains voltage frequency of 50 Hz we have T = 1/f = 1/50 = 0.02 s

For a mains voltage frequency of 60 Hz we have T = 1/f = 1/50 = 0.017 s

Since we have a double alternating rectification the pulsation frequency is doubled, so the period is halved

Thus the ripple period is: T = 0.01s for mains voltage with a frequency of 50 Hz and T = 0.0083s for mains voltage with a frequency of 60 Hz.

The voltage ripple on the filter capacitor C3 is: dU = (1.5A * 0.01s) / (2 * 0.001F) = 0.015 / 0.002 = 7.5 Volts for mains voltage with a frequency of 50 Hz.

The voltage ripple on the filter capacitor C3 is: dU = (1.5A * 0.0083s) / (2 * 0.001F) = 0.01245 / 0.002 = 6.225 Volts for mains voltage with a frequency of 60 Hz.

The minimum voltage on the filter capacitor C3 is: Vmin = Vmax – dU = 15.37V – 7.5V = 7.87 Volts for mains voltage with a frequency of 50 Hz.

The minimum voltage on the filter capacitor C3 is: Vmin = Vmax – dU = 15.37V – 6.225V = 9.145 Volts for mains voltage with a frequency of 60 Hz.

The average voltage on the filter capacitor C3 is: V = Vmax – dU/2 = 15.37V – 7.87V/2 = 15.37V – 3.935V = 11.435 Volts for mains voltage with a frequency of 50 Hz.

The average voltage on the filter capacitor C3 is: V = Vmax – dU/2 = 15.37V – 6.225V/2 = 15.37V – 3.1125V = 12.2575 Volts for mains voltage with a frequency of 60 Hz.

The maximum power dissipated by the LM340T-5 integrated regulator is: P = (Vin – Vout) * I = (11.435V – 5V) * 1.5A = 6.435V * 1.5A = 9.66 Watts for mains voltage with a frequency of 50 Hz.

The maximum power dissipated by the LM340T-5 integrated regulator is: P = (Vin – Vout) * I = (12.2575V – 5V) * 1.5A = 7.2575V * 1.5A = 10.87 Watts for mains voltage with a frequency of 60 Hz.

To dissipate this power, we have provided a radiator to cool the integrated stabilizer. Otherwise, it will go into overtemperature protection.

![ Figure 16 ](/Pictures/Figure16.png)

### ISAP-1 computer assembly
The Hierarchical Structure Diagram of the ISAP-1 Computer is as follows

![ Figure 17 ](/Pictures/Figure17.png)

An overview of the PCB is shown in the following figure

![ Figure 18 ](/Pictures/Figure18.png)

This is what the completed PCB looks like for ISAP-1 Model A Version 1.0

![ Figure 19 ](/Pictures/Figure19.png)

The ISAP-1 computer project made in KiCAD is here: \
https://github.com/LincaMarius/ISAP-1_Schematic/tree/main/KiCAD/ISAP-1_modelA_ver1_0.zip

*A total of 48 chips were used to implement this version of the ISAP-1 computer.*

## ISAP-1 Model A Version 1.1
In Version 1.1, an improvement is made to the ISAP-1 computer by implementing the Variable Machine Cycle.

The Instruction Set remains unchanged but the Control Block implementation changes.

In the book on page 163 the authors present a method of improving the SAP-1 Computer by implementing the Variable Machine Cycle.

The schematic is shown in Figure 10-17 and consists of 5 inverters and a 12-input NAND gate that generates the #NOP signal when the Control Block output has the NOP instruction encoded in Hexadecimal as 3E3h and a two-input AND gate that resets the Ring Counter when the #NOP or #CLR signal is low. 

We can note that the SAP-1 Computer schematic is not modified to implement this functionality, only two logic gates are added.

### Control Block Update
Version 1.1 of the ISAP-1 computer presents the modification of the Control Block as described by the authors, which implements Variable Length Microcode.

The schematic is modified by adding 2 gates and 5 inverters, but it is not necessary to redesign the computer.

The starting point is the Control Block diagram of version 1.0 shown in figure 15.

The scheme presented in the book to be implemented is intended for a control matrix made with ROM memory.

Because in the current version we use logic gates to implement the control matrix, we have greater freedom to select the signals we are interested in.

The signals CP, PE, EA, SI and EU must be inverted.

The CP signal is T2 and must be inverted.

The EP signal is T1, so the inverted EP is the inverted T1. This is available at the output of the inverter U35E.

The EA signal is the output of gate U42A inverted by U35F, so if EA is inverted once more it is the same signal as that available before the double inversion, i.e. the signal from the output of gate U42A can be used directly without inversion.

The SU signal is the output of gate U42B inverted by U48A, so if SU is inverted once more it is the same signal as that available before the double inversion, i.e. the signal from the output of gate U42B can be used directly without inversion.

The EU signal is the output of gate U42B and must be inverted.

In conclusion, only the CP and EU signals need to be inverted.

All of these signals act as inputs to a 12-input NAND gate.

For implementation, a 12-input NAND gate of the 74S134 type, a 13-input NAND gate of the 74ALS133 type can be used.

Another variant is using:
- one 8-input NAND part of the 74LS30 type, one 4-input NAND part of the 74LS20 type and one 2-input OR part of the 74LS32 type
- three 4-input NAND parts of the 74LS20 type, one 3-input NOR part of the 74LS27 type and one 74LS04 type inverter
- four 3-input NAND parts of the 74LS10 type, one 4-input NOR part of the 74LS29 type and one 74LS04 type inverter
- or six 2-input NAND parts of the 74LS00 type, three 3-input NOR parts of the 74LS27 type and one 74LS04 type inverter

I implemented the new version using the available logic gates that were not used by the authors of the book, so I added only one chip.

I used the U48B inverter and the U48C inverter to invert the CP and EU signals.

I used the 74LS133 chip which is a 13-input NAND gate.

For the reset signal control, instead of adding a new 74LS08 chip to use a single AND logic gate, I used an available two-input 74LS00 NAND gate marked U43D and inverted its output signal with the U48D inverter.

The Control Block schematic of the ISAP-1 Model A Version 1.1 computer is shown in the following figure:

![ Figure 20 ](/Pictures/Figure20.png)

This is what the completed PCB looks like for ISAP-1 Model A Version 1.1

![ Figure 21 ](/Pictures/Figure21.png)

An overview of the PCB is shown in the following figure

![ Figure 22 ](/Pictures/Figure22.png)

The ISAP-1 Model A Version 1.1 computer project made in KiCAD is here: \
https://github.com/LincaMarius/ISAP-1_Schematic/blob/main/KiCAD/ISAP-1_modelA_ver1_1.zip

*A total of 49 chips were used to implement this version of the ISAP-1 computer. One more than in the previous implementation.*

## ISAP-1 Model B version 1.0
Revision B of the ISAP-1 computer presents the modification of the Control Block as described by the authors, whereby the hard-wired logic is replaced with programmed logic.

In previous implementations, 18 chips were used in the Control Block.

One solution for implementation at the time the card was published in 1975 was to use the 74S188 (32 x 8 PROM open-collector), 74S288 (32 x 8 PROM tree-state), 74S387 (256 x 4 PROM open-collector), 74S287 (256 x 4 PROM tree-state), 74S470 (256 x 8 PROM open-collector), 74S471 (256 x 8 PROM tree-state), 74S473 (512 x 8 PROM open-collector), 74S472 (512 x 8 PROM tree-state), 74S475 (512 x 8 PROM open-collector), 74S474 (512 x 8 PROM tree-state), 74S451 (1024 x 8 PROM open-collector), 74S450 (1024 x 8 tree-state PROM), 74S479 (1024 x 8 open-collector PROM), 74S478 (1024 x 8 tree-state PROM), 74S3708 (1024 x 8 open-collector PROM), 74S2708 (1024 x 8 tree-state PROM), 74S477 (1024 x 4 open-collector PROM), 74S476 (1024 x 4 tree-state PROM).

But these chips are no longer manufactured and even if we could find one we would not be able to program it because it requires a programmer built specifically for this purpose. These PROMs are programmable only once and cannot be reprogrammed. They use tungsten fuses to store information and require a programming current of 150mA.

A modern solution is the use of PROM, EPROM, EPROM-OTP, EEPROM, FLASH memories

For me the best solution is to use an EEPROM or FLASH memory because they allow the information to be rewritten many times which leads to the possibility of improving the final product over time.

In the current implementation scheme of revision B in the Control Block, 10 chips were used

The schematic uses 8k EPROMs, but any type of ROM of any capacity can be used with minor modifications.

![ Figure 23 ](/Pictures/Figure23.png)

This is what the completed PCB looks like for ISAP-1 Model B Version 1.0

![ Figure 24 ](/Pictures/Figure24.png)

An overview of the PCB is shown in the following figure

![ Figure 25 ](/Pictures/Figure25.png)

The ISAP-1 Computer Model B version 1.0 project made in KiCAD is here: \
https://github.com/LincaMarius/ISAP-1_Schematic/blob/main/KiCAD/ISAP-1_modelB_ver1_0.zip

A total of 40 chips were used to build the ISAP-1 Model B Version 1.0 computer. Compared to the ISAP-1 Model A Version 1.0 where 49 were used, we have a reduction in the number of chips by 9 pieces while maintaining the same functionality of the computer.

## ISAP-1 Model B Version 1.1
Revision B of the ISAP-1 computer presents the modification of the Control Block as described by the authors, whereby the hard-wired logic is replaced with programmed logic.

In Version 1.1, an improvement is made to the ISAP-1 computer by implementing the Variable Machine Cycle.

The Instruction Set remains unchanged but the Control Block implementation changes.

In the book on page 163 the authors present a method of improving the SAP-1 Computer by implementing the Variable Machine Cycle.

The schematic is shown in Figure 10-17 and consists of 5 inverters and a 12-input NAND gate that generates the #NOP signal when the Control Block output has the NOP instruction encoded in Hexadecimal as 3E3h and a two-input AND gate that resets the Ring Counter when the #NOP or #CLR signal is low. 

The starting point is the Control Block diagram of version 1.0 shown in figure 23.

The scheme presented in the book that needs to be implemented is for a control matrix made with ROM memory with a capacity of 16 x 12 bits. So we only have 12 outputs that are used for control.

The signals CP, PE, EA, SI and EU must be inverted.

All of these signals act as inputs to a 12-input NAND gate.

For implementation, a 12-input NAND gate of the 74S134 type, a 13-input NAND gate of the 74ALS133 type can be used.

I implemented the new version using available logic gates that were not used by the authors of the book, so I added two chips. I used an unused 74LS00 NAND gate and an inverter to make the AND gate in the Ring Counter Reset circuit.

I used the 74LS133 chip which is a 13-input NAND gate.

In the current implementation scheme of revision B in the Control Block, 12 chips were used

The Control Block schematic of the ISAP-1 Model B Version 1.1 Computer is shown in the following figure:

![ Figure 26 ](/Pictures/Figure26.png)

This is what the completed PCB looks like for ISAP-1 Model B Version 1.1

![ Figure 27 ](/Pictures/Figure27.png)

An overview of the PCB is shown in the following figure

![ Figure 28 ](/Pictures/Figure28.png)

The ISAP-1 Model B Version 1.1 computer project made in KiCAD is here: \
https://github.com/LincaMarius/ISAP-1_Schematic/blob/main/KiCAD/ISAP-1_modelB_ver1_1.zip

A total of 42 chips were used to build the ISAP-1 Model B Version 1.1 computer. Compared to the ISAP-1 Model A Version 1.0 where 49 were used, we have a reduction in the number of chips by 7 pieces while maintaining the same functionality of the computer.

## ISAP-1 Model B Version 1.2
In this version I will modify the ISAP-1 Computer by changing it from a Single Board Computer to a modular version.

The functionality of the Computer does not change and the Instruction Set does not change.

Since the SAP-1 Computer does not have decoupling capacitors provided in the original schematic, I will make improvements to the electronic schematic by adding decoupling capacitors for each chip used.

Since the SAP-1 Computer was originally designed in 1975, the power supply uses a mains transformer and a Linear Voltage Regulator. This technology is specific to that time period.

Nowadays, building such a power supply is more expensive compared to modern switching power supplies that are easily available. The purchase price of just the mains transformer is comparable to the purchase price of a modern 5 Volt power supply.

Therefore, I will remove the original power supply from the Project and the Computer will be powered using an external 5 Volt source. This will reduce the overall size and weight of the Computer.

### Program Counter
The schematic and functionality are unchanged from the original. I added decoupling capacitors with a value of 100 nF for each chip used.

For example, for 74LS107 the High to Low switching time is normally 15 ns. This time is desired as small as possible to have a high working speed of the Computer. So if we consider the transition as half a period of a signal we obtain a maximum period of 30 ns. This corresponds to a frequency of 33 MHz. At these frequencies the wires on the PCB behave as inductances and will increase the switching time. To eliminate this phenomenon we put decoupling capacitors as close as possible to the power pins of the chip.

The new schematic for the Program Counter Block is:

![ Figure 29 ](/Pictures/Figure29.png)

### Address Register
The schematic and functionality are unchanged from the original. I added a decoupling capacitor with a value of 100 nF for the chip used.

The new Address Register schematic is:

![ Figure 30 ](/Pictures/Figure30.png)

### Instruction Register
The schematic and functionality are unchanged from the original. I added decoupling capacitors with a value of 100 nF for each chip used.

I also added a 10 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

The new schematic for the Instruction Register is:

![ Figure 31 ](/Pictures/Figure31.png)

### Accumulator Register
The schematic and functionality are unchanged from the original. I added decoupling capacitors with a value of 100 nF for each chip used.

I also added a 10 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

The new schematic for the Accumulator Register is:

![ Figure 32 ](/Pictures/Figure32.png)

### Arithmetic Unit
The schematic and functionality are unchanged from the original. I added decoupling capacitors with a value of 100 nF for each chip used.

I also added a 100 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

The new schematic for the Arithmetic Unit is:

![ Figure 33 ](/Pictures/Figure33.png)

### Register B
The schematic and functionality are unchanged from the original. I added decoupling capacitors with a value of 100 nF for each chip used.

I also added a 10 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

The new schematic for Register B is:

![ Figure 34 ](/Pictures/Figure34.png)

All these Modules are part of the Central Processing Unit of the ISAP-1 Model B Version 1.2 Computer

This is what the completed PCB looks like for the Central Processing Unit of ISAP-1 Computer Model B Version 1.2

![ Figure 35 ](/Pictures/Figure35.png)

An overview of the completed PCB for the ISAP-1 Model B Version 1.2 Central Processing Unit is as follows

![ Figure 36 ](/Pictures/Figure36.png)

At the bottom of the PCB we have the 4-pin J1 connector for 5V power supply and the 40-pin J2 connector for connection to the Bus.

To reduce the size of the CPU module I decided to make the Control Block as an independent Module that will attach to the CPU Module like an extension.

The connection between the CPU Module and the Control Unit Module is made through two 15-pin connectors each marked J3 and J4.

By physically separating the Control Unit into an independent Module, it has the major advantage that for modifying the Instruction Set, most changes are made at the Control Block level while the rest of the modules remain unchanged.

### Control Unit
The Control Unit's role is to direct the flow of data between the various Component Blocks of the Computer to ensure its operation and achieve the expected results.

It consists of three elements: the Instruction Decoder, the Ring Counter, and the Control Matrix.

The ISAP-1 Model B computer has a Control Matrix made with ROM memories.

For the current version of the ISAP-1 Computer to be modular, the CPU portion must be made on a single PCB. Since the CPU consists of many chips, I decided to divide its construction into two separate PCBs that will sit back to back.

We will have one PCB that contains all the building blocks of the CPU part and the second PCB contains only the Control Block.

Therefore, the Control Block will be treated as an independent module within the ISAP-1 Computer.

For connection to the CPU base module, we have provided two 10-pin connectors each, marked in the diagram as J3 and J4.
These will be mounted on the back of the PCB.

The functionality does not change from the original. I added decoupling capacitors with a value of 100 nF for each chip used.

I also added a 220 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

The new schematic for the Control Unit is:

![ Figure 37 ](/Pictures/Figure37.png)

This is the finished PCB layout for the Control Block Module of ISAP-1 Model B Computer Version 1.2

![ Figure 38 ](/Pictures/Figure38.png)

An overview of the completed PCB for the ISAP-1 Model B Computer Control Block Module Version 1.2 is as follows

![ Figure 39 ](/Pictures/Figure39.png)

To indicate the wrong mounting position of this module, I positioned the J3 connector on the PCB offset from the J4 connector.

If the module is mounted upside down due to the gap between the pins we will not have the alignment of the PCBs at the top. Normally the two PCBs should be at the same level at the top

### Memory Module
The modular version of the ISAP-1 Computer allows us to implement the Memory as an independent Module with its own PCB

Now all switches used for memory programming have been moved to the Front Panel Module

The functionality is unchanged from the original. I added a 100 nF decoupling capacitor for the chip used.

I also added a 10 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

This module communicates with the rest of the computer through the three System Buses. To connect the module to the buses, I added a connector marked J7 in the diagram.

To prevent the Module from being mounted in the wrong orientation, which would lead to its failure, we added a special power connector offset from the Bus connector by 14 mm.

The new schematic for the ISAP-1 Model B Computer Memory Module Version 1.2 is:

![ Figure 40 ](/Pictures/Figure40.png)

This is the finished PCB layout for the Memory Module of ISAP-1 Model B Computer Version 1.2

![ Figure 41 ](/Pictures/Figure41.png)

An overview of the completed PCB for the ISAP-1 Model B Version 1.2 Computer Memory Module is as follows

![ Figure 42 ](/Pictures/Figure42.png)

### Output Register Module
The modular version of the ISAP-1 Computer allows us to implement the Output Register as an independent Module with its own PCB

The schematic and functionality are unchanged from the original. I added a 100 nF decoupling capacitor for the chip used.

I also added a 100 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

This module communicates with the rest of the computer through the three system buses. To connect the module to the buses, I added a connector marked J9 in the diagram.

To prevent the Module from being mounted in the wrong orientation, which would lead to its failure, I added a special power connector offset from the Bus connector by 14 mm, marked J8 in the diagram. The Module will stand vertically in the ISAP-1 Computer

The Binary Display is designed as a separate Module and connects to the Output Register Module via the 10-pin connector marked J10 in the schematic.

The new schematic for the Output Register Module for the ISAP-1 Model B Computer Version 1.2 is:

![ Figure 43 ](/Pictures/Figure43.png)

This is the finished PCB layout for the Output Register Module of ISAP-1 Model B Computer Version 1.2

![ Figure 44 ](/Pictures/Figure44.png)

An overview of the completed PCB for the ISAP-1 Model B Version 1.2 Computer Output Register Module is as follows

![ Figure 45 ](/Pictures/Figure45.png)

### Binary Display Module
The modular version of the ISAP-1 Computer allows us to implement the Binary Display as an independent Module with its own PCB

The schematic and functionality are unchanged from the original. 

The Binary Display is designed as a separate Module and connects to the Output Register Module via the 10-pin connector marked J10 in the schematic.

The new schematic for the Binary Display Module for the ISAP-1 Model B Computer Version 1.2 is:

![ Figure 46 ](/Pictures/Figure46.png)

This is the finished PCB layout for the Binary Display Module of ISAP-1 Model B Computer Version 1.2

![ Figure 47 ](/Pictures/Figure47.png)

An overview of the completed PCB for the ISAP-1 Model B Version 1.2 Binary Computer Display Module is as follows

![ Figure 48 ](/Pictures/Figure48.png)

### Front Panel Module
The modular version of the ISAP-1 Computer allows us to implement the Front Panel as an independent Module with its own PCB

The schematic and functionality are unchanged from the original. I added a 100 nF decoupling capacitor for the chip used.

I also added a 22 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

This module communicates with the rest of the computer through the three system buses. To connect the module to the buses, I added a connector marked J12 in the diagram.

To prevent the Module from being mounted in the wrong orientation, which would lead to its failure, I added a special power connector offset from the Bus connector by 14 mm, marked J11 in the diagram. The Module will stand vertically in the ISAP-1 Computer

I designed this module to be positioned in position 1 on the BackPlane. This module will sit horizontally when attached to the BackPlane.

The new schematic for the Front Panel Module for the ISAP-1 Model B Computer Version 1.2 is:

![ Figure 49 ](/Pictures/Figure49.png)

This is the finished PCB layout for the Front Panel Module of ISAP-1 Model B Computer Version 1.2

![ Figure 50 ](/Pictures/Figure50.png)

An overview of the completed PCB for the ISAP-1 Model B Computer Front Panel Module Version 1.2 is as follows

![ Figure 51 ](/Pictures/Figure51.png)

### Backplane Module
The modular version of the ISAP-1 Computer allows us to implement the Backplane as an independent Module with its own PCB

This module is an addition to the original scheme and is intended to ensure the modularity of the Computer.

I also added a 100 uF filter capacitor to filter out low frequency noise that may appear on the power supply circuit.

The LED marked D9 signals the presence of supply voltage. The current limiting resistor is calculated as follows:

R11 = (Vcc – VF) / I_Led = (5V – 1.8V) / 15mA = 3.2V / 0.015A =  213 Ohms

The closest standard value is 220 Ohm. VF = 1.8V was used to drive a red LED.

The communication of all modules is done through the three buses (Address Bus, Data Bus and Command Bus) for which 7 40-pin connectors are provided, which are associated with 7 4-pin connectors for the 5 Volt power supply.

To prevent the Modules from being mounted in the wrong orientation, which would lead to their failure, I added this power connector offset from the Bus connector.

The new schematic for the Backplane Module for the ISAP-1 Model B Computer Version 1.2 is:

![ Figure 52 ](/Pictures/Figure52.png)

This is the finished PCB layout for the Backplane Module of ISAP-1 Model B Computer Version 1.2

![ Figure 53 ](/Pictures/Figure53.png)

An overview of the completed PCB for the ISAP-1 Model B Computer Backplane Module Version 1.2 is as follows

![ Figure 54 ](/Pictures/Figure54.png)

The ISAP-1 Model B Version 1.2 computer project made in KiCAD is here: \
https://github.com/LincaMarius/ISAP-1_Schematic/blob/main/KiCAD/ISAP-1_modelB_ver1_2.zip

A total of 41 chips were used to build the ISAP-1 Model B Version 1.2 Computer. Compared to the ISAP-1 Model A Version 1.1 where 42 were used, we have a reduction in the number of chips by 1 pieces while maintaining the same functionality of the computer.

