## jupyter配置

1. 安装所需要的包

   ```
   pip install -i https://pypi.tuna.tsinghua.edu.cn/simple jupyterthemes
   
   conda install -c conda-forge jupyter_contrib_nbextensions
   ```

2. 执行命令

   ```
   jupyter contrib nbextension install --user --skip-running-check
   jupyter notebook --generate-config
   ```

3. 设置主题

   ```
   jt -t monokai -T -N -f fira -fs 12
   ```

4. 启用插件

5. 在 Jupyter 中使用 Anaconda 环境

   1. 在 Jupyter 所在 root 环境中安装以下包

      ```
      conda install nb_conda
      ```

   2. 在其他环境中安装以下包

      ```
      conda install ipykernel
      ```