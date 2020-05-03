# Docker 下的一些有用的命令

## 1. 容器生命周期管理

1. 全部容器的启动、停止和删除

```
" 启动所有容器
docker start $(docker ps -aq)

" 停止所有容器
docker stop $(docker ps -aq)

" 删除所有容器
docker rm $(docker ps -aq)
```

2. 在指定容器中开启一个交互的终端（exec 命令）

```
docker exec -it 容器的ID或者名称 /bin/bash
```

## 2. 容器操作

1. 列出全部容器（ps 命令）

```
docker ps -a
```

2. 查看容器中运行的进程（top 命令）

```
docker top 容器的ID或者名称

" 查看所有运行容器的进程
for i in  `docker ps |grep Up|awk '{print $1}'`;do echo \ &&docker top $i; done
```

3. 链接容器（attach 命令）

```
docker attach 容器的ID或者名称
```

4. 列出指定容器的端口映射情况

```
docker port 容器ID或者名称
```

## 3. 容器rootfs命令

1. 从容器创建一个新的镜像（commit 命令）

```
docker commit -a "提交的作者名称" -m "提交时的说明" 容器名称或者
```

2. 容器和主机之间文件交换（cp 命令）

```
" 容器内复制到主机
docker cp 容器的ID或者名称:/path/of/container/file /path/of/host

" 主机复制到容器内
docker cp path/of/hostFile 容器的ID或者名称:/path/of/container
```

## 4. 镜像

1. 查找Docker Hub上的镜像（search 命令）

```
docker search --no-trunc 镜像名称
```

2. 移除本地镜像（rmi 命令）

```
docker rmi -f 镜像名称
```

3. 将指定镜像导出（save 命令）

```
docker save -o 镜像名称.tar 镜像名称
```

4. 导入镜像（load 命令）

```
docker load -i 待导入的镜像包.tar
```

