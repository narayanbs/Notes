#### How to Burn an ISO file to USB drive in Linux
List all the block devices
$ lsblk

Identify your USB drive - /dev/sdb1 or similar

Unmount the USB drive
$ sudo umount /dev/sdb1

Check if the USB is unmounted.
$ lsblk

Burn the iso to USB drive
$ sudo dd bs=4M if=ubuntu-24.04.1-desktop-amd64.iso of=/dev/sdb status=progress oflag=sync


#### How to open a file using a default application from command line in linux
$ xdg-open <file>
for ex: To open a pdf file in the document viewer
$ xdg-open sample.pdf

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
* Find the IP of the the devices.
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
