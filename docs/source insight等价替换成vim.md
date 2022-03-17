# 四大功能界面
source insight（下面简写为SI）的四大功能界面：
1. 左边的函数列表界面      --- vim Taglist 插件 
2. 中间的编码界面
3. 右边的代码目录树界面    --- vim NERD Tree 插件
4. 最下面的代码预览界面    --- vim SrcExpl 插件

# 查找打开文件
SI 使用 `ctrl + o` 就可以打开后输入文件名
vim的 cscope插件使用 `cs find f filename` 可以等价替换
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


# 跳转到代码的定义处
SI的 jump to define 功能
vim的 taglist 插件的 `ctrl + ]` 可以等价替换，`ctrl + t` 可以跳回原来的位置
vim的 SrcExpl 插件也有功能可以实现 jump to define 功能， 把鼠标放在指定的变量
	上面, src expl界面会显示对应的定位位置，鼠标双击可以实现调整，空格可以跳回
	原来的位置

# 查找函数调用所有位置
SI的 lookup references 功能
vim的 cscope插件使用 `cs find c name` 可以等价替换
或者使用 vim的 vimgrep 功能来替换，可以查找后还能使用，具体命令如下:
```
- `vimgrep` /匹配模式/[g][j] 要搜索的文件/范围 
- `vim` 可作为 `vimgrep` 的缩写
- `!` 可紧随 `vimgrep` 之后，表示强制执行该命令
- 索引的关键字 `pattern` 放在了两个 `/` 中间，并且支持正则表达式
- `g`：表示是否把每一行的多个匹配结果都加入
- `j`：表示是否搜索完后定位到第一个匹配位置
- `g, j` 可选。 如果添加 `g`，将显示重复行， 如果添加 `j`，`Vim` 将不会自动跳转到第一个匹配的行（可能是别的文件）
- `file` 可以是正则文件名，也可以是多个确定的文件名
- `vimgrep /pattern/ %`       在当前打开文件中查找
- `vimgrep /pattern/ *`       在当前目录下查找所有
- `vimgrep /pattern/ **`      在当前目录及子目录下查找所有
- `vimgrep /pattern/ *.c`     查找当前目录下所有.c文件
- `vimgrep /pattern/ **/*`    只查找子目录

:cnext, :cn         # 当前页下一个结果 可以设置为快捷键，nmap <F5> :cp<cr> 
:cprevious, :cp     # 当前页上一个结果 可以设置为快捷键，nmap <F6> :cn<cr>
:clist, :cl         # 使用 more 打开 Quickfix 窗口
:copen, :cope, :cw  # 打开 Quickfix 窗口，列出所有结果
:ccl[ose]           # 关闭 Quickfix 窗口。
```