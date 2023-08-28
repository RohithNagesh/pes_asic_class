# VLSI Physical Design for ASICs
The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a digital circuit's logical representation into a physical layout that meets various performance, power, area, and manufacturability requirements.
# SKILL OUTCOMES
+ Architectural Design
+ RTL Design / Behavioral Modeling
+ Floorplanning
+ placement
+ clock Tree Synthesis
+ Routing

# INSTALLATION
<details>
<summary> RISC-V toolchain </summary>

 1. Download riscv_toolchain.sh from the repo
 2. Open terminal and go to the directory where riscv_toolchain.sh is present
 3. run the commands `chmod +x riscv_toolchain.sh` `./riscv_toolchain.sh`

This would install riscv toolchain along with iverilog
</details>

<details>
<summary> Yosys </summary>

1. Download yosys.sh from the repo
2. Open terminal and go to the directory where yosys.sh is present
3. run the commands `chmod +x yosys.sh` `./yosys.sh`
</details>

# TABLE OF CONTENTS
## DAY 1 
**Introduction to RISCV ISA and GNU Compiler Toolchain**
+ [Introduction to Basic Keywords](#introduction-to-basic-keywords)
  - Introduction
  - From Apps to Hardware
  - Detail Description of Course Content

+ [Labwork for RISCV Toolchain](#labwork-for-riscv-toolchain)
  - C Program
  - RISCV GCC Compiler and Dissemble
  - Spike Simulation and Debug

+ [Integer Number Representation](#integer-number-representation)
  - 64-bit Unsigned Numbers
  - 64-bit Signed Numbers
  - Labwork For Signed and Unsigned Numbers
    
## DAY 2 
**Introduction to ABI and Basic Verification Flow**
+ [Application Binary Interface](#application-binary-interface)
  - Introduction to ABI
  - Memmory Allocation for Double Words
  - Load, Add and Store Instructions
  - 32-Registers and their ABI Names

+ [Labwork using ABI Function Calls](#labwork-using-abi-function-calls)
  - Algorithm for C Program using ASM
  - Review ASM Function Calls
  - Simulate C Program using Function Call
  - Lab to Run C-Program on RISCV-CPU

## DAY 3
**Introduction to Verilog RTL design and Synthesis**
+ [Introduction to open-source simulator iverilog](#introduction-to-open-source-simulator-iverilog)
+ [Labs using iverilog and gtkwave](#labs-using-iverilog-and-gtkwave)
   - Introduction to lab
   - Introduction iverilog gtkwave 
+ [Introduction to Yosys and Logic synthesis](#introduction-to-yosys-and-logic-synthesis)
   - Introduction to yosys
   - Introduction to logic synthesis
+ [Lab using Yosys and Sky130 PDKs](#lab-using-yosys-and-sky130-pdks)

## DAY 4
**Timing libs, hierarchical vs flat synthesis and efficient flop coding styles**
+ [Introduction to timing dot libs](#introduction-to-timing-dot-libs)
+ [Hierarchical vs Flat Synthesis](#hierarchical-vs-flat-synthesis)
+ [Various Flop Coding Styles and optimization](#various-flop-coding-styles-and-optimization)
   - Flop coding styles 
   - Lab flop synthesis simulations
   - Interesting optimisations 

## DAY 5
**Combinational and sequential optmizations**
+ [Introduction to optimizations](#introduction-to-optimizations)
+ [Combinational logic optimizations](#combinational-logic-optimizations)
+ [Sequential logic optimizations](#sequential-logic-optimizations)
+ [Sequential optimzations for unused outputs](#sequential-optimzations-for-unused-outputs)

## DAY 6
**GLS, blocking vs non-blocking and Synthesis-Simulation mismatch**
+ [GLS Synthesis-Simulation mismatch and Blocking/Non-blocking statements](#gls-synthesis-simulation-mismatch-and-blocking-non-blocking-statements)
   - GLS Concepts And Flow Using Iverilog
   - Synthesis Simulation Mismatch
   - Blocking And Non Blocking Statements In Verilog
   - Caveats With Blocking Statements
+ [Labs on GLS and Synthesis-Simulation Mismatch](#labs-on-gls-and-synthesis-simulation-mismatch)
+ [Lab on synth-sim mismatch for blocking statement](#lab-on-synth-sim-mismatch-for-blocking-statement)

***
# Introduction to Basic Keywords
## Introduction
- **ISA (Instruction Set Archhitecture)**
  - ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
  - It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.

- **RISC-V (Reduced Instruction Set Computing - Five)**.
  - It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
  - RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<img width="536" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4eabe0b7-4581-419b-88e7-84c7ac1dac8e">

## From Apps to Hardware
1. **Apps:** Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.
2. **System software:** System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'
3. **Operating System:** The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

4. **Compiler:** A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5. **Assembler:** An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6. **RTL:** RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

 7. **Hardware:** Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

## Detail Description of Course Content
**Pseudo Instructions:** Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions.
`Ex: li, mv`.

**Base Integer Instructions:** The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations.
`Ex: add, sub, and, or, xor, sll`.

**Multiply Extension Intructions:** The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations.
`Ex: mul, mulh, mulhu, mulhsu`.

**Single and Double Precision Floating Point Extension:** The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

**Application Binary Interface:** ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

**Memory Allocation and Stack Pointer** 
- Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
- The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack. 

# Labwork for RISCV Toolchain
## C Program
We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

`leafpad sumton.c`
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=26;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```

Using the gcc compiler, we compiled the program to get the output.

`gcc sumton.c`
`./a.out`

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/c7eca245-fb7a-441f-9965-f4628658e014)

## RISCV GCC Compiler and Dissemble

Using the riscv gcc compiler `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sumton.o sumton.c`, we compiled the C program.

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/7e8cfb78-97f8-4f77-bc07-c3a7983a4761)

To get the assembly code for the C program, `riscv64-unknown-elf-objdump -d sumton.o | less` .

In order to view the main section, type `/main`.

Here, since we used `-O1` optimisation, the number of instructions are 14.

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/46189555-4bd1-41cc-aa3d-eb2542588350)

When we use `-Ofast` optimisation, we can see that the number of instructions have been 11

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/b0873b53-f854-4b91-89bd-40135b2d8824)

## Spike Simulation and Debug

`spike pk sumton.o` is used to check whether the instructions produced are right to give the correct output.

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/30f7da1b-dc0d-41f5-b3e6-df89193e03a5)

`spike -d pk sumton.c` is used for debugging.

The contents of the registers can also be viewed.

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/50bc3470-bedb-48df-a8e6-0d60c51e4d0d)

# Integer Number Representation 

## Unsigned Numbers
- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
- Range: 0 to 2^(N) - 1.

## Signed Numbers
- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
- Range : -(2^(N-1)) to 2^(N-1) - 1.
 
## Labwork
**Unsigned 64-bit Number**

``` c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/68566f80-7ea4-4249-ac80-5d0fae736720)

**Signed 64-bit Number**
``` c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/5df8b32d-6eb1-4dfe-8452-7a352bedbdce)

# Application Binary Interface
## Introduction to ABI
+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.
## Memmory Allocation for Double Words
64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. **Little-Endian:**
In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:**
In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
#### For example, consider the 64-bit hexadecimal value 0x0123456789ABCDEF. 
In Little-Endian representation, it would be stored as follows in memory:

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/307fabf6-7f58-4337-8171-6d62d99a4386)

In Big-Endian representation, it would be stored as follows in memory:

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/aa53e082-5878-4e3f-948a-f6f080ed0ed2)
## Load, Add and Store Instructions
Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.
## 32-Registers and their ABI Names
The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
#### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components. 

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/b735fc44-0c08-40e8-8303-c338647dbd9f)
# Labwork using ABI Function Calls
## Algorithm for C Program using ASM
- Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/1d76b7ef-cac9-4331-9190-31af36525e0c)
## Review ASM Function Calls
- You write your C code in one file and your assembly code in a separate file.
- In the assembly file, you declare assembly functions with appropriate signatures that match the calling conventions of your platform.

**C Program**
`custom1to9.c`
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
```
**Asseembly File**
`load.s`
``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
## Simulate C Program using Function Call
**Compilation:** To compile C code and Asseembly file use the command `riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o custom1to9.o custom1to9.c load.s` this would generate object file `custom1to9.o`.

**Execution:** To execute the object file run the command `spike pk custom1to9.o`

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/4f8f612c-82a6-48ab-9e67-6dce4eab704d)

## Lab to Run C-Program on RISCV-CPU

`git clone https://github.com/kunalg123/riscv_workshop_collaterals.git`

`cd riscv_workshop_collaterals`

`ls -ltr`

`cd labs`

`ls -ltr`

`chmod 777 rv32im.sh`

`./rv32im.sh`

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/3b8e5a8d-8f66-4621-ae35-3123f8e4f3f0)
# Introduction to open-source simulator iverilog
**Simulator:** RTL design is checked for adherence to the spec by simulating the design. Simulator is the tool used for simulating the design

**Design:** Design is the actual verilog codeor set of verilog codes which has the intended functionality to meet with the required specification

**Testbench:** Testbench is the setup to apply stimulus to the design to check its functionality
### How do simulator works?
- It looks for the changes in input signal
- upon change to the input the out put is evaluated

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/bc8c633a-7955-4bd1-8796-343db61642c3)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/27cf3101-8f13-44d0-a878-a56163a5d311)

# Labs using iverilog and gtkwave
## Introduction to lab
- Make new directory `mkdie VSD`
- `git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git`
- This should create a folder `sky130RTLDesignAndSynthesisWorkshop` in `VDS` directory
- You could see two folders under `sky130RTLDesignAndSynthesisWorkshop`
   1. my_lib: It contains all the standard cell libraries and verilog module
   2. verilog_files: It contains all the source code and testbench required for the lab
  
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/eff9cd5c-8777-4fd1-9c44-7049a8888f69)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/7b5ecd53-ea8c-455c-97cd-494186205d38)

## Introduction iverilog gtkwave
- Go to verilog_files directory
- Load Design and Testbench using the command `iverilog good_mux.v tb_good_mux.v`
### good_mux.v
``` v
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
### tb_good_mux.v
``` v
timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/08c3765f-68a7-4ce9-a85e-dba11388535d)

- Upon loading sucessfully `a.out` will be generated
- Execute the generated file it would dump `gtkwave tb_good_mux.vcd` file

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/4aa3e2c6-cd9c-4c95-85d2-119263f89fb5)

- Load the vcd file to simulator using the command `gtkwave tb_good_mux.vcd`
  
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/ff5aadc9-fefc-4bdf-9b34-35d55d4c198d)

# Introduction to Yosys and Logic synthesis
## Introduction to yosys
Yosys is an synthesizer which is used to convert RTL to netlist

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/bceda35c-e373-485b-8092-e210e37543f8)

**`netlist` is the representation of `DESIGN` in the form of standard cells present in `.lib`**

- To verify synthesis Netlist need to be fed to iverilog along with testbench
- vcd file generated from iverilog need to be fed to gtkwave simulator
- The output we get should be same as the output we got during RTL simulator

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/4c2fdb59-fa8c-4512-978a-ccf4bd6bbf6d)

## Introduction to logic synthesis
Logic synthesis is a vital step in digital circuit design where high-level descriptions of circuits are transformed into specific implementations using logic gates. It optimizes circuits for factors like performance, area, power, and cost. The process includes library mapping, optimization, technology mapping, timing analysis, and verification. It's an iterative process often done with specialized software tools, enabling efficient hardware design.

**.lib:** 
- Logic synthesis tools use a library of standard cells. These cells are predefined logic gates with different functionalities and characteristics
- It will also contain fast and slow version of same gate
### why fast and slow version of same gate?
Fast and slow versions of gates are essential in digital circuit design to balance between clock frequency and timing constraints. Fast gates have shorter propagation delays and are used to reduce setup and hold time violations, allowing for higher clock frequencies. Slow gates, with longer delays, can be used to intentionally slow down critical paths or address timing issues. The Tclk formula helps calculate the maximum clock frequency while considering these factors.

**Tclk formula:** ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/4737db4a-c1db-47a3-8c6b-1c8634c00189)

- **t_setup:** The setup time is the minimum time before the clock edge when the input data must be stable.
- **t_hold:** The hold time is the minimum time after the clock edge during which the input data must remain stable.
- **t_propagation:** This term represents the propagation delay of the logic gates in the critical path.
- **Tcq:** This term represents the clock-to-q delay of the flip-flops or registers used in the design. It's often a fixed value based on the chosen flip-flop technology.

# Lab using Yosys and Sky130 PDKs
Steps to realize good_mux(design) in terms of standard cells avilable in library sky130_fd_sc_hd__tt_025C_1v80.lib
+ Go to verilog_files directory
+ once you get to verilog_files directory, Invoke yosys by using the command `yosys`
  ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/5f168642-82a8-4ad9-8541-ff484076757e)

  1. Read library: `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
     ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/b0ad59a0-9d69-4a67-a553-5bdc80a8b530)

  3. Read design: `read_verilog good_mux.v`
     ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/2e3da0ba-5af4-4f76-98b1-829924177dba)

  5. Synthesis: `synth -top good_mux`
     ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/f25366a7-f109-4eeb-b692-959a3824d9bd)

  7. Generate netlist: `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
     ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/a392baf5-8d4d-4e16-84df-7cb80c744815)

  9. Logic realized: `show`
      ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/9926df63-37ad-49c2-b936-e6e763a81f9a)

  10. Write netlist: `write_verilog -noattr good_mux_netlist.v`, `!gvim good_mux_netlist.v`
      ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/47c48966-4f66-4bcc-8858-30649485c8f3)
### good_mux_netlist.v
``` v
/* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

module good_mux(i0, i1, sel, y);
  wire _0_;
  wire _1_;
  wire _2_;
  wire _3_;
  input i0;
  wire i0;
  input i1;
  wire i1;
  input sel;
  wire sel;
  output y;
  wire y;
  sky130_fd_sc_hd__mux2_1 _4_ (
    .A0(_0_),
    .A1(_1_),
    .S(_2_),
    .X(_3_)
  );
  assign _0_ = i0;
  assign _1_ = i1;
  assign _2_ = sel;
  assign y = _3_;
endmodule
```
# Introduction to timing dot libs
### sky130_fd_sc_hd__tt_025C_1v80.lib

+ **sky130:** This indicates that the library is associated with the SkyWater 130nm process technology. Process technology refers to the manufacturing process used to create integrated circuits (ICs) and determines factors like transistor size and performance characteristics.
  
+ **fd_sc_hd:** These letters likely stand for different aspects of the library. "fd" might refer to "Foundation," suggesting that this library contains fundamental building blocks for digital IC design. "sc" could stand for "Standard Cells," which are pre-designed logic gates used in IC design. "hd" could refer to "high-density" libraries, which typically contain smaller, more compact cell designs for achieving higher logic density in ICs.
  
+ **tt_025C:** This part of the name could refer to the library's operating conditions or temperature and voltage settings. "tt" might stand for "typical temperature," and "025C" could refer to 25 degrees Celsius, a common temperature for IC specifications. These conditions are important for characterizing the library's performance.
  
+ **1v80:** This likely represents the supply voltage for the library. In this case, "1v80" indicates a supply voltage of 1.8 volts, which is a common voltage level for digital ICs.

### Libraries contain

+ **Standard Cells:** This library is likely to include a variety of standard cells, which are pre-designed building blocks for digital logic. Standard cells consist of logic gates (e.g., AND, OR, XOR), flip-flops, latches, multiplexers, and other fundamental digital components. These cells are characterized for the specific process technology (in this case, SkyWater 130nm) and operating conditions (temperature and voltage).
  
+ **Timing Information:** The library will provide timing information for each standard cell. This information includes parameters like propagation delay, setup time, hold time, and other timing characteristics. Designers use this data to ensure that signals propagate correctly through the logic gates.
  
+ **Power Characteristics:** Power consumption data is crucial for estimating the energy usage of a design. The library will typically include information on dynamic power (power consumed when the circuit is switching) and static power (power consumed when the circuit is idle).
  
+ **Pin and I/O Information:** The library will specify the input and output pins for each standard cell, including pin names, directions (input or output), and electrical characteristics.
  
+ **Library Files:** These library files often come in various formats, including Liberty (.lib) files, which contain detailed timing and power information, and Verilog models, which allow designers to use these standard cells in their digital designs.
  
+ **Characterization Data:** The library may include data characterizing how the standard cells perform under different operating conditions, including variations in temperature and supply voltage. This helps designers account for variability in their designs.
  
+ **Technology Files:** These files might also include information about the specific characteristics of the SkyWater 130nm process technology, such as transistor models, interconnect information, and other process-related data.

# Hierarchical vs Flat Synthesis
### Hierarchical Synthesis
- Hierarchical synthesis involves dividing the design into logical modules or blocks and synthesizing each module separately.
- These modules can have their own hierarchies, and they communicate through well-defined interfaces
- It enhances reusability, as individual modules can be reused in other designs.
- Supports better scalability for large, complex designs.

### Steps to Hierarchical Synthesis
- Go to verilog_files directory
- once you get to verilog_files directory, Invoke yosys by using the command `yosys`
- once yosys is invoked follow the above sequence of commands
  ``` sh
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog multiple_modules.v
  synth -top multiple_modules
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show multiple_modules
  write_verilog -noattr multiple_modules_hier.v
  !gvim multiple_modules_hier.v
  ```
  ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/377a4c27-2da0-494a-9b60-b4d34f564334)

  **multiple_modules_hier.v**
  ``` v
  /* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

  module multiple_modules(a, b, c, y);
    input a;
    wire a;
    input b;
    wire b;
    input c;
    wire c;
    wire net1;
    output y;
    wire y;
    sub_module1 u1 (
      .a(a),
      .b(b),
      .y(net1)
    );
    sub_module2 u2 (
      .a(net1),
      .b(c),
      .y(y)
    );
  endmodule
 
  module sub_module1(a, b, y);
    wire _0_;
    wire _1_;
    wire _2_;
    input a;
    wire a;
    input b;
    wire b;
    output y;
    wire y;
    sky130_fd_sc_hd__and2_0 _3_ (
      .A(_1_),
      .B(_0_),
      .X(_2_)
    );
    assign _1_ = b;
    assign _0_ = a;
    assign y = _2_;
  endmodule

  module sub_module2(a, b, y);
    wire _0_;
    wire _1_;
    wire _2_;
    input a;
    wire a;
    input b;
    wire b;
    output y;
    wire y;
    sky130_fd_sc_hd__or2_0 _3_ (
      .A(_1_),
      .B(_0_),
      .X(_2_)
    );
    assign _1_ = b;
    assign _0_ = a;
    assign y = _2_;
  endmodule
  ```
### Flat Synthesis
- In flat synthesis, the entire design is synthesized as a single, monolithic entity.
- All modules, submodules, and logic are flattened into a single level of hierarchy.
- This means that all components, regardless of their intended functionality, are combined into a single giant netlist
- Best suited for simple designs where complexity is low and maintainability isn't a significant concern.

### Steps to Flat Synthesis
- Go to verilog_files directory
- once you get to verilog_files directory, Invoke yosys by using the command `yosys`
- once yosys is invoked follow the above sequence of commands
  ``` sh
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog multiple_modules.v
  synth -top multiple_modules
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  flatten
  show
  write_verilog -noattr multiple_modules_flat.v
  !gvim multiple_modules_flat.v
  ```
  ![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/54c5a8af-be44-4a08-976b-bc63df3563a2)

  **multiple_modules_flat.v**
  ``` v
  /* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

  module multiple_modules(a, b, c, y);
    wire _0_;
    wire _1_;
    wire _2_;
    wire _3_;
    wire _4_;
    wire _5_;
    input a;
    wire a;
    input b;
    wire b;
    input c;
    wire c;
    wire net1;
    wire \u1.a ;
    wire \u1.b ;
    wire \u1.y ;
    wire \u2.a ;
    wire \u2.b ;
    wire \u2.y ;
    output y;
    wire y;
    sky130_fd_sc_hd__and2_0 _6_ (
      .A(_1_),
      .B(_0_),
      .X(_2_)
    );
    sky130_fd_sc_hd__or2_0 _7_ (
      .A(_4_),
      .B(_3_),
      .X(_5_)
    );
    assign _4_ = \u2.b ;
    assign _3_ = \u2.a ;
    assign \u2.y  = _5_;
    assign \u2.a  = net1;
    assign \u2.b  = c;
    assign y = \u2.y ;
    assign _1_ = \u1.b ;
    assign _0_ = \u1.a ;
    assign \u1.y  = _2_;
    assign \u1.a  = a;
    assign \u1.b  = b;
    assign net1 = \u1.y ;
  endmodule
  ```
# Various Flop Coding Styles and optimization
## Flop coding styles
**Asynchronous Reset D Flip-Flop**
- When an asynchronous reset input is activated (set to '1'), regardless of the clock signal, the stored value is forced to '0'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
### dff_asyncres_syncres.v
``` v
module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```

**Asynchronous Set D Flip-Flop**
- When an asynchronous set input is activated (set to '1'), regardless of the clock signal, the stored value is forced to '1'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
### dff_async_set.v
``` v
module dff_async_set ( input clk ,  input async_set , input d , output reg q );
always @ (posedge clk , posedge async_set)
begin
	if(async_set)
		q <= 1'b1;
	else	
		q <= d;
end
endmodule
```

**Synchronous Reset D Flip-Flop**
- When a synchronous reset input is activated (set to '1') at the positive edge of the clock signal, the stored value is forced to '0'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
### dff_syncres.v
``` v
module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk )
begin
	if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```

**D Flip-Flop with Asynchronous Reset and Synchronous Reset**
- This flip-flop combines both asynchronous and synchronous reset features.
- When the asynchronous reset input is activated (set to '1'), the stored value is immediately forced to '0'.
- When the synchronous reset input is activated (set to '1') at the positive edge of the clock signal, the stored value is forced to '0'.
- Otherwise, on the positive edge of the clock signal, the stored value is updated with the data input.
### dff_asyncres_syncres.v
``` v
module dff_asyncres_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
always @ (posedge clk , posedge async_reset)
begin
	if(async_reset)
		q <= 1'b0;
	else if (sync_reset)
		q <= 1'b0;
	else	
		q <= d;
end
endmodule
```
## Flop synthesis simulations 
**Asynchronous Reset D Flip-Flop**

**Simulation**

Go to verilog_files directory where the design and test_bench are present

Run the following commands to simulate dff_asyncres.v
```
iverilog dff_asyncres.v tb_dff_asyncres.v
./a.ot
gtkwave tb_dff_asyncres.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/fbd85981-4df1-4bf3-a163-0a3aded4e15c)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/1a7778f4-ba78-42e0-ab43-39b75364ccde)

**Synthsis**

Go to verilog_files directory and invoke yosys

Once you invoke yosys, Run following commands to Synthsis dff_asyncres
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog dff_asyncres.v
  synth -top dff_asyncres
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/1549a409-e731-4a58-a7cb-66d59669d030)

**Asynchronous set D Flip-Flop**

**Simulation**

Go to verilog_files directory where the design and test_bench are present

Run the following commands to simulate dff_async_set.v
```
iverilog dff_async_set.v tb_dff_async_set.v
./a.ot
gtkwave tb_dff_async_set.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/d72175bd-f0ad-49b8-ab8d-ff67eda7ae64)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/c8e3250e-da10-41d0-9993-97a531949ca3)

**Synthsis**

Go to verilog_files directory and invoke yosys

Once you invoke yosys, Run following commands to Synthsis dff_async_set
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog dff_async_set.v
  synth -top dff_async_set
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/427946a3-c7d7-46f9-8dc8-75649126b4ed)

**Asynchronous Reset D Flip-Flop**

**Simulation**

Go to verilog_files directory where the design and test_bench are present

Run the following commands to simulate dff_syncres.v
```
iverilog dff_asyncres.v tb_dff_syncres.v
./a.ot
gtkwave tb_dff_syncres.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/9d5d7632-bc01-4fc2-a38f-9a6565261280)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/26064cde-211e-42b2-b1fc-7852120a01eb)

**Synthsis**

Go to verilog_files directory and invoke yosys

Once you invoke yosys, Run following commands to Synthsis dff_syncres
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog dff_syncres.v
  synth -top dff_syncres
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/6b39b840-7294-460d-93ec-c6c7da59d7ca)

 ## Interesting optimisations 
 **mult_2.v**
``` v
module mul2 (input [2:0] a, output [3:0] y);
	assign y = a * 2;
endmodule
```
**Synthsis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog mult_2.v
synth -top mul2
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mul2_netlist.v
!gvim mul2_netlist.v
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/7aa10ce6-4797-4e09-b44c-5fa73b82b889)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/56eeaf43-fa5b-4b44-a2ba-6fbf874c423d)

**mul2_netlist.v**
``` v
/* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

module mul2(a, y);
  input [2:0] a;
  wire [2:0] a;
  output [3:0] y;
  wire [3:0] y;
  assign y = { a, 1'h0 };
endmodule
```

 **mult_8.v**
``` v
module mult8 (input [2:0] a , output [5:0] y);
	assign y = a * 9;
endmodule
```
**Synthsis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog mult_2.v
synth -top mult8
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult8_netlist.v
!gvim mult8_netlist.v
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/dc0ab421-deb8-4449-b5ef-58946b2ddd27)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/f3bcbe12-1b0e-4dc9-b906-09d320a87de7)

**mult8_netlist.v**
``` v
/* Generated by Yosys 0.32+51 (git sha1 6405bbab1, gcc 12.3.0-1ubuntu1~22.04 -fPIC -Os) */

module mult8(a, y);
  input [2:0] a;
  wire [2:0] a;
  output [5:0] y;
  wire [5:0] y;
  assign y = { a, a };
endmodule
```
# Introduction to optimizations
1. **CCombinational optimization**
    - Combinational optimization is a branch of mathematical optimization that focuses on selecting the best combination of discrete options to optimize a given function. 
    - Two methods within computational optimization are:
       + **Constant Propagation:** This technique identifies and replaces variables or expressions with their constant values, reducing redundancy in code and improving performance.
       + **Boolean Optimization:** This method simplifies boolean expressions or logic circuits by reducing the number of logical gates or terms while preserving the same logical behavior, which is useful in digital circuit design and logical reasoning.

2. **Sequential logic optimization**
    - Sequential logic optimization is the process of enhancing the performance and efficiency of digital circuits containing flip-flops and state elements.
    - Methods under this optimization umbrella include:
       + **Sequential Constant Propagation:** Identifies and propagates constant values through flip-flops to reduce redundant state transitions.
       + **State Optimization:** Reduces the number of states in finite state machines (FSMs) by merging equivalent states, simplifying the circuit.
       + **Sequential Logic Cloning:** Replicates portions of sequential logic to alleviate bottlenecks and improve circuit throughput.
       + **Retiming:** Adjusts the placement of flip-flops within a circuit to optimize timing, balance critical paths, and enhance overall performance.

# Combinational logic optimizations
**opt_check.v**
``` v
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule
```
**Synthesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog opt_check.v
synth -top opt_check
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/329b7b8d-4858-4717-b1fa-d3a1ef437e33)

**opt_check2.v**
``` v
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule
```
**Synthesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog opt_check2.v
synth -top opt_check2
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/fa65b4a0-f13e-44f8-b2aa-693aa105902c)

**opt_check3.v**
``` v
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule
```
**Synthesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog opt_check3.v
synth -top opt_check3
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/bb364cb3-a852-4216-a4be-e3a323b9e8c1)

**multiple_module_opt.v**
``` v
module sub_module1(input a , input b , output y);
 assign y = a & b;
endmodule


module sub_module2(input a , input b , output y);
 assign y = a^b;
endmodule


module multiple_module_opt(input a , input b , input c , input d , output y);
wire n1,n2,n3;

sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
sub_module2 U3 (.a(b), .b(d) , .y(n3));

assign y = c | (b & n1); 


endmodule
```
**Synthesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
read_verilog multiple_module_opt.v
synth -top multiple_module_opt
flatten
opt_clean -purge
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/75e74cb0-a5e5-4b27-a2d8-0db5a0bd8bc0)

# Sequential logic optimizations
**dff_const1.v**
``` v
module dff_const1(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b0;
	else
		q <= 1'b1;
end

endmodule
```
**Simulate**
```
iverilog dff_const1.v tb_dff_const1.v
./a.out
gtkwave tb_dff_const1.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/d7910d52-cd13-4936-b759-f19aa2ac7309)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/e6bb2a84-b7d2-4b2b-b16e-89ca790d4bb2)

**Synthesis**
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog dff_const1.v
  synth -top dff_const1
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/5d6a00fe-5d86-45c1-a4e9-5c66fc5c3dfb)

**dff_const2.v**
``` v
module dff_const2(input clk, input reset, output reg q);
always @(posedge clk, posedge reset)
begin
	if(reset)
		q <= 1'b1;
	else
		q <= 1'b1;
end

endmodule
```
**Simulate**
```
iverilog dff_const1.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const2.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/246d73d4-e13b-4987-bc22-d90aaf9e3df1)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/23829be5-95f7-4ee1-a9bb-f054e655bf2b)

**Synthesis**
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog dff_const2.v
  synth -top dff_const2
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/e1b5b3d6-59d4-4f42-acb1-395c497aa1fd)

**dff_const3.v**
``` v
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
		q <= 1'b1;
		q1 <= 1'b0;
	end
	else
	begin
		q1 <= 1'b1;
		q <= q1;
	end
end

endmodule
```

**Simulate**
```
iverilog dff_const3.v tb_dff_const2.v
./a.out
gtkwave tb_dff_const3.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/1a58abbc-eb10-47a8-b248-fd46f406cb63)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/39f7fb82-cb6f-439b-b625-651758f4028f)

**Synthesis**
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog dff_const3.v
  synth -top dff_const3
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/1b3f5f7a-950b-4ecd-b420-eb82c70f19ae)

# Sequential optimzations for unused outputs
**counter_opt.v**
``` v
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```
**Synthesis**
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog counter_opt.v
  synth -top counter_opt
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/2b562581-9081-4975-875a-d1e97bb47eb3)

**counter_opt2.v**
``` v
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = (count[2:0] == 3'b100);

always @(posedge clk ,posedge reset)
begin
	if(reset)
		count <= 3'b000;
	else
		count <= count + 1;
end

endmodule
```
**Synthesis**
```
  read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  
  read_verilog counter_opt2.v
  synth -top counter_opt
  dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib 
  abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
  show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/665b9150-3faa-4fb2-96f0-149022c4f864)

# GLS Synthesis-Simulation mismatch and Blocking Non-blocking statements
## GLS Concepts And Flow Using Iverilog
### Gate level simulation
+ Gate-level simulation is a method used in electronics design to test and verify digital circuits at the level of individual logic gates and flip-flops.
+ It's crucial for checking functionality, timing, power consumption, and generating test patterns for integrated circuits.
+ It operates at a lower abstraction level than higher-level simulations and is essential for debugging and ensuring circuit correctness.

### To perform gate-level simulation using Icarus Verilog (iverilog):

1. Write RTL code.
2. Synthesize to generate gate-level netlist.
3. Create a testbench in Verilog.
4. Compile both netlist and testbench.
5. Run simulation with compiled files.Debug and iterate as needed.
6. Perform timing analysis if necessary.
7. Generate test vectors for manufacturing tests.

## Synthesis-Simulation mismatch
+ Synthesis-simulation mismatch is when there are differences between how a digital circuit behaves in simulation at the RTL level and how it behaves after gate-level synthesis.
+ This can occur due to optimization, clock domain issues, library differences, or other factors.
+ To address it, ensure consistent tool versions, check synthesis settings, debug with simulation tools, and follow best practices in RTL coding and design.
+ Resolving these mismatches is crucial for reliable hardware implementation.

## Blocking And Non-Blocking Statements
**Blocking Statements**
+ Blocking statements execute sequentially in the order they appear within a procedural block or always block.
+ When a blocking assignment or operation is encountered, the simulation halts and waits for it to complete before moving on to the next statement.
+ Blocking assignments are typically used to describe combinational logic, where the order of execution doesn't matter, and each assignment depends on the previous one.

**Example (Blocking Assignment):** `a = b + c; // b and c must be known before calculating 'a'`

**Non-Blocking Statements**
+ Non-blocking statements allow concurrent execution within a procedural block or always block, making them suitable for describing synchronous digital circuits.
+ When a non-blocking assignment or operation is encountered, the simulation does not wait for it to complete. Instead, it schedules the assignments to occur in parallel.
+ Non-blocking assignments are typically used to model sequential logic, like flip-flops and registers, where parallel execution is required.

**Example (Non-Blocking Assignment):** 
```
always @(posedge clk)
  begin
    b <= a; // Concurrently scheduled assignment
    c <= b; // Concurrently scheduled assignment
  end
```
## Caveats With Blocking Statements
**Caveats with blocking statements in hardware description languages like Verilog include:**
+ **Sequential Execution:** Blocking statements execute sequentially, which may not accurately represent concurrent hardware behavior in the design.

+ **Order Dependency:** The order of blocking statements can affect simulation results, leading to race conditions or unintended behavior.

+ **Combinational Logic Only:** Blocking statements are primarily used for modeling combinational logic, making them less suitable for sequential or synchronous logic.

+ **Limited for Testbenches:** In testbench code, excessive use of blocking statements can lead to simulation race conditions that don't reflect real-world hardware behavior.

+ **Initialization Issues:** In some cases, initializing variables with blocking assignments can lead to unexpected results due to order-dependent initialization.

To mitigate these issues, designers often use non-blocking statements for modeling sequential logic and adopt good coding practices to minimize order dependencies and improve code clarity.

# Labs on GLS and Synthesis-Simulation Mismatch
**ternary_operator_mux.v**
``` v
module ternary_operator_mux (input i0 , input i1 , input sel , output y);
	assign y = sel?i1:i0;
endmodule
```
**RTL Simulation**
```
iverilog ternary_operator_mux.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/bdfe93c4-f8aa-49d6-a9f1-a8af4fcea1d1)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/f52e5c83-9790-4eef-8693-e1e1bc7895c5)

**Synthesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog ternary_operator_mux.v
synth -top ternary_operator_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr ternary_operator_mux_netlist.v
show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/e9567674-3a50-477f-b10b-39c84daaa1ff)

**GLS**
To to Gate level simulation, Invoke iverilog with verilog modules
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_netlist.v tb_ternary_operator_mux.v
./a.out
gtkwave tb_ternary_operator_mux.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/e6289486-1ddb-4521-9307-97a5ed13fb78)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/77468c92-bf03-4d97-9e54-3b41def938d8)

** bad_mux.v**
``` v
module bad_mux (input i0 , input i1 , input sel , output reg y);
always @ (sel)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
**RTL Simulation**
```
iverilog bad_mux.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/26ab96d7-78d0-4cc9-a762-1f5ec30e06a7)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/ac7bdfe2-bd98-4734-a1d3-f137bd22f1ac)

**Synthesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog bad_mux.v
synth -top bad_mux
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr bad_mux_netlist.v
show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/b1480eef-1e3a-494c-b63d-b7f8ca9d2f74)

**GLS**
To to Gate level simulation, Invoke iverilog with verilog modules
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_netlist.v tb_bad_mux.v
./a.out
gtkwave tb_bad_mux.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/5242720b-aaf0-487b-9b5c-837aba9b73c1)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/c17f5011-5d5a-43dd-8159-8dbedc75380d)

# Labs on synth-sim mismatch for blocking statement
**blocking_caveat.v**
``` v
module blocking_caveat (input a , input b , input  c, output reg d); 
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule
```
**RTL Simulation**
```
iverilog blocking_caveat.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/63ea0db3-06d1-4b38-91e4-a69cec585ef6)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/5616eece-735a-496c-be5c-49c78e0d0ead)

**Synrhesis**
```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog blocking_caveat.v
synth -top blocking_caveat
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
write_verilog -noattr blocking_caveat_netlist.v
show
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/93d5f4fd-87ce-4c8b-bd9d-2796ec160843)

**GLS**
To to Gate level simulation, Invoke iverilog with verilog modules
```
iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_netlist.v tb_blocking_caveat.v
./a.out
gtkwave tb_blocking_caveat.vcd
```
![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/27dcbc2c-4d95-4b3b-b84a-535d2b3dc63a)

![image](https://github.com/RohithNagesh/pes_asic_class/assets/103078929/ecb37ebd-1c53-4ac5-b4e7-1197ab815ec0)
