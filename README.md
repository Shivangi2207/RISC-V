# RISC-V
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
<details><summary><strong>Digital Logic with TL-Verilog and Makerchip</strong></summary>
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


<details><summmary><strong>Pipeline Logic</strong></summmary>

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

</details>


</details>


