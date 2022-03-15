# 安装vim的插件管理工具
1. 在~/.vim 目录下创建以下三个目录
```
drwxr-xr-x 1 ych ych 512 Mar 15 15:32 ./
drwxr-xr-x 1 ych ych 512 Mar 15 15:32 ../
drwxrwxr-x 1 ych ych 512 Mar 15 15:26 autoload/
drwxrwxr-x 1 ych ych 512 Mar 15 15:31 bundle/
drwxrwxr-x 1 ych ych 512 Mar 15 15:25 doc/
```

2. 进入到bundle文件夹（以后的插件都放在这里统一管理）下
```
cd bundle
git clone https://github.com/air5005/vim-pathogen.git
```

3. 此时可以在bundle文件夹下看到vim-pathogen文件夹， 
进入里面的autoload目录， 将里面的pathogen.vim拷贝到 .vim/autoload路径下面， 
并且在修改用户路径下的.vimrc文件， 在最后添加一行 `call pathogen#infect()` 即可

至此， 插件管理工具的安装到此结束！！！

# 管理目录结构插件 nerdtree 
1. 下载插件源码
```
cd bundle
git clone https://github.com/air5005/nerdtree.git
```
2. 增加vim快捷键

此时再次修改用户目录下的.vimrc文件， 在最后添加
```
map <F3> : NERDTreeMirror<CR>
map <F3> : NERDTreeToggle<CR>
```
即可用F3键实现快速打开和关闭目录结构的功能

# 函数列表功能插件 taglist 
这里推荐一款vim的插件，可以查看当前文件的函数列表， 这个插件名为taglist
1. 要使用这款插件，首先需要安装ctags，可以使用如下命令来安装：
`sudo apt-get install exuberant-ctags`
2. 下载插件源码
```
cd bundle
git clone https://github.com/air5005/taglist.git
```
3. 拷贝taglist文件到vim
```
cd taglist
cp -a autoload ~/.vim/
cp -a doc ~/.vim/
cp -a plugin ~/.vim/
```
4. 修改vimrc配置文件
```
" taglist
let   Tlist_Inc_Winwidth=0           " 配置打开函数列表的时候不改变窗口大小
let   Tlist_Use_Right_Window=1       " 配置函数列表挂靠在屏幕右手边
let   Tlist_File_Fold_Auto_Close=1   " 配置自动关闭非活动的文件
let   Tlist_Exit_OnlyWindow=1        " 配置当前只有函数列表窗口的时候退出vim
map <F4> :TlistToggle<cr>            " 快捷键F4切换函数列表
```

# 相关链接
https://github.com/air5005/vimhandbook.github.io
https://github.com/air5005/vim-pathogen
https://github.com/air5005/nerdtree
https://github.com/air5005/taglist