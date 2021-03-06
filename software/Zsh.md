# Linux系统下 zsh 终端的使用和配置

zsh 是一个比 bash 强大的终端，可以安装多种插件

1. 查看当前默认shell

    ```
    echo $SHELL
    ```

2. 查看是否有zsh

    ```
    cat /etc/shells
    ```

3. 安装zsh

    ```
    apt install zsh
    ```

4. 修改shell类型

    ```
    chsh -s /bin/zsh xyy
    
    另一种修改方式
    vim /etc/passwd
    ```

5. 安装oh-my-zsh

    ```
    wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
    ```

6. 复制zsh配置文件

    ```
    cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc=
    ```
    
7. 安装zsh-autosuggestions和zsh-syntax-highlighting

    ```
    cd ~/.oh-my-zsh/custom/plugins/
    
    git clone https://github.com/zsh-users/zsh-autosuggestions
    
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
    ```

    安装完成后记得在 .zshrc 中进行配置Plug

8. 一个终端主题配置文件---jtriley.zsh-theme

    ```
    #PROMPT='%{$fg_bold[red]%}➜ %{$fg_bold[green]%}%p %{$fg[cyan]%}%c %{$fg_bold[blue]%}$(git_prompt_info)%{$fg_bold[blue]%} % %{$reset_color%}'
    PROMPT="%{$fg_bold[cyan]%}%T%{$fg_bold[green]%} %{$terminfo[bold]$fg[green]%}%~ %{$fg_bold[yellow]%}➤ %{$reset_color%}"
    
    #ZSH_THEME_GIT_PROMPT_PREFIX="git:(%{$fg[red]%}"
    #ZSH_THEME_GIT_PROMPT_SUFFIX="%{$reset_color%}"
    #ZSH_THEME_GIT_PROMPT_DIRTY="%{$fg[blue]%}) %{$fg[yellow]%}✗%{$reset_color%}"
    #ZSH_THEME_GIT_PROMPT_CLEAN="%{$fg[blue]%})"
    
    ```

9. 将 .bashrc 中的一些自己环境变量移到.zshrc中

