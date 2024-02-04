The correct terms are memory mapped _files_ and anonymous mappings. When referring to memory mapping, one is usually referring to mmap(2). There are 2 categories for using mmap. One category is SHARED vs PRIVATE mappings. The other category is FILE vs ANONYMOUS mappings. Mixed together you get the 4 following combinations:

1. PRIVATE FILE MAPPING
2. SHARED FILE MAPPING
3. PRIVATE ANONYMOUS MAPPING
4. SHARED ANONYMOUS MAPPING

A File Mapping specifies a file, on disk, that will have N many bytes mapped into memory. The function mmap(2) takes, as its 4th argument a file descriptor to the file to be mapped into memory. The 5th argument is the number of bytes to be read in, as an offset. The typical process of using mmap to create a memory mapped file goes

1. open(2) file to get a file descriptor.
2. fstat(2) the file to get the size from the file descriptor data structure.
3. mmap(2) the file using the file descriptor returned from open(2).
4. close(2) the file descriptor.
5. do whatever to the memory mapped file.

When a file is mapped in as PRIVATE, changes made are not committed to the underlying file. It is a PRIVATE, in-memory copy of the file. When a file is mapped SHARED, changes made are committed to the underlying file by the kernel automatically. Files mapped in as shared can be used for what is called Memory Mapped I/O, and IPC. You would use a memory mapped file for IPC instead of a shared memory segment if you need the persistence of the file

If you use strace(1) to watch a process initialize, you will notice that the different sections of the file are mapped in using mmap(2) as private file mappings. The same is true for system libs.

Examples of output from strace(1) where mmap(2) is being used to map in libraries to the process.
```
open("/etc/ld.so.cache", O_RDONLY)      = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=42238, ...}) = 0
mmap(NULL, 42238, PROT_READ, MAP_PRIVATE, 3, 0) = 0x7ff7ca71e000
close(3)                                = 0
open("/lib64/libc.so.6", O_RDONLY)      = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0p\356\341n8\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0755, st_size=1926760, ...}) = 0
mmap(0x386ee00000, 3750152, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x386ee00000
```

Anonymous mappings are not backed by a file. To be specific, the 4th (file descriptor) and 5th (offset) argument of mmap(2) are not even used when the MAP_ANONYMOUS flag is used as the 3rd argument to mmap(2). An alternative to using the MAP_ANONYMOUS flag is to use /dev/zero as the file.

The word 'Anonymous' is, to me, a poor choice in that it sounds as if the file is mapped anonymously. Instead, it is the file that is anonymous, ie. there isn't a file specified.

The most common use of anonymous private mappings is the heap and stack segments of a process. You could use a shared anonymous mapping so that applications could share a region of memory, but I do not know the reason why you wouldn't use SYSV or POSIX shared memory instead.

Since memory mapped in using Anonymous mappings is guaranteed to be zero filled, it could be useful for some applications that expect/require zero filled regions of memory to use mmap(2) in this way instead of the malloc(2) + memset(2) combo.