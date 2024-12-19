
### Task 1
- before you do antyhing install the nginx and ufw packages
```
sudo pacman -S nginx ufw
```
- create the webgen system user
```
sudo useradd --system -d /var/lib/webgen -s /usr/bin/nologin -m webgen
```
- create directories inside webgen home directory which is `/var/lib/webgen`
```
mkdir /var/lib/webgen/bin
mkdir /var/lib/webgen/HTML
```
- you'll need to change ownership of these directories 
```
chown -R webgen:webgen /var/lib/webgen
```
- -R used here to recursively give ownership to webgen to all the subdirectories
- copy the generate_index script from the repository nathan gives us into `/var/lib/webgen/bin`
- give ownership to that script 
```
chown webgen:webgen /var/lib/webgen/bin/generate_index
```
### Task 2
- make the generate-index.service file inside of `/etc/systemd/system`
- make the generate-index.timer file inside of `/etc/systemd/system`
- you can copy the code from my github for both of these
- run the command 
```
sudo systemctl daemon-reload
```
- this will make sure systemd knows you added the 2 files

- now you can start generate-index.service to make an index.html inside `/var/lib/webgen/HTML`
```
sudo systemctl start generate-index.service
```

- now start and enable the generate-index.timer
```
sudo systemctl enable --now generate-index.timer
```

### Task 3
- you'll want to edit the `/etc/nginx/nginx.conf` file. add these 2 lines into it![[Pasted image 20241126191903.png]]
- now create some folders where the serverblock.conf file will go
```
mkdir /etc/nginx/sites-available
mkdir /etc/nginx/sites-enabled
```
- make a `serverblock.conf` file inside of `/etc/nginx/sites-available`
- copy the code from my `assignment3-serverblock.conf `file in my github into your `serverblock.conf`
- now you need to make a symbolic link from that serverblock.conf file you just made into the `sites-enabled` directory
```
ln -s /etc/nginx/sites-available/serverblock.conf /etc/nginx/sites-enabled/serverblock.conf
```
- now run this command to start and enable nginx
```
sudo systemctl enable --now nginx
```
- copy the IP address of your droplet and paste it into your chrome to see if you see anything or if you get a 404 let me know if you have issues

### Task 4

- start and enable ufw.service
```
sudo systemctl enable --now ufw.service
```
- run all these commands in sequence
```
sudo ufw allow ssh
sudo ufw limit ssh
sudo ufw allow http
sudo ufw enable
```