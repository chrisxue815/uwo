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

1. `MOV r3, r1, LSL r2` = FFF0<sub>16</sub>
1. `MOV r3, r1, LSR r2` = 00FF<sub>16</sub>
1. `MVN r3, r1, LSL r2` = 000F<sub>16</sub> or FFFF000F<sub>16</sub>
1. `MVN r3, r1, LSR r2` = FF00<sub>16</sub> or FFFFFF00<sub>16</sub>

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

1. `ADD r0, r1, r1, LSL #2` = 04FB<sub>16</sub>
1. `ADD r0, r1, r1, LSL #4` = 10EF<sub>16</sub>
1. `ADD r0, r1, r1, ROR #4` = F000010E<sub>16</sub>

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

TODO: routine

Python:
```
r1 = 0
while True:
	r2 = r0 & 1
	r1 += r2
	r0 = (r0 >> 1) & 0xFFFFFFFF
	if r0 == 0:
		break
```

ARM assembly:
```
		MOV r1, #0
Loop	AND r2, r0, #1
		ADD r1, r2
		MOVS r0, r0, LSR #1
		BNE Loop
```

</details>

## 3.16
A word consists of the bytes b4, b3, b2, and b1. Write a function to re-order (transpose) these bytes in the order b1, b3, b2, and b4.

<details>
<summary>Answer</summary>

Python:
```
r0 = 0x12345678
r1 = (r0 << 24) & 0xFFFFFFFF
r1 |= (r0 >> 24) & 0xFFFFFFFF
r0 &= 0x00FFFF00
r0 |= r1
```

ARM assembly:
```
		LDR r0, =0x12345678
		MOV r1, r0, LSL #24
		ORR r1, r0, LSR #24
		BIC r0, #0x000000FF
		BIC r0, #0xFF000000
		ORR r0, r1
```

</details>

## 3.17
ARM instructions have a 12-bit literal. Instead of permitting a word in the range 0 to 2<sup>12</sup> - 1, the ARM uses an 8-bit format for the integer and a 4-bit alignment field that allows the integer to be shifted in steps of 2. What are the advantages and disadvantages of this mechanism in comparison with a straight 12-bit integer?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.18
Write one or more ARM instructions that will clear bits 20 to 25 inclusive in register r0. All the other bits of r0 should remain unchanged.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.19
This is a classic problem of assembly language programming. Write a sequence of ARM instructions that swap the contents of registers r0 and r1 without using any additional registers or memory storage (that is, you can't move r1 to a temporary location).

<details>
<summary>Answer</summary>

TODO

</details>

## 3.20
What is the difference between the TEQ and CMP and CMN comparison instructions?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.21
What are the advantages and disadvantages of the use of the ARM's BL (branch and load) subroutine call mechanism in comparison with the conventional CISC BSR (branch to subroutine) mechanism?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.22
Write ARM code to implement the following C operation.

```C
int s = 0;
for (i = 0; i < 10; i++) {
	s = s + i * i;
}
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.23
What is the effect of the following addressing mode?

```
STR r0, [r2, r3, ROR #3]!
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.24
What is the meaning of each of the P, U, B, W, and L bits in the encoding of an ARM memory reference instruction?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.25
What is the binary encoding of the following instructions?
1. `STRB r1, [r2]`
1. `LDR r3, [r4, r5]!`
1. `LDR r3, [r4], r5`
1. `LDR r3, [r4, #-6]!`

<details>
<summary>Answer</summary>

TODO

</details>

## 3.26
What is the effect of `LDR r0, [r5, r6, LSL r2]`?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.27
You go for a job as a computer architecture designer. At your interview, you tell the panel that you have some real neat ideas for some cool processors. For example, you have an instruction that can set an individual bit in memory. The format of your instruction is

```
BITSET r0, r1, [(r2), r3, r4 LSR r5, #n]
```

This instruction sets a bit in memory located r0 plus r1 bits from the word address whose address is given by the contents of memory location r2, plus the contents of register r3, plus the contents of register r4, and shifted left by register r5 plus the constant n.

You don't get the job. Why?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.28
What effective address is generated by the instruction `LDR r0, [r2, -r3, LSL #1]`?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.29
Some machines have a find-first-one instruction that counts the location of the first bit set to 1 within the word. Write an ARM sequence of instructions that takes the word in r0 and puts the locations of the first bit set to 1 in r1. Count from the left, so that if bit 31 is set, the value returned should be 0. If bit 0 is set, the value returned is 31. If no bit is set, the value returned should be 32.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.30
What is the meaning of sign-extension in the context of copying data from one location to another?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.31
Why is sign-extension an important issue when we use a LDR instruction to load a register from memory but of no importance when we use an STR to store a register in memory?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.32
Assume that r2 contains the initial value 00001000<sub>16</sub>. Explain the effect of each of the following six instructions, and give the value in r2 after each instruction executes.
1. `STR r1, [r2]`
1. `STR r1, [r2, #8]`
1. `STR r1, [r2, #8]!`
1. `STR r1, [r2] #8`
1. `STR r1, [r2, r0, LSL #8]`
1. `STMFD r2!, {r1, r2}`

<details>
<summary>Answer</summary>

TODO

</details>

## 3.33
Most RISC processors do not include a block move instruction. What are the advantages and disadvantages of the ARM's LDM and STM instructions?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.34
What is the effect of executing `STMIB r13!, {r0 - r2, r4}`? Draw a picture of the state of the stack pointed at by r13 before and after this operation.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.35
The two pairs of instructions LDMIA, STMDB and (LDMFD, STMFD)do exactly the same things. Why do these two pairs have different or alternative mnemonics? Why does the first pair have different suffixes IA and DB? Why does the second pair have the same suffix FD?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.36
Without using the ARM's multiplication instruction, write one or more instructions (using ADD,SUB, and shifting) to multiply by the following integers.
1. 33
1. 1025
1. 4095

<details>
<summary>Answer</summary>

TODO

</details>

## 3.37
A word consists of the bytes b4, b3, b2, and b1. Write a function to invert the bits of b3 and clear the bits of b2, leaving all other bits unchanged.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.38
Write suitable ARM code to implement

```
if x = y call PQR else call ZXY
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.39
Write an ARM assembly language program that scans a string terminated by the null byte 0x00 and copies the string from a source location pointed at by r0 to a destination pointed at by r1.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.40
Write a program to copy text from the location pointed at by r0 to the location pointed at by r1. The copied version must be in reverse order. Assume the string you are copying is non-null (it contains at least one character) and that it is terminated.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.41
Write a program to reverse a character string with an odd number of characters pointed at by r0. Assume the string you are copying is non-null (it contains at least one character) and that it is terminated by 0x0D (the number of characters included the terminator). You must not use an additional memory buffer (i.e., you can use only registers and the string storage itself).

<details>
<summary>Answer</summary>

TODO

</details>

## 3.42
Repeat Problem 3.39, but when you transfer the string, remove any occurrences of the word “the.” For example, “and the man said” would become “and man said.”

<details>
<summary>Answer</summary>

TODO

</details>

## 3.43
Repeat Problem 3.39, but when you transfer the string, reverse the sequence of any words beginning with “t.” For example, “and the man said” would become “and eht man said.”

<details>
<summary>Answer</summary>

TODO

</details>

## 3.44
What does the following code do?

```
TEQ r0, #0
RSBMI r0, r0, #0
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.45
What is the meaning of the following mnemonics (and what do they do)?
1. `LDRSH`
1. `RSBLES`
1. `CMPS`
1. `MRS r0,CPSR`

<details>
<summary>Answer</summary>

TODO

</details>

## 3.46
What is the meaning of sign-extension in the context of copying data from one location to another?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.47
What is wrong with the following instruction?

```
MLA r0, r0, r1, r2
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.48
What, in the contest of assembly language, is a pseudo-operation?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.49
Explain the meaning of the following two ARM pseudo-operations. What do they do and why have they been implemented?
1. `ADR r0, table`
1. `LDR = r0, 0x1234FEDC`

<details>
<summary>Answer</summary>

TODO

</details>

## 3.50
Suppose you execute `LDR, r0=0x12345678` on an ARM machine followed by `STR r0, [r1]` where `r1 = 0x1000`. Now, suppose you do a byte read to the same address with `LDRB r2, [r1]`. What would the value be in r2 if (a) the ARM was big-endian configured and (b) it was little-endian configured?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.51
Write an ARM assembly language program to determine whether a string of characters with an odd length is a palindrome (for example, mom) under the following constraints.
1. The string of ASIC-encoded characters is stored in memory.
1. At the start of the program, register r1 contains the address of the first character in the string, and r2 contains the address of the last character. On exit from the program, register r 0 contains a 0 if the string is not a palindrome, and 1 if it is.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.52
How would you deal with the previous problem if the palindrome could have an odd or even length?

<details>
<summary>Answer</summary>

TODO

</details>

## 3.53
A singly linked list (Figure P3.53), whose first element is pointed at by r0, consists of elements whose head is a 32-bit address pointing to the next element in the list and a variable-length tail. The tail may be of any length greater than four bytes. The last element in the list points to the null address 0. Write a program to search the list for an element whose tail begins with the word in data register r1. On success, set r4 to 0xFF, and r0 should contain the address of the desired record. On failure, load r1 with 0xFFFFFFFF.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.54
Explain what this fragment of code does instruction by instruction and what purpose it achieves (assuming that register r0 is the register of interest). Note that the data in r0 must not be 0 on entry.

```
		MOV r1, #0
loop	MOVS r0, r0, LSL #1
		ADDCC r1, r1, #l
		BCC loop
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.55
Consider the following Java constructs. Express each in ARM assembly language. Assume all variables are single-bit Booleans and are in registers r0 = A, r1 = B, r2 = C, and r3 = D. Note: The Java
operators &, |, ! are AND, OR, and NOT, respectively. The operators && and || are AND and OR operators that support short-circuit evaluation (that is, if the expression yields false AND or true OR further evaluation is halted).

1. `A = (B & C) | (!D);`
2. `A = (B && C) || (!D);`

<details>
<summary>Answer</summary>

TODO

</details>

## 3.56
The following is a loop expressed in ARM code. The code is wrong. Why?

```
		MOV r0, #10     ;Loop counter- ten times round the loop
Next	ADD r1, r1, r0  ;add loop counter to total
		SUB r0, r0, #1  ;decrement loop counter
		BEQ Next        ;continue until all done
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.57
We need to swap the following registers. Do this using block moves.

```
Before After
r1     r3
r2     r4
r3     r5
r4     r6
r5     r7
r6     r1
r7     r2
```

<details>
<summary>Answer</summary>

TODO

</details>

## 3.58
Why is the assembly language structure (format) of ARM's block move instructions inconsistent with ARM's normal assembler conventions? If you were redesigning ARM's assembly language, how might you express these operations (remember, changing the assembly language does not change the architecture — it affects only programmer productivity and accuracy).

<details>
<summary>Answer</summary>

TODO

</details>

## 3.59
Write a function (subroutine) that inputs a data value in register r0 and returns value in r0. The function returns $y = a + bx + cx^2$, where a, b, and c are parameters built into the function (i.e., they are not passed to it). The subroutine also performs clipping. If the output is greater than a value d, it is constrained to d (clipped). The input in r0 is a positive binary value in the range 0 to 0xFF. Apart from r0, no other registers may be modified by this subroutine.

<details>
<summary>Answer</summary>

TODO

</details>

## 3.60
A computer has three eight-element vectors in memory, Va, Vb, and Vc. Each element of a vector is a 32-bit word. Write the code to calculate all elements of Vc if the ith element is given by

$$
Vc_i = ½ (Va_i + Vb_i)
$$

<details>
<summary>Answer</summary>

TODO

</details>

## 3.61
Register r15 is the program counter. You can use it with certain instructions such as a MOV (e.g., `MOV pc, r14`). However, r15 cannot be used in conjunction with most data processing instructions. Why?

<details>
<summary>Answer</summary>

TODO

</details>
