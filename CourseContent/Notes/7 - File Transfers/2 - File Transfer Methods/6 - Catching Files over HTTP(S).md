web transfer is common because HTTP(S) is almost never blocked on the firewall. also HTTPS is encrypted which is beautiful cause no more IDS picking up that a password was just sent in plain text
this section is all about setting up Apache or Nginx 

### Nginx - Enabling PUT
Nginx is less complicated than Apache, and doesn't have the same security issues as Apache. 
When allowing HTTP uploads it is critical to be 100% positive that users cannot upload web shells and execute them. Apache mackes it easy to shoot ourselves in the foot with this as the PHP module loves to execute anything ending in PHP. 
##### Create a Directory to Handle Uploaded Files
```
n00blyfe@htb$ sudo mkdir -p /var/www/uploads/secretuploaddirectory
```
##### Change the Owner to www-data
```
n00blyfe@htb$ sudo chown -R www-data:www-data /var/www/uploadls/secretuploaddirectory
```
##### Create Nginx config file
create the following file
```
n00blyfe@htb$ sudo vim /etc/nginx/sites-available/upload.conf


server{
    listen 9001;
    
    location /secretuploaddirectory/{
        root    /var/www/uploads;
        dav_methods PUT;
    }
}

```
##### Symlink our site to the sites-enabled Directory
```
n00blyfe@htb$ sudo -ln -s /etc/nginx/sites-available/upload.conf /etc/nginx/sites-enabled/
```
##### Start Nginx
```
n00blyfe@htb$ sudo systemctl restart nginx.service
```
errors will go to `/var/log/nginx/error.log`

if you're using pwnbox port 80 is already in use so we can change the default port for nginx
##### Remove Nginx Default Configuration
```
n00blyfe@htb$ sudo rm /etc/nginx/sites-enabled/default
```
