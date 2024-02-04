
##### Debugging network using strace and netstat

**netstat for simplicity**

Using netstat and grepping on the PID or process name:
```
$ netstat -np --inet | grep "thunderbird"

tcp        0      0 192.168.134.142:45348   192.168.138.30:143      ESTABLISHED 16875/thunderbird
tcp        0      0 192.168.134.142:58470   192.168.138.30:443      ESTABLISHED 16875/thunderbird

```

And you could use watch for dynamic updates:
```
watch 'netstat -np --inet | grep "thunderbird"'
```

With:
*	-n: Show numerical addresses instead of trying to determine symbolic host, port or user names
*	-p: Show the PID and name of the program to which each socket belongs.
*	--inet: Only show raw, udp and tcp protocol sockets.

**strace for verbosity**
```
strace -f -e trace=network <your command> 2>&1 | grep sin_addr
```

The output might be verbose , so you might need some grepping. You could start by grepping on "sin_addr".
	Or, 
for an already running process, use the PID:

```
strace -f -e trace=network -p <PID> 2>&1 | grep sin_addr
```
 
 
 