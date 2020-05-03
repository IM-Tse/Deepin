1. 使用清华镜像

    ```scss
    " 使用清华镜像源
    pip install -i https://pypi.tuna.tsinghua.edu.cn/simple
    
    " conda 使用清华镜像源
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
    conda config --set show_channel_urls yes
    ```

2. conda环境

    ```scss
    " 导出环境
    pip freeze > ~/Desktop/1.txt
    conda list -e > requirements.txt
    conda env export > ai_project.yml
    
    " 安装环境
    pip install -r ~/Desktop/1.txt
    conda install --yes --file requirements.txt
    
    " 创建环境
    conda env create -f requirements.yml
    ```
    
3. 加入环境变量

    ```bash
    # >>> conda initialize >>>
    # 路径会有所不同, 注意按自己安装目录进行配置
    # !! Contents within this block are managed by 'conda init' !!
    __conda_setup="$('~/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
    if [ $? -eq 0 ]; then
        eval "$__conda_setup"
    else
        if [ -f "~/anaconda3/etc/profile.d/conda.sh" ]; then
            . "~/anaconda3/etc/profile.d/conda.sh"
        else
            export PATH="~/anaconda3/bin:$PATH"
        fi
    fi
    unset __conda_setup
    # <<< conda initialize <<<
    ```

    

4. jupyter

    ```
    pip install jupyter_contrib_nbextensions
    jupyter contrib nbextension install --user --skip-running-check
    
    " 如果出现No address associated with hostname
    修改ip为0.0.0.0
    ```
