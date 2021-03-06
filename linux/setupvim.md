Title: 编辑器之神vim养成
Date: 2014-1-16
Modified: 2014-4-29
Tags: ubuntu, vim
Slug: setupvim

坐电脑面前，写文章敲代码，大部分时间是和编辑器交互的，所以编辑器效率高不高，好不好用体验都是最直接的。以前也试过Sublime
Text，不过没有上手。编辑器之神vim的大名倒是早有耳闻，不过陡峭的学习曲线也不是盖的，所以也一直不敢亵玩。倒是最近转到linux下面，整天泡在终端里不出来，vim来vim去的倒也慢慢的喜欢上了，昨天一咬牙，找了参考自己配置了一番，硬把原本不比windows下面记事本高端的玩意儿武装成了战斗机，最大的感受是，好玩！下面把我的配置写在这里，留作参考。

开始之前先说说我是怎么上手vim的。窃以为学习使用vim，一开始的生存阶段能否坚持下来是最重要的，而我一开始是从使用chrome的一个叫[Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb)的插件开始的。装上以后可以用vim的浏览模式看网页，所有操作都可以通过键盘执行，尤其是我经常包着笔记本又懒得带鼠标，简直吊且酷。这无疑是个不错的切入点，有不懂的按一下问号查帮助，很方便。等基本操作熟悉了以后再来学着用vim就自然的多。至于说明书、教程之类的网上很多，这里就不废话了。

#配置vim

vim的配置我认为在于两个方面，一是vim本身提供的各种设置选项，通过写配置文件`~/.vimrc`来调整，二是安装插件，这个就看想象力了。两者相结合，vim登神。

##注意事项

所有的命令都有两种设置生效的方法。比如你希望设置一下搜索的高亮匹配，首先你可以进入vim中，在normal模式下直接输入：

    :::vim
    :set hlsearch

`:`让你进入命令行模式，后面的`set hlsearch`则是具体的命令。在命令行中做的设置可以立刻生效，但随着你退出vim该设置也就被废弃了。

如果你希望某些设置每次进入vim都能生效，则需要第二种方法：直接编写`.vimrc`文件，也就是你vim的配置文件。具体方式是，在home下面新建名为`.vimrc`的文件，把你需要的配置命令直接写进去。还以搜索高亮为例，你可以直接写：

    :::vim
    set hlsearch

这里不需要`:`，只写想要的命令就行。这样，每次vim启动都会自动读取你的配置文件，并将里面的命令逐个运行一遍。

将所有配置都集中在一个文本文件里的好处是方便备份和转移，有了它随便给你一台装有vim的机器，只需要一个拷贝，就能立刻还原你熟悉的工作环境。另外人们也热衷于分享自己的配置文件，尤其是近年来github人气爆棚，很多开发者都将自己的配置文件（不仅仅是vim的）托管在上面，其中不乏一些大神级人物，只需要简单的搜索就能看到行内高人的配置文件，这听上去就很诱人。

但我不建议新手一上来就拿别人的配置做自己用，毕竟，那些所谓的配置、技巧，甚至花样繁多的插件都不过是锦上添花的东西，如果连其中最基本的命令的含义都搞不清楚，也不明白为什么要这么设置，贸然把别人上百行的配置文件拿过来除了让你更加的迷惑和沮丧以外，起不到任何正面的意义。

正确的做法是先去理解vim的设计哲学，熟悉最基本的操作，体会vim自身的强大。你作出的每一项设定都应该是实际需求驱动的，并应保持简单和明确。如此不断积累下来的配置文件才能真正为你所用，并发挥出应有的威力。

##一些最基本的设置

第一次在终端里打开vim的经历我至今记忆犹新，虽然被传的神乎其神（当然是真的），可看着没有经过配置的vim犹如石器时代穿越过来的界面我还是满心的怀疑。

我想这和linux的设计哲学有关，一开始只把最基本的东西给你，摒弃一切干扰，留出最大的定制空间，老手们觉得事情本该如此，但对新人来说却是个不大不小的障碍。

下面的一些基本配置主要目的是让光秃秃的vim变得友好一些，此外几乎每个vim的用户都会做出这些配置，所以仔细的了解一下很有必要。

如果你还记得前面提到的每个命令都有两种生效的方式，我希望你在将这些命令写进配置文件之前能在vim中切实地感受以下它的作用，只需简单的动手效果就超过我的千言万语。

----

第一件事是解开vim身上的封印

    :::vim
    set nocompatible

这条命令的意思是让vim不要和vi一个德行。vim本身是vi的增强版，默认情况下vim行为和vi保持一致，这意味着很多vim的强大特性是无效的，这条命令将释放出一个真正强大的vim出来。

---

    :::vim
    set mouse=a

这样做使得鼠标操作在vim中生效，主要方便浏览和选取。实际上你对vim掌握的越熟练，就越会发现，鼠标才是制约你操作效率的最大问题，所以我建议从一开始就放弃鼠标，专注于vim强大的功能。这里之所以有这么一条，完全是因为刚接触vim时有鼠标在手能安心很多。

---

    :::vim
    set scrolloff=3

scrolloff的意思是翻页时屏幕上下沿保留的部分，3表示三行，这么设置的结果是你在移动光标时还有三行到底的时候就开始翻动整个页面了。我这么说估计还是不清楚，所以你最好试一下，一看便知这是一个多么舒心的设定了。3行是个人比较喜欢的值，你也可以根据自己的喜好来改动。

---

    :::vim
    set nobackup
    set noswapfile

这两条加起来是要求vim不生成备份文件和临时文件。我的文档有其他的备份途径，不太操心丢失的问题，这里觉得烦就一关了事。


---

    :::vim
    set backspace=indent,eol,start

vim默认情况下的回删行为相当不人性，遇到缩进或者在行首无效。这样设定的结果令vim中回删的行为和一般的编辑器没有区别。


---

    :::vim
    set relativenumber number

严格来说这是两条命令。只设定`number`时vim会显示行号，只设定`relativenumber`时会显示相对行号，即以当前行为0行，向上向下1234依此排开。

vim的很多操作需要明确的行数，用相对行号则省了你还得多做一次减法的尴尬，所以我觉得更加实用一些。

至于这里把两个设定写在一行的效果则是当前行依旧显示其行号，上下两侧则是相对行号依次排开。该特性需要vim7.4版本的支持。

---

    :::vim
    set wildmenu

用于命令行补完，比如在命令行输入`:color`再按`<Tab>`键所有的备选色彩方案都会以列表的形式列出，按`<Tab>`可以切换。


---

    :::vim
    set ruler

在右下角显示光标当前的位置。


---

    :::vim
    set encoding=utf8

所有文件统一成utf8的编码。


---

    :::vim
    autocmd BufReadPost *
        \ if line("'\"") > 0 && line("'\"") <= line("$") |
        \   exe "normal g`\"" |
        \ endif

这一段可能看上去有些吓人，用了一些vim的脚本语言，大可不管它是如何工作的。

作用是打开vim时光标回到上次退出时的位置。这是个非常有用的特性，不知道为什么vim不能以更加简单的配置方式来实现，但不管如何这样确实管用。



---

下面几条主要和搜索匹配有关

    :::vim
    set hlsearch
    set incsearch

在nromal模式下键入`/`或`?`进入搜索模式，设定了`incsearch`后会实时匹配，设定了`hlsearch`后会高亮匹配到的结果。但是用过这个功能的也清楚，搜索完成以后高亮是不会自动消失的，很烦人，所以vim还有一个配套的命令：

    :::vim
    set nohlearch

字面上是取消高亮的意思，因为会和前面那条冲突，肯定不能写进配置文件，所以使用的话就是搜索完成以后在命令行模式里面输入一下，高亮就没了。这条命令也比较智能，其作用只是暂时的，下次再搜索依旧会高亮显示。

不过老这么输入命令一点也不酷啊，所以这里还有一个键盘映射，配合使用，效果拔群：

    :::vim
    nnoremap <CR> :nohlsearch<cr>

这条命令把normal模式下的回车键映射到`nohlsearch`上，具体的效果是你搜索完毕后按以下回车回到normal模式，再按以下回车高亮就没了。


    :::vim
    set ignorecase

令搜索时忽略大小写。输入大写字母很痛苦，我认为这样可以省很多事。

    :::vim
    set smartcase

输入大写字母时会严格匹配，输入小写时配合上一条也可以匹配大写。这两条可以根据自己的需要设置。


---

    :::vim
    set showmatch

光标移动到某个括号上时可以自动高亮配对的另一个，写代码时很方便。


---

下面几条和tab有关

    :::vim
    set expandtab

将`<Tab>`键换成空格。好像现在没人写程序还在用制表符了吧。

    :::vim
    set smarttab

在行首时插入`shiftwidth`规定的空格数，其他地方则插入`tabstop`规定的空格数。

    :::vim
    set shiftwidth=4
    set tabstop=4

大意是一个tab换成几个空格，我主要写python，所以都换成了4个。有些人偏爱2个一些。


---

下面几条和缩进有关

    :::vim
    set autoindent

顾名思义就是自动缩进的意思，新起一行时自动拷贝上一行的缩进。

    :::vim
    set smartindent

智能缩进，写代码时很贴心。


---

    :::vim
    set wrap

wrap的意思是比如你的窗口只有50列宽，当你一行内容超过50列时会自动折断另起一行显示，vim默认开启这个特性。而之所以这里提到这个是为了介绍真实行和显示行的区别。

所谓真实行在行尾有EOL的标记，最简单的判定方法就是看行号，行号不同的肯定是不同的两行。而上面通过wrap得到的两行只是为了看上去方便而故意显示成两行，实则还是一行，从行号上就能看出来。

---

    :::vim
    filetype on

打开后vim会自动侦测编辑的文件类型，常用的类型都有支持，上面的`smartindent`和`smarttab`等功能对此有依赖。


---

    :::vim
    syntax on

打开vim的高亮系统。写代码没高亮就太说不过去了。同样对文件侦测功能有依赖。vim自带了一些配色方案，可以在命令行模式下`:color <Tab>`查看选择。


##一些个人设置

下面有一些个人设定，主要是一些映射。

自己添加映射的结果实际上是改变了vim的操作方式，除非你有足够的理由，否则请不要这样做。理由有：vim默认的操作是经过精心设计和多年检测的，里面自有一套逻辑（当然也有不合逻辑的地方），贸然改动会带来很多意想不到的冲突和问题；vim的默认操作放之四海皆准，这也是vim的优势，你改动的越多，离这个标准就越远，等于自动放弃了这份普适性。

下面这些改动之所以存在，主要是因为用的太多，而原有的操作又太过反人类。你不需要照抄，但可以当成参考。



---

    :::vim
    let mapleader = '/'

vim里面有一个特殊的键叫`<Leader>`，特点是你可以自己定义它的值，经常在一些插件的操作中可以见到，很常用。它的默认值是`\`比如某个功能的快捷键是`<Leader>t`，可以先后按下`\` `t`来启用这个功能。

上面的命令则把`<Leader>`映射到`/`。常用的做法其实是映射到`,`，但`,`本身和`;`是一对互补的功能键，放弃太可惜，所以我更喜欢`/`一些。


---

    :::vim
    imap jj <Esc>

把insert模式中连按两次`j`映射到了`<Esc>`上，这绝对不是惯常的做法，但我觉得无比受用。

使用vim时最常见的操作恐怕就是在不同模式之间切换了，这其中`<Esc>`键意义重大，无奈位置太过偏远。

有人提倡把大小写键和ESC键对调，据我了解除了mac可以轻松做到这一点以外其他的系统都需要在底层做一些改动，或者需要键盘硬件的支持，我这里都不具备，况且即使可以我也会把大小写键换成ctrl的，所以必须另寻他法。

用连按两下`j`来代替ESC的好处是手不需要离开键盘最核心的位置就能完成操作，习惯后节奏也很好。缺点是偶尔会造成误操，鱼和熊掌不可兼得。


---

    :::vim
    imap kk <C-o>

这个映射比上面的更奇葩，不过同样受用。

`<C-o>`的意思是Ctrl和o的组合键，在insert模式下按`<C-o>`同样会回到normal模式，不同的是完成一个操作后会立刻返回insert模式。

我主要用它来跳出括号用。

情况大概是这样的，我在用一个叫Atuoclose的插件，效果是输入左括号会自动补上右括号，并且光标移动到括号中间供进一步的输入。但括号里面的内容编辑完想接着编辑括号外面的内容就比较麻烦了，直接回到normal模式vim会自动将光标往前移动一位，这样就不得不先右移一位再按`a`来接着编辑，用`<C-o>`则不存在光标自动往前移动一位的问题，跟着直接按`a`就能跳出括号接着编辑。

这种映射下虽然跳一个括号出来要按三次键，但胜在普适性好闭着眼也能操作，熟练之后节奏很棒。


---

    :::vim
    nmap Y y$

这个映射主要解决了一个vim默认设定不合逻辑的地方。

先看`d`这个操作，是剪切的意思，按`D`则会直接对光标当前的位置到行末执行剪切操作，等价于`d$`，`c`和`C`也有这样的性质，但唯独`Y`没有这个效果，那就只能自己补上了。

这里也是想说明，vim虽然操作繁多，但多数是成对出现功能互补的，并且背后有一些统领性的原则，有了这样的视角再去看vim，会发现逻辑清晰地多，记忆起来也不是那么困难了。



---

    :::vim
    nmap <C-j> <C-w>j
    nmap <C-k> <C-w>k
    nmap <C-h> <C-w>h
    nmap <C-l> <C-w>l

这一套映射简化了在分屏的不同窗口中移动光标的动作。分屏的所有操作都需要同时按下Ctrl和`w`键再配合其他按键，对我来说难度太大了。


---

    :::vim
    map j gj
    map k gk

希望你还记得前面提到的真实行和显示行的区别。vim中`j`和`k`的移动是基于真实行的，如果遇到几个显示行在一起的情况就会直接跳过去，让人有些摸不到头脑，`gj`和`gk`同样是上下移动，但基于显示行，这样映射一下操作起来顺畅很多。



---

下面几条主要是我针对不同文件类型的设定，供参考。

    :::vim
    autocmd FileType python set columns=90 lines=50

这条命令的意思是，如果编辑的文件是python脚本，那么自动将窗口设定为90列乘50行大小。

    :::vim
    autocmd FileType python set cul cuc colorcolumn=81

这里面主要有三个命令，`cul`和`cuc`分别是高亮光标所在行和所在列的意思，效果上看犹如一个十字准星，中心就是你的光标。

`colorcolum=81`表示高亮第81列，python不提倡一行的代码超过80列宽，所以设定了一条高亮的线供参考。

    :::vim
    autocmd BufNewFile *.py 0r /home/kevin/document/templates/python_header.template

这条命令的效果是用vim新建python脚本时自动套用后面的模板。模板内容随意，我的只有一行：

    :::python
    # -*- coding: utf8 -*-

接着是关于markdown的

    :::vim
    autocmd FileType markdown set columns=90 lines=50
    autocmd BufNewFile,BufRead *.md,*.mkdn,*.markdown :set filetype=markdown

我发现vim无法正确识别markdown的文件，后面一条命令可以纠正这一点。



##安装插件

安装插件的方法比较多，这里推荐用vundle，github项目主页在[这里](https://github.com/gmarik/vundle)。需要注意的是vundle需要git的支持。

###vundle的安装

把vundle从github上克隆下来：
    
    :::bash
    $ git clone https://github.com/gmarik/vundle.git ~/.vim/bundle/vundle

剩下的配置在`.vimrc`里写

    :::vim
    "Vundle vim的插件管理程序{
    """"""""
    filetype off
    set rtp+=~/.vim/bundle/vundle/
    call vundle#rc()
    " 让Bundle管理Vundle
    Bundle 'gmarik/vundle'
    """"""""以上为必须的部分

    filetype plugin indent on     " 必须的

这样vundle就配置好了，如果需要安装插件则可以在上面的语句后面添加如下的语句，我以安装`autoclose`这个插件为例

    :::vim
    Bundle 'AutoClose'

保存之后再打开一个vim的窗口，在命令行里输入`:BundleList`，可以看到你的插件列表，输入`:BundleInstall`就可以对列表里面的插件安装/升级了。

###插件来源

首先你可以去[vim-scripts.org](http://vim-scripts.org/vim/scripts.html)上搜搜看，现在插件作者们都在把自己的作品往这上面迁移，还是比较全的。找到心仪的插件后复制一下名字，在`.vimrc`后面添加语句
    
    :::vim
    Bundle '插件名'

按上面的步骤安装就好。

另外托管在github上的项目也是支持的，下面的两种写法都合法，注意名字中间不要有空格

    :::vim
    Bundle 'klen/python-mode'
    Bundle 'git://github.com/davidhalter/jedi-vim'
