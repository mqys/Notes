# Content
- [docker concept](#docker concept)
- [docker cmd](#docker cmd)
- [Dockerfile](#Dockerfile)
- [Private Registry](#Private Registry)
- [Docker Compose](#Docker Compose)

## docker concept
### Image
- 类似虚拟机的快照, 只读的模板
- 拥有唯一ID, 供人阅读的名字和标签对

### Container
- 类似快照中的虚拟机
- 在镜像中创建容器, 容器在启动的时候在镜像的只读层上创建一层可写层
- 应用由容器运行
- 容器是隔离的
- 拥有唯一ID, 名字
- 被设计用来运行单线程

### Repository
- 存放镜像文件的仓库

### 数据卷
- 用来数据持久化, 不受容器生命周期影响; 表现在容器内, 实际保存在容器外
- docker允许定义应用部分和数据部分, 并提供工具使他们分开
- 卷是针对容器的, 容器应该是短暂和一次性的

### 链接
- 容器启动的时候, 将被分配一个随机的私有IP
  - 容器间相互通信的渠道
  - 容器将共享一个本地网络
- 开启容器间通信: 在开启一个新容器的时候, 引用其他现有的容器, 在新创建的容器中被引用的容器将得到一个别名. 这两个容器就被链接了.
- 需要声明容器被链接的时候开放哪些端口给其他容器使用

### Implementation
- cgroups: 提供容器隔离
  - 限制进程组的资源占用
  - 为进程组制作PID, UTS, IPC, 网络, 用户及装载空间
- union文件系统: 保存容器并使容器变得短暂
  - 分层的积累变化
  - 在创建一个容器的时候, docker会创建一个空白的union文件系统加载在与该镜像关联的union文件系统之上
  - 卷所做的就是在容器内指定一个目录, 以便在union文件系统之外保存它

## docker cmd
```
# version
docker version
docker info

# search image
docker search <image name>

# run cmd inside image, use -d to run in background, then check logs to get the output 
docker run <username/imageName> <cmd>
docker logs <containerID or name>
# -t:tty -i:interative --rm: remove container when exit
docker run --rm -t -i  ubuntu /bin/bash 
# install inside image, need to -y when using apt-get to avoid interative mode
docker run <username/imageName> apt-get install -y <software name>

# get container to front
docker attach <Containerid>

# run cmd in a running container
docker exec [-d/i/t] <containerName> <cmd>


# get container ID, -a: all, -l: latest, none: now
docker ps [-l/-a]

# list all the images installed
docker images

# check details of an image/container
docker inspect <id>

# create images
# save changes, commit an container to an image, need the first 3 to 4 chars of the ID
docker commit <id> <username/imageName>
# create Dockerfile, then use docker build cmd to build new docker images
docker build -t="user/imagename:tag" <Dockerfile path>

# download image 
docker pull <username/imageName>
# release images
docker push <username/imageName>

# save images
docker save -o <output file> imageName

# load images
docker load --input <input file>

# remove images
docker rmi <imageName>

# remove container
docker rm <containerName>

# show processes inside a container
docker top <id>

# show port mapping
 docker port <id> [port]

# kill a runnning container
docker kill <container>

# e.g: rm all container: docker rm $(docker ps -a -q)

# start, stop, restart Container
docker start/stop/restart <Containerid>

# tag images
docker tag <id> <username/imagename:tags>
```

## Dockerfile
- use DSL to build new images
- `#` to comment
- `FROM` to use a base image
- `RUN` to exec a cmd
- `ADD` to cp local file to image
- `EXPOSE` to expose port
- `CMD` the cmd to run when init, only one cmd, otherwise the later will cover the preivous one; docker run will cover the CMD
- `ENTRYPOINT` 
- `VOLUME` set volume
- `ENV` set environment variable
- `WORKDIR` change working directory
- `ONBUILD` cmd to exec when this images become base image of other
- 每条指令都创建镜像的一层

## Private Registry
```
# step 1: run registry
sudo docker run -p 5000:5000 registry
# step 2: tag images
sudo docker tag <id> 127.0.0.1:5000/<name>
# step 3: push
sudo docker push 127.0.0.1:5000/<name>

# problem
# 修改Docker配置文件
vim /etc/default/docker
# 增加以下一行
DOCKER_OPTS="$DOCKER_OPTS --insecure-registry=104.131.173.242:5000"
# 重启Docker
sudo service docker restart
```

## Docker Compose
同时定义和使用多个容器的应用, 使用YAML文件来进行描述

```
# create and run containers
docker-compose up -d 
```

YAML(.yml)文件格式:
```
# demo
image: ubuntu
build: /path/to/build/directory
command: bundle exec thin -p 3000
links:
    - db
    - db:database
    - redis
ports:
    - "3000"
    - "9999:8080"
expose:
    - "3000"
    - "8080"
volumes:
    - /var/lib/mysql:/home/mysql
environment:
    RACK_ENV: /development
dns:
    - 8.8.8.8
    - 9.9.9.9
```
