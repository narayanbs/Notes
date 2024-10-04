- Open the terminal
- List your block storage and identify your pen drive
	```
	lsblk -e7
	or 
	lsblk -f 
	```
- Make sure the drive is unmounted
```
	 sudo umount /dev/sdb?
```
- Erase everything on the pen-drive (this is optional and you can skip to the next step)
	```
	sudo dd if=/dev/zero of=/dev/sdb bs=4M status=progress && sync
	```
	It will pretend to be stuck. Just be patient. for example:
```
dd if=/dev/zero of=/dev/sdb bs=4k && sync
dd: error writing '/dev/sdb': No space left on device

1984257+0 records in
1984256+0 records out
8127512576 bytes (8.1 GB) copied, 1236.37 s, 6.6 MB/s
```
- if you don't do the previous step, you can do the following
- erase filesystem or partition-table signatures which may exist on the device.
	```
	sudo wipefs --all --force /dev/sdb
	```
- Open parted and create a partition table
	```
	sudo parted /dev/sdb
	(parted)print
	(parted)mklabel msdos
	(parted)mkpart primary fat32 1MiB 100% 
	(parted)print	
    (parted)q
	```
- Create a filesystem in the new partition we created
	```
	sudo mkfs.vfat -F32 /dev/sdb1
	```

# Creating Bootable USB
- Open the terminal
- List your block storage and identify your pen drive
	```
	lsblk -e7
	or 
	lsblk -f 
	```
- Make sure the drive is unmounted
	```
	 sudo umount /dev/sdb?
	```
- Now create the bootable disk using dd
	```
	sudo dd if=~/Downloads/archlinux-2023.07.01-x86_64.iso of=/dev/sdb bs=4M 
status=progress conv=fsync
	```

##### Note:
- dd may seem to freeze, but it is actually syncing the data on-disk after the operation. 
In order to optimize IO operations
you should be able to estimate how much data there is left to write by looking at the 
"Dirty:" value in `/proc/meminfo` - this is the total amount of data pending to be 
written to disk.

