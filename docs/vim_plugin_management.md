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
使用ctr 和两次w在侧窗口和主窗口之间进行切换

# 源码符号生成和快速定位插件 ctags
ctags工具是用来遍历源代码文件生成tags文件，
这些tags文件能被编辑器或其它工具用来快速查找定位源代码中的符号（tag/symbol），
如变量名，函数名等。比如，tags文件就是Taglist和OmniCppComplete工作的基础

## 安装方式

1.1 ubuntu安装命令 
`sudo apt-get install exuberant-ctags`

1.2 源码方式安装
1.2.1 从 http://ctags.sourceforge.net/ 下载源代码包后，解压缩生成源代码目录，
1.2.2 然后进入源代码根目录执行./configure，
1.2.3 然后执行make，
1.2.4 编译成功后执行make install。

## 基本功能使用方法
1.1  `$ ctags -R *`      ($ 为Linux系统Shell提示符)
	ctags -R *”：“-R”表示递归创建，也就包括源代码根目录（当前目录）下的所有子目录。
“*”表示所有文件。这条命令会在当前目录下产生一个“tags”文件，

当用户在当前目录中运行vi时，会自动载入此tags文件

Tags文件中包括这些对象的列表：

- 用#define定义的宏
- 枚举型变量的值
- 函数的定义、原型和声明
- 名字空间（namespace）
- 类型定义（typedefs）
- 变量（包括定义和声明）
- 类（class）、结构（struct）、枚举类型（enum）和联合（union）
- 类、结构和联合中成员变量或函数

1.2  `$ vi –t tag`       (请把tag替换为您欲查找的变量或函数名)
1.3  `:ts`               (ts 助记字：tags list, “:”开头的命令为VI中命令行模式命令)
1.4  `:tp`               (tp 助记字：tags preview)
1.5  `:tn`               (tn 助记字：tags next)
1.6  `ctrl + ]`          (跳转到定义处)
1.7  `ctrl + t`          (退回至跳转前)
1.8  `:ta x`             (跳转到符号x的定义处，如果有多个符号，直接跳转到第一处)
1.9  `:ts x`             (列出符号x的定义)
1.10 `:tj x`             (可以看做上面两个命令的合并，如果只找到一个符号定义，那么直接跳转到符号定义处，如果有多个，则让用户自行选择)

## 注意事项
 运行vim的时候，必须在“tags”文件所在的目录下运行。
 否则，运行vim的时候还要用“:set tag=”命令设定“tags”文件的路径，
 这样vim才能找到“tags”文件。在完成编码时，可以手工删掉tags文件

# 函数列表功能插件 taglist 
这里推荐一款vim的插件，可以查看当前文件的函数列表， 这个插件名为taglist
1. 要使用这款插件，首先需要安装ctags，具体安装使用命令参考上文

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
使用ctr 和两次w在侧窗口和主窗口之间进行切换

# cscope 插件
## 安装
`sudo apt-get install csope`

## 索引生成和使用
1. 在代码目录中，使用命令 `cscope -Rbq`

   其中cscope.out是基本的符号索引，后两个文件是使用"-q"选项生成的，可以加快cscope的索引速度。上面命令的参数含义如下：
```
   -R: 在生成索引文件时，搜索子目录树中的代码
   -b: 只生成索引文件，不进入cscope的界面
   -k: 在生成索引文件时，不搜索/usr/include目录
   -q: 生成cscope.in.out和cscope.po.out文件，加快cscope的索引速度
   -i: 如果保存文件列表的文件名不是cscope.files时，需要加此选项告诉cscope到哪儿去找源文件列表。可以使用"-"，表示由标准输入获得文件列表。
   -I dir: 在-I选项指出的目录中查找头文件
   -u: 扫描所有文件，重新生成交叉索引文件
   -C: 在搜索时忽略大小写
   -P path: 在以相对路径表示的文件前加上的path，这样，你不用切换到你数据库文件所在的目录也可以使用它了。
```

2. 添加cscope索引
`:cs add cscope.out `

## 相关功能
Cscope的功能通过它的子命令“find”来实现。

```
cs find c|d|e|g|f|i|s|t name

s：查找C代码符号
g：查找本定义
d：查找本函数调用的函数
c：查找调用本函数的函数
t：查找本字符串
e：查找本egrep模式
f：查找本文件
i：查找包含本文件的文件
　　可以在.vimrc中添加下面的快捷键，免得每次都要输入一长串命令。

nmap <C-@>s :cs find s <C-R>=expand("<cword>")<CR><CR>
nmap <C-@>g :cs find g <C-R>=expand("<cword>")<CR><CR>
nmap <C-@>c :cs find c <C-R>=expand("<cword>")<CR><CR>
nmap <C-@>t :cs find t <C-R>=expand("<cword>")<CR><CR>
nmap <C-@>e :cs find e <C-R>=expand("<cword>")<CR><CR>
nmap <C-@>f :cs find f <C-R>=expand("<cword>")<CR><CR>
nmap <C-@>i :cs find i ^<C-R>=expand("<cword>")<CR>$<CR>
nmap <C-@>d :cs find d <C-R>=expand("<cword>")<CR><CR>
　　使用时，将光标停留在要查找的对象上，按下<C-@>g，即先按Ctrl+@，然后很快再按g，将会查找该对象的定义。
```

# 源代码浏览器插件 SrcExpl 
它通过在单独的窗口中显示函数或类型定义或声明来为当前选定的关键字提供上下文。该插件旨在重新创建 IDE 中可用的上下文窗口

1. 下载插件源码
```
cd bundle
git clone https://github.com/air5005/SrcExpl.git
```

2. 修改vimrc配置文件
```
nmap <F7> :SrcExplToggle<CR>
let g:Srcexpl_winHeight = 8
" // Set 100 ms for refreshing the Source Explorer 
let g:SrcExpl_refreshTime = 100
" // Set "Enter" key to jump into the exact definition context 
let g:SrcExpl_jumpKey = "<ENTER>"
" // Set "Space" key for back  the definition context 
let g:SrcExpl_gobackKey = "<SPACE>"
let g:SrcExpl_isUpdateTags = 0
```

3. 命令定义
用F8快捷键打开或者关闭预览窗口
回车跳转到定义的文本
空格跳转回来


# Trinity 插件
trinity插件主要是用来同时管理 SrcExpl, Taglist and NERD Tree 三个插件的

1. 下载插件源码
```
cd bundle
git clone https://github.com/air5005/Trinity.git
```

2. 修改vimrc配置文件
```
" Open and close all the three plugins on the same time 
nmap <F8>  :TrinityToggleAll<CR> 

" Open and close the Source Explorer separately 
nmap <F9>  :TrinityToggleSourceExplorer<CR> 

" Open and close the Taglist separately 
nmap <F10> :TrinityToggleTagList<CR> 

" Open and close the NERD Tree separately 
nmap <F11> :TrinityToggleNERDTree<CR> 
```

3. 命令定义
用F8可以同时打开、关闭三个插件
F9  打开、关闭SrcExpl
F10 打开、关闭Taglist
F11 打开、关闭NERD Tree

# 相关链接
https://github.com/air5005/vimhandbook.github.io
https://github.com/air5005/vim-pathogen
https://github.com/air5005/nerdtree
https://github.com/air5005/taglist
https://github.com/air5005/vim_install
ctags官网 http://ctags.sourceforge.net/
cscope官网 http://cscope.sourceforge.net/
https://www.cnblogs.com/linux-sir/p/4675919.html
https://github.com/air5005/SrcExpl
https://www.cnblogs.com/ims-/p/9825968.html
https://github.com/air5005/Trinity