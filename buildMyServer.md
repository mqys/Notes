
### ShadowSocks
for freedom!!!
```Shell
# ubuntu
apt-get install python-pip
pip install shadowsocks
# centOS
yum install python-setuptools && easy_install pip
pip install shadowsocks

# start the server
ssserver -p 8836 -k 'password' -m rc4-md5 [-d start|stop]

ssserver -c /etc/shadowsocks.json [-d start|stop]
```
```json
{
    "server":"<ip_address>",
    "server_port":8836,
    "local_address":"127.0.0.1",
    "local_port":1080,
    "password":"<password>",
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open":false
}
```

### Git server
```shell
# add user: git 
sudo adduser git
# edit the sudoer file 
su git
# create the .ssh file 
mkdir .ssh && chmod 700 .ssh
touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
# copy my public key append to .ssh/authorized_keys

# create the server project repo
mkdir project.git
cd project.git
git init --bare

################
# on my computer
git remote add mygit git@182.254.215.237:/home/git/project.git
git push mygit 
```

### Upload file to server
```shell
# use sftp
sftp -i ~/mqys ubuntu@182.254.215.237
# then can use help to see the commands
```

