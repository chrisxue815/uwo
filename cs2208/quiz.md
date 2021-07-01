## 3.1
Why is the program counter a pointer and not a counter?

<details>
<summary>Answer</summary>
TODO
</details>

## 3.2
Explain the function of the following registers in a CPU.
1. PC
1. MAR
1. MBR
1. IR

<details>
<summary>Answer</summary>

1. PC: The program counter contains the address of the next instruction to be executed.
1. MAR: The memory address register stores the address of the location in main memory that is currently being accessed by a read or write operation.
1. MBR: The memory buffer register stores data that has just been read from main memory or data to be immediately written to main memory.
1. IR: The instruction register stores the instruction most recently read from main memory. This is the instruction currently being executed.

</details>

## 3.3
For each of the following 6-bit operations, calculate the values of the C, Z, V, and N flags.

```
a.  001011   b.  111111   c.  000000
   +001101      +000001      -111111
   -------      -------      -------

d.  101101   e.  000000   f.  111110
   +011011      -000001      +111111
   -------      -------      -------
```

<details>
<summary>Answer</summary>

```
a.  001011   b.  111111   c.  000000
   +001101      +000001      -111111
   -------      -------      -------
    011000      1000000       000001
  Z=0, N=0     Z=1, N=0     Z=0, N=0
  C=0, V=0     C=1, V=0     C=0, V=0

d.  101101   e.  000000   f.  111110
   +011011      -000001      +111111
   -------      -------      -------
   1001000       111111      1111101
  Z=0, N=0     Z=0, N=1     Z=0, N=1
  C=1, V=0     C=0, V=0     C=1, V=0
```

* Z=1 if all bits are zero
* N=1 if the highest bit of the result is one
* C=1 if an extra bit is generated
* V=1 if the highest bits of the operands are the same and they are different from the highest bit of the result (not including the carry bit)

Code (in 32-bit):
```
		MOV r0, #2_001011
		ADDS r0, #2_001101

		MOV r0, #2_111111
		ADDS r0, #2_000001

		MOV r0, #2_000000
		SUBS r0, #2_111111

		MOV r0, #2_101101
		ADDS r0, #2_011011

		MOV r0, #2_000000
		SUBS r0, #2_000001

		MOV r0, #2_111110
		ADDS r0, #2_111111
```

</details>

## 3.4
The classic processors flags are C, N, V, and Z. Conditional branches may be made on these flags being true or false (branch on zero or not zero). Branches may be on combinations of flags (branch on greater than or equal to zero). Can you think of any other conditional branch conditions that could be included?

<details>
<summary>Answer</summary>
TODO
</details>

## 3.5
The ARM's r13 and r14 registers are overlapped (banked or windowed), and a separate register pair exists for each of the exception modes. What do we mean when we say these registers are overlapped? Explain why the ARM's designers have taken this approach.

<details>
<summary>Answer</summary>
TODO
</details>

## 3.6
ARM's literature often describes its assembly language instruction syntax in BNF notation. Suppose an instruction is described in BNF as having the syntax:
```
This|That{B}{S}{,P|Q}
```
Give examples of possible legal instructions using this format.

<details>
<summary>Answer</summary>
TODO
</details>

## 3.7
The ARM puts the program counter in register r15, making it visible to the programmer. Someone writing about the ARM stated that this exposed the ARM's pipeline. What did he mean, and why? Note: You may have to look at the section on pipelining to answer this.

<details>
<summary>Answer</summary>
TODO
</details>

## 3.8
What are the relative advantages and disadvantages of general-purpose registers compared separate address and data registers?

<details>
<summary>Answer</summary>
TODO
</details>

## 3.9
Why is a misaligned operand? Why are misaligned operands such a problem in programming?

<details>
<summary>Answer</summary>
TODO
</details>

## 3.10
Why does the ARM provide a reverse subtract instruction `RSB r0, r1, r2` that implements `[r0] = [r2] - [r1]` when the normal subtraction instruction `SUB r0, r2, r1` will do exactly the same job?

<details>
<summary>Answer</summary>
TODO
</details>

## 3.11
If

```
r1 = 11110000111000101010000011111101
r2 = 00000000111111110000111100001111
```

what is the value of r2 after executing `BIC r3, r1, r2`?

<details>
<summary>Answer</summary>

```
r1 = 11110000111000101010000011111101
r2 = 00000000111111110000111100001111
r3 = 11110000000000001010000011110000
```

Code:
```
		LDR r0, =2_11110000111000101010000011111101
		LDR r1, =2_00000000111111110000111100001111
		BIC r0, r1
```

</details>

## 3.12
If r1 = 0FFF<sub>16</sub> and r2 = 4, what is the value of r3 after each of the following instructions has been executed (assume that each instruction uses the same data)?

1. `MOV r3, r1, LSL r2`
1. `MOV r3, r1, LSR r2`
1. `MVN r3, r1, LSL r2`
1. `MVN r3, r1, LSR r2`

<details>
<summary>Answer</summary>

1. FFF0<sub>16</sub>
1. 00FF<sub>16</sub>
1. 000F<sub>16</sub> or FFFF000F<sub>16</sub>
1. FF00<sub>16</sub> or FFFFFF00<sub>16</sub>

Code:
```
		LDR r1, =0x0FFF
		MOV r2, #4
		MOV r3, r1, LSL r2

		LDR r1, =0x0FFF
		MOV r2, #4
		MOV r3, r1, LSR r2

		LDR r1, =0x0FFF
		MOV r2, #4
		MVN r3, r1, LSL r2

		LDR r1, =0x0FFF
		MOV r2, #4
		MVN r3, r1, LSR r2
```

</details>

## 3.13
If r1 = 00FF<sub>16</sub> and r2 = 4, what is the value of r0 after each of the following instructions has been executed (assume that each instruction uses the same data)?

1. `ADD r0, r1, r1, LSL #2`
1. `ADD r0, r1, r1, LSL #4`
1. `ADD r0, r1, r1, ROR #4`

<details>
<summary>Answer</summary>

1. 04FB<sub>16</sub>
1. 10EF<sub>16</sub>
1. F000010E<sub>16</sub>

</details>

## 3.14
What is the effect of the instruction `MOV r0, r0, ASR #31`?

<details>
<summary>Answer</summary>

If r0 is non-negative, set it to 0.

If r0 is negative, set it to -1.

</details>

## 3.15
Write an ARM assembly language routine to count the number of 1s in a 32-bit word in r0 and return the result in r1.

<details>
<summary>Answer</summary>



</details>
