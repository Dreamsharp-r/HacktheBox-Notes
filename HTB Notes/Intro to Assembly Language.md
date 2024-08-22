   

Intro to Assembly Language

Binary exploitation is important in buffer overflow, ROP chains, heap exploitation and others. Custom exploits are built using assembly instructions to manipulate the code in memory.

- Bus Interfaces
- ISA
- Hertz

Commands  
lscpu // linux cmd show architecture

Tools Used:

- nasm
- GNU Debugger (GDB)
    - To install  
        ![816db73f36952e8761d2b3bd268d225a.png](cd7b23a440944b0fa46c09cb59e8d400.png)  
        Bash Code:  
        ``#!/bin/bash

fileName="${1%%.*}" # remove .s extension

nasm -f elf64 ${fileName}".s"  
ld ${fileName}".o" -o ${fileName}  
[ "$2" == "-g" ] && gdb -q {fileName} || ./fileName∣∣./{fileName} || ./fileName∣∣./{fileName}``

- Write the script to assembler.sh then chmod +x

---

![10673e8d9c38c1b7065518e6e408c93a.png](9180910643994e87a2fb223fc7819b62.png)

---

Processor Specific

- Each processor type (x64, ARM) has its Instruction Set Architecture (RISC or CISC), and each architecture can be further represented in several syntax formats

---

Computer Architecture  
![0b37e605d99a5239cb50b8b80cb25fda.png](3bdf561a85f74cb9aff2f391b41410b8.png)

- How a CPU processes its instuctions depend on its Instruction Set Architecture (ISA)
    - RISC: simple instructions. More cycles. But each cycle is shorter and less power
    - ARM & Apple
    - CISC: Complex instructions. Less cycles. More time and power
    - Intel & AMD

---

Two main types of memory

- Cache
    - ![9f0a86326dcae1f3dbace7d1ef948370.png](bc0bbe4531494c489245603db09734f9.png)
- RAM
    - ![a71306f9e21e62509a090d2c6eb089c3.png](30d8c8f347b0463c9439edd4634985e7.png)

---

Instruction Cycle

- An instruction cycle is the cycle it takes the CPU to process a single machine instruction

![c536184ebceabbd960c5be0f9f9d6884.png](5c8957b5f9e64a34b10867bd93bc4c21.png)

- All of the stages in the instruction cycle are carried out by the Control Unit, except when arithmetic instructions need to be executed "add,sub,etc", which are executed by the ALU

![9777f1d22f81e4a5b811d704be4fd543.png](cddb375f010743bea783b63a42c7f6c1.png)  
Modern CPUs  
![dd203979a734b05ed9babdf21a719d1e.png](6675c4370347432f9079680103beb4f3.png)

---

Instruction Set Architecture (ISA)  
![ecc681539c1a5285923d61c01c5f4143.png](2dc35d2c5f48444497e523cd61576bf2.png)  
![08b5143fd505733498f09886f8a7110e.png](d6bee0caaf0c45d29b291fc3d0ae79cb.png)

---

![35be46968316b08f8eefd404d4488a41.png](ccd7878284fb47239ccb0ce79331136f.png)  
![86c0d8313018e9207c2aae17eda259e7.png](c3ccdc98fb04461eb9a311c8980129b8.png)  
![6398e6ebd707c45fea50a701b0b4a1ff.png](de784ccf129040b18d9c16494414cd3c.png)

---

Two types of CPUs

- Intel x86
- ARM

Address Endianness

- Little-Endian (right-to-left) EX. 0x0011223344556677 = 0x7766554433221100
- Big-Endian (left-to-right)

![f63503980add88bad4181d715e6a43a5.png](c1dd23e0e444468185aaf0b745bd54ec.png)

Assembly File Structure  
![96f9444cf07cb00b91951266275a7947.png](bd44d9ccb3ab42cab5a6d66fe9e36a1b.png)

1. Labels
2. Instructions
3. Operands  
    ![3b5b797113d962818cf44539726aa490.png](15d0ad9bf8dc48cd8563287442b16725.png)
    - How Variables are defined![1b665838817395b7117d6b3b278aac85.png](e67694802c244c2fa8b59a91efd0af9b.png)

Finding the specific instruction in the register

1. Set a breakpoint at '_start+blank' (EX. start+1, start+2)
2. when the program breaks at that point inspect the value of the instruction using info registers
3. Note the hexadecimal value of 'rax'

---

Assembly Instructions:  
![6ae82d2e10e12143dd588d16a5c53ae0.png](419862ef48ff46dabd79ed0b83253415.png)  
![9ec7c02fe605b589b37c822b3eb3ea28.png](6fca85bf416545d7b53c9982f2fbe090.png)  
![c555c2bb0bc6dec840c9f5ee480c46a0.png](ad424b86a13a4a17afd2d537f5e7f85c.png)  
![49140621f235b7664f417475b147a4ce.png](37e1676555784983a4c41cce164e64f4.png)