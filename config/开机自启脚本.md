# Linux 开机启动脚本

用来设置需要开机启动的命令

参考链接：https://bbs.deepin.org/forum.php?mod=viewthread&tid=169824

1. #### 修改 ~/.profile 文件(不建议)

2. #### 新建 /etc/rc.local 文件(需 root 权限)

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
        # 应用程序名
        Name=
        # 数值为 Application 或者 Link，Application 表示指向一个应用程序，Link表示指向一个URL
        Type=Application
        # 应用程序或脚本完整路径
Exec=
        # 应用程序图标的完整路径
        Icon=
        
        
        # 以下内容为可选
        # 指明应用程序是否需要在终端中运行
        # Terminal=
        # 应用在启动器中的类别，多个类别用英文分号分隔
        # Categories=
        # 对应用程序的简单描述
        # Comment=
        # 只有在 Type 为 Link 时才有用
        # URL=
        
        # 参考链接
        # https://blog.csdn.net/liguangxianbin/article/details/86479653
        ```
        
