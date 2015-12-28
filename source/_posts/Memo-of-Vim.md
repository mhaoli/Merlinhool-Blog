title: vim相关
comment: true
date: 2014-12-27 11:59:55
categories: 文本编辑工具
tags: [Vim,memo]
---
RT 		
last updated：2015.05.02
<!--more-->

##编码问题
搭了静态的blog以后开始用markdown写文章，但是尝试了几天sublime以后准备换回vim...                 
于是设置utf-8。关于该问题，[详见这篇文章](http://edyfox.codecarver.org/html/vim_fileencodings_detection.html)。
```
set encoding=utf-8
set fileencoding=utf-8
```
但是，对于windows下的gvim，仅这样设置会出现命令提示，菜单等乱码问题...          
于是把所有东西设置为英文。
```
set langmenu=en_US
let $LANG = 'en_US'
source $VIMRUNTIME/delmenu.vim
source $VIMRUNTIME/menu.vim
```
<p align = "right">2014.12.27</p>

##《Vim 哲学四部全书》
今天在segmentfault上面读了这个系列的[文章](http://segmentfault.com/bookmark/1230000000761666)。		
感觉还是不错的，不过我并不觉得适合新手看，比较适合像我这样已经对vim基础操作比较熟悉的人。
<p align = "right">2015.01.01</p>

##vimrc中的单引号
vimrc中，使用setline函数的话内容需要用单引号括起来，对这部分内容含有单引号的每个地方都需要特殊处理————每次写两个单引号。

##filetype
vim能够自动识别filetype，但是不要被cpp和java误导了，这个filetype并不是文件的后缀，而是所用语言。比如说.hs文件的filetype为haskell。 		
查看当前文件的filetype，set filetype。

##tab
set expandtab 表示用空格代替tab，set noexpandtab时才是输入的tab。

##当前文件名
利用内置函数expand('%')获取当前文件名。可以用的修饰符：:p绝对路径，:t当前文件名，:r当前文件名去掉扩展名，:e当前文件的扩展名。 				
比如temp.java，expand('%:r') = temp，expand('%:e') = java，expand('%:t') = temp.java。