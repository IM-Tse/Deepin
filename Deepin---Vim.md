- [ ] ##  1. 安装Vim

1. 安装依赖包

    1. Ubuntu/Deepin

    ```
    sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev libgtk2.0-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev ruby-dev liblua5.1 lua5.1-dev libperl-dev git
    ```

2. 创建文件夹

    ```
    sudo mkdir /usr/local/vim8
    ```

3. 下载Vim源码

    ```
    git clone https://github.com/vim/vim.git
    
    cd vim/src
    ```

4. 配置

    ```
    ./configure --with-features=huge \
        --enable-multibyte \
        --enable-rubyinterp=yes \
        --enable-python3interp=yes \
        --with-python3-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu/ \
        --enable-perlinterp=yes \
        --enable-luainterp=yes \
        --enable-gui=gtk2 \
        --enable-cscope \
        --prefix=/usr/local/vim8/
    ```

    开启支持python3路径，有些系统可不需要填写，会自动搜索

    ```
    --with-python3-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu/ 
    ```

    安装路径

    ```
    --prefix=/usr/local/vim8/
    ```

5. 编译安装

    ```
    sudo make && make install
    ```

6. 创建软连接

    ```
    sudo ln -s /usr/local/vim8/bin/vim /usr/bin/
    ```

- [ ] ## 2. 配置Vim

1. 创建文件夹

    ```
    mkdir ~/.vim
    mkdir ~/.vim/autoload
    mkdir ~/.vim/plugged
    mkdir ~/.vim/plugin
    mkdir ~/.vim/colors
    ```

2. 安装Vim-Plug

    ```
    cd ~/.vim/autoload/
    
    wget https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
    ```

3. 编写配置文件.vimrc

    ```
    vim ~/.vimrc
    ```

- [ ] ## 3. 安装插件

1. YouCompleteMe

    ```
    Plug 'Valloric/YouCompleteMe'
    ```

    配置信息

    ```vbscript
    """""""""""""""""""""""""""""""""""
    "	YouCompleteMe:语句补全插件配置	 "
    """""""""""""""""""""""""""""""""""
    set runtimepath+=~/.vim/plugged/YouCompleteMe
    " 让Vim的补全菜单行为与一般IDE一致(参考VimTip1228)
    set completeopt=longest,menu
    " 离开插入模式后自动关闭预览窗口"
    autocmd InsertLeave * if pumvisible() == 0|pclose|endif
    " 开启 YCM基于标签引擎
    let g:ycm_collect_identifiers_from_tags_files = 1
     " 注释与字符串中的内容也用于补全
    let g:ycm_collect_identifiers_from_comments_and_strings = 1
    let g:syntastic_ignore_files=[".*\.py$"]
    " 语法关键字补全
    let g:ycm_seed_identifiers_with_syntax = 1
    let g:ycm_complete_in_comments = 1
    " 关闭加载.ycm_extra_conf.py提示
    let g:ycm_confirm_extra_conf = 0
    " 映射按键,没有这个会拦截掉tab, 导致其他插件的tab不能用.
    let g:ycm_key_list_select_completion = ['<c-n>', '<Down>']
    let g:ycm_key_list_previous_completion = ['<c-p>', '<Up>']
    " 在注释输入中也能补全
    let g:ycm_complete_in_comments = 1
    " 在字符串输入中也能补全
    let g:ycm_complete_in_strings = 1
    " 注释和字符串中的文字也会被收入补全
    let g:ycm_collect_identifiers_from_comments_and_strings = 1
    let g:ycm_global_ycm_extra_conf='~/.vim/plugged/YouCompleteMe/third_party/ycmd/cpp/ycm/.ycm_extra_conf.py'
    " 禁用语法检查
    let g:ycm_show_diagnostics_ui = 0
    " 回车即选中当前项
    inoremap <expr> <CR> pumvisible() ? "\<C-y>" : "\<CR>"
    " 跳转到定义处
    nnoremap <c-j> :YcmCompleter GoToDefinitionElseDeclaration<CR>
    " 从第1个键入字符就开始罗列匹配项
    let g:ycm_min_num_of_chars_for_completion=1
    
    ```

2. 状态栏

    ```
    Plug 'vim-airline/vim-airline'
    ```

    配置

    ```vbscript
    """"""""""""""""""
    "	airline配置	"
    """"""""""""""""""
    
    "vim-airline配置:优化vim界面"
    let g:airline#extensions#tabline#enabled = 1
    " 显示颜色
    set t_Co=256
    set laststatus=2
    " 使用powerline打过补丁的字体
    let g:airline_powerline_fonts = 1
    " 开启tabline
    let g:airline#extensions#tabline#enabled = 1
    " tabline中当前buffer两端的分隔字符
    let g:airline#extensions#tabline#left_sep = ' '
    " tabline中未激活buffer两端的分隔字符
    let g:airline#extensions#tabline#left_alt_sep = ' '
    " tabline中buffer显示编号
    let g:airline#extensions#tabline#buffer_nr_show = 1
    " 映射切换buffer的键位
    nnoremap [b :bp<CR>
    nnoremap ]b :bn<CR>
    " 映射<leader>num到num buffer
    map <leader>1 :b 1<CR>
    map <leader>2 :b 2<CR>
    map <leader>3 :b 3<CR>
    map <leader>4 :b 4<CR>
    map <leader>5 :b 5<CR>
    map <leader>6 :b 6<CR>
    map <leader>7 :b 7<CR>
    map <leader>8 :b 8<CR>
    map <leader>9 :b 9<CR>
    ```

3. 函数标签

    ```
    Plug 'ludovicchabant/vim-gutentags'
    ```

    下载依赖

    ```
    sudo apt-get install exuberant-ctags
    
    下载taglist，解压到 ~/.vim 文件夹中
    http://vim-taglist.sourceforge.net/index.html
    ```

    配置信息

    ```vbscript
    
    """""""""""""""""""""""""
    "	显示函数	"
    """""""""""""""""""""""""
    
    " gutentags搜索工程目录的标志，碰到这些文件/目录名就停止向上一级目录递归 "
    "let g:gutentags_project_root = ['.root', '.svn', '.git', '.project']
    
    " 所生成的数据文件的名称 "
    "let g:gutentags_ctags_tagfile = '.tags'
    
    " 将自动生成的 tags 文件全部放入 ~/.cache/tags 目录中，避免污染工程目录 "
    "let s:vim_tags = expand('~/.cache/tags')
    "let g:gutentags_cache_dir = s:vim_tags
    " 检测 ~/.cache/tags 不存在就新建 "
    "if !isdirectory(s:vim_tags)
    "   silent! call mkdir(s:vim_tags, 'p')
    "endif
    
    " 配置 ctags 的参数 "
    let g:gutentags_ctags_extra_args = ['--fields=+niazS', '--extra=+q']
    let g:gutentags_ctags_extra_args += ['--c++-kinds=+pxI']
    let g:gutentags_ctags_extra_args += ['--c-kinds=+px']
    
    " F3快捷键显示taglist窗口
    map <F3> :TlistToggle<CR>
    " taglist窗口出现在右侧，缺省显示在左侧
    let Tlist_Use_Right_Window=1
    " 不同时显示多个文件的tag，只显示当前文件的
    let Tlist_Show_One_File=0
    " taglist窗口是最后一个窗口时退出Vim
    let Tlist_Exit_OnlyWindow=1
    " 设置窗口的宽度
    let Tlist_WinWidth=25
    " 指定你的Exuberant ctags程序的位置,没在你PATH变量所定义的路径中，需要使用此选项设置一下
    let Tlist_Ctags_Cmd='/usr/bin/ctags'
    " 打开taglist窗口时，输入焦点在taglist窗口中
    let Tlist_GainFocus_On_ToggleOpen=1
    " 单击tag就跳转,缺省情况下双击跳转
    let Tlist_Use_SingleClick=1
    " 选择了tag后自动关闭taglist窗口
    let Tlist_Close_On_Select=1
    " 当同时显示多个文件中的tag时，只显示当前文件tag，其它文件的tag都被折叠起来
    let Tlist_File_Fold_Auto_Close=1
    " 始终解析文件中的tag，不管taglist窗口有没有打开
    let Tlist_Process_File_Always=1
    ```

4. FZF

    ```
    gem install rouge
    gem install coderay
    ```

    