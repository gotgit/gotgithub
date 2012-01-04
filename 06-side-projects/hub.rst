.. _hub:

hub
------------

对于命令行用户，GitHub提供了名为\ ``hub``\ 的命令行工具，对Git进行了简单的\
封装。该项目在GitHub上的地址为： https://github.com/defunkt/hub 。

使用\ ``hub``\ 可以在命令行中简化对GitHub的操作。例如克隆本电子书的版本库，\
若用\ ``hub``\ 命令，地址可大大简化：

::

  $ hub clone gotgit/gotgithub

若要在自己账号下创建派生项目，无需登录GitHub网站，直接通过命令行即可实现：

::

  $ cd gotgithub
  $ hub fork

安装\ ``hub``\ 很简单，可使用如下方法任意一种方法。

* 克隆\ ``hub``\ 的版本库，从源码安装。安装步骤如下：

  ::
  
    $ git clone git://github.com/defunkt/hub.git
    $ cd hub
    $ rake install prefix=/usr/local

* 用 RubyGems 包方式安装。

  ``hub``\ 用 Ruby 开发，也可用 RubyGems 包方式安装。需要注意，在安装完毕后\
  最好将\ ``hub``\ 打包为一独立运行脚本，以便运行时不再靠 RubyGems 加载，\
  提高加载速度。安装步骤如下：

  ::
  
    $ gem install hub
    $ hub hub standalone > ~/bin/hub && chmod 755 ~/bin/hub

安装完毕后，还需要对\ ``hub``\ 进行设置。定义两个Git风格的配置变量，以便\
``hub``\ 命令能确定当前GitHub用户账号，并能够完成所需的 GitHub API 认证。

::

  $ git config --global github.user "your-github-username"
  $ git config --global github.token "your-github-token"

其中\ ``github.token``\ 中保存的是用户的API TOKEN，这在“2.1 创建GitHub账号”\
一节有过介绍。

在使用\ ``hub``\ 过程中，如果要为区分哪些命令是\ ``git``\ 的，哪些是\ ``hub``\
的，而不断在两个命令间切换显然太不方便了。``hub`` 命令支持以系统别名\ ``git``\
的方式运行，即设置\ ``hub``\ 的系统别名为\ ``git``\ ，然后只需执行\ ``git``\
命令，这样无论是\ ``git``\ 本身的命令还是\ ``hub``\ 扩展的命令都可正常运行。\
但要注意要用系统提供的别名方式，而不能把\ ``hub``\ 脚本改名为\ ``git``\ ，\
因为\ ``hub``\ 只是简单地对Git进行封装，运行时仍依赖\ ``git``\ 命令。在 bash \
环境下建立别名可运行如下命令：

::

  $ alias git=hub

其他 shell 环境下如何建立系统别名呢？运行\ ``hub alias <shell>``\ 命令查看\
相关 shell 环境下建立别名的方法。例如对于 csh：

::

  $ hub alias csh
  Run this in your shell to start using `hub` as `git`:
    alias git hub

下面介绍\ ``hub``\ 的常用命令，节选自\ ``hub``\ 的项目页\ [#]_\ 。示例使用\
了别名命令\ ``git``\ 调用，并把对应的原始的\ ``git``\ 命令写在命令的下面\
（用提示符\ ``>``\ 表示，方括号中是说明）。

* git create

  在GitHub上创建项目。

  ::

    $ git create -d '项目表述'
    > [ 在GitHub上创建版本库 ]
    > git remote add origin git@github.com:YOUR_USER/CURRENT_REPO.git

    $ git create recipes
    > [ 在GitHub上创建版本库 ]
    > git remote add origin git@github.com:YOUR_USER/recipes.git

    $ git create sinatra/recipes
    > [ 在组织账号 sinatra 下创建版本库 ]
    > git remote add origin git@github.com:sinatra/recipes.git

* git clone

  克隆版本库可使用URL简写，即“用户名/版本库”格式地址会自动扩展为Git协议\
  （只读）地址或SSH协议（可写）地址。

  ::

    $ git clone schacon/ticgit
    > git clone git://github.com/schacon/ticgit.git

    $ git clone -p schacon/ticgit
    > git clone git@github.com:schacon/ticgit.git

    $ git clone resque
    > git clone git@github.com/YOUR_USER/resque.git

* git fork

  在GitHub自己账号下建立派生项目。

  ::

    $ git fork
    > [ 先在GitHub 上建立派生项目 ]
    > git remote add -f YOUR_USER git@github.com:YOUR_USER/CURRENT_REPO.git

* git pull-request

  打开编辑器输入标题和内容，然后在 GitHub 上创建 Pull Request。


* git remote add

  设置远程版本库。和\ ``git clone``\ 命令一样支持URL简写。

  ::

    $ git remote add rtomayko
    > git remote add rtomayko git://github.com/rtomayko/CURRENT_REPO.git

    $ git remote add -p rtomayko
    > git remote add rtomayko git@github.com:rtomayko/CURRENT_REPO.git

    $ git remote add origin
    > git remote add origin git://github.com/YOUR_USER/CURRENT_REPO.git

* git fetch

  获取他人同名版本库。自动建立远程版本库并获取提交。

  ::

    $ git fetch mislav
    > git remote add mislav git://github.com/mislav/REPO.git
    > git fetch mislav

    $ git fetch mislav,xoebus
    > git remote add mislav ...
    > git remote add xoebus ...
    > git fetch --multiple mislav xoebus

* git cherry-pick

  获取远程提交，并拣选至本地版本库。

  ::

    $ git cherry-pick http://github.com/mislav/REPO/commit/SHA
    > git remote add -f mislav git://github.com/mislav/REPO.git
    > git cherry-pick SHA

* git am, git apply

  获取 Pull Request，并应用于本地版本库。

  ::

    $ git am https://github.com/defunkt/hub/pull/55
    > curl https://github.com/defunkt/hub/pull/55.patch -o /tmp/55.patch
    > git am /tmp/55.patch

* git browse

  打开浏览器访问相应的URL地址。

  ::

    $ git browse
    > open https://github.com/YOUR_USER/CURRENT_REPO

    $ git browse -- commit/SHA
    > open https://github.com/YOUR_USER/CURRENT_REPO/commit/SHA

    $ git browse -- issues
    > open https://github.com/YOUR_USER/CURRENT_REPO/issues

    $ git browse resque
    > open https://github.com/YOUR_USER/resque

    $ git browse schacon/ticgit
    > open https://github.com/schacon/ticgit

    $ git browse schacon/ticgit commit/SHA
    > open https://github.com/schacon/ticgit/commit/SHA

* git help hub

  查看\ ``hub``\ 命令的帮助。

.. [#] https://github.com/defunkt/hub#readme
