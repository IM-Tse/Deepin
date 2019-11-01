1. 开机启动项

    ```scss
    " 查看开机启动项
    systemctl list-unit-files

    " 允许开机启动
    systemctl enable 名称

    " 禁止开机启动
    systemctl disable 名称

    systemctl disable vmware-USBArbitrator.service
    systemctl disable vmware-workstation-server.service
    systemctl disable vmware.service
    NetworkManager-wait-online.service
    ```

2. 挂载分区

    ```
    sudo fdisk -l
    mkdir /home/xyy/amber
    sudo mount /dev/sdc1 /home/xyy/amber
    ```

3. 查看系统启动时间

    ```scss
    systemd-analyze
    systemd-analyze blame
    ```

4. 解决安装 mysqlclient 失败

    ```scss
    sudo apt-get install libmysqlclient-dev
    ```

5. 清空缓存

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

6. 强制清空回收站

    ```scss
    sudo rm -rf ~/.local/share/Trash/
    ```

7. dpkg: 处理软件包 XXXX (--configure)时出错解决方法

    ```scss
    "  现将info文件夹更名
    sudo mv /var/lib/dpkg/info /var/lib/dpkg/info_old

    "  再新建一个新的info文件夹
    sudo mkdir /var/lib/dpkg/info
    "  不用解释了吧
    sudo apt-get update && apt-get -f install
    "  执行完上一步操作后会在新的info文件夹下生成一些文件，现将这些文件全部移到info_old文件夹下
    sudo mv /var/lib/dpkg/info/* /var/lib/dpkg/info_old
    "  把自己新建的info文件夹删掉
    sudo rm -rf /var/lib/dpkg/info
    "  把以前的info文件夹重新改
    sudo mv /var/lib/dpkg/info_old /var/lib/dpkg/info
    ```

8. subprocess.CalledProcessError: Command ‘(‘lsb_release’, ‘-a’)’ returned non-zero exit status 1.

    ```scss
    find / -name lsb_release
    rm -rf /usr/bin/lsb_release
    ```

9. 强制dpkg解锁

    ```scss
    sudo rm /var/cache/apt/archives/lock

    sudo rm /var/lib/dpkg/lock
    ```

10. 添加字体

    ```scss
    " 1. .ttc文件重命名为.ttf文件
    mv xx.ttc xx.ttf

    " 2. 拷贝到
    mv xx.ttf /user/share/fonts/truetype/

    " 3. 清空缓存
    fc-cache /user/share/fonts/truetype/
    ```

11. 修复图标

     ```
    sudo apt install --reinstall deepin-icon-theme
     ```

12. 修复WPS的PDF文件图标

      ```
    sudo rm /usr/share/mime/packages/wps-office-*.xml
    sudo update-mime-database /usr/share/mime
      ```

13. Centos7开放防火墙端口

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

14. 查看占用内存前10的进程

      ```
    ps aux|head -1;ps aux|grep -v PID|sort -rn -k +4|head
      ```

15. CentOs7查看系统内核

    ```
    " 查看内核
    rpm -qa | grep kernel
    cat /boot/grub2/grub.cfg |grep menuentry
    " 修改默认内核
    grub2-set-default 'CentOS Linux (4.17.4-1.el7.elrepo.x86_64) 7 (Core)'
    grub2-mkconfig -o /boot/grub2/grub.cfg
    " 删除多余内核
    使用yum remove 或rpm -e 删除多余内核
    ```
