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
	* check the `$VIRTUAL_ENV` variable. When active, it should contain the virtual environment's directory.


#### Vim Scrolling through highlighted documentation
We use `<shift+k>` to show the documentation of the variable. But to scroll through it we can 
* either use the mouse
* or `<C-w>w` and use vim like `j,k` to scroll up and down, and `<C-w>q` to close the window

##### Adding Unicode characters in Linux on Neovim
* Press Ctrl+Shift+u, then type the hexadecimal code of the Unicode character and press enter
