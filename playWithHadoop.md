notes about installation of Hadoop and Hbase
- [config hadoop](#Configure hadoop)
- [config hbase](#Configure hbase)
- [code with IDE](#Code the job)

-----
### JAVA environment required

### Using homebrew to install hadoop and hbase
```shell
brew install hadoop hbase
# installed in /usr/local/Cellar/
```
### SSH into localhost
- need to change the System Preference 

-----

## Configure hadoop 
- config diff in modes
- /usr/local/Cellar/hadoop/2.7.1/libexec/etc/hadoop/
- hadoop-env.sh: `export JAVA_HOME="$(/usr/libexec/java_home)"`

### 1. Standalone Operation Mode(just for test)
- one single java process

``` shell
mkdir input
cp etc/hadoop/*.xml input
bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.1.jar grep input output 'dfs[a-z.]+'
cat output/*
```

### 2. Pseudo-Distributed Operation Mode
- one single-node in pseudo-distributed mode
- each Hadoop daemon runs in a separate java process
- core-site.xml (fs.defaultFS necessary)

```xml
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
    <property>
        <name>hadoop.tmp.dir</name>
        <value>file:/usr/local/Cellar/hadoop/2.7.1/tmp</value>
        <description>Abase for other temporary directories.</description>
    </property>
</configuration>
```
- hdfs-site.xml (dfs.replication necessary)

```xml
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
    <property>
        <name>dfs.namenode.name.dir</name>
        <value>file:/usr/local/Cellar/hadoop/2.7.1/tmp/dfs/name</value>
    </property>
    <property>
        <name>dfs.datanode.data.dir</name>
        <value>file:/usr/local/Cellar/hadoop/2.7.1/tmp/dfs/data</value>
    </property>
</configuration>
```

- execution 

```shell
# format the filesystem
hdfs namenode -format

# Start NameNode daemon and DataNode daemon
sbin/start-dfs.sh
# The hadoop daemon log output is written to the $HADOOP_LOG_DIR directory (defaults to $HADOOP_HOME/logs).
# if show up `namenode`,`datanode`,`secondary namenode`, that means start successfully
# use jps to show processes
jps

# Browse the web interface for the NameNode
# http://localhost:50070 

# create HDFS user dir
# after create the user dir can use relative path
＃ user dir name must same to the computer user name, otherwise relative path maybe wrong
hdfs dfs -mkdir -p /user/mqys

# do the same demo as before
# copy the input file 
hdfs dfs -mkdir /user/mqys/input
hdfs dfs -put ./etc/hadoop/*.xml /user/mqys/input
hdfs dfs -ls /user/mqys/input

hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-2.7.1.jar grep input output 'dfs[a-z.]+'

hdfs dfs -cat output/*

./sbin/stop-dfs.sh
```

#### YARN on single node
- mapred-site.xml

```xml
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
</configuration>
```

- yarn-site.xml

```xml
<configuration>
<property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
</configuration>
```

- execution

```shell
# start ResourceManager daemon and NodeManager daemon
./sbin/start-yarn.sh

# then do the map-reduce job as before

# Browse the web interface for the ResourceManager
# http://localhost:8088/

# stop 
./sbin/stop-yarn.sh
``` 

-----
## Configure hbase

### Pseudo-Distributed Local install 

- hbase-site.xml
- attention to the port number

```xml
<property>
  <name>hbase.rootdir</name>
  <value>hdfs://localhost:9000/hbase</value>
</property>
<!--<property>
    <name>hbase.zookeeper.property.dataDir</name>
    <value>/home/testuser/zookeeper</value>
</property>-->
<property>
  <name>hbase.cluster.distributed</name>
  <value>true</value>
</property>
```

- execution

```shell
# start hbase, should start hadoop first
bin/star-hbase.sh 

# use Hbase Shell to operate the database
bin/hbase shell
create 'test', 'cf'
list 'test'
put 'test', 'row111', 'cf:aaa', 'value111'
scan 'test'
get 'test', 'row111'
disable 'test'
drop 'test'

# stop 
bin/stop-hbase.sh 
```
-----
### Code the job
code the process job with IDEA
- create an empty project in IDEA
- add the lib, `cmd+,`, add modules
    - /usr/local/Cellar/hadoop/2.7.1/libexec/share/hadoop/
    - /usr/local/Cellar/hbase/1.1.2/libexec/lib
- write the job code 
- Edit Configuration: program arguments: `input` `output` 
    - `input` `output` can be local file or dir
    - could access hdfs like `hdfs://localhost:9000/user/mqys/input`
