
#####  SSE vs AVX Instructions

SSE --> SIMD standard extensions
AVX --> Advanced vector extensions

AVX can be used to process 256 bits per instruction, whereas SSE processes 128 bits. AVX instructions can be used with YMM registers as well as XMM, where SSE only processes using XMM.

AVX instructions have an extra destination operand encoded with a new VEX prefix, so they can be non-destructive, unlike SSE which generally overwrites one of the input operands:

SSE: A = A + B ← One of the inputs is overwritten in SSE!

AVX: C = A + B ← Result can be written to a new operand in AVX

AVX introduced several new instructions, included the long-overdue broadcast instructions, which copy a value to all elements of a vector.

AVX relaxed the data alignment restrictions of SSE, so we no longer need to ensure our data is aligned to 16 bytes in order to use memory operands.

AVX is newer, so SSE instruction sets are available on more hardware. Although nowadays, almost all x86/64 CPU’s in use are capable of both SSE and AVX instruction sets, with the exception of AVX512, which is a completely different kettle of fish.

AVX512 is an extension to AVX. It is by far the largest extension ever added to the x86/64 instruction set. It introduces many new mechanisms and increases the processing from 256 to 512 bit vectors. At the moment AVX512 is Intel exclusive, and supposed to be available from AMD in their upcoming Zen 4 architecture later this year. Though I think AMD will only implement a small sub-set of the complete AVX512 instruction sets.

##### X64 linux ABI
- x64 linux abi -- specifies the following registers to be saved/restored
`RAX, RCX, RDX, R8, R9, R10, R11` --> caller saved registers -- save before calling a function and restore after return
`RBX, RBP, R12, R13, R14, R15` --> calleee saved registers  -- the called function must save before modifying it and restoring while exiting 
- In x64 stack should be aligned to 16-bytes before making a function call.  see `Repos/ex03.asm` for more details
- if global main is used, the main return address will already be on the stack, so before making a call, another 8-bytes need to be  subtracted.  if global `_start` is used, then there is no return address on the stack, stack is already aligned before making a call. 

##### GNU inline assembly 
---------------------
The format of basic inline assembly is very much straight forward. Its basic form is 
	`asm("assembly code");`

Example:

`asm("movl %ecx %eax"); /* moves the contents of ecx to eax */`
`__asm__("movb %bh (%eax)"); /*moves the byte from bh to the memory pointed by eax */`

we can use asm or `__asm__` (if asm conflicts with something in our program).

If we have more than one instructions, we write one per line in double quotes, and also suffix a ’\n’ and ’\t’ to the instruction. This is because gcc sends each instruction as a string to as(GAS) and by using the newline/tab we send correctly formatted lines to the assembler.

```
_asm__ ("movl %eax, %ebx\n\t"
          "movl $56, %esi\n\t"
          "movl %ecx, $label(%edx,%ebx,$4)\n\t"
          "movb %ah, (%ebx)");
```

##### Extended Assembly
---
asm(assembly template : output operands : input operands : clobbered registers list);

The assembler template consists of assembly instructions. Each operand is described by an operand-constraint string followed by the C expression in parentheses. A colon separates the assembler template from the first output operand and another separates the last output operand from the first input, if any. Commas separate the operands within each group. The total number of operands is limited to ten or to the maximum number of operands in any instruction pattern in the machine description, whichever is greater.

If there are no output operands but there are input operands, you must place two consecutive colons surrounding the place where the output operands would go.

Example:
```bash
        asm ("cld\n\t"
             "rep\n\t"
             "stosl"
             : /* no output registers */
             : "c" (count), "a" (fill_value), "D" (dest)
             : "%ecx", "%edi" 
             );
```


Now, what does this code do? The above inline fills the fill_value count times to the location pointed to by the register edi. It also says to gcc that, the contents of registers eax and edi are no longer valid. Let us see one more example to make things more clearer.
```bash
       
        int a=10, b;
        asm ("movl %1, %%eax; 
              movl %%eax, %0;"
             :"=r"(b)        /* output */
             :"r"(a)         /* input */
             :"%eax"         /* clobbered register */
             );       
```

Here what we did is we made the value of ’b’ equal to that of ’a’ using assembly instructions. Some points of interest are:

"b" is the output operand, referred to by %0 and "a" is the input operand, referred to by %1.
"r" is a constraint on the operands. We’ll see constraints in detail later. For the time being, "r" says to GCC to use any register for storing the operands. output operand constraint should have a constraint modifier "=". And this modifier says that it is the output operand and is write-only.
There are two %’s prefixed to the register name. This helps GCC to distinguish between the operands and registers. operands have a single % as prefix.
The clobbered register %eax after the third colon tells GCC that the value of %eax is to be modified inside "asm", so GCC won’t use this register to store any other value.
When the execution of "asm" is complete, "b" will reflect the updated value, as it is specified as an output operand. In other words, the change made to "b" inside "asm" is supposed to be reflected outside the "asm".


##### Compilation
---
- for asm files with no c functions and with global `_start`
`nasm -f elf64 ex06.asm && ld ex06.o -o ex06`

- for asm files with c functions and with global main
`nasm -f elf64 ex06.asm && gcc -no-pie ex06.o -o ex06`

- for asm files with c functions and  _start instead of main
`nasm -f elf64 ex06.asm && gcc -nostartfiles -no-pie ex06.o -o ex06`

You'd use `-nostartfiles` when you are building the start files themselves i. e `global _start_`.  command line arguments will not be passed to `main()` and environment variables will not be available to the executable, among other things

