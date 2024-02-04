##### readelf  -- display information about elf files
ex: 
`readelf -h ./powerex` --> displays the header information of the elf file (exe or lib)
`readelf -r ./libmls.so` --> displays the relocation entries of the elf file
`readelf --segments ./libmls.so` --> displays the segments  of an elf 

##### objdump -- display information from object files
ex:
`objdump -d -Mintel libmls.so` --> disassembly using intel flavor

##### nm -- list symbols from object files
ex:
`nm ./libmls.so`