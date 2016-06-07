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
```json
{
    "server":"0.0.0.0",
    "port_password": {
        "端口1": "连接密码1",
        "端口2" : "连接密码2"
    },
    "timeout":300,
    "method":"aes-256-cfb",
    "fast_open": false
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

### JAVA
```
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update

sudo apt-get install oracle-java6-installer
sudo apt-get install oracle-java7-installer
sudo apt-get install oracle-java8-installer

sudo apt-get install oracle-java7-set-default

sudo update-alternatives --config java
sudo nano /etc/environment
JAVA_HOME="YOUR_PATH"
source /etc/environment
echo $JAVA_HOME

// manual
tar zxvf jdk-7u45-linux-i586.tar.gz 
mv jdk1.7.0_45/ /usr/local/java
vi /etc/profile 

export JAVA_HOME=/usr/local/java
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin

source /etc/profile 
```