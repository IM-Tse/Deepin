# 在服务器上搭建自己的私人网盘

下面是一些可用的命令


```scss
" 停止所有容器
docker stop $(docker ps -aq)

" 删除所有容器
docker rm $(docker ps -aq)

" 查看docker的磁盘使用情况
docker system df

" 清理磁盘, 删除关闭的容器, 无用的数据卷和镜像
docker system prune
```

## 1. 服务器安装Docker

**<u>需要服务器开放8000、8081和6800端口</u>**

1. Ubuntu

    - 安装以下包以使apt可以通过HTTPS使用存储库

    ```
    sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
    ```

    - 添加Docker官方的GPG密钥：

    ```
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

    - 使用下面的命令来设置**stable**存储库：

    ```
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

    - 再更新一下apt包索引：

    ```
    sudo apt-get update
    ```

    - 安装最新版本的Docker CE：

    ```
    sudo apt-get install -y docker-ce
    ```

    - 启动Docker服务

    ```
    service start docker
    ```

2. Centos

    - 安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的

    ```
    sudo yum install -y yum-utils device-mapper-persistent-data lvm2
    ```
    - 设置yum源
    ```
    sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
    ```
    - 可以查看所有仓库中所有docker版本，并选择特定版本安装
    ```
    yum list docker-ce --showduplicates | sort -r
    ```
    - 安装docker
    ```
    sudo yum install docker-ce
    #由于repo中默认只开启stable仓库，故这里安装的是最新稳定版17.12.0
    
    " 或者
    sudo yum install <FQPN> 
    # 例如：sudo yum install docker-ce-17.12.0.ce
    ```
    - 启动
    ```
    service start docker
    ```
    
3. Deepin

    - GPG

    ```
    curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
    ```

    - r

    ```
    sudo echo "deb [arch=amd64] https://mirrors.aliyun.com/docker-ce/linux/debian buster  stable" >> /etc/apt/sources.list.d/docker-ce.list
    ```

    - 更新软件源

    ```
    sudo apt update
    ```

    - 安装软件

    ```
    sudo apt-get install docker-ce docker-ce-cli containerd.io
    ```

    - 将普通用户组加入docker用户组，免ROOT使用

    ```
    sudo gpasswd -a ${USER} docker
    ```

## 2 . Filerun + AriaNg + Aria2

1. Run

    ```
    docker run --name=pan  -dti -p 8081:80 -p 6800:6800 jaegerdocker/pan
    ```

    ```
    docker run --name=pan -v /data/pan:/var/www/html/system/data/default_home_folder  -dti -p 8081:80 -p 6800:6800 jaegerdocker/pan
    ```

2. 访问地址

    ```
    Filerun:http://IP:8081
    登陆用户名:superuser 登陆密码:superuser
    
    AriaNg:http://IP:8081/dweb
    ```

3. 错误处理

    数据库报错:`Database error: SQLSTATE[HY000] [2002] No such file or directory` 解决方法:进入 docker，运行一下下面命令，然后再重启就好了

    ```
    chown -R mysql /var/lib/mysql
    chgrp -R mysql /var/lib/mysql
    ```

## 3. ownCloud

- 安装 ownCloud 和 MySQL 镜像

```
$sudo docker pull owncloud
$sudo docker pull mysql:5.7
```

- 启动MySQL容器

```
docker run --name owncloud-mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7
```

- 启动ownCloud容器

```
$sudo docker run --name owncloud -p 80:80 --link owncloud-mysql:db -d owncloud
```

- 初始化ownCloud

```
root
root
owncloud
db:3360
```

## 4. NextCloud + AriaNg + Aria2

- 下载资源

```
git clone https://github.com/wahyd4/aria2-ariang-x-docker-compose.git
```
- 启用NextCloud

```
cd aria2-ariang-x-docker-compose/nextcloud

docker-compose up -d
```
- 网址

```
Nextcloud： http://ip:8000
AriaNg：http://ip:8000/aria2/
```
- 配置NextCloud外部存储
    1. 进入应用(APP)
    2. 启用插件 External storage support （在禁用插件的列表中可以找到）
    3. 点击右上角 设置->管理->外部存储 进行添加外部存储,`Aria2`下载的文件会存在`/user-files/`目录下，存储类型选择本地存储，当存储添加成功，且可用时，最左端会显示出绿色。

##  5. Docker-Compose

**教程和仓库链接**：https://github.com/wahyd4/aria2-ariang-x-docker-compose

1. 安装 Docker Compose

    ```
    sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    ```

    ```
    sudo chmod +x /usr/local/bin/docker-compose
    ```

2. 下载安装配置文件

    ```
    git clone https://github.com/wahyd4/aria2-ariang-x-docker-compose.git
    ```

3. #### Filebrowser

    ```
     cd aria2-ariang-x-docker-compose/plex-filebrowser
     docker-compose up -d
    ```

    ```
    Filebrowser http://localhost
    AriaNg： http://localhost/ui
    Plex: http://localhost:32400
    ```

4. #### h5ai 

    ```
    cd aria2-ariang-x-docker-compose/h5ai
    docker-compose up -d
    ```

    ```
    查看文件h5ai： http://localhost:8000
    
    AriaNg： http://localhost:8000/aria2/
    ```

5. #### FileRun

    ```
    cd aria2-ariang-x-docker-compose/filerun
    docker-compose up -d
    ```

    ```
    " 下载翻译语言文件
    git clone https://github.com/filerun/translations.git
    ```

    ```
    文件管理Filerun, 请使用 superuser / superuser 进行登录： http://localhost:8000
    
    AriaNg： http://localhost:8000/aria2/
    ```

6. #### Nextcloud

    ```
    cd aria2-ariang-x-docker-compose/nextcloud
    docker-compose up -d
    ```

    ```
    文件管理Nextcloud： http://localhost:8000， 使用你喜欢的任意用户名和密码登录
    
    AriaNg： http://localhost:8000/aria2/
    ```
    
7. #### FileRun + h5ai + Filebrowser + Aria2

    1. docker-compose.yml(不能改名字)

        ```yml
        version: '2'
        
        services:
          db:
            image: mysql:5.7
            environment:
              MYSQL_ROOT_PASSWORD: filerun
              MYSQL_USER: filerun
              MYSQL_PASSWORD: filerun
              MYSQL_DATABASE: filerun
            restart: always
          web:
            depends_on:
              - db
            links:
              - db
            image: afian/filerun
            ports:
              - "8081:80"
            volumes:
              - "/home/YunPan:/user-files:rw"
            restart: always
          h5ai:
            image: ilemonrain/h5ai:full
            ports:
              - "8000:80"
            volumes:
              - "/home/YunPan/UserFiles/h5ai:/user-files:rw"
            restart: always
          aria2:
            image: wahyd4/aria2-ui
            links:
              - web:file-manager
            ports:
              - "8082:80"
              - "6800:6800"
              - "443:443"
            environment:
              - DOMAIN=:80
              # - SSL=true
              # - RPC_SECRET=Hello
              # - ARIA2_USER=admin
              # - ARIA2_PWD=password
              # - ENABLE_AUTH=true
            # volumes:
        	  # - /some_folder:/root/conf/key
              # - ~/test/aria2.conf:/root/conf/aria2.conf
        volumes:
              - "/home/YunPan/UserFiles:/user-files:rw"
              - "/home/YunPan/UserFiles/h5ai:/h5ai:rw"
              - "/home/YunPan/Downloads:/Downloads:rw"
        restart: always
        ```
    
    2. 进入到对应目录执行命令即可
    
        ```
        docker-compose up -d
        ```
    
        