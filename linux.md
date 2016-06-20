## Content
- tips
- command help
- user management
- file and directory
- text processing
- process management
- network tools
- disk management
- monitor
- regular expression

---
### Linux 设置定时启动脚本(crontab)
```
# 编辑
crontab -e
# e.g: 5 * * * * /usr/bin/python /home/pengnan/service/up.py

# 查看cron服务
crontab -l

#删除cron服务
crontab -r
```

### Command help
```
whatis <command>
info <command>
man <command>
which <command> 
whereis <command>
```

### User management
```
# change user
su <user>
# add user to sudoers
vim /etc/sudoers
```

### File and directory
```
mkdir <newDirName>
rm <file>
rm -rf <dir>
mv <src> <des> 
cp <src> <des>
cp -r <srcDir> <desDir>
# change to the last working directory
cd -
pwd
ls

# find and rm the file, notice the space
find ./ -name haha.txt -exec rm {} \;

# locate command need to use local database
locate string

# show line numbers
cat -n <filename>

# show first/last n lines
head -<n> <file>
tail -<n> <file>
diff <file1> <file2>

# change owner and rights
chown
chmod

# create links to file 
ln <src> <des>
ln -s <src> <des>

# pipe use | or ; to exec some cmd in order, if one fails the abort
# use || if one fails then exec the next one
# use > or >> redirect 

# ctrl + w: delete line or text before the cursor
# ctrl + h: delete the char before the cursor
```

### Text processing
[regex](#Regular Expression)
```
grep <match_pattern> <file>
# list n lines
grep -m 10 'haha' haha.txt

# use xargs command can change input into command args format
cat haha.txt | xargs

# sort: output lines in order
sort haha.txt
# unique line
sort haha.txt | uniq

# tr: repalce, filter input 
echo "1234567" | tr '0-9' '9876543210'

# conut lines, words, chars
wc -l/w/c <file>

# sed awk ...
```


### Process management
```
# display current processing information
ps -ef

# display info and refresh 
top 

# list open file
lsof
kill <pid>

# run cmd and ignore hangup signals
nohup Command [ Arg ... ] [　& ]
```

### Network tools
```
netstat
route 
ping
traceroute
host <ip|domain>
ssh id@host

# secure file transfer program
sftp id@host
get filename # 下载文件
put filename # 上传文件
ls # 列出host上当前路径的所有文件
cd # 在host上更改当前路径
lls # 列出本地主机上当前路径的所有文件
lcd # 在本地主机更改当前路径

# secure copy
scp localpsth id@host:path
```

### Disk management
```
# show disk space, df: display free disk place
# du: display disk usage statistics
df -h
# show current dir space
du -sh

# pack & compress
tar -cvf <dec> <src1> <src2> ...
gzip <src.tar>
# unpack & uncompress
gunzip demo.tar.gz
bzip2 demo.tar.bz2
tar -xvf demo.tar
```

### Monitor
```
# sar: system acticity reporter
sar
```

### Regular Expression
```
# regex dealing with lines
# []: char set, '^' inside '[]' means reverse selection
grep -n 't[as]st' haha.txt
grep -n '[^0-9]' haha.txt

# ^: line start, $: line end
grep -n '^the' haha.txt
grep -n '^$' haha.txt

# .:one char, *:repeat the char before 0 to n times
grep -n 't..t' haha.txt
grep -n 'oo*' haha.txt

# \{n,m\}: repeat the char before n to m times
# \{n\}: n times
# \{n,\}: at least n times
grep -n 'go\{2,3\}g' haha.txt

# extension:
# +: repeat the char before 1 to n times
# ?: repeat the char before 0 or 1 time 
# |: or
# (): group, can use * + ? behind
grep -n 'g(oo|la)d' haha.txt 

# chinese : [\u4E00-\u9FA5]
# find chinese word, more than one character
# match double-bit character
grep  '[^\x00-\xff]\{3,\}' haha.txt
```