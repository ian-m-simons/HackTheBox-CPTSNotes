a protocol for copying files to and from remote computers, it's fast and efficient basically just sends differences between two files if the file already exists on both devices, usually piggybacks on SSH 
basic enumeration syntax
```
n00blyfe@htb$ rsync -av --list-only rsync://<target>/<directory>
```
sync files to attack host:
```
n00blyfe@htb$ rsync -av rsync://<target>/<directory>
```