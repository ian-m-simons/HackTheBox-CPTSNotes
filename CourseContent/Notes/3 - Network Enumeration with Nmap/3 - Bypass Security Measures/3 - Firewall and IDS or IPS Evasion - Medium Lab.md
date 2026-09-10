changes have been made to IDS/IPS and firewall, for this exercise we want to identify the target's DNS server version which is using udp lets start simple
`sudo nmap -sU -p 53 <TARGET_IP> -sC -sV`
in the output we see `bind.version HTB{GoTtgUnyze9Psw4vGjcuMpHRp}`
and if we put that in, it turns out that is in fact the answer
