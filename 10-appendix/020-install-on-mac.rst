Mac OS X 下安装和使用 Git
==========================

Mac OS X 被称为最人性化的操作系统，工作在 Mac 上是件非常惬意的事情，工作中怎能没有 Git？

以二进制发布包的形式安装
-------------------------

Git 在 Mac OS X 中也有好几种安装方法。最为简单的方式是安装 ``.dmg`` 格式的安装包。

访问 git-osx-installer 的官方网站： http://code.google.com/p/git-osx-installer/ ，下载 Git 安装包。安装包带有 ``.dmg`` 扩展名，是苹果磁盘镜像（Apple Disk Image）格式的软件发布包。从官方网站上下载文件名类似 git-<version>-<arch>-leopard.dmg 的安装包文件，例如：git-1.7.3.5-x86_64-leopard.dmg 是 64 位的安装包，git-1.7.3.5-i386-leopard.dmg 是 32 位的安装包。建议选择 64 位的软件包，因为 Mac OS X 10.6 雪豹完美的兼容 32 位和 64位（开机按住键盘数字3和2进入32位系统，按住6和4进入64位系统），即使在核心处于32位架构下，也可以放心的运行64位软件包。

苹果的 ``.dmg`` 格式的软件包实际上是一个磁盘映像，安装起来非常方便，点击该文件就直接挂载到 Finder 中，并打开，如图3-1所示。

.. figure:: /images/meet-git/mac-install-1.png
   :scale: 100

   图3-1：在 Mac OS X 下打开 .dmg 格式磁盘镜像

其中带有一个正在解包图标的文件（扩展名为 ``.pkg`` ）是 Git 的安装程序，另外的两个脚本程序，一个用于应用的卸载（ ``uninstall.sh`` ），另外一个带有长长文件名的脚本可以在 Git 安装后执行的，为非终端应用注册 Git 的安装路径，因为 Git 部署在标准的系统路径之外 ``/usr/local/git/bin`` 。

点击扩展名为 ``.pkg`` 的安装程序，开始 Git 的安装，根据提示按步骤完成安装，如图3-2所示。

.. figure:: /images/meet-git/mac-install-2.png
   :scale: 100

   图3-2：在 Mac OS X 下安装 Git。

安装完毕，git 会被安装到 ``/usr/local/git/bin/`` 目录下。重启终端程序，才能让 ``/etc/paths.d/git`` 文件为 PATH 环境变量中添加的新路径注册生效。然后就可以在终端中直接运行 ``git`` 命令了。

安装 Xcode
-------------------------

Mac OS X 基于 Unix 内核，因此也可以很方便的通过源码编译的方式进行安装，但是缺省安装的 Mac OS X 缺乏相应的开发工具，需要安装苹果提供的 Xcode 软件包。在 Mac 随机附送的光盘（Mac OS X Install DVD）的可选安装文件夹下就有 Xcode 的安装包（如图3-3所示），通过随机光盘安装 Xcode 可以省去了网络下载的麻烦，要知道 Xcode 有3GB以上。

.. figure:: /images/meet-git/xcode-install.png
   :scale: 100

   图3-3：在 Mac OS X 下安装 Xcode。

使用 Homebrew 安装 Git
-------------------------

Mac OS X 有好几个包管理器实现对一些开源软件在 Mac OS X 上的安装和升级进行管理。有传统的 MacPort, Fink，还有更为简单易用的 Homebrew。下面就介绍一下如何通过 Homebrew 包管理器，以源码包编译的方式安装 Git。

Homebrew 用 ruby 语言开发，支持千余种开源软件在 Mac OS X 中的部署和管理。Homebrew 项目托管在 Github 上，网址为: https://github.com/mxcl/homebrew 。

首先是安装 Homebrew，执行下面的命令：

::

  $ ruby -e \
    "$(curl -fsSL https://gist.github.com/raw/323731/install_homebrew.rb)"

安装完成后，Homebrew 的主程序安装在 ``/usr/local/bin/brew`` ，在目录 ``/usr/local/Library/Formula/`` 下保存了所有 Homebrew 支持的软件的安装指引文件。

运行 ``brew`` 安装 Git，使用下面的命令。

::

  $ brew install git

使用 Homebrew 方式安装，Git 被安装在 ``/usr/local/Cellar/git/1.7.3.5`` ，可执行程序自动在 ``/usr/local/bin`` 目录下创建符号连接，可以直接在终端程序中访问。

通过 ``brew list`` 命令可以查看安装的开源软件包。

::

  $ brew list
  git

也可以查看某个软件包安装的详细路径和安装内容。

::

  $ brew list git
  /usr/local/Cellar/git/1.7.3.5/bin/gitk
  ...

从Git源码进行安装
-------------------------

如果需要安装历史版本的 Git 或是安装尚在开发中的未发布版本的 Git，就需要从源码安装或通过克隆 Git 源码库进行安装。既然 Homebrew 就是通过源码编译方式安装 Git 的，那么也应该可以直接从源码进行安装，但是使用 Homebrew 安装 Git 和直接通过 Git 源码安装并不完全等同，例如 Homebrew 安装 Git 的过程中，是通过下载已经编译好的 Git 文档包进行安装，而非从头对文档进行编译。

直接通过源码安装 Git 包括文档，遇到主要的问题就是文档的编译，因为 Git 文档编译所需要的相关工具没有在 Xcode 中提供。但是这些工具可以通过 Homebrew 进行安装。下面工具软件的安装过程可能会遇到一些小麻烦，不过大多可以通过参考命令输出予以解决。

::

  $ brew install asciidoc
  $ brew install docbook2x
  $ brew install xmlto

当编译源码及文档的工具部署完全后，就可以通过源码编译 Git。

::

  $ make prefix=/usr/local all doc info
  $ sudo make prefix=/usr/local install \
    install-doc install-html install-info

命令自动补齐
-------------------------

Git 通过 bash-completion 软件包实现命令补齐，在 Mac OS X 下可以通过 Homebrew 进行安装。

::

  $ brew search completion
  bash-completion
  $ brew install bash-completion
  ...
  Add the following lines to your ~/.bash_profile file:
  if [ -f `brew --prefix`/etc/bash_completion ]; then
    . `brew --prefix`/etc/bash_completion
  fi
  ...

根据 bash-completion 安装过程中的提示，修改文件 ``~/.bash_profile`` 文件，并在其中加入如下内容，以便在终端加载时自动启用命令补齐。

::

  if [ -f `brew --prefix`/etc/bash_completion ]; then
    . `brew --prefix`/etc/bash_completion
  fi

将 Git 的命令补齐脚本拷贝到 bash-completion 对应的目录中。

::

  $ cp contrib/completion/git-completion.bash \
       `brew --prefix`/etc/bash_completion.d/

不用重启终端程序，只需要运行下面的命令，即可立即在当前的 shell 中加载命令补齐。

::

  . `brew --prefix`/etc/bash_completion

其他辅助工具的安装
-------------------------

本书中还会用到一些常用的 GNU 或其他开源软件，在 Mac OS X 下也可以通过 Homebrew 进行安装。这些软件包有：

* gnupg: 数字签名和加密工具。在为 Git 版本库建立签名里程碑时会用到。
* md5sha1sum: 生成 MD5 或 SHA1 摘要。在研究 Git 版本库中的对象过程中会用到。
* cvs2svn: CVS 版本库迁移到 SVN 或 Git 的工具。在版本库迁移时会用到。
* stgit: Git 的补丁和提交管理工具。
* quilt: 一种补丁管理工具。在介绍 StGit 时用到。

在 Mac OS X 下能够使用到的 Git 图形工具除了 Git 软件包自带的 ``gitk`` 和 ``git gui`` 之外，还可以安装 GitX。下载地址：

* GitX 的原始版本：http://gitx.frim.nl/
* 或 GitX 的一个分支版本，提供增强的功能：
  https://github.com/brotherbard/gitx/downloads

Git 的图形工具一般需要在本地克隆版本库的工作区中执行，为了能和 Mac OS X 有更好的整合，可以安装插件实现和 Finder 的整合。在 git-osx-installer 的官方网站： http://code.google.com/p/git-osx-installer/ ，有两个以 ``OpenInGitGui-`` 和 ``OpenInGitX-`` 为前缀的软件包，可以分别实现和 ``git gui`` 以及 ``gitx`` 的整合：在 Finder 中进入工作区目录，点击对应插件的图标，启动 ``git gui`` 或 ``gitx`` 。

中文支持
-------------------

由于 Mac OS X 采用 Unix 内核，在中文支持上和 Linux 相近，请参照前面介绍Git在Linux下安装中3.1.5节相关内容。
