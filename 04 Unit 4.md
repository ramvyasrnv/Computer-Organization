# Unit -4  Central Processing Unit and Pipeline Processing
# Topics Covered
-  Stack Organization
-  General Register Organization
-  Instruction format
-  Addressing Modes, data transfer and manipulation, 
-  Program Control
-  Reduced Instruction Set Computer (RISC) 
-  Complex Instruction Set Computer (CISC)
-  Parallel processing
# Stack Organization
-  A stack is a storage device that stores information in such a manner that the item stored last is the first item retrieved (LIFO).
-  The register that holds the address for the stack is called a stack pointer (SP) because its value always points at the top item in the stack. 
-  The physical registers of a stack are always available for reading or writing. It is the content of the word that is inserted or deleted.
-  There are two types of stack organization
	- Register stack – built using registers
	- Memory stack – logical part of memory allocated as stack
## Register Stack
-  A stack can be placed in a portion of a large memory or it can be organized as a collection of a finite number of memory words or registers. Figure shows the organization of a 64-word register stack. 
-  The stack pointer register SP contains a binary number whose value is equal to the address of the word that is currently on top of the stack.
-  In a 64-word stack, the stack pointer contains 6 bits because 26 = 64. 
-  Since SP has only six bits, it cannot exceed a number greater than 63 (111111 in binary).
-  The one-bit register FULL is set to 1 when the stack is full, and the one-bit register EMTY is set to 1 when the stack is empty of items. 
-  DR is the data register that holds the binary data to be written into or read out of the stack.

![image-20220202141025011](images/image-20220202141025011.png)

## Memory Stack
-  The implementation of a stack in the CPU is done by assigning a portion of memory to a stack operation and using a processor register as a stack pointer. 
-  Figure shows a portion of computer memory partitioned into three segments: program, data, and stack. 
-  The program counter PC points at the address of the next instruction in the program which is used during the fetch phase to read an instruction.
-  The address registers AR points at an array of data which is used during the execute phase to read an operand.
-  The stack pointer SP points at the top of the stack which is used to push or pop items into or from the stack.
-  We assume that the items in the stack communicate with a data register DR. 

![image-20220202141106035](images/image-20220202141106035.png)

# Reverse Polish Notation

-  The common mathematical method of writing arithmetic expressions imposes difficulties when evaluated by a computer.
-  The Polish mathematician Lukasiewicz showed that arithmetic expressions can be represented in prefix notation as well as postfix notation.

![image-20220202141211773](images/image-20220202141211773.png)



## Evaluation of Arithmetic Expression

![image-20220202141308976](images/image-20220202141308976.png)

# General Register based CPU Organization
-  When we are using multiple general-purpose registers, instead of a single accumulator register, in the CPU Organization then this type of organization is known as General register-based CPU Organization. 
-  In this type of organization, the computer uses two or three address fields in their instruction format. Each address field may specify a general register or a memory word. 
-  If many CPU registers are available for heavily used variables and intermediate results, we can avoid memory references much of the time, thus vastly increasing program execution speed, and reducing program size. 

![image-20220202141356271](images/image-20220202141356271.png)

![image-20220202141414183](images/image-20220202141414183.png)

-  The CPU bus system is managed by the control unit. The control unit explicit the data flow through the ALU by choosing the function of the ALU and components of the system.
-  Consider R1 ← R2 + R3, the following are the functions implemented within the CPU
-  MUX A Selector (SELA) − It can place R2 into bus A.
-  MUX B Selector (SELB) − It can place R3 into bus B.
-  ALU Operation Selector (OPR) − It can select the arithmetic addition (ADD).
-  Decoder Destination Selector (SELD) − It can transfers the result into R1.

| **Binary Code** | **SELA** | **SELB** | **SELD** |
| --------------- | -------- | -------- | -------- |
| **000**         | Input    | Input    | None     |
| **001**         | R1       | R1       | R1       |
| **010**         | R2       | R2       | R2       |
| **011**         | R3       | R3       | R3       |
| **100**         | R4       | R4       | R4       |
| **101**         | R5       | R5       | R5       |
| **110**         | R6       | R6       | R6       |
| **111**         | R7       | R7       | R7       |

| **OPR Select** | **Operation**  | **Symbol** |
| -------------- | -------------- | ---------- |
| **00000**      | Transfer A     | TSFA       |
| **00001**      | Increment A    | INCA       |
| **00010**      | Add A + B      | ADD        |
| **00101**      | Subtract A - B | SUB        |
| **00110**      | Decrement A    | DECA       |
| **01000**      | ADD A and B    | AND        |
| **01010**      | OR A and B     | OR         |
| **01100**      | XOR A and B    | XOR        |
| **01110**      | Complement A   | COMA       |
| **10000**      | Shift right A  | SHRA       |
| **11000**      | Shift left A   | SHLA       |

## Advantages of General register based CPU organization

-  Efficiency of CPU increases as there are a large number of registers are used in this organization.
-  Less memory space is used to store the program since the instructions are written in a compact way. 
-  The disadvantages of General register based CPU organization
-  Care should be taken to avoid unnecessary usage of registers. Thus, compilers need to be more intelligent in this aspect.
-  Since a large number of registers are used, thus extra cost is required in this organization. 

## Disadvantages of General register based CPU organization

- Care should be taken to avoid unnecessary usage of registers. Thus, compilers need to be more intelligent in this aspect.
- Since a large number of registers are used, thus extra cost is required in this organization

# Instruction Format
-  Instructions are categorized into different formats with respect to the operand fields in the instructions.
-  Three Address Instructions
-  Two Address Instruction
-  One Address Instruction
-  Zero Address Instruction
-  RISC Instructions
## Three Address Instructions
-  Computers with three-address instruction formats can use each address field to specify either a processor register or a memory operand.
-  The program in assembly language that evaluates X = (A + B) * (C + D) is shown below.

![image-20220202141712849](images/image-20220202141712849.png)

-  The advantage of three-address format is that it results in short programs when evaluating arithmetic expressions.
-  The disadvantage is that the binary-coded instructions require too many bits to specify three addresses.



## Two Address Instructions
-  Two address instructions are the most common in commercial computers. Here again each address field can specify either a processor register or a memory word. 
-  The program to evaluate X = (A + B) * (C + D) is as follows:

![image-20220202141642960](images/image-20220202141642960.png)

## One Address Instruction
-  One address instructions use an implied accumulator (AC) register for all data manipulation.
-  For multiplication and division these is a need for a second register.
-  However, here we will neglect the second register and assume that the AC contains the result of all operations. 
-  The program to evaluate X = (A + B) * (C + D) is

![image-20220202141738799](images/image-20220202141738799.png)

## Zero Address Instruction
-  A stack-organized computer does not use an address field for the instructions ADD and MUL.
-  The PUSH and POP instructions, however, need an address field to specify the operand that communicates with the stack. 
-  The program to evaluate X = (A + B) * (C + D) will be written for a stack-organized computer.
-  To evaluate arithmetic expressions in a stack computer, it is necessary to convert the expression into reverse polish notation.
-  The program to evaluate X = (A + B) * (C + D)

![image-20220202141810199](images/image-20220202141810199.png)

## RISC Instruction
-  The instruction set of a typical RISC processor is restricted to the use of load and store instructions when communicating between memory and CPU.
-  All other instructions are executed within the registers of the CPU without referring to memory.
-  A program for a RISC type CPU consists of LOAD and STORE instructions that have one memory and one register address, and computational-type instructions that have three addresses with all three specifying processor registers.
-  The following is a program to evaluate X = (A + B) * (C + D)

![image-20220202141837176](images/image-20220202141837176.png)

# Addressing Modes
- The addressing mode specifies a rule for interpreting or modifying the address field of the instruction before the operand is actually referenced.
- Computers use addressing mode techniques for the purpose of accommodating one or both of the following provisions:

- To give programming versatility to the user by providing such facilities as pointers to memory, counters for loop control, indexing of data, and program relocation.
  -  To reduce the number of bits in the addressing field of the instruction.
- There are basic 10 addressing modes supported by the computer.
    - Implied Mode
    - Immediate Mode
    - Register Mode
    - Register Indirect Mode
    - Autoincrement or Autodecrement Mode
    - Direct Address Mode
    - Indirect Address Mode
    - Relative Address Mode
    - Indexed Addressing Mode
    - Base Register Addressing Mode


## Implied Mode
-  Operands are specified implicitly in the definition of the instruction. 
-  For example, the instruction “complement accumulator (CMA)” is an implied-mode instruction because the operand in the accumulator register is implied in the definition of the instruction.
-  In fact, all register reference instructions that use an accumulator and zero address instructions are implied mode instructions.
## Immediate Mode
-  Operand is specified in the instruction itself. 
-  In other words, an immediate-mode instruction has an operand field rather than an address field.
-  The operand field contains the actual operand to be used in conjunction with the operation specified in the instruction.
-  Immediate mode of instructions is useful for initializing register to constant value.
-  E.g. MOV R1, 05H
   -  Instruction copies immediate number 05H to R1 register.
## Register Mode
-  Operands are in registers that reside within the CPU.
-  The particular register is selected from a register field in the instruction. 
-  E.g. MOV AX, BX
   -  Move value from BX to AX register
## Register Indirect Mode
-  In this mode the instruction specifies a register in the CPU whose contents give the address of the operand in memory.
-  Before using a register indirect mode instruction, the programmer must ensure that the memory address of the operand is placed in the processor register with a previous instruction.
-  E.g. MOV [R1], R2
   -  Value of R2 is moved to the memory location specified in R1.
## Auto increment or Auto decrement Mode
-  This is similar to the register indirect mode expect that the register is incremented or decremented after (or before) its value is used to access memory.
-  When the address stored in the register refers to a table of data in memory, it is necessary to increment or decrement the register after every access to the table. This can be achieved by using the increment or decrement instruction.
-  Effective address of the operand is the contents of a register specified in the instruction. After accessing the operand, the contents of this register are automatically incremented to point to the next consecutive memory location.
-  E.g. Add R1, (R2)+
## Direct Address Mode
-  Also known as absolute addressing mode.
-  In this mode the effective address is equal to the address part of the instruction.
-  The operand resides in memory and its address is given directly by the address field of the instruction.
> **E.g. ADD 457**

> **Value located at memory location 457 is added to AC**

## Indirect Address Mode
-  In this mode the address field of the instruction gives the address where the effective address is stored in memory.
-  Control fetches the instruction from memory and uses its address part to access memory again to read the effective address.
-  Based on the availability of Effective address, Indirect mode is of two kind:
-  Register Indirect: In this mode effective address is in the register, and corresponding register will be maintained in the address field of an instruction. 
-  Memory Indirect: In this mode effective address is in the memory, and corresponding memory address will be maintained in the address field of an instruction.
## Relative Address Mode
- In this mode the content of the program counter is added to the address part of the instruction in order to obtain the effective address.

- The address part of the instruction is usually a signed number which can be either positive or negative.

> **Effective address = address part of instruction + content of PC**

## Indexed Addressing Mode
- In this mode the content of an index register is added to the address part of the instruction to obtain the effective address.

- The indexed register is a special CPU register that contain an index value.

- The address field of the instruction defines the beginning address of a data array in memory.

- Each operand in the array is stored in memory relative to the begging address.

> **Effective address = address part of instruction + content of index register**
## Base Register Addressing Mode
-  In this mode the content of a base register is added to the address part of the instruction to obtain the effective address.
-  A base register is assumed to hold a base address and the address field of the instruction gives a displacement relative to this base address.

> **Effective address = address part of instruction + content of base register**

# RISC & CISC

**Reduced Instruction Set Architecture (RISC)**

- The main idea behind this is to make hardware simpler by using an instruction set composed of a few basic steps for loading, evaluating, and storing operations just like a load command will load data, a store command will store the data. 

**Complex Instruction Set Architecture (CISC)**

- The main idea is that a single instruction will do all loading, evaluating, and storing operations just like a multiplication command will do stuff like loading data, evaluating, and storing it, hence it’s complex. 



# RISC & CISC Characteristics

| RISC                                                    | CISC                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Simpler instruction, hence simple instruction decoding. | Complex instruction, hence complex instruction decoding.     |
| Instruction comes undersize of one word.                | Instructions are larger than one-word size.                  |
| Instruction takes a single clock cycle to get executed. | Instruction may take more than a single clock cycle to get executed. |
| More general-purpose registers.                         | Less number of general-purpose registers as operations get performed in memory itself. |
| Simple Addressing Modes.                                | Complex Addressing Modes.                                    |
| A pipeline can be achieved.                             |                                                              |

# RISC v/s CISC

| RISC                                                        | CISC                                               |
| ----------------------------------------------------------- | -------------------------------------------------- |
| Fixed sized instructions                                    | Variable sized instructions                        |
| Can perform only Register to Register Arithmetic operations | Can perform REG to REG or REG to MEM or MEM to MEM |
| Requires more number of registers                           | Requires less number of registers                  |
| Code size is large                                          | Code size is small                                 |
| An instruction executed in a single clock cycle             | Instruction takes more than one clock cycle        |