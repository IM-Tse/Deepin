# Deepin 安装VS code 开发版

此教程来自[官网](https://code.visualstudio.com/docs/setup/linux)，因为有时候打开官网比较慢，所以保存下载。

1. 安装秘钥配置软件源

    ```
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    
    sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
    
    sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
    ```

2. 更新软件源

    ```
    sudo apt-get install apt-transport-https
    sudo apt-get update
    ```

3. 安装

    ```
    # 如果想安装开发则将 code 替换为 code-insiders
    sudo apt-get install code
    ```

    

