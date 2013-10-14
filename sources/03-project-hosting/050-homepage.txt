.. _homepage:

建立主页
=================

很多开源项目托管平台都支持为托管的项目建立主页，但主页的维护方式都没有GitHub\
这么酷。大多数托管平台无非是开放一个FTP或类似服务，用户把制作好的网页或脚本\
上传了事，而在GitHub用户通过创建特殊名称的Git版本库或在Git库中建立特别的分支\
实现对主页的维护。

.. _user-homepage:

创建个人主页
--------------

GitHub 为每一个用户分配了一个二级域名\ ``<user-id>.github.io``\ ，用户为自己\
的二级域名创建主页很容易，只要在托管空间下创建一个名为\ ``<user-id>.github.io``\
的版本库，向其\ ``master``\ 分支提交网站静态页面即可，其中网站首页为\
``index.html``\ 。下面以\ ``gotgithub``\ 用户为例介绍如何创建个人主页。

* 用户\ ``gotgithub``\ 创建一个名为\ ``gotgithub.github.io``\ 的Git版本库。

  在GitHub上创建版本库的操作，参见“第3.1节 :ref:`new-project`\ ”。

* 在本地克隆新建立的版本库。

  ::

    $ git clone git@github.com:gotgithub/gotgithub.github.io.git
    $ cd gotgithub.github.io/

* 在版本库根目录中创建文件\ ``index.html``\ 作为首页。

  ::

    $ printf "<h1>GotGitHub's HomePage</h1>It works.\n" > index.html

* 建立提交。

  ::

    $ git add index.html
    $ git commit -m "Homepage test version."

* 推送到GitHub，完成远程版本库创建。

  ::

    $ git push origin master

* 访问网址： http://gotgithub.github.io/ 。

  最多等待10分钟，GitHub就可以完成新网站的部署。网站完成部署后版本库\
  的所有者会收到邮件通知。

  还有要注意访问用户二级域名的主页要使用HTTP协议非HTTPS协议。

.. _project-homepage:

创建项目主页
---------------

如前所述，GitHub会为每个账号分配一个二级域名\ ``<user-id>.github.io``\
作为用户的首页地址。实际上还可以为每个项目设置主页，项目主页也通过\
此二级域名进行访问。

例如\ ``gotgithub``\ 用户创建的\ ``helloworld``\ 项目如果启用了项目主页，\
则可通过网址\ ``http://gotgithub.github.io/helloworld/``\ 访问。

为项目启用项目主页很简单，只需要在项目版本库中创建一个名为\ ``gh-pages``\
的分支，并向其中添加静态网页即可。也就是说如果项目的Git版本库中包含了名为\
``gh-pages``\ 分支的话，则表明该项目提供静态网页构成的主页，可以通过网址\
``http://<user-id>.github.io/<project-name>``\ 访问到。

下面以用户\ ``gotgithub``\ 的项目\ ``helloworld``\ 为例，介绍如何维护项目主页。

如果本地尚未从GitHub克隆\ ``helloworld``\ 版本库，执行如下命令。

::

  $ git clone git@github.com:gotgithub/helloworld.git
  $ cd helloworld

当前版本库只有一个名为\ ``master``\ 的分支，如果直接从\ ``master``\ 分支创建\
``gh-pages``\ 分支操作非常简单，但是作为保存网页的\ ``gh-pages``\ 分支中的内容\
和\ ``master``\ 分支中的可能完全不同。如果不希望\ ``gh-pages``\ 分支继承\
``master``\ 分支的历史和文件，即想要创建一个干净的\ ``gh-pages``\ 分支，\
需要一点小技巧。

若使用命令行创建干净的\ ``gh-pages``\ 分支，可以从下面三个方法任选一种。

第一种方法用到两个Git底层命令：\ ``git write-tree``\ 和\ ``git commit-tree``\ 。\
步骤如下：

* 基于\ ``master``\ 分支建立分支\ ``gh-pages``\ 。

  ::

    $ git checkout -b gh-pages

* 删除暂存区文件，即相当于清空暂存区。

  ::

    $ rm .git/index

* 创建项目首页\ ``index.html``\ 。

  ::

    $ printf "hello world.\n" > index.html

* 添加文件\ ``index.html``\ 到暂存区。

  ::

    $ git add index.html

* 用Git底层命令创建新的根提交，并将分支\ ``gh-pages``\ 重置。

  ::

    $ git reset --hard $(echo "branch gh-pages init." | git commit-tree $(git write-tree))

* 执行推送命令，在GitHub远程版本库创建分支\ ``gh-pages``\ 。

  ::

    $ git push -u origin gh-pages

第二种方法用到Git底层命令：\ ``git symbolic-ref``\ 。步骤如下：


* 用\ ``git symbolic-ref``\ 命令将当前工作分支由\ ``master``\ 切换到一个尚不\
  存在的分支\ ``gh-pages``\ 。

  ::

    $ git symbolic-ref HEAD refs/heads/gh-pages

* 删除暂存区文件，即相当于清空暂存区。

  ::

    $ rm .git/index

* 创建项目首页\ ``index.html``\ 。

  ::

    $ printf "hello world.\n" > index.html

* 添加文件\ ``index.html``\ 到暂存区。

  ::

    $ git add index.html

* 执行提交。提交完毕分支\ ``gh-pages``\ 完成创建。

  ::

    $ git commit -m "branch gh-pages init."

* 执行推送命令，在GitHub远程版本库创建分支\ ``gh-pages``\ 。

  ::

    $ git push -u origin gh-pages

第三种方法没有使用任何Git底层命令，是从另外的版本库获取提交建立分支。\
操作如下：

* 在\ ``helloworld``\ 版本库之外创建另外一个版本库，例如\ ``helloworld-web``\ 。

  ::

    $ git init ../helloworld-web
    $ cd ../helloworld-web

* 在\ ``helloworld-web``\ 版本库中创建主页文件\ ``index.html``\ 。

  ::

    $ printf "hello world.\n" > index.html

* 添加文件\ ``index.html``\ 到暂存区。

  ::

    $ git add index.html

* 执行提交。

  实际提交到\ ``master``\ 分支，虽然提交说明中出现的是\ ``gh-pages`` \。

  ::

    $ git commit -m "branch gh-pages init."

* 切换到\ ``helloworld``\ 版本库目录。

  ::

    $ cd ../helloworld

* 从\ ``helloworld-web``\ 版本库获取提交，并据此创建\ ``gh-pages``\ 分支。

  ::

    $ git fetch ../helloworld-web
    $ git checkout -b gh-pages FETCH_HEAD


* 执行推送命令，在GitHub远程版本库创建分支\ ``gh-pages``\ 。

  ::

    $ git push -u origin gh-pages


无论哪种方法，一旦在GitHub远程版本库中创建分支\ ``gh-pages``\ ，项目的主页\
就已经建立。稍后（不超过10分钟），用浏览器访问下面的地址即可看到刚刚提交的\
项目首页： http://gotgithub.github.io/helloworld/ 。

除了以上通过命令行创建\ ``gh-pages``\ 分支为项目设定主页之外，GitHub还提供\
了图形操作界面。如图3-19所示。

.. figure:: /images/project-hosting/github-pages.png
   :scale: 100

   图3-19：项目管理页面中的GitHub Pages选项

当在项目管理页面中勾选“GitHub Pages”选项，并按照提示操作，会自动在项目版本库\
中创建\ ``gh-pages``\ 分支。然后执行下面命令从版本库检出\ ``gh-pages``\ 分支，\
对项目主页进行相应定制。

::

  $ git fetch
  $ git checkout gh-pages

.. _dedicate-domain:

使用专有域名
---------------

无论是用户主页还是项目主页，除了使用\ ``github.com``\ 下的二级域名访问之外，\
还可以使用专有域名。实现起来也非常简单，只要在\ ``master``\ 分支（用户主页\
所在版本库）或\ ``gh-pages``\ 分支（项目版本库）的根目录下检入一个名为\
``CNAME``\ 的文件，内容为相应的专有域名。当然还要更改专有域名的域名解析，\
使得该专有域名的IP地址指向相应的GitHub二级域名的IP地址。

例如\ ``worldhello.net``\ [#]_\ 是我的个人网站，若计划将网站改为由GitHub托管，\
并由账号\ ``gotgit``\ 通过个人主页提供服务，可做如下操作。

首先按照前面章节介绍的步骤，为账号\ ``gotgit``\ 设置账户主页。

1. 在账户\ ``gotgit``\ 下创建版本库\ ``gotgit.github.io``\ 以维护该账号主页。

   地址： https://github.com/gotgit/gotgit.github.io/

2. 将网站内容提交并推送到该版本库\ ``master``\ 分支中。

   即在\ ``gotgit.github.io``\ 版本库的根目录下至少包含一个首页文件，如\
   ``index.html``\ 。还可以使用下节将要介绍到的 Jekyll 技术，让网页有统一的\
   显示风格，此时首页文件可能并非一个完整的HTML文档，而是套用了页面模版。

3. 至此当访问网址\ http://gotgit.github.io\ 时，会将账号\ ``gotgit``\
   的版本库\ ``gotgit.github.io``\ 中的内容作为网站内容显示出来。

接下来进行如下操作，使得该网站能够使用专有域名\ ``www.worldhello.net``\
提供服务。

1. 在账号\ ``gotgit``\ 的版本库\ ``gotgit.github.io``\ 根目录下添加文件\
   ``CNAME``\ ，文件内容为：\ ``www.worldhello.net``\ 。

   参见： https://github.com/gotgit/gotgit.github.io/blob/master/CNAME

2. 然后更改域名\ ``www.worldhello.net``\ 的IP地址，指向域名\ ``gotgit.github.io``\
   对应的IP地址（注意不是\ ``github.com``\ 的IP地址）。

   完成域名的DNS指向后，可试着用\ ``ping``\ 或\ ``dig``\ 命令确认域名\
   ``www.worldhello.net``\ 和\ ``gotgit.github.io``\ 指向同一IP地址。

   ::

     $ dig @8.8.8.8 -t a www.worldhello.net
     ...
     ; ANSWER SECTION:
     www.worldhello.net.     81078   IN      A       204.232.175.78
     
     $ dig @8.8.8.8 -t a gotgit.github.io
     ...
     ; ANSWER SECTION:
     gotgit.github.io.      43200   IN      A       204.232.175.78

设置完成后用浏览器访问 http://www.worldhello.net/ 即可看到由账号\ ``gotgit``\
的版本库\ ``gotgit.github.io``\ 维护的页面。若将域名\ ``worldhello.net``\
（不带www前缀）也指向IP地址\ ``204.232.175.78``\ ，则访问网址\
http://worldhello.net/\ 会发现GitHub体贴地将该网址重定向到正确的地址\
http://www.worldhello.net/\ 。

在账号\ ``gotgit``\ 下的其他版本库，若包含了\ ``gh-pages``\ 分支，亦可由域名\
``www.worldhello.net``\ 访问到。

* 网址 http://www.worldhello.net/doc 实际对应于版本库 `gotgit/doc <https://github.com/gotgit/doc>`_ 。
* 网址 http://www.worldhello.net/gotgit 实际对应于版本库 `gotgit/gotgit <https://github.com/gotgit/gotgit>`_ 。
* 网址 http://www.worldhello.net/gotgithub 实际对应于版本库 `gotgit/gotgithub <https://github.com/gotgit/gotgithub>`_ 。


.. _jekyll:

使用Jekyll维护网站
-------------------------

Jekyll是一个支持Textile、Markdown等标记语言的静态网站生成软件，还支持博客和\
网页模版，由Tom Preston-Werner（GitHub创始人之一）开发。Jekyll用Ruby语言实现，\
项目在GitHub的托管地址： http://github.com/mojombo/jekyll/ ，专有的URL地址为：\
http://jekyllrb.com/\ 。

GitHub为用户账号或项目提供主页服务，会从相应版本库的\ ``master``\ 分支或\
``gh-pages``\ 分支检出网页文件，然后执行 Jekyll 相应的命令对网页进行编译。\
因此在设计GitHub的用户主页和项目主页时都可以利用Jekyll，实现用Markdown等标记\
语言撰写网页及博客，并用页面模版实现网页风格的统一。

安装Jekyll最简单的方法是通过RubyGems安装，会自动将Jekyll依赖的\
directory_watcher、liquid、open4、maruku和classifier等Gem包一并安装。

::

  $ gem install jekyll

如果安装过程因编译扩展模组遇到错误，可能是因为尚未安装所需的头文件，需要进行如下操作：

* 对于Debian Linux、Ubuntu等可以用如下方法安装所需软件包：

  ::
  
    $ sudo apt-get install ruby1.8-dev

* 如果是Red Hat、CentOS或Fedora等系统，使用如下命令安装：

  ::
  
    $ sudo yum install ruby-devel

* 对于Mac OSX，可能需要更新RubyGems，如下：

  ::
  
    $ sudo gem update --system

Jekyll安装完毕，执行下面的命令显示软件版本：

::

  $ jekyll -v
  Jekyll 0.11.0

要学习如何用Jekyll设计网站，可以先看一下作者Tom Preston-Werner在GitHub上的\
个人网站是如何用Jekyll制作出来的。

克隆版本库：

::

  $ git clone git://github.com/mojombo/mojombo.github.com.git

版本库包含的文件如下：

::

  $ cd mojombo.github.com
  $ ls -F
  CNAME           _config.yml     _posts/         css/            index.html
  README.textile  _layouts/       atom.xml        images/         random/

版本库根目录下的\ ``index.html``\ 文件不是一个普通的HTML文件，而是使用Liquid\
模版语言\ [#]_\ 定义的页面。

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

为方便描述为内容添加了行号，说明如下：

* 第1-4行是YAML格式的文件头，设定了该文件所使用的模版文件及模版中要用到的变量。

  凡是设置有YAML文件头的文件（目录\ ``_layouts``\ 除外）无论文件扩展名是什么，\
  都会在Jekyll编译时进行转换。若源文件由Markdown等标记语言撰写（扩展名为\ ``.md``\ 、\
  ``.textile``\ 等），Jekyll还会将编译后的文件还将以扩展名\ ``.html``\ 来保存。

* 其中第2行含义为使用default模版。

  对应的模版文件为\ ``_layouts/default.html``\ 。

* 第3行设定本页面的标题。

  在模版文件\ ``_layouts/default.html``\ 中用\ ``{{ page.title }}``\ 语法嵌入\
  所设置的标题。下面是模版文件中部分内容：

  ::

    <head>
       <meta http-equiv="content-type" content="text/html; charset=utf-8" />
       <title>{{ page.title }}</title>

* 第6行开始的内容绝大多数是标准的HTML语法，其中夹杂少量Liquid模版特有的语法。

* 第9行和第11行，对于有着Liquid或其他模版编程经验的用户，不难理解其中出现的由\
  “{%”和“%}”标识的指令是一个循环指令（for循环），用于逐条对博客进行相关操作。

* 第10行中由“{{”和“}}”标识的表达式则用于显示博文的日期、链接和标题。

非下划线（_）开头的文件（包括子目录中文件），如果包含YAML文件头，就会使用Jekyll\
进行编译，并将编译后的文件复制到目标文件夹（默认为\ ``_site``\ 目录）下。\
对于包含YAML文件头并用标记语言Markdown等撰写的文件，还会将编译后的文件以\
``.html``\ 扩展名保存。而以下划线开头的文件和目录有的直接忽略不予处理（如\
``_layouts``\ 、\ ``_site``\ 目录等），有的则需要特殊处理（如\ ``_post``\ 目录）。

目录\ ``_post``\ 用于保存博客条目，每个博客条目都以\ ``<YYYY>-<MM>-<DD>-<blog-tiltle>``\
格式的文件名命名。扩展名为\ ``.md``\ 的为Markdown格式，扩展名为\ ``.textile``\
的为Textile格式。这些文件都包含类似的文件头：

::

  ---
  layout: post
  title: How I Turned Down $300,000 from Microsoft to go Full-Time on GitHub
  ---

即博客使用文件\ ``_layouts/post.html``\ 作为页面模版，而不是\ ``index.html``\
等文件所使用的\ ``_layouts/default.html``\ 模版。这些模版文件都采用Liquid模版\
语法。保存于\ ``_post``\ 目录下的博客文件编译后会以\
``<YYYY>/<MM>/<DD>/<blog-title>.html``\ 文件名保存在输出目录中。

在根目录下还有一个配置文件\ ``_config.yml``\ 用于覆盖Jekyll的默认设置，例如\
本版本库中的设置。

::

  markdown: rdiscount
  pygments: true

第1行设置使用rdiscount软件包作为Markdown的解析引擎，而非默认的Maruku。第2行开启\
pygments支持。对于中文用户强烈建议通过配置文件\ ``_config.yml``\ 重设 markdown \
解析引擎，默认的 Maruku 对中文支持不好，而使用 rdiscount 或 kramdown 均可。\
关于该配置文件的更多参数详见Jekyll项目维基\ [#]_\  。

编译Jekyll编辑网站只需在根目录执行\ ``jekyll``\ 命令，下面的命令是GitHub更新\
网站所使用的默认指令。

::

  $ jekyll --pygments --safe

现在执行这条命令，就会将整个网站创建在目录\ ``_site``\ 下。

如果没有安装Apache等Web服务器，还可以使用Jekyll的内置Web服务器。

::

  $ jekyll --server

默认在端口4000开启Web服务器。

网址 http://gitready.com/ 是一个提供Git使用小窍门的网站，如图3-20所示。

.. figure:: /images/project-hosting/gitready.png
   :scale: 100

   图3-20：Git Ready 网站

你相信这是一个用Jekyll制作的网站么？看看该网站对应的IP，会发现其指向的正是GitHub。\
研究GitHub上 `gitready`_ 用户托管的版本库，会发现\ ``en``\ 版本库的\ ``gh-pages``\
分支负责生成\ ``gitready.com``\ 网站，\ ``de``\ 版本库的\ ``gh-pages``\ 分支负责\
生成德文网站\ ``de.gitready.com``\ ，等等。而\ ``gitready``\ 版本库则是各种语种网站的汇总。

.. _`gitready`: https://github.com/gitready 

我的个人网站也使用Jekyll构建并托管在GitHub上，网址：\ http://www.worldhello.net/\ 。

----

.. [#] “Hello, world”最为程序员所熟知，2002年申请不到helloworld相关域名便\
       退而求其次，申请了 worldhello.net。
.. [#] http://liquidmarkup.org/
.. [#] https://github.com/mojombo/jekyll/wiki/configuration
