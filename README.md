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


</details>
</details>
