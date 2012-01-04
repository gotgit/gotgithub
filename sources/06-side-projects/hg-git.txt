.. _hg-git:

用Hg操作GitHub
===============

Hg（又称Mercurial）和 Git 一样也是一个被广泛使用的分布式版本库控制工具。如果\
一个熟悉 Hg 的开发者参与托管在 GitHub 上的项目，大可不必为更换版本控制工具而\
苦恼，GitHub 上的一个名为 hg-git\ [#]_\ 的开源项目可以帮上忙。

得益于 Hg 的强大的插件扩展机制，安装 hg-git 并将其注册为Hg 插件后可提供Hg\ 
操作 Git 版本库的能力。安装 hg-git 可以直接使用 :program:`easy_install` 命令：

::

  $ sudo easy_install hg-git


还可以直接从GitHub上下载hg-git最新代码进行安装：

::

  $ curl -L -k -o hg-git.zip https://github.com/schacon/hg-git/zipball/master
  $ unzip hg-git.zip 
  $ cd schacon-hg-git-*
  $ sudo easy_install .

插件 hg-git 依赖于 Dulwich 项目，如果在安装过程遇到 Dulwich 无法编译，可能\
是因为缺乏 C 编译器，或者尚未安装 python-dev 软件包。Dulwich 是一个Python\
语言的 Git 实现，因此 hg-git 在运行过程中无需 Git 命令行。

和其他 Hg 插件类似，安装完毕后需要修改Hg配置文件（如文件 :file:`~/.hgrc` ）\
如下，以启用 hg-git 插件以及另外一个必须的 Hg 内置插件 —— bookmarks 插件。

::

  [extensions]
  bookmarks =
  hggit = 

对 hg-git 安装配置完毕，就可以使用 Hg 操作 Git 版本库了。

* 克隆 Git 版本库。

  ::

    $ hg clone git://github.com/ossxp-com/hello-world.git
    $ cd hello-world

* Git 版本库的分支转换为 Hg 版本库中的 bookmarks。

  新克隆的 Hg 版本库默认会更新到最新提交（即 tip 版本），未必处于所需的分支上。\
  用命令\ :command:`hg bookmarks`\ 显示分支列表，命令\ :command:`hg parents`\
  显示工作区对应的版本。

  ::

    $ hg bookmarks
       helper/master             10:2767ad9d7008
       helper/v1.x               8:994c2f0adc0b
       master                    1:dcd365e3175c

    $ hg parents
    修改集:      12:928384ca1e87
    标签:        jx/v1.0-i18n
    标签:        tip
    用户:        Jiang Xin <jiangxin@ossxp.com>
    日期:        Fri Dec 31 12:12:42 2010 +0800
    摘要:        Translate for Chinese.

* 切换到所需的工作分支（如\ ``master``\ 分支）。

  用\ `hg update -r`\ 命令切换分支。之后执行\ :command:`hg bookmarks`\ 命令会\
  看到当前工作分支用星号标识出来。

  ::

    $ hg update -r master
    $ hg book
       helper/master             10:2767ad9d7008
       helper/v1.x               8:994c2f0adc0b
     * master                    1:dcd365e3175c

* Git 的里程碑也被记录，并可被 :command:`hg tags` 命令显示。

  ::

    $ hg tags
    tip                               12:928384ca1e87
    jx/v1.0-i18n                      12:928384ca1e87
    jx/v2.3                           10:2767ad9d7008
    ...

* 使用\ :command:`hg pull`\ 命令和\ :command:`hg push`\ 命令可以实现和\
  Git版本库的同步。

* 有的命令如\ :command:`hg outgoing`\ 可在 1.7 版本的Hg中运行正常，\
  但对于高版本库的 Hg 存在兼容性问题。

实际上 hg-git 插件并非只针对 GitHub 的版本库，而是可以支持任意 Git 版本库\
包括本地 Git 版本库。为了提供对 Git 版本库的透明支持，对 Git 版本库的 URL\
的写法有特殊要求，即要能够从协议名称区分开 Git 版本库和默认的 Hg 版本库。

* Git协议：

  `git://example.com[:port]/path/to/repo.git`

* SSH协议： 

  `git+ssh://[user@]example.com[:port]/path/to/repo.git`

* HTTP协议： 

  `git+http://[user@]example.com[:port]/path/to/repo.git`

* HTTPS协议： 

  `git+https://[user@]example.com[:port]/path/to/repo.git`

* 本地协议：

  `/path/to/repo.git`


----

.. [#] https://github.com/schacon/hg-git
