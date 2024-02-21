#### Redirection 

**Redirecting input**
`[n]<word`
* This causes the file denoted by the word to be opened for reading on file descriptor n.
* If n is not specified then stdin (fd 0) is assumed.

Ex:

cat < sample.txt - sample.txt is opened for reading using stdin
cat 10< sample.txt - sample.txt is opened for reading using the fd 10

**Redirecting output**
`[n]>word`
* This causes the file denoted by word to be opened for writing on file descriptor n.
* If n is not specified then stdout (fd 1) is assumed. File is created if it doesn't exist.

Ex:
ls > sample.txt - sample.txt is opened (or created) for writing using stdout
ls 10> sample.txt - sample.txt is opened (or created) for writing using fd 10

**Appending Redirected output**
`[n]>>word`
* This causes the file denoted by word to be opened for appending on file descriptor n.
* If n is not specified then stdout (fd 1) is assumed. File is created if it doesn't exist.

ls >> sample.txt - sample.txt is opened (or created) for appending using stdout
ls 10>> sample.txt - sample.txt is opened (or created) for appending using fd 10

**Redirecting stdout and stderr**
`&>word` and it is semantically equivalent to `>word 2>&1`
* This causes stdout and stderr to be redirected to the file denoted by the word.

Ex:
ls /bin/usr &> /dev/null
ls /bin/usr > /dev/null 2>&1

**Appending stdout and stderr
`&>>word` and it is semantically equivalent to `>>word 2>&1`
* This causes stdout and stderr to be appended to the file denoted by the word.

Ex:
ls /bin/usr &>> /dev/null
ls /bin/usr >> /dev/null 2>&1

**Duplicating File Descriptors**
`[n]<&word`
* This is used to duplicate input file descriptors. 
* The fd denoted by n is made a copy of the fd denoted by the word. If n is not specified then stdin (fd 0) is used.

Ex:
`exec 10<&0` --> fd 10 is a copy of the fd 0 (stdin). So reading from 10 is similar to reading from stdin

`[n]>&word`
* This is used to duplicate output file descriptors.
* The fd denoted by n is made a copy of the fd denoted by the word. If n is not specified then stdout (fd 1) is used.

Ex:
exec 2>&1 --> fd 2 is a copy of fd 1 (stdout). So writing to 2 is similar to writing to stdout. 

**Moving File Descriptors**
`[n]<&digit-`
* moves file descriptor digit to file descriptor n, or stdin if n is not not specified.
* digit is closed after being duplicated to n. 

Ex:
`exec 10<&-` - close file descriptor 10

`[n]>&digt-`
* moves file descriptor digit to file descriptor n, or stdout if n is not not specified.
* digit is closed after being duplicated to n.

**Opening File descriptors for reading and writing**
`[n]<>word`
* This causes the file denoted by the word to be opened for both reading and writing on the descriptor n or on fd 0 if n is not specified. 
* If the file doesn't exist, it is created.

**Here Documents and Here strings**
The format of Here documents is:
```
[n]<<[-]word
        here-document
delimiter
```
Ex:
Suppose we need to send several commands over ssh, like
	ssh -T baeldung@example.com "touch log1.txt"
	ssh -T baeldung@example.com "touch log2.txt"

However, if we’ve more commands to execute, the solution above will become cluttered and verbose. To make it more succinct, we can replace it with a heredoc:

	ssh -T baeldung@host.com << EOF
	touch log1.txt
	touch log2.txt
	EOF

Ex:
	cat << EOF
	This is line1
	Another line
	Finally 3rd line
	EOF

The format of Here strings is:
```
[n]<<< word
```

Ex:
	COMMAND <<< $VAR
	What it essentially does is expanding the variable _VAR_ and redirect the output string to the _COMMAND_

cat <<< "This is a string"

WELCOME_MESSAGE="Welcome to dashboard"
cat <<< $WELCOME_MESSAGE

