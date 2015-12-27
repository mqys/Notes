
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
