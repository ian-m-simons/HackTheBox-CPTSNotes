Here we will discuss many of the common issues people tend to run into in penetration testing and HTB  boxes/labs
### VPN Issues
when troubleshooting vpn issues, always start by checking that you are in fact connected to HTB
##### Still Connected to VPN
if you see `Initialization Sequence Completed` after you run the openvpn command then you are connected, else there was an issue
##### Getting VPN Address
you can also check your ip address with `ip -4 a show tun0`
if we get our IP back then we should be connected to the VPN network
##### Check the Routing table
check your routing table with `sudo netstat -rn`
##### Pinging the gateway
see if yoeu can ping the default gateway or not
##### Working on Two Devices
The HTB VPN cannot be connected to more than one device simultaneously (can't use pwnbox AND your own vm simultaneously)
##### Checking Region
if there is noticeable lag, check your region. 
##### VPN Troubleshooting
For other VPN issues check the [HackTheBox Help page](https://help.hackthebox.eu/troubleshooting/v2-vpn-connection-troubleshooting).
### Burp Suite Proxy Issues
a few burp quirks
##### Not Disabling Proxy
remember the burp proxy captures all traffic, remember to turn it off when not in use. Otherwise it will keep intercepting traffic and nothing will load. 
### Changing SSH Key and Password
if you are having issues connecting to SSH servers etc it is worth renewing or rotating SSH keys and passwords.