建立主页
=================

很多开源项目托管平台都支持为托管的项目建立主页，但主页的维护方式都没有GitHub这么酷。大多数托管平台无非是开放一个FTP或类似服务，用户把制作好的网页或脚本上传了事，而GitHub采用创建特殊名称的Git版本库或在Git库中建立特别的分支实现主页的创建。

创建个人主页
--------------

为自己在GitHub的账号创建主页很容易，只要在托管空间下创建一个名为 ``<userid>.github.com`` 的版本库，在其中提交网站页面即可。以 ``gotgithub`` 用户为例。

* 创建一个名为 ``gotgithub.github.com`` 的Git版本库。

* 在本地克隆新建立的版本库。

  ::

    $ git clone git@github.com:gotgithub/gotgithub.github.com.git
    $ cd gotgithub.github.com/

* 在版本库根目录中创建文件 ``index.html`` 作为首页。

  ::

    $ printf "<h1>GotGitHub's HomePage</h1>It works.\n" > index.html

* 建立提交。

  ::

    $ git add index.html
    $ git commit -m "Homepage test version."

* 推送到GitHub，完成远程版本库创建。

  ::

    $ git push origin master

* 访问网址： http://gotgithub.github.com/ 。

  最多等待10分钟，GitHub就可以完成新网站的部署。注意个人首页使用HTTP协议非HTTPS协议。

创建项目主页
---------------

GitHub会为每个用户分配一个子域名作为用户主页，同样用户创建的每一个项目也会在用户主页下创建一个子网站。例如 ``gotgithub`` 用户创建的 ``helloworld`` 项目经过简单的定制，会在地址 ``http://gotgithub.github.com/helloworld/`` 下创建项目首页。为项目建立自定义项目首页只需要在项目版本库中创建一个名为 ``gh-pages`` 的分支，并把网页提交到该分支即可。

如果本地尚未建立 ``helloworld`` 版本库克隆，执行如下命令。

::

  $ git clone git@github.com:gotgithub/helloworld.git
  $ cd helloworld

当前版本库只有一个名为 ``master`` 的分支，如果直接从 ``master`` 分支创建 ``gh-pages`` 分支操作非常简单，但是作为保存网页的 ``gh-pages`` 分支中的内容和 ``master`` 分支中的完全不同。如果不希望 ``gh-pages`` 分支继承 ``master`` 分支的历史和文件，即想要创建一个干净的 ``gh-pages`` 分支，需要一点小技巧。可以从下面两个方法任选一种。

第一种方法用到两个Git底层命令： ``git write-tree`` 和 ``git commit-tree`` 。步骤如下：

* 基于 ``master`` 分支建立分支 ``gh-pages`` 。

  ::

    $ git checkout -b gh-pages

* 删除暂存区文件，即相当于清空暂存区。

  ::

    $ rm .git/index

* 创建项目首页 ``index.html`` 。

  ::

    $ printf "hello world.\n" > index.html

* 添加文件 ``index.html`` 到暂存区。

  ::

    $ git add index.html

* 用Git底层命令创建新的根提交，并将分支 ``gh-pages`` 重置。

  ::

    $ git reset --hard $(echo "branch gh-pages init." | git commit-tree $(git write-tree))

* 执行推送命令，在GitHub远程版本库创建分支 ``gh-pages`` 。

  ::

    $ git push origin gh-pages

第二种方法用到Git底层命令： ``git symbolic-ref`` 。步骤如下：


* 用 ``git symbolic-ref`` 命令将当前工作分支由 ``master`` 切换到一个尚不存在的分支 ``gh-pages`` 。

  ::

    $ git symbolic-ref HEAD refs/heads/gh-pages

* 删除暂存区文件，即相当于清空暂存区。

  ::

    $ rm .git/index

* 创建项目首页 ``index.html`` 。

  ::

    $ printf "hello world.\n" > index.html

* 添加文件 ``index.html`` 到暂存区。

  ::

    $ git add index.html

* 执行提交。提交完毕分支 ``gh-pages`` 完成创建。

  ::

    $ git commit --m "branch gh-pages init."

* 执行推送命令，在GitHub远程版本库创建分支 ``gh-pages`` 。

  ::

    $ git push origin gh-pages

无论哪种方法，一旦在GitHub远程版本库中创建分支 ``gh-pages`` ，项目的主页就已经建立。稍后（不超过10分钟），用浏览器访问下面的地址即可看到刚刚提交的项目首页。

* http://gotgithub.github.com/helloworld/

除了以上用命令行方式创建 ``gh-pages`` 分支的方式为项目设定主页外，GitHub还在项目管理界面还提供了图形操作界面。如图3-19所示。

.. figure:: /images/project-hosting/github-pages.png
   :scale: 100

   图3-19：项目管理页面中的GitHub Pages选项

当在项目管理页面中勾选”GitHub Pages“选项，并按照提示操作，自动在项目版本库中创建 ``gh-pages`` 分支。然后执行下面命令从版本库检出 ``gh-pages`` 分支，对项目主页进行相应定制。

::

  $ cd helloworld
  $ git fetch
  $ git clone -b gh-pages origin/gh-pages

使用专有域名
---------------

无论是用户主页还是项目主页，除了使用 ``github.com`` 下的子域名访问之外，还可以使用指定的专有域名。实现起来也非常简单，只要在 ``master`` 分支（用户主页所在版本库）或 ``gh-pages`` 分支（项目版本库）的根目录下检入一个名为 ``CNAME`` 的文件，内容为相应的专有域名。

例如用户拥有的专有域名为 ``example.com`` ，希望访问 ``example.com`` 时实际得到的是 ``gotgithub.github.com`` 网页的内容。只需进行如下操作：

* 在GitHub的 ``gotgithub`` 账户的 ``gotgithub.github.com`` 版本库的根目录下添加文件 ``CNAME`` ，文件内容为： ``example.com`` 。
* 然后将域名 ``example.com`` 的IP指向 ``gotgithub.github.com`` 的IP地址（注意不是 ``github.com`` 的IP地址）。

设置完成后，访问 ``example.com`` 即可看到 ``gotgithub`` 用户在GitHub的个人主页。访问 ``gotgithub.github.com`` 网站亦会重定向到 ``example.com`` 。

看一个实际的例子： http://github.com/mojombo/mojombo.github.com/ → http://tom.preston-werner.com/ 。

使用Jekyll维护网站
-------------------------

Jekyll是由Tom Preston-Werner（GitHub创始人之一）开发的静态网站生成软件，支持博客及网页模版。使用Jekyll，可以直接使用Markdown或其他标记语言撰写页面及博客，当GitHub托管的版本库更新后，GitHub会自动运行Jekyll将标记语言撰写的文件转换为网页。

Jekyll用Ruby语言开发，项目在GitHub的托管地址： http://github.com/mojombo/jekyll/ ，专有的URL地址为： http://jekyllrb.com/ 。安装Jekyll最简单的方法是通过RubyGems安装，会自动将Jekyll依赖的directory_watcher、liquid、open4、maruku和classifier等Gem包一并安装。

::

  $ gem install jekyll

如果安装过程因编译扩展模组遇到错误，可能是因为尚未安装所需的头文件。对于Debian Linux、Ubuntu等可以用如下方法安装所需软件包：

::

  $ sudo apt-get install ruby1.8-dev

如果是Red Hat、CentOS或Fedora等系统，使用如下命令安装：

::

  $ sudo yum install ruby-devel

对于Mac OSX，可能需要更新RubyGems，如下：

::

  $ sudo gem update --system

安装完毕，执行下面的命令显示Jekyll的版本：

::

  $ jekyll -v
  Jekyll 0.11.0

先来看一下作者Tom Preston-Werner在GitHub上的个人网站，看看是如何用Jekyll制作出来的。

先克隆版本库：

::

  $ git clone git://github.com/mojombo/mojombo.github.com.git
  $ cd mojombo.github.com

版本库根目录下的 ``index.html`` 文件不是一个完整的HTML文件，而是套用了模版（Liquid格式模版）的页面，对其关键内容添加行号显示如下：

::

   1 ---
   2 layout: default
   3 title: Tom Preston-Werner
   4 ---
   5 
   6 <div id="home">
   7   <h1>Blog Posts</h1>
   8   <ul class="posts">
   9     {% for post in site.posts %}
  10       <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
  11     {% endfor %}
  12   </ul>
     ...
  63 </div>

第1-4行是YAML格式的文件头，确定模版的对应关系并设定相关属性。凡是设置有YAML文件头的文件（目录 ``_layouts`` 等除外）无论文件扩展名为何，都会在Jekyll编译时转换为对应的HTML文件。其中第2行含义为使用default模版（对应于的模版文件为 ``_layouts/default.html`` ），第3行设定本页面的标题。

第6行开始的内容绝大多数是标准的HTML语法，其中夹杂少量liquid模版特有的语法。有着liquid或其他模版编程经验的用户，不难理解其中第9行和第11行出现的由”{%“和”%}“标识的指令是一个循环指令（for循环）用于逐条对博客进行相关操作，而第10行中由”{{“和”}}“标识的表达式则用于显示博文的日期、链接和标题。

根目录下的 ``atom.xml`` 文件亦套用 ``default`` 模版。

目录 ``_post`` 下的文件是博客文章列表，每个博文都以 ``<YYYY>-<MM>-<DD>-<blog-tiltle>`` 格式的文件名命名。扩展名为 ``.md`` 的为Markdown格式，扩展名为 ``.textile`` 的为Textile格式。这些文件都类似如下格式的文件头：

::

  ---
  layout: post
  title: How I Turned Down $300,000 from Microsoft to go Full-Time on GitHub
  ---

在 ``_layouts`` 目录下定义网页模版，其中文件 ``_layouts/post.html`` 是博客用到的模版，而 ``_layouts/default.html`` 是默认模版。模版文件亦是liquid格式文件。

在根目录下还有一个配置文件 ``_config.yml`` 用于覆盖Jekyll的默认设置，例如本版本库中的设置。

::

  markdown: rdiscount
  pygments: true

第1行设置使用rdiscount软件包作为Markdown的解析引擎，而非默认的Maruku。第2行开启pygments支持。关于该配置文件的详细介绍参见 `Jekyll项目维基`_  。

.. _`Jekyll项目维基`: https://github.com/mojombo/jekyll/wiki/configuration

编译Jekyll编辑网站只需在根目录执行 ``jekyll`` 命令，下面的命令是GitHub更新网站所使用的默认指令。

::

  $ jekyll --pygments --safe

现在执行这条命令，就会将整个网站创建在目录 ``_site`` 下。

如果没有安装Apache等Web服务器，还可以使用Jekyll的内置Web服务器。

::

  $ jekyll --server

默认在端口4000开启Web服务器。

网址 http://gitready.com/ 是一个提供Git使用小窍门的网站，如图3-20所示。

.. figure:: /images/project-hosting/gitready.png
   :scale: 100

   图3-20：Git Ready 网站

你相信这是一个用Jekyll制作的网站么？看看该网站对应的IP，会发现其指向的正是GitHub。研究GitHub上 `gitready`_ 用户托管的版本库，会发现 ``en`` 版本库的 ``gh-pages`` 分支负责生成 ``gitready.com`` 网站， ``de`` 版本库的 ``gh-pages`` 分支负责生成德文网站 ``de.gitready.com`` ，等等。而 ``gitready`` 版本库则是各种语种网站的汇总。

.. _`gitready`: https://github.com/gitready 

