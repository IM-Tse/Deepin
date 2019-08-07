1. 下载MySQL

    ```
    sudo apt install libmysqlclient-dev mysql-server mysql-client
    ```

2. 登录MySQL数据库

    ```
    mysql -u root -p 
    ```

3. 设置用户和密码

    ```
    grant all on *.* to root@'%' identified by '0919' with grant option;
    
    flush privileges;
    
    退出MySQL后重启
    service mysql restart
    ```

    

4. 设置MySQL数据库允许远程访问

    ```
    sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
    
    注释掉 bind-address = 127.0.0.1：
    ```

    