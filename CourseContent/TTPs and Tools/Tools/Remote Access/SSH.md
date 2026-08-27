Used to securely access a remote machine common syntax examples below
```shell
#basic ssh connection using password
n00blyfe@htb$ ssh Bob@10.0.69.69
Password:
Bob@remoteHost$

#ssh using private key instead of password
n00blyfe@htb$ ssh -i Path/to/private/key Bob@10.0.69.69
Banner will be displayed
Enter passphrase for key 'Path/to/private/key':
Bob@remoteHost$


```