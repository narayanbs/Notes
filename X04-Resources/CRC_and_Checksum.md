A CRC which is short for a Cyclic Redundancy Code is a powerful type of a checksum.  A 
checksum is any sort of a mathematical operation that you can perform on data to make 
sure that the bits don’t get flipped accidentally when it’s stored in a memory or 
when it’s transmitted over to a network.  A CRC is a particularly powerful type of a 
checksum, mostly because it’s very difficult to fool a CRC.  So, CRCs are widely 
used.  One of the benefits of them is not only are they difficult to fool, but they’re 
relatively compact most are either 16 or 32 bits, so just taking up two or four bytes of 
additional storage. 

So, you might have a large packet that’s going to go out over to the network like a 
network packet for the Internet Protocol might be 1500 bytes long.  But you only need 
four additional bytes to store a 32-bit CRC to ensure that the data has not been 
corrupted.  It’s not universally perfect, but mathematically it’s very difficult to 
fool.  There are lots of – CRC is just a general concept.  There is lots of – 
it’s a mathematical process, but there are different specific algorithms or formulas 
that you can apply based on what’s known as the generator polynomial.  And so, one of 
the standards that’s widely used is what’s called the CRC-32 written like this and 
that’s the standard CRC-32 meaning 32 bits that is used widely over the internet for 
ensuring that data is accurate.  But there are others as well including 16-bit CRCs and 
a variety of different generator polynomials and other specific techniques.

One of the things that’s tricky for engineers when you’re going to implement a CRC is 
that if you’re using a general purpose processor or even a pen and a paper, computing a 
CRC is complex mathematically, because it operates on something that’s called Modulo-2 
addition which is the kind of binary arithmetic.  And you can build special dedicated 
hardware to do this quickly and sometimes you see that.  But if you’ve got to write it 
in your C program or your C++ program for embedded systems it can be tricky and it’s 
something that you shouldn’t waste your time doing because there are existing solutions 
for it.

CRCs are used for error detection across multiple computer networking technologies, 
such as Ethernet (both wired and wireless variants), Token Ring, Asynchronous Transfer 
Mode (ATM), and Frame Relay. Ethernet frames have a 32-bit Frame Check Sequence (FCS) 
field at the end of the frame (immediately after the payload of the frame) where a 
32-bit CRC value is inserted. 

For example, consider a scenario where two hosts named Host-A and Host-B are directly 
connected to each other through their Network Interface Cards (NICs). Host-A needs to 
send the sentence “This is an example” to Host-B over the network. Host-A crafts 
an Ethernet frame destined to Host-B with a payload of “This is an example” and 
calculates that the CRC value of the frame is a hexadecimal value of 0xABCD. Host-A 
inserts the CRC value of 0xABCD into the FCS field of the Ethernet frame, then transmits 
the Ethernet frame out of Host-A's NIC towards Host-B.

When Host-B receives this frame, it will calculate the CRC value of the frame with the 
use of the exact same algorithm as Host-A. Host-B calculates that the CRC value of the 
frame is a hexadecimal value of 0xABCD, which indicates to Host-B that the Ethernet frame 
was not corrupted while the frame was transmitted to Host-B.
As a result, Host-B cannot trust the contents of this Ethernet frame, so it will drop it. 
Host-B will usually increment some sort of error counter on its Network Interface Card 
(NIC) as well, such as the “input errors”, “CRC errors”, or “RX 
errors” counters.


##### CRC errors

CRC errors can be caused by a number of factors. Typically they are caused by either 
defective cable, transceiver (SFP), switch port, upstream network device, etc. To address 
this error, try replacing the cable or transceiver (SFP) and check the switch port and 
upstream network device

CRC errors typically manifest themselves in one of two ways: 

1. Incrementing or non-zero error counters on interfaces of network-connected devices.
2. Packet/Frame loss for traffic traversing the network due to network-connected devices 
dropping corrupted frames.

**RX Errors on Linux Hosts**

CRC errors on Linux hosts typically manifest as a non-zero “RX errors” counter 
displayed in the output of the **ifconfig** command. An example of a non-zero RX 
errors counter from a Linux host is here: 

$ **ifconfig eth0**  
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500   
        inet 192.0.2.10  netmask 255.255.255.128  broadcast 192.0.2.255   
        inet6 fe80::10  prefixlen 64  scopeid 0x20<link>   
        ether 08:62:66:be:48:9b  txqueuelen 1000  (Ethernet)   
        RX packets 591511682  bytes 214790684016 (200.0 GiB)   
        **RX errors 478920**  dropped 0  overruns 0  frame 0   
        TX packets 85495109  bytes 288004112030 (268.2 GiB)   
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0 

CRC errors on Linux hosts can also manifest as a non-zero “RX errors” counter 
displayed in the output of **ip -s link show** command. An example of a non-zero RX 
errors counter from a Linux host is here: 

$ **ip -s link show eth0**  
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT 
group default qlen 1000   
    link/ether 08:62:66:84:8f:6d brd ff:ff:ff:ff:ff:ff   
    RX: bytes  packets  errors  dropped overrun mcast   
    32246366102 444908978 478920       647     0       419445867   
    TX: bytes  packets  errors  dropped carrier collsns   
    3352693923 30185715 0       0       0       0   
    altname enp11s0 

The NIC and its respective driver must support accounting of CRC errors received by the 
NIC in order for the number of RX Errors reported by the **ifconfig** or **ip -s link 
show** commands to be accurate. Most modern NICs and their respective drivers support 
accurate accounting of CRC errors received by the NIC.


--------------------
Ref: 
https://www.cisco.com/c/en/us/support/docs/ios-nx-os-software/nx-os-software/217554-unders
tand-cyclic-redundancy-check-crc.html#:~:text=to%20Host%2DB.-,CRC%20Error%20Definition,bes
t%20demonstrated%20through%20an%20example.