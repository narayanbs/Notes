
#### Installation in Ubuntu 

* Install the necessary dependencies and Kernel headers in Ubuntu Linux with command:
~~~bash
  $ sudo apt install dkms git build-essential libelf-dev linux-headers-$(uname -r)
~~~
* For 24.04 do the following
~~~bash
sudo apt install git
git clone https://github.com/morrownr/8821au-20210708.git
cd 8821au-20210708
sudo ./install-driver.sh
Press enter to accept the default and reboot
~~~

* For versions below 24.04

* Clone the `rtl8812au` repository
~~~bash
  $ git clone -b v5.6.4.2 https://github.com/aircrack-ng/rtl8812au.git
  $ cd rtl8812au/
~~~

* Finally, install TP-Link AC600 Archer T2U Nano WiFi USB adapter in Ubuntu using command:
~~~bash
  $ sudo make dkms_install
~~~

* Unplug the TP-Link Archer T2U nano adapter and plug it again. The LED will start to blink. Verify if the driver is installed and loaded using command:
~~~bash
  $ sudo dkms status
~~~

* If the TP-Link AC600 WiFi USB adapter is installed, you will see the following output:
~~~bash
  8812au, 5.6.4.2_35491.20191025, 5.11.15-1-default, x86_64: installed
~~~

#### Uninstall driver

* To remove the driver from your system, 
After 24.04
~~~bash
$ cd 8812au-20210708
$ sudo ./remove-driver.sh
~~~

Pre 24.04
cd into the directory that contains the source code and execute the following command:
~~~bash
  $ sudo make dkms_remove
~~~

#### Disable the existing internal Wifi adapter

* Find the exisiting Wifi driver in your system
~~~bash
  $ sudo readlink /sys/class/net/wlp2s0/device/driver
~~~

* Remove it using
~~~bash
  $ sudo modprobe -r ath9k
~~~

* To make the changes permanent, open blacklist.conf using nano
~~~bash
  $ sudo nano /etc/modprobe.d/blacklist.conf
  # Add this at the end
  $ blacklist ath9k
~~~
  * ctrl+x and y for save & exit and restart the system.


#### To enable internal wifi adapter
~~~bash
  $ sudo modprobe ath9k
~~~
* To make the changes permanent, remove the blacklist entry in blacklist.conf and restart the system.

##### Alternative way
~~~bash
  $ sudo apt purge rtl8812au-dkms
~~~

* Next, let's install a newer driver:
~~~bash
  $ git clone https://github.com/morrownr/8821au-20210708.git
  $ cd 8821au-20210708
  $ sudo ./install-driver.sh
~~~

* For more details visit https://github.com/morrownr/8821au-20210708
