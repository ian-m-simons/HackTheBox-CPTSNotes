[Nmap](../../../TTPs%20and%20Tools/Tools/Host%20Discovery%20and%20Scanning/Nmap.md) is written in C, C++, Python, and Lua. It scans networks and identifies hosts, services and applications. It can also identify packet filters, firewalls, or IDS
### Use Cases
[Nmap](../../../TTPs%20and%20Tools/Tools/Host%20Discovery%20and%20Scanning/Nmap.md) is one of the most commonly used tools by network administrators,  and IT security specialists. Uses include:
- Audit the security aspects of networks
- Simulate penetration tests
- Check firewall and IDS settings and configurations
- Types of possible connections
- Network mapping
- Response analysis
- Identify open ports
- Vulnerability Assessment
### Nmap Architecture
Scanning techniques include:
- Host discovery
- Port scanning
- Service enumeration and detection
- OS detection
- Scriptable interaction with the target service (Nmap Scripting Engine)
### Syntax
basic syntax is below
```
n00blyfe@htb$ nmap <scan types> <options> <target>
```
### Scan Techniques
Different scanning techniques make different types of connections using differently structured packets see below
```
n00blfye@htb$ nmap --help
<snip>
SCAN TECHNIQUES:
	-sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Maimon scans
	-sU: UDP Scan
	-sN/sF/sX: TCP Null, FIX, and Xmas scans
	--scanflags <flags>: Custamize TCP scan flags
	-sI <zombie host[:probeport]>: Idle scan
	-sY/sZ: SCTP INIT/COOKIE-ECHO scans
	-sO: IP protocol scan 
	-b <FTP relay host>: FTP bounce scan
<snip>
```
TCP-SYN (`-sS`) is one of the default settings. This scan method can scan thousands of ports per second. The TCP-SYN scan sends one packet with a SYN flag and then never completes the handshake. 
- SYN-ACK packet sent back = Nmap says port is open
- RST packet sent back = Nmap says port is closed
- no response = Nmap says port is filtered.