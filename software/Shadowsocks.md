# Linux 下使用富强 SS 

此方法在没有 Linux 客户端的情况下可用

1. Shadowsocks 配置文件

    ```json
    {
        "server":"ip地址",
        "server_port": 服务器端口,
        "local_address": "127.0.0.1",
        "local_port":1080,
        "password":"密码",
        "timeout":300,
        "method":"加密方式"
    }
    ```

2. 使用Shadowsocks代理

    先安装 pip 或 Anaconda

    ```scss
    pip install shadowsocks
    " 安装完后需要修改openssl中的两处cleanup为reset
    " 不知道文件在哪里可以先运行一下,根据输出错误提示修改
    
    sslocal -c /etc/shadowsocks.json
    ```

3. 终端代理

    1. 安装 proxychains

        ```scss
        sudo apt install proxychains
        ```
        
    2. 修改配置文件

        sudo vim /etc/proxychains.conf

        ```
        (上面内容省略)
        ...
        ...
        [ProxyList]
        # add proxy here ...
        # meanwile
        # 配置以下内容
        socks5 	127.0.0.1 1080
        ```

    3. 使用，在要使用的命令前面加上 proxychains 即可

        如：proxychains git clone 

4. 终端代理另一种方式，不一定好使

    ```bash
    " 在代理命令前使用,仅对部分命令有效
    " 例如: proxy git clone https://github.com/nlpinaction/learning-nlp.git
    alias proxy='ALL_PROXY=socks5://127.0.0.1:1080'
    
    " 临时全局代理,关闭终端失效
    alias setproxy='export ALL_PROXY=socks5://127.0.0.1:1080'
    
    " 取消代理
    alias unsetproxy='unset ALL_PROXY'
    
    " Chrome使用的是proxy-server代理
    google-chrome-stable --proxy-server="socks5://127.0.0.1:1080"生成PAC文件
    ```

5. Pac 代理

    1. 安装 genpac

        ```
        pip install genpac
        ```

    2. 生成 Pac 文件

        ```
        genpac --pac-compress --pac-proxy 'SOCKS5 127.0.0.1:1080' --format pac  -o ~/autoproxy.pac
        " 或者
        genpac --proxy="SOCKS5 127.0.0.1:1080" --gfwlist-proxy="SOCKS5 127.0.0.1:1080" -o ~/autoproxy.pac --gfwlist-url="https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt"
        ```

    3. 在应用代理自动模式设置

        ```
        file:///home/用户名/autoproxy.pac
        ```