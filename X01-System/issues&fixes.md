# kitty default terminal
To make kitty the default terminal 
```bash
$ sudo update-alternatives --install /usr/bin/x-terminal-emulator x-terminal-emulator /home/narayan/.local/kitty.app/bin/kitty 100
```
# tmux status bar 
To turn off the status bar, launch tmux and then in the command line type
```bash
$ tmux set status off
```
To turn on
```bash
$ tmux set status on
```
To make the changes permanent, add the following at the bottom of tmux.conf
```bash
set -g status off
```

# neovim clipboard issue
```bash
sudo apt install xsel
```
#### Disable bluetooth 
```bash
sudo systemctl stop bluetooth.service, sudo systemctl disable bluetooth.service
```

----------
#### clang issues

**libc++ not found because multiple gcc is installed**

Verify 

```bash
$ clang++ -v -E
```

If you find two versions of gcc, then you need to install the appropriate g++. In my case i found gcc-11 and gcc-12.
so i had to install g++-12.

```bash
$ sudo apt install g++-12
```

Update alternatives (Note 10,20,30 are priority.. higher the number more is the priority)

```bash
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-11 10
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-12 20

sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-11 10
sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-12 20

sudo update-alternatives --install /usr/bin/cc cc /usr/bin/gcc 30
sudo update-alternatives --set cc /usr/bin/gcc

sudo update-alternatives --install /usr/bin/c++ c++ /usr/bin/g++ 30
sudo update-alternatives --set c++ /usr/bin/g++
```

---
#### Adding a custom app to favorites 

1. Let's add Obsidian appimage to the favorites. 
2. First create a desktop entry in `/usr/share/applications/`
	`$ sudo nano /usr/share/applications/Obsidian.desktop`
3. Add the following to the file
   
```bash
#!/usr/bin/env xdg-open
[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Exec=/home/phoenix/devide/Obsidian-1.1.16.AppImage
Name=Obsidian
Comment=Markdown Editor
```

4. Log out and log in again
5. You can find the Obsidian application in the launcher 
6. Right-click on the Obsidian icon and click on add to favories. 

------------------------
#### Wifi drop issue

The following issues were noticed after i installed Ubuntu 22.04.

1. wifi used to drop regularly after the kernel upgrade to 5.15. Internet search revealed that the fix has been put into 5.17.2 version of the kernel.
2. Bluetooth was not working with error "Patch file not found ar3k/AthrBT_0x31010000.dfu" at startup.
3. Another issue was lack of ntfs3 support in kernel 5.15 and later, so i had to install ntfs-3g package.
4. Missing desktop icons and folders

#### Fix 1

##### Upgrading to the latest kernel

```bash
$ wget https://raw.githubusercontent.com/pimlie/ubuntu-mainline-kernel.sh/master/ubuntu-mainline-kernel.sh
$ sudo install ubuntu-mainline-kernel.sh /usr/local/bin/
$ sudo ubuntu-mainline-kernel.sh -i
```

`Press y to progress with the installation process`

Reboot after completion of installation.

or

```bash
$ cd /tmp

wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.17.4/amd64/linux-headers-5.17.4-051704_5.17.4-051704.202204200842_all.deb
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.17.4/amd64/linux-headers-5.17.4-051704-generic_5.17.4-051704.202204200842_amd64.deb
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.17.4/amd64/linux-image-unsigned-5.17.4-051704-generic_5.17.4-051704.202204200842_amd64.deb
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.17.4/amd64/linux-modules-5.17.4-051704-generic_5.17.4-051704.202204200842_amd64.deb

$ sudo dpkg -i *.deb
```

##### delete previous versions of kernel

```bash
# get list of existing kernels
$ dpkg --list | grep -i -E --color 'linux-image|linux-kernel' | grep '^ii'

# delete 5.15.0-25-generic
$ sudo apt remove --purge linux-image-5.15.0-25-generic
$ sudo apt autoremove
```

##### Install intel-microcode

```bash
$ sudo apt install intel-microcode
```

####

### Fix 2

##### Download linux-firmware (you can look at the packages at https://packages.ubuntu.com/impish/linux-firmware)

```bash
$ curl -SLO http://archive.ubuntu.com/ubuntu/pool/main/l/linux-firmware/linux-firmware_1.201.tar.xz
$ tar -xf linux-firmware_1.201.tar.xz
$ sudo mv linux-firmware/ar3k /lib/firmware
$ reboot
```

### Fix 3

##### ntfs-3g

```bash
$ sudo apt install ntfs-3g
```

### Fix 4

```bash
$ sudo apt install gnome-shell-extension-desktop-icons-ng
$ reboot
```
