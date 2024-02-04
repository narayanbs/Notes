**Debugging assembly using gdb**

We have a simple nasm program that prints a message 

```
; hello world asm

global _start

section .data
msg:  db 'Hello World!', 0Ah

section .text
_start:
  mov rax, 1
  mov rdi, 1
  mov rsi, msg
  mov rdx, 13
  syscall

  mov rax, 60
  mov rdi, 0
  syscall
```
Let's debug this using gdb

```
$ gdb lesson01
GNU gdb (Ubuntu 13.1-2ubuntu2) 13.1
Copyright (C) 2023 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from lesson01...
(No debugging symbols found in lesson01)
(gdb) break _start
Breakpoint 1 at 0x401000

(gdb) run
Starting program: /home/phoenix/Programs/testbed/lesson01

This GDB supports auto-downloading debuginfo from the following URLs:
  <https://debuginfod.ubuntu.com>
Enable debuginfod for this session? (y or [n]) n
Debuginfod has been disabled.
To make this setting permanent, add 'set debuginfod enabled off' to .gdbinit.

Breakpoint 1, 0x0000000000401000 in _start ()
(gdb) disass _start
Dump of assembler code for function _start:
=> 0x0000000000401000 <+0>:	mov    $0x1,%eax
   0x0000000000401005 <+5>:	mov    $0x1,%edi
   0x000000000040100a <+10>:	movabs $0x402000,%rsi
   0x0000000000401014 <+20>:	mov    $0xd,%edx
   0x0000000000401019 <+25>:	syscall
   0x000000000040101b <+27>:	mov    $0x3c,%eax
   0x0000000000401020 <+32>:	mov    $0x0,%edi
   0x0000000000401025 <+37>:	syscall
End of assembler dump.
(gdb) show disassembly-flavor
The disassembly flavor is "att".
(gdb) set disassembly-flavor intel
(gdb) disass _start
Dump of assembler code for function _start:
=> 0x0000000000401000 <+0>:	mov    eax,0x1
   0x0000000000401005 <+5>:	mov    edi,0x1
   0x000000000040100a <+10>:	movabs rsi,0x402000
   0x0000000000401014 <+20>:	mov    edx,0xd
   0x0000000000401019 <+25>:	syscall
   0x000000000040101b <+27>:	mov    eax,0x3c
   0x0000000000401020 <+32>:	mov    edi,0x0
   0x0000000000401025 <+37>:	syscall
End of assembler dump.
(gdb) x/s 0x402000
0x402000:	"Hello World!\n"
(gdb) Quit
(gdb)
```
