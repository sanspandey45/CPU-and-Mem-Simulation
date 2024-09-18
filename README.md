# README

## CPU-and-Mem-Simulation
Models the behavior of CPU and memory using inter-process communication in C to analyze system performance and resource management. 

## Explanation

### CPU
   It will have these registers:  PC, SP, IR, AC, X, Y.<br>
   It will support the instructions shown on the next page of this document.<br>
   It will run the user program at address 0.<br>
   Instructions are fetched into the IR from memory.  The operand can be fetched into a local variable.<br>
   Each instruction should be executed before the next instruction is fetched.<br>
   The user stack resides at the end of user memory and grows down toward address 0.<br>
   The system stack resides at the end of system memory and grows down toward address 0.<br>
   There is no hardware enforcement of stack size.<br>
   The program ends when the End instruction is executed.  The 2 processes should end at that time.<br>
   The user program cannot access system memory (exits with error message).<br>
   
### Memory
   It will consist of 2000 integer entries, 0-999 for the user program, 1000-1999 for system code.<br>
   It will support two operations:<br>
       1. read(address) -  returns the value at the address<br>
       2. write(address, data) - writes the data to the address<br>
   Memory will read an input file containing a program into its array, before any CPU fetching begins.<br>
   Note that the memory is simply storage; it has no real logic beyond reading and writing.<br>
 
 ### Timer
A timer will interrupt the processor after every X instructions, where X is a command-line parameter.
The timer is always counting, whether in user mode or kernel mode.


### Interrupt processing
There are two forms of interrupts:  the timer and a system call using the int instruction.<br>
In both cases the CPU should enter kernel mode.<br>
The stack pointer should be switched to the system stack.<br>
The SP and PC registers (and only these registers) should be saved on the system stack by the CPU.<br>
The handler may save additional registers. <br>
A timer interrupt should cause execution at address 1000.<br>
The int instruction should cause execution at address 1500.<br>
The iret instruction returns from an interrupt.<br>
Interrupts should be disabled during interrupt processing to avoid nested execution.<br>
To make it easy, do not allow interrupts during system calls or vice versa<br>

### Instruction Set

1 = Load value<br>
2 = Load addr<br>
3 = LoadInd addr   <br>
4 = LoadIdxX addr<br>
5 = LoadIdxY addr<br>
6 = LoadSpX<br>
7 = Store addr<br>
8 = Get <br>
9 = Put port<br>
10 = AddX<br>
11 = AddY<br>
12 = SubX<br>
13 = SubY<br>
14 = CopyToX<br>
15 = CopyFromX<br>
16 = CopyToY<br>
17 = CopyFromY<br>
18 = CopyToSp<br>
19 = CopyFromSp   <br>
20 = Jump addr<br>
21 = JumpIfEqual addr<br>
22 = JumpIfNotEqual addr<br>
23 = Call addr<br>
24 = Ret <br>
25 = IncX <br>
26 = DecX <br>
27 = Push<br>
28 = Pop<br>
29 = Int <br>
30 = IRet<br>
50 = End	Load the value into the AC<br>



