# Vim 安装

安装支持 python 的Vim，因为有些插件需要 vim 支持 Python

##  1. 手动编译安装 Vim

1. 安装依赖包

    1. Ubuntu/Deepin

    ```
    sudo apt-get install libncurses5-dev python-dev python3-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev
    ```

2. 创建安装文件夹

    ```
    sudo mkdir /usr/local/vim8
    ```

3. 下载Vim源码

    ```
    git clone https://github.com/vim/vim.git

    cd vim
    ```

4. 配置

    ```
    ./configure --with-features=huge \
        --enable-multibyte \
        --enable-rubyinterp=yes \
        --enable-python3interp=yes \
        --enable-perlinterp=yes \
        --enable-luainterp=yes \
        --enable-gui=gtk2 \
        --enable-cscope \
        --prefix=/usr/local/vim8/
    ```
    

开启支持python3路径，有些系统可不需要填写，会自动搜索
    
```
    --with-python3-config-dir=
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
    
7. 验证是否开启 Python 支持

    ```
    vim --version
    ```

## 2. 配置Vim

1. 创建文件夹

    ```
    mkdir ~/.vim
    mkdir ~/.vim/autoload ~/.vim/plugged ~/.vim/plugin ~/.vim/colors
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
    
4. 配置文件

    ```
    """""""""""""""""""""""""
    "    插件管理
    """""""""""""""""""""""""
    call plug#begin('~/.vim/plugged')
    
    " 在这里设置安装插件
    
    call plug#end()
    
    
    
    """""""""""""""""""""""""
    "    Vim设置
    """""""""""""""""""""""""
    " 显示行号
    set number
    " 光标所在行高亮
    set cursorline
    " 自动换行
    set wrap
    set linebreak
    " 显示状态栏,0-不显示，1-只在多窗口显示，2-显示
    set laststatus=2
    " 设置在状态栏显示的信息
    set foldcolumn=0
    set foldmethod=indent 
    set foldlevel=3 
    set foldenable
    " 不要使用vi的键盘模式，而是vim自己的
    set nocompatible
    " 自动缩进
    set autoindent
    set cindent
    " Tab键的宽度
    set tabstop=4
    " 统一缩进为4
    set softtabstop=4
    set shiftwidth=4
    " 不要用空格代替制表符
    set noexpandtab
    " 在行和段开始处使用制表符
    set smarttab
    " 语法高亮
    set syntax=on
    " 去掉输入错误的提示声音
    set noeb
    " 在状态栏显示光标的当前位置
    set ruler
    " 支持使用鼠标
    set mouse=a
    " 字符编码
    set encoding=utf-8
    set fencs=utf-8,ucs-bom,shift-jis,gb18030,gbk,gb2312,cp936
    " 语言设置
    set langmenu=zh_CN.UTF-8
    set helplang=cn
    " 我的状态行显示的内容（包括文件类型和解码）
    set statusline=%F%m%r%h%w\ [FORMAT=%{&ff}]\ [TYPE=%Y]\ [POS=%l,%v][%p%%]\ %{strftime(\"%d/%m/%y\ -\ %H:%M\")}
    set statusline=[%F]%y%r%m%*%=[Line:%l/%L,Column:%c][%p%%]
    " 出错发出提示,屏幕闪烁
    "set visualbell
    " 记住历史操作数
    set history=1000
    " 自动格式化
    set formatoptions=tcrqn
    " 禁止生成临时文件
    set nobackup
    set noswapfile
    " 搜索忽略大小写
    set ignorecase
    " 搜索字符高亮
    set hlsearch
    set incsearch
    " 行内替换
    set gdefault
    " 命令行（在状态行下）的高度，默认为1，这里是2
    set cmdheight=2
    " 侦测文件类型
    filetype on
    " 不要生成swap文件，当buffer被丢弃的时候隐藏它
    setlocal noswapfile
    " 载入文件类型插件
    filetype plugin on
    " 为特定文件类型载入相关缩进文件
    filetype indent on
    " 保存全局变量
    set viminfo+=!
    " 带有如下符号的单词不要被换行分割
    set iskeyword+=_,$,@,%,#,-
    " 字符间插入的像素行数目
    set linespace=0
    " 增强模式中的命令行自动完成操作
    set wildmenu
    " 使回格键（backspace）正常处理indent, eol, start等
    set backspace=2
    " 允许backspace和光标键跨越行边界
    set whichwrap+=<,>,h,l
    " 可以在buffer的任何地方使用鼠标（类似office中在工作区双击鼠标定位）
    set mouse=a
    set selection=exclusive
    set selectmode=mouse,key
    " 通过使用: commands命令，告诉我们文件的哪一行被改变过
    set report=0
    " 在被分割的窗口间显示空白，便于阅读
    set fillchars=vert:\ ,stl:\ ,stlnc:\
    " 高亮显示匹配的括号
    set showmatch
    " 匹配括号高亮的时间（单位是十分之一秒）
    set matchtime=1
    " 光标移动到buffer的顶部和底部时保持3行距离
    set scrolloff=3
    " 为C程序提供自动缩进
    set smartindent
    " 高亮显示普通txt文件（需要txt.vim脚本）
    au BufRead,BufNewFile *  setfiletype txt
    
    " 开启文件类型检查
    filetype plugin indent on 
    "打开文件类型检测, 加了这句才可以用智能补全
    set completeopt=longest,menu
    
    
    
    """""""""""""""""""""""""
    "    其他设置
    """""""""""""""""""""""""
    " 去除乌干达
    set shortmess=atI
    
    
    " 设置主题，得自己先下载主题
    "colorscheme molokai
    "colorscheme flattened_dark
    "colorscheme flattened_light
    "colorscheme janah
    "colorscheme jellybeans
    "colorscheme railscasts
    "colorscheme solarized
    ```

    

## 3. 安装插件

1. YouCompleteMe

    ```
    Plug 'Valloric/YouCompleteMe'
    
    " 如果编译时出现: No CMAKE_CXX_COMPILER could be found. 执行下面命令
    sudo apt-get install build-essential
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

    一个大坑，不要配置了
    
    ```
    sudo gem install rouge coderay
    ```
