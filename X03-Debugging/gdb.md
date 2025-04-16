* Use `ctrl+x 1` or `ctrl+x a` to enter tui mode
* Use `ctrl+x 2` repeatedly to get different windows. (assembly, assembly + C source code, assembly + C + registers)


  (gdb) `break main`
  (gdb) `run  6`              # run with the command line argument 6
  (gdb) show disassembly-flavor  # either "att" or intel 
  (gdb) set disassembly-flavor intel   # to set the disassembly flavor explicitly (intel in this case)
  (gdb) `disass main`         # disassemble the main function
  (gdb) `break sum`           # set a break point at the beginning of a function
  (gdb) `cont`               # continue execution of the program
  (gdb) `break *0x0804851a`   # set a break point at memory address 0x0804851a
  (gdb) `ni`                  # execute the next instruction
  (gdb) `si`                  # step into a function call (step instruction)
  (gdb) `info registers`      # list the register contents
  (gdb) `p $eax`              # print the value stored in register %eax
  (gdb) `p  *(int *)($ebp+8)` # print out value of an int at addr (%ebp+8)
  (gdb) `x/wd $ebp+8`         # examine the contents of memory at the given address
                            # as an int (w: word-size value d: in decimal) 
                            # display type in x is sticky: subsequent x commands
                            # will display values in decimal until another type is
                            # specified (ex. x/a $ebp+8  # as an address in hex)
  (gdb) `x/s 0x0800004`       # examine contents of memory at address as a string
  (gdb) `x/s $rdi`	    # examine contents of address in register as a string
  (gdb) `x/wd 0xff5634`       # after x/s, the unit size is 1 byte, so if want
                            # to examine as an int specify both the width w and d 
                            
                            
##### Examining register and memory contents
-------------------------------------------
Using a combination of breakpoints and single-stepping, you should be able to trace through the sections of your code that you suspect to be buggy. This allows you to look at the contents of the registers and memory when the execution of the program has halted. The command:
```
info registers
```
  
  
prints out the contents of every register, including all the segment registers. This is often too much information. The "print" command is much more useful. For example, the commands:
```
   print/d $ecx
   print/x $ecx
   print/t $ecx
```   
print out the contents of the ECX register in decimal, hexadecimal, and binary, respectively.

Memory contents can be examined using the "x" command. The "x" command is optionally followed by a "/", a count field, a format field, a size field and finally a memory address. The count field is a number in decimal. The format field is a single letter with 'd' for decimal, 'x' for hexadecimal, 't' for binary and 'c' for ASCII. The size field is also a single letter with 'b' for byte, 'h' for 16-bit word (half word) and 'w' for a 32-bit word. For example, if your program has a label "msg", the following commands:

```
  x/12cb &msg
  x/12db &msg
  x/12xh &msg
  x/12xw &msg
```  
will print out respectively the contents of memory starting at msg in the following manner: the next 12 bytes as ASCII characters, the next 12 bytes as decimal numbers, the next 12 16-bit words in hex, and the next 12 32-bit words in hex.
Sometimes, as you are tracing your program, you are really interested in the contents of a specific register. If you issue the command:
```
display $eax
```
   
   
then the contents of the EAX register will be printed to the screen every time the program is halted. This saves a lot of typing. You may issue more than one display command and you can use format codes like "/x" to output the values in hex. The gdb command "info display" will list all the active displays. Use "undisplay" to remove an item on this list.
A very good use of the display command is to have the next instruction of the program printed whenever the program is halted:

```
display/i $eip                            
```
  
