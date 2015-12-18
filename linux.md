### command help
```
whatis <command>
info <command>
man <command>
which <command> 
whereis <command>
```

### file and directory
```shell
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

### text processing
```shell
grep <match_pattern> <file>
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

### disk management
```shell
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

### process management
```shell
# display current processing information
ps -ef
# display info and refresh 
top 
# list open file
lsof
kill <pid>
```

### monitor
```shell
# sar: system acticity reporter
sar
```

### network tools
```shell
netstat
route 
ping
traceroute
host
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

### user management
```shell

```

### system & IPC resource management
```shell

```

