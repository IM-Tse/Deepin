1. 使用Shadowsocks代理

    ```scss
    pip install shadowsocks
    " 安装完后需要修改openssl中的两处cleanup为reset
    " 不知道文件在哪里可以先运行一下,根据输出错误提示修改
    
    sslocal -c /etc/shadowsocks.json
    ```

2. 终端代理

    1. 在.zshrc文件中加入一下内容

        ```scss
        " 在代理命令前使用,仅对部分命令有效
        " 例如: proxy git clone https://github.com/nlpinaction/learning-nlp.git
        alias proxy='ALL_PROXY=socks5://127.0.0.1:1080'
        
        " 临时全局代理,关闭终端失效
        alias setproxy='export ALL_PROXY=socks5://127.0.0.1:1080'
        
        " 取消代理
        alias unsetproxy='unset ALL_PROXY'
        
        " Chrome使用的是proxy-server代理
        google-chrome-stable --proxy-server="socks5://127.0.0.1:1080"
        ```

        

    
