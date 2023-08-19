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

An Application Binary Interface (ABI) is a set of rules and conventions that dictate how different software components interact with each other at the binary level. It defines the interface between software components, such as different programs, libraries, and the operating system, to ensure compatibility and proper communication. ABIs are particularly important in the context of compiled programming languages, as they provide the standards for how functions are called, parameters are passed, memory is allocated, and data is represented in binary format.
Key aspects of an ABI may include:

   1. Calling Conventions: Specifies how functions are called and how parameters are passed between the caller and callee. This includes the order in which parameters are pushed onto the stack or placed in registers, as well as how return values are retrieved.

  2.  Data Representation: Defines how different data types are represented in memory or registers. This covers integer, floating-point, and pointer data types.

  3.  Memory Layout: Specifies how memory is allocated, managed, and used by programs. It includes rules for stack frames, heap allocation, and data storage.

  4. Register Usage: Describes how registers are used for passing function arguments and return values, as well as which registers need to be preserved by callee functions.

  5.  Exception Handling: Outlines how exceptions, errors, and signals are managed and propagated between different parts of the software.

  6.  System Calls and Libraries: Specifies the interface between user-level programs and the operating system. It covers how system calls are made and how programs interact with shared libraries.

</details>
