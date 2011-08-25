Linux 下安装和使用 Git
=======================

Git 诞生于 Linux 平台并做为版本控制系统帅先服务于 Linux 核心，因此在 Linux 安装 Git 是非常方便的。可以通过不同的方式在 Linux 上安装 Git。一种方法是通过 Linux 发行版的包管理器安装已经编译好的二进制格式的 Git 软件包。另外一种方式就是从 Git 源码开始安装。

包管理器方式安装
-------------------------

用 Linux 发行版的包管理器安装 Git，最为简单，但安装的 Git 可能不是最新的版本。还有一点要注意，就是 Git 软件包在有的 Linux 发行版中可能不叫做 git，而叫做 git-core。这是因为在 Git 之前就有一款叫做 GNU 交互工具（GNU Interactive Tools）的 GNU 软件在有的 Linux 发行版（Deian lenny）中已经占用了 git 的名称。为了以示区分，作为版本控制系统的 Git ，其软件包在这些平台就被命名为 git-core。不过因为作为版本控制系统的 Git 太有名了，最终导致在一些 Linux 发行版的最新版本中，将 GNU Interactive Tools 软件包由 git 改名为 gnuit，将 git-core 改名为 git。所以在下面介绍的在不同的 Linux 发行版中安装 Git 时，会看到有 git 和 git-core 两个不同的名称。

* Ubuntu 10.10 (maverick) 或更新版本, Debian (squeeze) 或更新版本：

  ::

    $ sudo aptitude install git
    $ sudo aptitude install git-doc git-svn git-email gitk 

  其中 git 软件包包含了大部分 Git 命令，是必装的软件包。

  软件包 git-svn、git-email、gitk 本来也是 Git 软件包的一部分，但是因为有着不一样的软件包依赖（如更多 perl 模组，tk等），所以单独作为软件包发布。

  软件包 git-doc 则包含了 Git 的 HTML 格式文档，可以选择安装。如果安装了 Git 的 HTML 格式的文档，则可以通过执行 ``git help -w <sub-command>`` 命令，自动用 Web 浏览器打开相关子命令 <sub-command> 的 HTML 帮助。
  
* Ubuntu 10.04 (lucid) 或更老版本, Debian (lenny) 或更老版本：
 
  在老版本的 Debian 中，软件包 git 实际上是 Gnu Interactive Tools，而非作为版本控制系统的 Git。做为版本控制系统的 Git 在软件包 git-core 中。 

  ::

    $ sudo aptitude install git-core
    $ sudo aptitude install git-doc git-svn git-email gitk 

* RHEL, Fedora, CentOS:

  ::

    $ yum install git
    $ yum install git-svn git-email gitk 

其他发行版安装 Git 的过程和上面介绍的方法向类似。Git 软件包在这些发行版里或称为 git，或称为 git-core。

从源代码开始安装
-------------------------

访问 Git 的官方网站： http://git-scm.com/ 。下载 Git 源码包，例如: git-1.7.3.5.tar.bz2 。

* 展开源码包，并进入到相应的目录中。

  ::

    $ tar -jxvf git-1.7.3.5.tar.bz2
    $ cd git-1.7.3.5/

* 安装方法写在 INSTALL 文件当中，参照其中的指示完成安装。下面的命令将 Git 安装在 /usr/local/bin 中。

  ::

    $ make prefix=/usr/local all
    $ sudo make prefix=/usr/local install

* 安装 Git 文档（可选）。

  编译的文档主要是 HTML 格式文档，方便通过 ``git help -w <sub-command>`` 命令查看。实际上即使不安装 Git 文档，也可以使用 man 手册查看 Git 帮助，使用命令 ``git help <sub-command>`` 或者 ``git <sub-command> --help`` 。

  编译文档依赖 asciidoc，因此需要先安装 asciidoc（如果尚未安装的话），然后编译文档。在编译文档时要花费很多时间，要有耐心。

  ::

    $ make prefix=/usr/local doc info
    $ sudo make prefix=/usr/local \
      install-doc install-html install-info

安装完毕之后，就可以在 ``/usr/local/bin`` 下找到 ``git`` 命令。

从Git版本库进行安装
-------------------------

如果在本地克隆一个 Git 版本库，就可以用版本库同步的方式获取最新版本的 Git，这样在下载不同版本的 Git 源代码时实际上采用了增量方式，会非常的节省时间和空间。当然使用这种方法的前提是已经用其他方法安装好了 Git。

* 克隆 Git 版本库到本地。

  ::

    $ git clone git://git.kernel.org/pub/scm/git/git.git
    $ cd git

* 如果本地已经克隆过一个 Git 版本库，直接在工作区中更新，以获得最新版本的 Git。

  ::

    $ git pull

* 执行清理工作，避免前一次编译的遗留文件造成影响。注意下面的操作将丢弃本地对 Git 代码的改动。

  ::

    $ git clean -fdx
    $ git reset --hard

* 查看 Git 的里程碑，选择最新的版本进行安装。例如 v1.7.3.5 。

  ::

    $ git tag
    ...
    v1.7.3.5

* 检出该版本的代码。

  ::

    $ git checkout v1.7.3.5

* 执行安装。例如安装到 /usr/local 目录下。

  ::

    $ make prefix=/usr/local all doc info
    $ sudo make prefix=/usr/local install \
      install-doc install-html install-info

我在撰写本书的过程中，就通过 Git 版本库的方式安装，在 /opt/git 目录下安装了多个不同版本的 Git，以测试 Git 的兼容性。使用类似下面的脚本，可以批量安装不同版本的 Git。

::

  #!/bin/sh

  for ver in      \
      v1.5.0      \
      v1.7.3.5    \
      v1.7.4-rc1  \
  ; do
      echo "Begin install Git $ver.";
      git reset --hard
      git clean -fdx
      git checkout $ver || exit 1
      make prefix=/opt/git/$ver all && \
      sudo make prefix=/opt/git/$ver install || exit 1
      echo "Installed Git $ver."
  done

命令补齐
-------------------------

Linux 的 shell 环境（bash）通过 bash-completion 软件包提供命令补齐功能，能够实现在录入命令参数时按一下或两下 TAB 键，实现参数的自动补齐或提示。例如输入 ``git com`` 后按下 TAB 键，会自动补齐为 ``git commit`` 。

通过包管理器方式安装 Git，一般都已经为 Git 配置好了自动补齐，但是如果是以源码编译方式安装 Git，就需要为命令补齐多做些工作。

* 将 Git 源码包中的命令补齐脚本复制到 bash-completion 对应的目录中。

  ::

    $ cp contrib/completion/git-completion.bash \
         /etc/bash_completion.d/

* 重新加载自动补齐脚本，使之在当前 shell 中生效。

  ::

    $ . /etc/bash_completion

* 为了能够在终端开启时自动加载 bash_completion 脚本，需要在本地配置文件 ``~/.bash_profile`` 或全局文件 ``/etc/bashrc`` 文件中添加下面的内容。

  ::

    if [ -f /etc/bash_completion ]; then
      . /etc/bash_completion
    fi

中文支持
-------------------

Git 的本地化做的并不完善，命令的输出以及命令的帮助还只能输出英文，也许在未来版本会使用 gettext 实现本地化，就像目前对 git-gui 命令所做的那样。

使用中文的用户最关心的问题还有：是否可以在提交说明中使用中文？是否可以使用中文文件名或者目录名？是否可以使用中文来命名分支或者里程碑？简单的说，可以在提交说明中使用中文，但是若使用非 UTF-8 字符集，则需要为 Git 做些设置。至于使用中文来命名文件、目录或引用，只有在使用 UTF-8 字符集的环境下才可以（Windows 用户使用 Cygwin），否则尽量避免使用。

**UTF-8 字符集**

Linux 平台的中文用户一般会使用 utf-8 字符集，Git在 utf-8 字符集下可以工作的非常好。

* 在提交时，可以在提交说明中输入中文。
* 显示提交历史，能够正常显示提交说明中的中文字符。
* 可以添加中文文件名的文件，并可以在同样 utf-8 字符集的 Linux 环境中克隆及检出。
* 可以创建带有中文字符的里程碑名称。

但是默认设置下，带有中文文件名的文件，在工作区状态输出、查看历史更改概要、以及在补丁文件中，文件名不能正确显示为中文，而是用若干8进制编码来显示中文，如下：

::

  $ git status -s
  ?? "\350\257\264\346\230\216.txt"

通过设置变量 ``core.quotepath`` 为 ``false`` ，就可以解决中文文件名在这些 Git 命令输出中的显示问题。

::

  $ git config --global core.quotepath false
  $ git status -s
  ?? 说明.txt

**GBK 字符集**

但如果 Linux 平台采用非 UTF-8 字符集，例如用 zh_CN.GBK 字符集编码（有人这么做么？），就要另外再做些工作了。

* 设置提交说明显示所使用的字符集为 gbk，这样使用 ``git log`` 查看提交说明才能够正确显示其中的中文。

  ::

    $ git config --global i18n.logOutputEncoding gbk

* 设置录入提交说明时所使用的字符集，以便在 commit 对象中对字符集正确标注。

  Git 在提交时并不会对提交说明进行从 GBK 字符集到 UTF-8 的转换，但是可以在提交说明中标注所使用的字符集，因此在非 UTF-8 字符集的平台录入中文，需要用下面指令设置录入提交说明的字符集，以便在 commit 对象中嵌入正确的编码说明。

  ::

    $ git config --global i18n.commitEncoding gbk


