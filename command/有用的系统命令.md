# Linux 下部分系统命令

如果前面有写系统名称则表示我是在该系统下实现，其他系统请自己百度

1. Deepin 查看开机启动项

    ```scss
    " 查看开机启动项
    systemctl list-unit-files
    
    " 允许开机启动
    systemctl enable 名称
    
    " 禁止开机启动
    systemctl disable 名称
    " 例如如果你装了VMWare，可以禁止下列启动项
    " 但是需要在用的时候手动输入 sudo /etc/init.d/vmware start
    systemctl disable vmware-USBArbitrator.service
    systemctl disable vmware-workstation-server.service
    systemctl disable vmware.service
    
    NetworkManager-wait-online.service
    ```

2. 挂载分区

    ```scss
    " 首先查看要挂载的分区
    sudo fdisk -l
    
    " 创建挂载目的文件夹
    mkdir /home/用户名/挂载文件夹
    " 挂载
    sudo mount /dev/sdc1 /home/用户名/挂载文件夹
    ```

3. 查看系统启动消耗的时间

    ```scss
    " 查看启动时各模块消耗的时间
    " (firmware) + (loader) + (kernel) + (userspace)
    systemd-analyze
    
    " 查看详细信息
    systemd-analyze blame
    ```

4. 清空内存的缓存（慎用）

    ```scss
    " 同步缓存,将缓存写到硬盘中去,清空缓存前先同步
    sync
    
    " 不释放缓存
    echo 0 > /proc/sys/vm/drop_caches
    
    " 释放页缓存,用来清空最近放问过的文件页面缓存
    echo 1 > /proc/sys/vm/drop_caches
    
    " 释放dentries和inodes,用来清空文件节点缓存和目录项缓存
    echo 2 > /proc/sys/vm/drop_caches
    
    " 释放所有缓存,用来清空1和2所有内容的缓存
    echo 3 > /proc/sys/vm/drop_caches
    ```

5. 强制清空回收站，用来删除无法在图形化回收站中进行删除的文件

    ```scss
    sudo rm -rf ~/.local/share/Trash/
    ```

6. Deepin 添加字体

    ```scss
    " 1. .ttc文件重命名为.ttf文件
    mv xx.ttc xx.ttf
    
    " 2. 拷贝到
    mv xx.ttf /user/share/fonts/truetype/
    
    " 3. 清空缓存或者重启
    fc-cache /user/share/fonts/truetype/
    ```

7. Centos7 开放防火墙端口

    ```scss
    " 开启端口
    firewall-cmd --zone=public --add-port=50000/tcp --permanent
    firewall-cmd --zone=public --add-port=50000/udp --permanent
    
    " 批量开启端口
    firewall-cmd --permanent --zone=public --add-port=30000-40000/tcp
    firewall-cmd --permanent --zone=public --add-port=30000-40000/udp
    
    " 关闭端口
    firewall-cmd --permanent --zone=public --remove-port=30000-40000/tcp
    firewall-cmd --permanent --zone=public --remove-port=30000-40000/udp
    
    " 重启防火墙
    firewall-cmd --reload
    
    " 查询端口是否开启
    firewall-cmd --query-port=50000/tcp
    
    " 查询哪些端口是开启的
    firewall-cmd --list-port
    ```

8. 查看占用内存前10的进程

      ```
    ps aux|head -1;ps aux|grep -v PID|sort -rn -k +4|head
      ```

9. CentOs7 查看系统内核

    ```scss
    " 查看内核
    rpm -qa | grep kernel
    cat /boot/grub2/grub.cfg |grep menuentry
    " 修改默认内核
    grub2-set-default 'CentOS Linux (4.17.4-1.el7.elrepo.x86_64) 7 (Core)'
    grub2-mkconfig -o /boot/grub2/grub.cfg
    " 删除多余内核
    使用yum remove 或rpm -e 删除多余内核
    ```

     

