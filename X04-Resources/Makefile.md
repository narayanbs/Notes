A make file will have the following format. 
```sh
target: dependencies
command
command
command
```
Let's create a simple target with no dependencies or commands
```
hello:
```
By default make will look for a `hello.c` file and compile it to a `hello` executable
```sh
$ make
$ cc hello.c -o hello
```
This is because make was developed for building C projects. So by default it has implicit 
rules 
* \*.o is automatically made from \*.c files with the command `$(CC) -c $(CPPFLAGS) 
$(CFLAGS) $^ -o $@`

Let's consider another example
```sh
blah: blah.o 
	cc blah.o -o blah # Runs third 
blah.o: blah.c 
	cc -c blah.c -o blah.o # Runs second # 

#Typically blah.c would already exist, but I want to limit any additional required files 
blah.c: 
	echo "int main() { return 0; }" > blah.c # Runs first
```
A target is run only if it doesn't exist or any dependency is newer than it. 
In the example above, `blah` will be invoked only if `blah.o` is newer than `blah`. 
Likewise `blah.o` is invoked if `blah.c` is 
newer that it. 

if we prefix `.PHONY` to a target, then it will prevent make from looking for a file with 
the name of the target.
for ex:
``` sh
.PHONY: clean
clean: 
	rm -f *.c
```

Now if we create a file called clean, it doesn't prevent make from executing the target