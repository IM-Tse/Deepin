链接：https://bbs.deepin.org/forum.php?mod=viewthread&tid=169824

1. #### 修改 ~/.profile 文件(不建议)

2. #### 新建 /etc/rc.local 文件(root用户)

    1. ```
        vim /etc/rc.local
        ```

    2. 模板

        ```
        #!/bin/sh -e
        #
        # rc.local
        #
        # This script is executed at the end of each multiuser runlevel.
        # Make sure that the script will "exit 0" on success or any other
        # value on error.
        #
        # In order to enable or disable this script just change the execution
        # bits.
        #
        # By default this script does nothing.
        # 在此处加入开机后要执行的命令
        # 是以root用户执行的
        
        exit 0
        ```

    3. 给脚本加上 755 权限

        ```
        sudo chmod +755 /etc/rc.local
        ```

    4. 调试脚本(可选)

        ```
        sudo /etc/rc.local # 使用 sudo 模拟 root 用户开机自启 /etc/rc.local 文件
        ```

3. #### ~/.config/autostart 文件夹(普通用户)

    1. 新建一个.desktop文件,丢进~/.config/autostart 文件夹下

    2. 模板

        ```
        [Desktop Entry]
        Name=<应用程序名>
        Type=Application
        Exec=<应用程序或脚本完整路径>
        Icon=<应用程序图标的完整路径>
        ```

        ```
        echo "your password" | sudo -S some command
        ```
        
        

