A VPN connects a host to a remote network. This can be client based or SSL using the web browser as the VPN client. 
### Why Use a VPN
using a VPN obscures our browsing traffic and disguises our public IP address. This provides some limited security and privacy. Using a VPN does not guarantee anonymity or privacy but is useful for bypassing certain network/firewall restrictions. Remember if you are being truly nefarious, a VPN is not the solution you need
### Connecting to HTB VPN
when connecting to HTB VPN, or any pen testing/hacking focused lab, assume the network is hostile. Only connect from a virtual machine, disallow password authentication if SSH is enabled on our attacking VM, lockdown any web servers, and do not keep sensitive info on our attack VM. to connect use the following flow

```shell
n00blyfe@htb[/htb]$ sudo openvpn user.ovpn 

Thu Dec 10 18:42:41 2020 OpenVPN 2.4.9 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on Apr 21 2020 
Thu Dec 10 18:42:41 2020 library versions: OpenSSL 1.1.1g 21 Apr 2020, LZO 2.10 Thu Dec 10 18:42:41 2020 Outgoing Control Channel Authentication: Using 256 bit message hash 'SHA256' for HMAC authentication 
Thu Dec 10 18:42:41 2020 Incoming Control Channel Authentication: Using 256 bit message hash 'SHA256' for HMAC authentication 
Thu Dec 10 18:42:41 2020 TCP/UDP: Preserving recently used remote address: [AF_INET] 
Thu Dec 10 18:42:41 2020 Socket Buffers: R=[212992->212992] S=[212992->212992] 
Thu Dec 10 18:42:41 2020 UDP link local: (not bound) 
<SNIP> 
Thu Dec 10 18:42:41 2020 Initialization Sequence Completed
```
the last line `Initialization Sequence Completed` tells us that we successfully connected to the VPN. In the example above, `openvpn` is the VPN client we are using and `user.ovpn` is the VPN key that we would need to download to access the lab. Successful connection will create a `tun` adaptor as shown below
```shell
n00blyfe@htb[/htb]$ ifconfig 

<SNIP> 

tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST> mtu 1500 
	inet 10.10.x.2 netmask 255.255.254.0 destination 10.10.x.2 
	inet6 dead:beef:1::2000 prefixlen 64 scopeid 0x0<global> 
	inet6 fe80::d82f:301a:a94a:8723 prefixlen 64 scopeid 0x20<link> 
	unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00 txqueuelen
```
typing `netstat -rn` will show us the networks accessible via the VPN
```shell
n00blyfe@htb[/htb]$ netstat -rn

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.1.2     0.0.0.0         UG        0 0          0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG        0 0          0 tun0
192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 eth0
```
