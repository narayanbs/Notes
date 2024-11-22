#### How to get the PID of a process holding a particular port 
$ lsof -i TCP:22

COMMAND  PID  USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd     890  root    5u  IPv4  24658      0t0  TCP *:ssh (LISTEN)
sshd     890  root    7u  IPv6  24666      0t0  TCP *:ssh (LISTEN)

$ lsof -i :8080

COMMAND  PID  USER       FD   TYPE DEVICE SIZE/OFF NODE NAME
main    14571 narayan    3u  IPv4  72478      0t0  TCP localhost:http-alt (LISTEN)

#### To get what files a process has open
$ lsof -p 2479

#### To get what files a particular user has open
$ lsof -u narayan

#### To get what process is using a particular directory
$ lsof /run

COMMAND    PID  USER   FD   TYPE DEVICE SIZE/OFF  NODE NAME
systemd      1  root   31u  FIFO   0,24      0t0 19314 /run/initctl
systemd      1  root   38u  FIFO   0,24      0t0 19331 /run/dmeventd-server
systemd      1  root   39u  FIFO   0,24      0t0 19332 /run/dmeventd-client


#### How to view a file with line numbers in command line
$ nl <filename>
Line numbers won't be added to newlines by default. we can use the following 
command to add line numbers to all the lines
$ nl -b a <filename>

#### How to view a portion of a file in command line
$ sed -n 'start,endp;' filename 
ex:
$ sed -n '12,20p;' deadline.txt

If we do this on a very large file, we should add a quit command on the next line
to prevent sed from scanning the whole file
$ sed -n 'start,endp;end+1q' filename
ex:
$ sed -n '12,20p;21q' deadline.txt

#### How to Safely remove a drive from command line 
List all the block devices
$ lsblk -e7
Suppose the device we want to power off is as shown below 
sdb
|_ sdb1 

Unmount the filesystem in the partition and power-off the device using udisksctl
$ sudo udisksctl unmount -b /dev/sdb1
$ sudo udisksctl power-off -b /dev/sdb 

#### How to Burn an ISO file to USB drive in Linux
List all the block devices
$ lsblk -e7
    or
$ sudo lshw -class disk -short

Identify your USB drive - /dev/sdb1 or similar

Unmount the USB drive
$ sudo umount /dev/sdb1

Check if the USB is unmounted.
$ lsblk

Burn the iso to USB drive
$ sudo dd if=ubuntu-24.04.1-desktop-amd64.iso of=/dev/sdb bs=4M status=progress oflag=sync


#### How to open a file using a default application from command line in linux
$ xdg-open <file>
for ex: To open a pdf file in the document viewer
$ xdg-open sample.pdf

#### Using xsel to copy contents from Vim to Clipboard and vice versa
* Copy from vim to clipboard
Select the lines in visual mode 
Press ":" to go to command line and enter the following command
:'<,'> !tee >(xsel -b)

* Copy from clipboard and paste into vim
Press ":" to go to command line
:r !xsel -b

#### How to insert contents from clipboard into the current Vim buffer with width formatting.
We can use xclip or xsel to fetch the clipboard content
The following will open vim and run the command 'r !xsel -o | fold -w 80'
$ vim -c 'r !xsel -o | fold -w 80'
In the above command replace xsel with xclip if you are using xclip.

Let's understand the above command. 
- vim -c  says run the command after opening vim
- `:r`: This is a Vim command that stands for "read". It is used to read content from a file or
command and insert it into the current buffer at the cursor position.
- `!`: This symbol in Vim is used to run an external shell command. When you use `!` in a Vim command, 
it tells Vim to execute the following string as a shell command.
- `xsel -o`: This is a shell command that interacts with the clipboard. Specifically:
  - `xsel` is a utility for accessing the X clipboard.
  - `-o` stands for "output", which means it outputs the contents of the clipboard.

And the output is piped to the fold command and pasted into the current buffer.

We could have also done the following

$ xsel --clipboard --output | fold -w 80 > /tmp/clipboard_folded.txt
$ vim /tmp/clipboard_folded.txt

#### Search for all occurences of a string inside a file. 
for example, to search all **title="somerandomtext"** inside a file  

$ grep -o 'title="[^"]*"' blogs-i-follow.opml

$ cat blogs-i-follow.opml | grep -o 'title="[^"]*"' 

#### Search for a string inside all files in a directory
$ grep -rni "text string" /path/to/directory  

     -r performs a recursive search within subdirectories.
     -n displays the line number containing the pattern.
     -i ignores the case of the text string.



To filter the results and display only the filenames without duplication, you can use the following command:

$ grep -rli "text string" /path/to/directory  
    -l prints only the names of the files containing the pattern.

To find files containing a specific text string using the find command, you can utilize the following syntax:

$ find /path/to/directory -type f -exec grep -l "text string" {} \;  

    /path/to/directory specifies the directory in which the search will be performed.
    -type f filters the search to only include regular files.
    -exec grep -l "text string" {} \; executes the grep command on each file found and displays the filenames that contain the text string

#### Creating a large file with random bytes inside it in linux
dd if=/dev/random of=/tmp/file1.db count=100 bs=1M

Note: By default files inside /tmp are cleared in 10 days and  /var/tmp in 30 days. 

##### List all devices in the same network (IP and Mac address)
Create a shell script 
#!/bin/bash
for i in $(seq 1 254); do
    ping -c 1 -q 192.168.1.$i &
done 
And enter the following in the command line 
arp -a | grep 192.168.1. | grep ether

##### Connect two devices in the same network
* Find the IP of the devices.
* Ping the IP addresses to check if they are connected
* Run ssh
ssh -y root@your_ip_address
* after typing the password of the host computer in your client computer, you would
have successfully connected to the computer

#### Python Virtual Environment
* How do we know if a virtual environment is active?
	* check the `$VIRTUAL_ENV` variable. When active, it should contain the virtual 
environment's directory.


#### Vim Scrolling through highlighted documentation
We use `<shift+k>` to show the documentation of the variable. But to scroll through it we 
can 
* either use the mouse
* or `<C-w>w` and use vim like `j,k` to scroll up and down, and `<C-w>q` to close the 
window

##### Adding Unicode characters in Linux on Neovim
* Press Ctrl+Shift+u, then type the hexadecimal code of the Unicode character and press 
enter

