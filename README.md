# RISC-V

## Quick link

- [Day 1](#day-1)

- [Day 2](#day-2)

- [Day 3](#day-3)

- [Day 4](#day-4)

- [Day 5](#day-5)
  
- [References](#references)

## DAY 1
<details>
<summary><strong>Introduction to RISC-V ISA and GNU compiler toolchain
</strong></summary>
 
  ## Installation
  
<details>
 
  <summary><strong>Steps to install Risc-Tools</strong></summary>

 Clone the  mentioned RISC-V Toolchain repository
  ```
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod +x run.sh
./run.sh
```
  
Once we run it we have to type the following command:

```

cd ~/riscv_toolchain/iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install

```
After installation we will add following path to our .bashrc file at the last of the file :
```

gedit .bashrc
#Instead of shivangi put your username
export PATH="/home/shivangi/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH" #Type at last line # close the bashrc and type
source .bashrc

```
Test installation using following command:
```
riscv64-unknown-elf-gcc --version
```

</details>

## Introduction to RISC-V basic keywords
<details><summary><strong>What is Risc-v?</strong></summary><br>
RISC-V is an open-source instruction set architecture used to develop custom processors for a variety of applications, from embedded designs to supercomputers.

 RISC-V is a load-store architecture, meaning three things:
    
  (i) Its arithmetic instructions operate only on registers.
  
  (ii) Only load and store instructions transfer data to and from memory.
  
  (iii) Data must first be loaded into a register before it can be operated on.

  ![Screenshot from 2023-08-19 00-34-30](https://github.com/Shivangi2207/RISC-V/assets/140998647/1090fd1c-47a9-4387-8070-7ee4b14c2b80)

Now as in the figure shown above we want to see our C programm on a hardware which have this particular layout. Then we have to pass this information to this harware .
The C program is first complied using complier and then converted into a assembly  language ,like the Risc-v assembler language program as shown. Then this assembly language program got converted into machine level language (binary signals).
Finally obtained bits can easily be implemented on the desired layout and we will get our required result.

## How apps and application software runs on hardware?

![Screenshot from 2023-08-19 01-20-56](https://github.com/Shivangi2207/RISC-V/assets/140998647/2cd6e945-80d5-4660-81b9-bd2d6e42ae30)

So basically the application software enters into the system software block, and system software inturns convert the application software in the binary language.
system software have OS,Compiler, Assembler . OS gives output in some programming language like C,C++,JAVA etc these are the fed to the complier and we get set of instructions and once we get the instructions the next job of the assembler is to  convert the instructions into  respective binary code i.e machine language.
then this output is fed to the hardware and hardware can easily understand the job.

The different instructions included in RISC-V are listed below.

   1. Pseudo instructions - For e.g- mv,li,ret etc
   2. Base integer instruction (RV64I, RV32I)-For e.g-lui,addi etc
   3. Multiply extension (RV64M) -For e.g- mulw,divw etc
   4. Single and double floating point instruction (RV64F, RV64D) -For e.g flw,fadd etc
   5. Application binary instruction
   6. Memory allocation and stack pointer

</details>
<details><summary><strong>Labwork for RISC-V software toolchain
</strong></summary>

## Lab 1:C Program To Compute Sum From 1 to N

## Code 
```
#include <stdio.h>

int main () {
	int i,sum = 0, n = 6;
	for (i = 1; i <=n; ++i) {
		sum += i;
	}
	printf("The sum of the number from 1 to %d is %d\n", n,sum);
	return 0;
	}
```
## Commands to run:

```
gcc sum1ton.c
./a.out

```
## Output:

![Screenshot from 2023-08-19 01-39-09](https://github.com/Shivangi2207/RISC-V/assets/140998647/0897bb6a-8c74-4a0a-bc15-8c790702ac5d)

## Lab 2: RISCV GCC compile And Disassemble

## commands  
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c


```
To list the details of the file
```
ls -ltr sum1ton.o
```
![Screenshot from 2023-08-19 02-14-51](https://github.com/Shivangi2207/RISC-V/assets/140998647/f2efcafc-4b9d-41ba-802e-d318c902aefe)

To deassemble the object file
```

riscv64-unknown-elf-objdump sum1ton -d sum1ton.o

```
Below image shows the disassembled file sum1to6.o with main function highlighted.
![Screenshot from 2023-08-19 01-53-15](https://github.com/Shivangi2207/RISC-V/assets/140998647/0f6ec07b-5819-4e14-a70e-d9a59a74b03c)


```

riscv64-unknown-elf-objdump <object file> -d <object filename.o> | less

```
![Screenshot from 2023-08-19 01-56-03](https://github.com/Shivangi2207/RISC-V/assets/140998647/3dc503e5-2420-43ec-adb1-2bd54a950aad)

Therefore total no of instruction used is 8 as 100bc -100dc= 32 , 32/4=8

To compile
```
spike pk sum1ton.o
```
![Screenshot from 2023-08-19 16-13-00](https://github.com/Shivangi2207/RISC-V/assets/140998647/33e52978-24f3-44e2-9af1-cbea92c2bbe0)

To Debug

```
spike -d pk sum1ton.o
```

</details>
<details><summary><strong>Integer number representation
</strong></summary>

## 64-bit Number System For Unsigned Numbers 

The 64-bit number system refers to a binary number system where numbers are represented using 64 bits or binary digits. In this system, each digit can be either 0 or 1, and each bit holds a place value based on powers of 2. The leftmost bit is the most significant bit (MSB), and the rightmost bit is the least significant bit (LSB).

For unsigned numbers, the 64-bit number system can represent only non-negative integers. The value of a number is calculated by summing the products of each bit with its corresponding power of 2. The formula for calculating the value of a 64-bit binary number is:

Value = bit[63] * 2^63 + bit[62] * 2^62 + ... + bit[1] * 2^1 + bit[0] * 2^0

Here's an example of a 64-bit binary number and its decimal equivalent:

![Screenshot from 2023-08-19 14-32-58](https://github.com/Shivangi2207/RISC-V/assets/140998647/d1689678-5a4f-424d-a523-95bea5ad8b89)

The decimal number 17446744073708551615 can be represented in a 64-bit unsigned binary format as follows:

Decimal: 17446744073708551615

Binary: 111100100001111101001001010011000101100011001011110110111111

Keep in mind that the 64-bit number system has a limited range for representing integers. The maximum value that can be represented using a 64-bit unsigned number is 2^64 - 1, which is approximately 18.4 quintillion (18,446,744,073,709,551,615). The minimum value is always 0 since it only includes non-negative integers.


## 64-bit Number System For Signed Numbers 

The 64-bit number system can also be used to represent signed numbers, which includes both positive and negative integers. In a 64-bit signed number representation, one bit is used as the sign bit to indicate whether the number is positive or negative. The rest of the bits represent the magnitude of the number.

Here's how the 64-bit signed number representation works:

 The leftmost (most significant) bit is the sign bit. If this bit is 0, the number is positive. If this bit is 1, the number is negative.
The remaining 63 bits are used to represent the magnitude of the number in the same way as the unsigned 64-bit number system. Each bit has a place value based on powers of 2.

For example, let's say we want to represent the signed decimal number -12345 in a 64-bit signed binary format:

 1: Convert to Binary Magnitude: First, we convert the magnitude (absolute value) of the number to binary. The binary representation of 12345 is 11000000111001.
 
 2: Sign Bit: Since the number is negative, the sign bit is set to 1.
 
 3: Fill to 63 Bits: We have 63 bits left to fill, so we pad the binary magnitude with zeros on the left until we have a total of 63 bits.
 
 4: Combine Sign Bit and Magnitude: Combine the sign bit (1) and the padded binary magnitude.

 In this example, the binary representation of the signed decimal number -12345 in a 64-bit signed format is 10000000000000000000000000000000000000000000000000000000011000000111001.

The leftmost bit indicates that the number is negative, and the rest of the bits represent the magnitude of the number. The actual value of this binary representation can be calculated in the same way as for the unsigned 64-bit number system.

the actual range of representable values is from -2^63 + 1 to 2^63 - 1.


</details>

<details><summary><strong>Lab For Signed And Unsigned Numbers  </strong></summary>

## Code for unsignedHighest

```
#include <stdio.h>
#include <math.h>
int main() {
unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
printf("highest number represented by unsigned long long int is %llu\n", max);
return 0;
}

```
![Screenshot from 2023-08-19 15-17-14](https://github.com/Shivangi2207/RISC-V/assets/140998647/0f6a80ba-e070-43cb-a2e8-7080c9e4ab76)

This show the Highest value for Unsigned Numbers 

Now if we run our code by chnaging  (pow(2,64) * -1) we get the lowest value

![Screenshot from 2023-08-19 15-18-10](https://github.com/Shivangi2207/RISC-V/assets/140998647/f9df6c51-bf14-4041-b7a0-6a7dca62333a)

## Code for signedHighest

```
include <stdio.h>
#include <math.h>
int main() {
long long int max = (int) (pow(2,63) -1);
long long int min = (int) (pow(2,63) * -1);
printf("highest number represented by long long int is %lld\n", max);
printf("lowest number represented by long long int is %lld\n", min);
return 0;



```

![Screenshot from 2023-08-19 15-31-15](https://github.com/Shivangi2207/RISC-V/assets/140998647/e2f28df0-89b5-47ea-9ff4-162562e26685)

So  here we are not getting desired result as here we have used (int) due to which overflow condition arrives.
now to fix this we  will use long long int

```
include <stdio.h>
#include <math.h>
int main() {
long long int max = (long long int) (pow(2,63) -1);
long long int min = (long long int) (pow(2,63) * -1);
printf("highest number represented by long long int is %lld\n", max);
printf("lowest number represented by long long int is %lld\n", min);
return 0;

```
output:
![Screenshot from 2023-08-19 16-30-34](https://github.com/Shivangi2207/RISC-V/assets/140998647/6c37d24f-c250-4c17-bac0-848fdaaa8225)

## Table:


![Screenshot from 2023-08-19 15-29-51](https://github.com/Shivangi2207/RISC-V/assets/140998647/e161df13-b810-47a7-87af-29e7bc181284)

</details>
</details>

## Day 2

<details><summary><strong>Introduction to ABI and basic verification flow</strong></summary>

## What is ABI?


<details><summary><strong>Application Binary interface (ABI)
</strong></summary>

An Application Binary Interface (ABI) is a set of rules and conventions that dictate how different software components interact with each other at the binary level. It defines the interface between software components, such as different programs, libraries, and the operating system, to ensure compatibility and proper communication. ABIs are particularly important in the context of compiled programming languages, as they provide the standards for how functions are called, parameters are passed, memory is allocated, and data is represented in binary format.
Key aspects of an ABI may include:

   1. Calling Conventions: Specifies how functions are called and how parameters are passed between the caller and callee. This includes the order in which parameters are pushed onto the stack or placed in registers, as well as how return values are retrieved.

  2.  Data Representation: Defines how different data types are represented in memory or registers. This covers integer, floating-point, and pointer data types.

  3.  Memory Layout: Specifies how memory is allocated, managed, and used by programs. It includes rules for stack frames, heap allocation, and data storage.

  4. Register Usage: Describes how registers are used for passing function arguments and return values, as well as which registers need to be preserved by callee functions.

  5.  Exception Handling: Outlines how exceptions, errors, and signals are managed and propagated between different parts of the software.

  6.  System Calls and Libraries: Specifies the interface between user-level programs and the operating system. It covers how system calls are made and how programs interact with shared libraries.


![Screenshot from 2023-08-19 16-58-19](https://github.com/Shivangi2207/RISC-V/assets/140998647/88a05989-3062-4617-8481-79d272d84674)



 The application program can directly access the registers of the RISC V architecture using something known as system calls. The ABI (also known as system call interface enables the application to access the hardware resources via registers.

 In RISC V architecture, the width of the register is defined as XLEN. For RV64 and RV32, the widths are 64 bits and 32 bits, respectively.

  RISC V belongs to the little endian memory addressing system, which means that the least significant byte of a word is stored in the smallest memory address.


## Memory Allocation For Double Words

In the RISC-V architecture, memory allocation is not directly governed by the ABI (Application Binary Interface) itself. Instead, the ABI defines the conventions for function calling, register usage, and data representation between different software components. Memory allocation and deallocation are typically managed using memory management functions provided by the operating system or programming language runtime.

The way an ABI accesses registers depends on the specific calling convention and architecture being used. Different architectures and ABIs may have variations in how registers are used to pass function arguments, return values, and hold temporary data. 

Now, how does the ABI access the hardware resources?

1. The ABI defines which registers are used for function arguments, return values, and temporary storage. Hardware registers are allocated and managed according to these rules to facilitate efficient data exchange between functions.
2. The ABI defines memory alignment requirements for data types. Hardware ensures that data is stored and accessed efficiently in memory by enforcing these alignment rules.
3. The ABI's calling conventions and function parameter passing depend on the instruction set architecture. Hardware interprets these instructions and encodings to perform operations specified by the ABI.
4. When interacting with the operating system, the ABI's system call conventions are implemented using hardware interrupts and privileged execution modes to transition from user mode to kernel mode.

![Screenshot from 2023-08-19 17-08-06](https://github.com/Shivangi2207/RISC-V/assets/140998647/21de863d-a0b3-46cb-9abc-92ae4af60f5a)

Here we have 64 bit register but we have 32 bit wide register available for storage of our 64 bit instruction.
So 1st we divide 64 bits into eight 8 bit and store it into a paricular memory location.
Hence , In the context of RISC-V, a "word" typically refers to a 32-bit value, and a "byte" is 8 bits. The splitting of a 64-bit number into bytes and words is straightforward:

A 64-bit number consists of 8 bytes (64 bits / 8 bits per byte).
 A 64-bit number consists of 2 words (64 bits / 32 bits per word).

Each byte or word of the 64-bit number can be accessed and manipulated independently.

Keep in mind that RISC-V provides specific instructions for working with 64-bit data, including arithmetic, load/store, and conversion operations. These instructions handle the splitting and management of 64-bit data in a 32-bit architecture like RISC-V.

  It uses different registers(32 in number) which are each of width XLEN = 32 bit for RV32 (~XLEN = 64 for RV64) . On a higher level of abstraction these registers are accessed by their respective ABI names.

 For base integer instructions there are broadly 3 types of of such registers:
        I-type : For instructions having immediate values as operands.
        R-type : For instructions having only registers as operands.
        S-type : For instructions used for storing operations.

## LOAD, ADD and STORE Instructions

```
ld x8, 16(x23)
```
Here ld is for load instruction, x8 is for destination register, 16 is offset and x23 is source register.
This is  I type instruction.

![Screenshot from 2023-08-19 22-18-50](https://github.com/Shivangi2207/RISC-V/assets/140998647/a034039c-388e-4133-a1a8-bc1533418ac8)


```
add x8, x24,x8
```
Here add is for add instruction, x8 is the destination register, x23 & x8 is the source register.This is R type Instructions 

![Screenshot from 2023-08-19 22-24-34](https://github.com/Shivangi2207/RISC-V/assets/140998647/b7a34439-63cb-47e9-9626-00ff88834ba5)

```
sd x8,8(x23)
```
Here sd is for store doubleword,x8 is data registers,8 tell offset,x23 is source register. This is S type Instructions

![Screenshot from 2023-08-19 22-30-03](https://github.com/Shivangi2207/RISC-V/assets/140998647/f65b968e-3916-4137-9cce-500ebd52bc81)


Here in each Instructions set we can see register are of 5 bits so total number of register = 2^5 = 32 registers

## 32-registers And Their Respective ABI Names 

![Screenshot from 2023-08-19 19-54-21](https://github.com/Shivangi2207/RISC-V/assets/140998647/7cefd5c5-1554-41e4-b279-863481cead24)


</details>

<details><summary><strong>Lab work using ABI function calls </strong></summary>

## Study New Algorithm For Sum 1 to N Using ASM

![Screenshot from 2023-08-19 19-58-25](https://github.com/Shivangi2207/RISC-V/assets/140998647/453c547e-136f-4822-83d9-3c7184a30a23)

Now let's understand the algorithm behind the sum 1 to N program using ASM
Here first initialized a4 register with zero for storing temp variable.Similarly we initialized a3 with zero.Then after that we are storing 10 in a2 register. After that we are entering in a loop which says if value in a2>a3 then do a increment of +1 in a3  and add a3 in a4 (a4=a3+a4) .if its not true then print a0=a4+0


## Code for lab work
C program

```
#include<stdio.h>

extern int load(int x,int y);
int main(){

	int result=0;
	int count =9;
	result=load(0x0,count+1);
	printf("sum of number from 1 to %d\n",count,result);

}
```
Code of load file
```
.section .text
.global load
.type load,@function

load:
	add a4, a0, zero
	add a2, a0, a1
	add a3, a0, zero
loop:	add a4, a3, a4
	addi a3, a3, 1
	blt a3, a2, loop
	add a0, a4,zero
	ret

```

![Screenshot from 2023-08-19 22-49-18](https://github.com/Shivangi2207/RISC-V/assets/140998647/27173a6c-2a9d-409c-80b4-1cafcbe4aef5)

Memory Location of load Subroutine

![Screenshot from 2023-08-19 22-56-05](https://github.com/Shivangi2207/RISC-V/assets/140998647/515a3ff9-9099-45c4-8da8-952c25d0c767)

Spike debugging :

![Screenshot from 2023-08-19 23-03-15](https://github.com/Shivangi2207/RISC-V/assets/140998647/7e01302f-5706-4b36-84ee-96c2ddfe2fb3)

## Lab To Run C-Program On RISC-V CPU 
![Screenshot from 2023-08-19 21-39-50](https://github.com/Shivangi2207/RISC-V/assets/140998647/d7ae71df-6700-4bfc-bc65-9afa8fca672b)

Here we have riscv cpu program code through which we send the HEX format file of c program to show output the output of the given code

```
chmod 777 rv32im.sh
./rv32im.sh 

```
![Screenshot from 2023-08-19 23-07-48](https://github.com/Shivangi2207/RISC-V/assets/140998647/6a30c124-2156-4374-a4c3-3405e0189bf6)


Input hex file to sent through verilog code:

firmware.hex file
![Screenshot from 2023-08-19 23-09-33](https://github.com/Shivangi2207/RISC-V/assets/140998647/e375a0bb-5446-4f5e-996f-484997ff8a65)

firmware32.hex file

![Screenshot from 2023-08-19 23-10-06](https://github.com/Shivangi2207/RISC-V/assets/140998647/5a834ba3-693d-47cd-b613-7665cf557fda)

</details>

</details>

## Day 3
<details><summary><strong>Digital Logic with TL-Verilog and Makerchip</strong></summary><br>
<details><summary><strong>Combinational logic in TL-Verilog using Makerchip </strong></summary>

## Logic gates

![Screenshot from 2023-08-19 23-27-04](https://github.com/Shivangi2207/RISC-V/assets/140998647/f1b8d0c0-98a0-41a2-b98b-d0e856acc44d)

AND Gate: Outputs true if all inputs are true.
OR Gate: Outputs true if at least one input is true.
NOT Gate: Outputs the opposite (complement) of the input.
XOR Gate: Outputs true if the number of true inputs is odd.
NAND Gate: Outputs false only if all inputs are true.
NOR Gate: Outputs true only if all inputs are false.
XNOR Gate: Outputs true if the number of true inputs is even.

![Screenshot from 2023-08-20 00-26-15](https://github.com/Shivangi2207/RISC-V/assets/140998647/759bc912-5716-46ef-9b6c-9069c4911db0)


## Combinational Circuits

![Screenshot from 2023-08-19 23-29-39](https://github.com/Shivangi2207/RISC-V/assets/140998647/6ff026cd-6e1c-4904-813a-b563f7b5fc93)

Combinational circuits are digital electronic circuits where the outputs depend solely on the current input values and not on any previous inputs or internal states. These circuits use a combination of logic gates to perform specific logical functions without any memory or feedback elements. Combinational circuits are used for various purposes, such as arithmetic operations, data processing, and logic operations, where the output is determined only by the input conditions at that particular moment in time.

## Mux

A Multiplexer (MUX), also known as a data selector, is a digital circuit that selects and routes one of multiple input lines to a single output line based on the control signals. It's often depicted as having multiple data inputs, a control input (select lines), and a single output.
 ![Screenshot from 2023-08-20 00-27-04](https://github.com/Shivangi2207/RISC-V/assets/140998647/94012bef-654e-4c6a-87b3-6283ab3d4c84)

## Makerchip

Makerchip is an online platform that provides an integrated development environment (IDE) for designing, simulating, and testing digital circuits and systems. It's particularly focused on hardware description languages (HDLs) like Verilog and SystemVerilog.

Makerchip allows users to create, simulate, and debug digital designs using a web-based interface. It provides features such as code editing, simulation visualization, and waveform analysis. It's often used as a teaching and learning tool for digital design and hardware description languages.

However, please note that there might have been developments or changes to Makerchip since then. I recommend checking their official website or other reliable sources for the most up-to-date information.


## Lab works

## inverter

![Screenshot from 2023-08-20 00-44-24](https://github.com/Shivangi2207/RISC-V/assets/140998647/776716b3-5afe-4f61-ba70-ab5a91e1552a)

## AND gate

![Screenshot from 2023-08-20 00-46-02](https://github.com/Shivangi2207/RISC-V/assets/140998647/2001c43b-57f4-4174-83f0-d4985452a685)

## OR gate
![Screenshot from 2023-08-20 00-46-21](https://github.com/Shivangi2207/RISC-V/assets/140998647/adfce61a-4b34-410d-b3bf-7bed7a40d433)

## Xor gate
![Screenshot from 2023-08-20 00-46-45](https://github.com/Shivangi2207/RISC-V/assets/140998647/36f5b23b-fa51-44d9-acbc-199ac98025fa)

## Vector

![Screenshot from 2023-08-20 00-49-11](https://github.com/Shivangi2207/RISC-V/assets/140998647/cd48ff83-70df-4938-b499-fe2f838e6e09)

## MUX

![Screenshot from 2023-08-20 00-52-32](https://github.com/Shivangi2207/RISC-V/assets/140998647/c9ba6255-c2e2-46b5-a81b-1aded7f56247)
![Screenshot from 2023-08-20 00-53-41](https://github.com/Shivangi2207/RISC-V/assets/140998647/34f15a26-91a7-410e-9a76-246a9b1a38a5)



## Combinational calculator

![Screenshot from 2023-08-20 12-31-00](https://github.com/Shivangi2207/RISC-V/assets/140998647/7b8f51e6-c87c-4633-b7d8-72c0fde25b77)





</details>

<details>
<summary><strong>Sequential logic</strong></summary>
## What is sequential circuit?

A sequential circuit is a type of digital electronic circuit in which the output depends not only on the current input values but also on the previous history of inputs and the internal state of the circuit. Unlike combinational circuits, which produce outputs solely based on input values, sequential circuits have memory elements (such as flip-flops) that allow them to store and remember past input values or internal states.

Sequential circuits are used for tasks that involve memory and sequencing, such as counters, registers, and finite state machines. They are fundamental in designing systems that require controlled and ordered behavior over time. The behavior of sequential circuits is defined by a combination of their present input values, the previous state, and transition rules that determine how the internal state changes in response to inputs.



![Screenshot from 2023-08-20 01-32-11](https://github.com/Shivangi2207/RISC-V/assets/140998647/fbd8d615-c13f-4b97-8a10-b6a5609bec77)

## Lab work

## Fibonacci series


![Screenshot from 2023-08-20 14-15-16](https://github.com/Shivangi2207/RISC-V/assets/140998647/ce6ca185-dfd7-46ce-8053-c7c7be4cdf3f)

## Counter

![Screenshot from 2023-08-20 14-18-19](https://github.com/Shivangi2207/RISC-V/assets/140998647/c41b769d-c443-4d48-ab7d-cf7b72195b2a)

## Sequential Calculator


 ![Screenshot from 2023-08-20 12-37-44](https://github.com/Shivangi2207/RISC-V/assets/140998647/29f9ed75-575f-4f23-9bb4-31a2c250b607)


</details>
<details><summary><strong>Pipeline Logic</strong></summary>
## What is pipeline?

 Pipelining is a technique used in digital circuit design to improve the performance of a sequential process. In a pipeline, a complex task or operation is divided into a sequence of smaller stages. Each stage processes a part of the task, and the outputs of one stage are passed as inputs to the next stage. This allows multiple tasks to be in progress at different stages simultaneously, improving throughput and overall efficiency.

Now let's implement pythagorous theorem and compute  it on hardware

![Screenshot from 2023-08-20 15-06-32](https://github.com/Shivangi2207/RISC-V/assets/140998647/53ab4774-0a09-4f00-8209-bc213e82321b)

Let us compute the pythagoran's theorem over 3 cycles.

Cycle1: Squaring on the sides a and b.
 Cycle2: Adding the sqyared vales of a and b.
 Cycle3: Finding the square root value of the sum

## Makerchip implementation

![Screenshot from 2023-08-20 15-11-18](https://github.com/Shivangi2207/RISC-V/assets/140998647/91afe442-6246-46fc-9415-cd30002a4c5a)

 Code reduction is the most advanatageous property of the TL-Verilog when compared to System Verilog. 

 The Retiming property in TL-Verilog is very easy and safe to implement whereas in SystemVerilog, it is very bug-prone.

The pipelinig also allows us to run the clock at a high frequency. Regardless of the way we structure our logic, we will be able to produce new set of inputs on every clock edge. As a result, we get high throughput for our circuit.

## syntax in Tl-Verilog

 ![Screenshot from 2023-08-20 13-27-16](https://github.com/Shivangi2207/RISC-V/assets/140998647/2986c5d0-905d-47cf-b1a8-d1adb1dc9ecf)

## Implementation of Fibonacci series in a pipeline:

![Screenshot from 2023-08-20 15-38-11](https://github.com/Shivangi2207/RISC-V/assets/140998647/054b5cb7-123f-4637-8548-aaa17907e8c8)

## Implementation of pipeline through TL-Verilog:

![Screenshot from 2023-08-20 15-40-12](https://github.com/Shivangi2207/RISC-V/assets/140998647/4590d788-e40c-44e2-a972-937840b3ccf1)

we can observe errors in the pipeline
![Screenshot from 2023-08-20 15-41-17](https://github.com/Shivangi2207/RISC-V/assets/140998647/4f8bdec4-025e-4220-aa3b-414d2a447152)

## Lab 1: Counter and Calculator in pipeline
Pipeline structure:


![Screenshot from 2023-08-20 15-42-59](https://github.com/Shivangi2207/RISC-V/assets/140998647/e2fe6720-f561-430a-a39d-2c3441bf5643)

Makerchip Implementation
![Screenshot from 2023-08-20 16-21-23](https://github.com/Shivangi2207/RISC-V/assets/140998647/cac52711-21f8-430d-8d23-6c88673d8a5a)

## Lab2 : Cycle Calculator:
pipeline structure:

![Screenshot from 2023-08-20 16-23-15](https://github.com/Shivangi2207/RISC-V/assets/140998647/e3b39a75-c0d2-4958-a9fb-79b10d5e1b6d)

 Makerchip implementation:

 ![Screenshot from 2023-08-20 16-39-25](https://github.com/Shivangi2207/RISC-V/assets/140998647/31e4f643-894e-4370-9830-92b6524fb300)


</details>

<details><summary><strong>Validity</strong></summary>
"Validity" is a term often used in the context of designing communication interfaces or protocols. It typically refers to a signal that indicates whether the data present on another signal (usually a data signal) is valid and should be processed.

Validity provided:

 1: easier debug
 2: cleaner design
 3: better error checking
 4:automated clock gating


 ## Implementation of pythagoran's theorem with validity:

 
 
![Screenshot from 2023-08-20 16-51-08](https://github.com/Shivangi2207/RISC-V/assets/140998647/f85062ab-35aa-4644-8a52-7d44750ab5d4)

Clock Gating is a power-saving property.

## Lab1 : Distance Accumulator with pythagorean's theorem:

Pipeline structure:

![Screenshot from 2023-08-20 17-05-35](https://github.com/Shivangi2207/RISC-V/assets/140998647/217a0e1a-55f7-41a6-aa47-4f42e9182609)

Makerchhip Implementation:

![Screenshot from 2023-08-20 18-05-09](https://github.com/Shivangi2207/RISC-V/assets/140998647/d8dd50fb-1f93-4d7c-8768-5c7a5eb52c78)

## Lab2 : Cycle calculator with validity:

pipeline structute:

![Screenshot from 2023-08-20 18-07-06](https://github.com/Shivangi2207/RISC-V/assets/140998647/c3366353-69ad-412b-b8e7-935755bbc81a)

Makerchip implementatiom:

![Screenshot from 2023-08-20 18-09-06](https://github.com/Shivangi2207/RISC-V/assets/140998647/40f04672-543d-4705-b340-3ff00b774c1f)

## Lab3 : Calculator with single value memory:

![Screenshot from 2023-08-20 18-21-30](https://github.com/Shivangi2207/RISC-V/assets/140998647/e1a3acc0-4388-43fc-862b-dd197cad6617)


</details>

<details>
	<summary><strong>Wrap up</strong></summary>

## Hierarchy

## Lab1 : Conway's game of life

![Screenshot from 2023-08-20 18-15-20](https://github.com/Shivangi2207/RISC-V/assets/140998647/48b9a59c-d329-4e8b-9a73-956806ae8b0e)


## Lab2 : Pythagoran's theorem

Pipeline structure:
![Screenshot from 2023-08-20 18-17-09](https://github.com/Shivangi2207/RISC-V/assets/140998647/635ab276-17c3-4c28-a1fe-fb74380cfd96)


Makerchip Implementation:

![Screenshot from 2023-08-20 18-16-07](https://github.com/Shivangi2207/RISC-V/assets/140998647/72343c4b-d972-40ab-bf0d-6dfe32a09857)



 
</details>


</details>

## Day 4

<details><summary><strong>Basic RISC-V CPU micro-architecture
</strong></summary>

## Introduction to Simple RISC-V Micro-architecture 

![Screenshot from 2023-08-20 18-30-24](https://github.com/Shivangi2207/RISC-V/assets/140998647/c4589d82-eecb-4ed3-875a-40441e20ab5d)

A single-cycle microarchitecture for a RISC-V CPU is a simple and straightforward design in which each instruction is executed within a single clock cycle. While this approach is easy to understand, it has limitations in terms of performance and efficiency. Let's break down the key components of a single-cycle RISC-V CPU's microarchitecture:

1:Instruction Fetch (IF): The instruction memory fetches the instruction based on the 

2:Program counter (PC): The PC is updated to point to the next instruction.

3:Instruction Decode (ID): The fetched instruction is decoded to identify the operation and operands.Register values are read from the register file based on the instruction's register operands.

4:Execute (EX): The ALU (Arithmetic Logic Unit) performs the operation specified by the instruction.Immediate values are generated from the instruction for operations that require them.

5:Memory Access (MEM): Memory operations (load and store) are performed if the instruction requires memory access. For loads, data is fetched from memory and made available for the next stage. For stores, data is written to memory.

5:Write-Back (WB): The result of the instruction is written back to the destination register.
</details>

<details>
<summary><strong>Fetch and decode</strong></summary> 

## Lab1 : Next PC
Pipeline structure:


![Screenshot from 2023-08-20 18-57-55](https://github.com/Shivangi2207/RISC-V/assets/140998647/5f5de9c8-a506-4b65-adc7-c7f26637659d)


Implementation:


![Screenshot from 2023-08-20 19-01-45](https://github.com/Shivangi2207/RISC-V/assets/140998647/0aac34a9-6e0e-4d06-b6b5-413d0d07d462)


## Lab2 : Fetch logic

Pipeline structure (part 1):
![Screenshot from 2023-08-20 21-09-12](https://github.com/Shivangi2207/RISC-V/assets/140998647/d4f837f2-82b2-4253-b818-b336518e1476)

Pipeline structure (part 2):

![Screenshot from 2023-08-20 21-09-32](https://github.com/Shivangi2207/RISC-V/assets/140998647/3700e20f-e543-4c19-9d35-2c25b1d67bfe)


Makerchip Implementation:

![Screenshot from 2023-08-20 20-08-39](https://github.com/Shivangi2207/RISC-V/assets/140998647/65af2b67-1d70-43fa-8b02-8373334b40cf)

## Lab3 : Instruction type decode

Pipeline structure:

![Screenshot from 2023-08-20 21-15-43](https://github.com/Shivangi2207/RISC-V/assets/140998647/58ec9bda-6754-4337-8a77-ded3442cd3de)

Makerchip output:

![Screenshot from 2023-08-20 21-30-18](https://github.com/Shivangi2207/RISC-V/assets/140998647/cf7b1d85-31ee-442b-b367-d03026a50198)

## Lab4 : Instruction immediate decode

![Screenshot from 2023-08-20 21-24-36](https://github.com/Shivangi2207/RISC-V/assets/140998647/e040c77e-3bf8-452a-916e-c42f3b38b780)

Makerchip output:

![Screenshot from 2023-08-20 21-30-36](https://github.com/Shivangi2207/RISC-V/assets/140998647/48fdc48e-5d2c-448d-b2ab-811f9c035ed6)

## Lab5 : Instruction Decode

![Screenshot from 2023-08-20 21-38-28](https://github.com/Shivangi2207/RISC-V/assets/140998647/520d2924-cfda-4ddd-9779-ffa88619f976)

Makerchip output:

![Screenshot from 2023-08-20 21-30-56](https://github.com/Shivangi2207/RISC-V/assets/140998647/6b08bebf-3938-41ec-84ed-2bec32cae7e4)

## Lab6 : Instruction Field Decode:
![Screenshot from 2023-08-20 21-38-28](https://github.com/Shivangi2207/RISC-V/assets/140998647/3aa09860-ea31-4f94-a6d7-cb30dd9405dc)

Makerchip output:

![Screenshot from 2023-08-20 21-41-40](https://github.com/Shivangi2207/RISC-V/assets/140998647/41305a3a-ba44-4a58-912f-e286f6f58cc6)

## Lab7 : Instruction Decode_2

![Screenshot from 2023-08-20 21-40-45](https://github.com/Shivangi2207/RISC-V/assets/140998647/61a5ae40-8803-4fb4-b45f-dbc0316f05bf)

Makerchip output:

![Screenshot from 2023-08-20 21-42-28](https://github.com/Shivangi2207/RISC-V/assets/140998647/c268a250-e8fc-4cde-828e-3ed13f646ad8)

</details>

<details><summary><strong>RISC-V Control Logic</strong></summary>





## Lab1 : Register file read
Pipeline structure:
![Screenshot from 2023-08-20 21-59-23](https://github.com/Shivangi2207/RISC-V/assets/140998647/bb6d8153-9b7b-444c-bc76-f9c1b30cf097)

Makerchip Implementation:

![Screenshot from 2023-08-20 22-05-21](https://github.com/Shivangi2207/RISC-V/assets/140998647/0f770030-b163-4665-a201-3dea20163d35)


## lab2 : Arithmetic and Logic unit(ALU)
Pipeline structure:

![Screenshot from 2023-08-20 22-12-40](https://github.com/Shivangi2207/RISC-V/assets/140998647/354573dc-fdf5-4300-b207-7444128fd37c)

Makerchip Implementation

![Screenshot from 2023-08-20 22-17-54](https://github.com/Shivangi2207/RISC-V/assets/140998647/7fd0d43c-9e3a-48fb-a621-de17d6f76488)

## Lab3 : Register file write

Pipeline structure:

![Screenshot from 2023-08-20 22-12-40](https://github.com/Shivangi2207/RISC-V/assets/140998647/d2412f07-ffe3-43c1-b607-77d1a5929932)

Makerchip Implementation

![Screenshot from 2023-08-20 22-22-59](https://github.com/Shivangi2207/RISC-V/assets/140998647/23d81210-e835-4b26-a47b-5d1c4702b424)

</details>


## Day 5

## Complete Pipelined RISC-V CPU micro-architecture

<details><summary><strong>Pipeline Hazards<strong></summary>
  
##  Control Flow Hazards:
Control flow hazards occur when the execution of instructions is affected by changes in the program's control flow, such as branches or jumps. These hazards can lead to incorrect instruction execution and can slow down the pipeline. There are three main types of control flow hazards:

- Branch Hazards: These occur when a pipeline encounters a branch instruction that changes the program counter (PC) before the previous instructions have completed their execution. This can lead to wasted work if the pipeline has already started executing instructions following the branch that will not be needed.

- Control Hazards: Control hazards refer to situations where the pipeline has to stall or insert "bubble" stages in order to resolve the branch instruction. This happens when the outcome of a branch is not yet known, and subsequent instructions that depend on the branch outcome cannot proceed until the branch is resolved.

- Jump Hazards: Similar to branch hazards, jump hazards occur when a jump instruction changes the program counter before instructions following the jump have completed. This can also lead to wasted work and inefficient pipeline utilization.

## Read-After-Write (RAW) Hazards:

Read-after-write hazards occur when an instruction depends on the result of a previous instruction that writes to a register or memory location. These hazards can lead to incorrect results if not handled properly. There are three possible scenarios in RAW hazards:

- True Dependency (RAW): An instruction depends on the result of a previous instruction that writes to the same location. For example, if instruction B reads a value produced by instruction A, and instruction A has not yet completed execution, a hazard exists.

- Anti-Dependency (WAR): An instruction depends on a value that a subsequent instruction is going to write. For example, if instruction A writes to a register and then instruction B reads from the same register, instruction B might read the wrong value if it's executed before A's write.

- Output Dependency (WAW): Two instructions are trying to write to the same location, and the order of their execution affects the final result. This can lead to incorrect results if not properly managed.

![Screenshot from 2023-08-22 18-14-52](https://github.com/Shivangi2207/RISC-V/assets/140998647/de432e69-b349-4398-912b-53811cd7c4b0)

 
</details>
 
<details><summary><strong>Lab Works</strong></summary>

## Lab1 : CYCLE VALID SIGNAL


![Screenshot from 2023-08-22 21-52-28](https://github.com/Shivangi2207/RISC-V/assets/140998647/12203317-92eb-48f5-b1b6-5a96bc578d45)


## Lab2 : CYCLE RISC-V

![Screenshot from 2023-08-22 21-54-57](https://github.com/Shivangi2207/RISC-V/assets/140998647/122b0b9a-1e36-4df2-ba9c-161725bf2226)

## Lab3 : BRANCHES

![Screenshot from 2023-08-22 21-58-53](https://github.com/Shivangi2207/RISC-V/assets/140998647/3c1d47b0-08df-4e57-94e1-c53630f58ea1)


## Lab4 : ALU
![Screenshot from 2023-08-22 22-02-31](https://github.com/Shivangi2207/RISC-V/assets/140998647/f665778d-e727-4ca4-ba99-782ac4f445d8)


## Lab5 : LOAD

![Screenshot from 2023-08-22 22-04-55](https://github.com/Shivangi2207/RISC-V/assets/140998647/4766a3d4-9a89-4cc7-aee4-83eef849ba5d)

## Lab6 : LOAD/STORE


![Screenshot from 2023-08-22 22-06-28](https://github.com/Shivangi2207/RISC-V/assets/140998647/2b8288ee-5d00-4d7a-8041-a1c8e389b762)

</details>

<details><summary><strong>Final Implementation</strong></summary>

## Final Implementattion RISC-V Core CPU:

## Code 
```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop

 m4_include_lib(['(https://raw.githubusercontent.com/stevehoover/RISC-V_MYTH_Workshop/c1719d5b338896577b79ee76c2f443ca2a76e14f/tlv_lib/risc-v_shell_lib.tlv'])


\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV

   // /====================\
   // | Sum 1 to 9 Program |
   // \====================/
   //
   // Program for MYTH Workshop to test RV32I
   // Add 1,2,3,...,9 (in that order).
   //
   // Regs:
   //  r10 (a0): In: 0, Out: final sum
   //  r12 (a2): 10
   //  r13 (a3): 1..10
   //  r14 (a4): Sum
   //
   // External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the final result value to byte address 16
   m4_asm(LW, r15, r0, 10000)           // Load the final result value from adress 16 to x17
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)


   |cpu
      @0
         $reset = *reset;
         
         //MODIFIED NEXT PC LOGIC FOR INCLUDING BRANCH INSTRCUTIONS
         $pc[31:0] = >>1$reset ? 32'b0 :
                     >>3$valid_taken_branch ? >>3$br_target_pc :
                     >>3$valid_load ? >>3$inc_pc :
                     >>3$valid_jump && >>3$is_jal ? >>3$br_target_pc :
                     >>3$valid_jump && >>3$is_jalr ? >>3$jalr_target_pc :
                     >>1$inc_pc ;
         //START LOGIC TO PROVIDE FIRST VALID LOGIC
         //$start = (>>1$reset && $reset == 0) ? 1'b1 : 1'b0;
         //$valid = $reset ? 1'b0 :
                  //$start ? 1'b1 : >>3$valid;
     
      @1  
         //INSTRUCTION FETCH
         $inc_pc[31:0] = $pc + 32'd4;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
         $instr[31:0] = $imem_rd_data[31:0];
         
         //INSTRUCTION TYPES DECODE        
         
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         
         $is_r_instr = $instr[6:2] ==? 5'b011x0 ||
                       $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100;
         
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] ==? 5'b11001;
         
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         
         //INSTRUCTION IMMEDIATE DECODE
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                      $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                      $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                      $is_u_instr ? {$instr[31:12], 12'b0} :
                      $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                                            32'b0;
         //INSTRUCTION DECODE
         $opcode[6:0] = $instr[6:0];
         
         
         //INSTRUCTION FIELD DECODE
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
           
         $rs1_valid = $is_r_instr  || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         
         $funct3_valid = $is_r_instr  || $is_s_instr || $is_b_instr || $is_i_instr;
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
           
         $funct7_valid = $is_r_instr ;
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
           
         $rd_valid = $is_r_instr  || $is_u_instr || $is_j_instr || $is_i_instr;
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         
         
      @2
         //INSTRUCTION DECODE
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_load = $opcode == 7'b0000011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0100011;
         $is_xori = $dec_bits ==? 11'bx_100_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0100011;
         $is_andi = $dec_bits ==? 11'bx_111_0100011;
         $is_slli = $dec_bits ==? 11'b0_001_0100011;
         $is_srli = $dec_bits ==? 11'b0_101_0100011;
         $is_srai = $dec_bits ==? 11'b1_101_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         
         $jalr_target_pc[31:0] = $src1_value +$imm ;
      @3
         $is_jump = $is_jal || $is_jalr ;   
         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu $is_addi $is_add
                    $is_lui $is_auipc $is_jal $is_jalr $is_load $is_sb $is_sh $is_sw $is_slti
                    $is_sltiu $is_xori $is_ori $is_andi $is_slli $is_srli $is_srai $is_sub $is_sll
                    $is_slt $is_sltu $is_xor $is_srl $is_sra $is_or $is_and)
         
      @2  
         //REGISTER FILE READ
         //$rf_wr_en = 1'b0;
         //$rf_wr_index[4:0] = 5'b0;
         //$rf_wr_data[31:0] = 32'b0;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         
         $src1_value[31:0] = >>1$rf_wr_en && (>>1$rf_wr_index == $rf_rd_index1) ? >>1$result : $rf_rd_data1;
         $src2_value[31:0] = >>1$rf_wr_en && (>>1$rf_wr_index == $rf_rd_index2) ? >>1$result : $rf_rd_data2;
         $br_target_pc[31:0] = $pc +$imm;
         
      @3  
         //ARITHMETIC AND LOGIC UNIT (ALU)
         
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_ori ? $src1_value | $imm :
                         $is_xori ? $src1_value ^ $imm :
                         $is_slli ? $src1_value << $imm[5:0] :
                         ($is_addi || $is_load || $is_s_instr) ? $src1_value + $imm :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_and ? $src1_value & $src2_value :
                         $is_or ? $src1_value | $src2_value :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_sub ? $src1_value - $src2_value :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_srl ? $src1_value >> $src2_value[4:0] :
                         $is_sltu ? $sltu_rslt :
                         $is_sltiu ? $sltiu_rslt :
                         $is_lui ? {$imm[31:12],12'b0} :
                         $is_auipc ? $pc + $imm :
                         $is_jal ? $pc + 4 :
                         $is_jalr ? $pc + 4 :
                         $is_srai ? { {32{$src1_value[31]}},$src1_value} >> $imm[4:0] :
                         $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0,$src1_value[31]} :
                         $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0,$src1_value[31]} :
                         $is_sra ? { {32{$src1_value[31]}},$src1_value} >> $src2_value[4:0] :
                         32'bx;
         
         
         //REGISTER FILE WRITE
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         
         
         //BRANCH INSTRUCTIONS 1
         $taken_branch = $is_beq ? ($src1_value == $src2_value):
                         $is_bne ? ($src1_value != $src2_value):
                         $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])):
                         $is_bltu ? ($src1_value < $src2_value):
                         $is_bgeu ? ($src1_value >= $src2_value):
                         1'b0;
          //CYCLE VALID INSTRUCTIONS
         $valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch ||
                    >>1$valid_load || >>2$valid_load) ;
         
         $valid_load = $valid && $is_load ;
         //$valid = !(>>1$valid_taken_branch || >>2$valid_taken_branch);
         $valid_taken_branch = $valid && $taken_branch;
         $valid_jump = $is_jump && $valid ;
         `BOGUS_USE($taken_branch)
      @4
         //MINI 1-R/W MEMORY
         $dmem_wr_en = $is_s_instr && $valid ;
         $dmem_addr[3:0] = $result[5:2] ;
         $dmem_wr_data[31:0] = $src2_value ;
         $dmem_rd_en = $is_load ;
         
      @5
         //LOAD DATA
         $ld_data[31:0] = $dmem_rd_data ;   
         
         
         

      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

   
   // Assert these to end simulation (before Makerchip cycle limit).
   //*passed = *cyc_cnt > 40;
   *passed = |cpu/xreg[15]>>5$value == (1+2+3+4+5+6+7+8+9) ;
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
   //@4 would work for all lab
\SV
   endmodule



```
## Implemented output:


![Screenshot from 2023-08-22 19-55-15](https://github.com/Shivangi2207/RISC-V/assets/140998647/4409d727-dc02-43b9-b165-c491b9ef21bb)

</details>


## References

- https://github.com/stevehoover/RISC-V_MYTH_Workshop

- https://www.makerchip.com

- https://www.vsdiat.com
  
- https://github.com/RISCV-MYTH-WORKSHOP/riscv_myth_workshop_mar21-rahulgupta177

- https://github.com/Nancy0192/RISC-V-ISA
