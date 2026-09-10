for these labs we need to answer specific questions without getting blocked on the firewall/ids/ips etc lets do it! This one is supposed to be easy. our goal is to find the OS name
we decided to start pretty simple and basic 
`sudo nmap -sC -sV <TARGET_IP>` 
this revealed SSH on port 22 listing ubuntu as the host. 
this was the correct answer