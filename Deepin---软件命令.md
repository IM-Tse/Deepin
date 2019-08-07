
3. 解决百度网盘启动不了

    ```scss
    sudo rm -rf ~/baidunetdisk ~/.config/baidunetdisk
    ```

4. 使用 Shadowsocks

    ```scss
    pip install shadowsocks
    " 安装完后需要修改openssl中的两处cleanup为reset
    " 不知道文件在哪里可以先运行一下,根据输出错误提示修改
    
    sslocal -c /etc/shadowsocks.json
    ```

5. 编译C++文件

    ```scss
    g++ a.cpp -o a.out
    gdb a.out
    ```

6. Python调试

    ```scss
    python -m pdb aa.py
    ```

    











