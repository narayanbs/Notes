#### Creating a large file with random bytes inside it in linux
dd if=/dev/random of=/tmp/file1.db count=100 bs=1M

Note: By default files inside /tmp are cleared in 10 days and  /var/tmp in 30 days. 

#### Python Virtual Environment
* How do we know if a virtual environment is active?
	* check the `$VIRTUAL_ENV` variable. When active, it should contain the virtual environment's directory.


#### Vim Scrolling through highlighted documentation
We use `<shift+k>` to show the documentation of the variable. But to scroll through it we can 
* either use the mouse
* or `<C-w>w` and use vim like `j,k` to scroll up and down, and `<C-w>q` to close the window

##### Adding Unicode characters in Linux on Neovim
* Press Ctrl+Shift+u, then type the hexadecimal code of the Unicode character and press enter
