Title: 利用Pelican和Github简单迅速地搭建自己的博客
Date: 2013-12-14
Modified: 2013-12-15
Tags: how to, pelican, github, git, markdown, blog
Slug: build_your_blog


#思路

一般而言，搭建一个独立博客需要三样东西：

- 博客软件
- 托管服务器
- 独立的域名

博客软件用来生成你的博客页面，而生成好的页面则需要放到托管的服务器上才能被别人看到。

##博客软件

这里我选择`Pleican`作为博客软件主要是出于以下的考虑：

- 基于`Python`，简单易上手
- 生成静态页面，不需要数据库，访问速度快，易于维护
- 支持`markdown`标记语言

和著名的`wordpress`相比，`pelican`搭建起来的博客功能和界面会相对单薄一些，但对于我来说绝对够用，况且写博客的初衷也是想把注意力放在内容上，所以工具越简单反而越好。


##托管服务器

这里选择`github`的原因也很简单：

- 免费
- 省事
- 可以直接用`git`进行版本管理

##磨刀

这份教程中提到的方法虽然简单，但仍旧需要你有一些基础，主要有

####1.`python`基础

你至少应该能够配置`python`的环境，能够顺利的安装`python`的插件,了解一些简单的`python`语法。

####2.了解`Markdown`

如果你没听说过也不要紧，[这里](http://joinwee.com/lesson/10/)有一份简短的介绍，详细的语法说明则可以在[这里](http://wowubuntu.com/markdown/)找到。

####3.对`git`/`github`有所了解

如果不了解也同样没有关系，[这个](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)一站式的教程可以帮到你。

这里多说一点。`git`本身就是追踪文本的系统，虽然设定上是给程序做版本管理的，但未尝不能拿来管理文章。甚至，我相信`git`+`markdown`等轻量级标记语言代表了一种写作的未来。

---

#动手

这里提一下，我的配置环境是ubuntu13.04。windows则需要多一些折腾，请自行google。

##安装`Pelican`

这里假设你已经安装好了python2.x的环境，并装好了`pip`。可以直接用下面的命令安装`pelican`

	pip install pelican

要使用`markdown`，还需要一个`markdown`的支持

	pip install markdown

##首次配置

选定一个目录存放你的博客文件，我的叫`blog`

	mkdir blog
	cd blog

在你的`blog`目录下使用命令

	pelican-quickstart

接下来会询问你一系列问题，除了名字等必须要填的，其他建议使用默认值，随后还可以通过配置`pelicanconf.py`文件进行修改。

运行结束之后会生成的目录结构

	blog/
	├── content
	│   └── (pages)
	├── output
	├── develop_server.sh
	├── Makefile
	├── pelicanconf.py     
	└── publishconf.py

`pelican`的逻辑是，你把写好的用markdown写好的纯文本文档放进`content`这个目录下面，运行程序，就可以将你的整个博客页面生成到`output`中去了。

至此，文件系统部分已经配置完成了，接下来可以试着写一篇文档了

##第一篇博文

创建一个叫`first.md`的文档放到`content`目录下。`Pelican`对内容的格式有些要求，每一篇博文的开头都应该是这样的：

	Title: 第一篇博客
	Date: 2013-12-12 10:16
	Category: 测试
	Tags: 心情
	Author: 煎挠橙 

	这里开始可以书写正文了
	blabla....

所以你应该看明白了，必须要通过每篇博文开头的部分来告诉`pelican`这篇文章的标题、标签、分类等信息，以便最终呈现在博客页面上。其中，标题、时间是必填的，如果缺失则会被`pelican`忽略掉。

##生成页面

写完你的第一篇博文后，你应该还在`content`目录下，先回到blog根目录下

	cd ..

使用下面的命令`pelican`系统会将你放在`content`目录下的`.md`文档转换成网页文件

	make html

当然，你也可以让`pelican`在每次检测到文件变化的时候都重新生成一次网页，使用下面的命令

	make regenerate

实际上此时如果你去`output`目录下就会看到生成的页面已经躺在那里了，但为了方便本地的调试，你可以用下面的命令开启一个本地的服务器

	make serve

这样，通过访问 http://127.0.0.1:8000 你就已经可以看到你的博客页面了！


调试完毕后你应该关闭之前开启的服务器

	./develop_server.sh stop

至此，尽管有些丑，但你已经完成了自己博客的创建，随后只需要把你的文章放进`content`目录下面并运行以上命令就可以轻松生成博客了。如果需要备份，也只需要将`content`目录下的文件备份好就行，非常省心。

当然此时别人还无法访问到你的页面，下面就教你如何把你的博客放到网上去。

##在`github`上创建个人页面

首先你要有个`github`账号。`github`为每个账号提供一个子域名以供存放个人页面，使用的方法是创建一个新的版本库，命名为

	username.github.io

其中`username`必须为你的`github`用户名，否则将无法启动页面。

这时你新创建的版本库是空的，你会获得一个地址

	https://github.com/username/username.github.io.git

先记下来。

接下来要做的是将你本地`output`目录下的所有内容都推送到你刚刚建立的远程版本库中。在本地，进到`output`目录下面

	cd output

在这里新建一个本地的版本库

	git init

建议按照`github`的惯例添加一个新的`readme`文档

	touch README.md

接下来可以将目录下面所有的文件都添加进缓存区

	git add .

可以提交了

	git commit -m 'First commit'

下面将你的本地仓库和远程仓库关联起来，还记的之前获得的一个地址吧，用在这里

	git remote add origin https://github.com/username/username.github.io.git

最后将本地仓库推送到`github`上就好，由于是第一次，用上`-u`字段

	git push -u origin master

待推送成功，稍等片刻，登陆

	username.github.io

应该就能看到你的博客了，没错，它已经正式上线了。此后每次变更博客内容或设置，只需事后将`output`目录下的内容推送到`github`就可以了，听上去和做上去都很简单。

这样，如果你不在意域名的问题，你的博客就算搭建成功了，而且没有花费一分钱！但是基本主题这么丑，博客的各种功能也都还没有这怎么行呢，接着看。

---

#锦上添花

##使用主题

`pelican`目前提供了数款主题可供选择。先到`pelican`这个项目的`github`页面上把主题的版本库`clone`到本地，在你选定的本地目录下面

	git clone https://github.com/getpelican/pelican-themes.git

进`pelican-themes`目录

	cd pelican-themes

你可以浏览该目录下的文件，每个子目录存放了一个主题，里面会留有一个截图供你预览。比如我看中了`bootstrap`这一款，使用命令

	pelican-themes -i bootstrap

安装该主题。这时使用命令

	pelican-themes -l

查看已安装主题，应该就能看到刚刚安装的`bootstrap`主题了。这还不够，你还需要在`pelicanconf.py`文档中加上一句

	THEME = 'bootstrap'

这样你在生成博客页面时新主题就被应用上了。

##添加静态的页面

`pelican`提供了一种不同于一般博客文章的'页面'方便你存放一些需要置顶的信息，比如`about`页面和`contact`页面。

创建方法也很简单，只需要在`content`目录下再新建一个名为`pages`的目录，将你想要展示的内容放进去就行，格式和普通的博客文章相同。

##安装评论系统

由于`pelican`生成的是静态页面，没有数据库的支持所以本身无法实现评论的功能，不过我们还有第三方的服务可以选择。

这里推荐`disqus`，功能齐备，免费。

到[官方页面](www.disqus.com)上注册一个账号。找到'Add Disqus to your site'选项，在跳转后的页面上填写的网站名字，你填写的名字也将是你的'shortname'，记好了。

接下来在你的`pelicanconf.py`文档中添加一下字段

	DISQUS_SITENAME = shortname

用你自己的'shortname'替换进去，剩下的交给`pelican`。

