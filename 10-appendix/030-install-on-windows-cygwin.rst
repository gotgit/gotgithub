Windows 下安装和使用 Git（Cygwin篇）
=====================================

在 Windows 下安装和使用 Git 有两个不同的方案，通过安装 msysGit 或者通过安装 Cygwin 来使用 Git。在这两种不同的方案下，Git 的使用和在 Linux 下使用完全一致。再有一个就是基于 msysGit 的图形界面工具 —— TortoiseGit，也就是在 CVS 和 SVN 时代就已经广为人知的 Tortoise 系列软件的 Git 版本。TortoiseGit 提供和资源管理器的整合，提供 Git 操作的图形化界面。

先介绍通过 Cygwin 来使用 Git 的原因，不是因为这是最便捷的方法，如果需要在 Windows 快速安装和使用 Git，下节介绍的 msysGit 才是。之所以将 Cygwin 放在前面介绍是因为本书在介绍 Git 原理部分以及介绍其他 Git 相关软件时用到了大量的开源工具，这些开源工具在 Cygwin 下很容易获得，而 msysGit 的 MSYS（Minimal SYStem，最简系统）则不能满足我们的需要。因此我建议使用 Windows 平台的读者在跟随本书学习 Git 的过程中，首选 Cygwin，当完成 Git 的学习后，无论是 msysGit 或者 TortoiseGit 也都会应对自足。

Cygwin 是一款伟大的软件，通过一个小小的DLL（cygwin1.dll）建立 Linux 和 Windows 系统调用及API之间的转换，实现了 Linux 下绝大多数软件到 Windows 的迁移。Cygwin 通过 cygwin1.dll 所建立的中间层和诸如 VMWare、VirtualBox 等虚拟机软件完全不同，不会对系统资源进行独占。像 VMWare 等虚拟机，只要启动一个虚拟机（操作系统），即使不在其中执行任何命令，同样会占用大量的系统资源：内存、CPU时间等等。

Cygwin 还提供了一个强大易用的包管理工具（setup.exe），实现了几千个开源软件包在 Cygwin 下便捷的安装和升级，Git 就是 Cygwin 下支持的几千个开源软件中的一员。

我对 Cygwin 有着深厚的感情，Cygwin 让我在 Windows 平台能用 Linux 的方式更有效率的做事，使用 Linux 风格的控制台替换 Windows 黑乎乎的、冰冷的、由 cmd.exe 提供的命令行。Cygwin 帮助我逐渐摆脱对 Windows 的依赖，当我完全转换到 Linux 平台时，没有感到一丝的障碍。


安装 Cygwin
-------------

安装 Cygwin 非常简单，访问其官方网站 http://www.cygwin.com/ ，下载安装程序 —— 一个只有几百KB的 ``setup.exe`` ，即可开始安装。

安装过程会让用户选择安装模式，可以选择网络安装、仅下载，或者通过本地软件包缓存（在安装过程自动在本地目录下建立软件包缓存）进行安装。如果是第一次安装 Cygwin，因为本地尚没有软件包缓存，当然只能选择从网络安装，如图3-4所示。


.. figure:: images/windows/cygwin-2.png
   :scale: 80

   图3-4：选择安装模式

接下来，Cygwin 询问安装目录，默认为 ``C:\\cygwin`` ，如图3-5所示。这个目录将作为 Cygwin shell 环境的根目录（根卷），Windows 的各个盘符将挂载在根卷一个特殊目录之下。

.. figure:: /images/windows/cygwin-3.png
   :scale: 80

   图3-5：选择安装目录

询问本地软件包缓存目录，默认是 ``setup.exe`` 所处的目录，如图3-6所示。

.. figure:: /images/windows/cygwin-4.png
   :scale: 80

   图3-6：选择本地软件包缓存目录

询问网络连接方式，是否使用代理等，如图3-7所示。默认会选择第一项：“直接网络连接”。如果一个团队有很多人要使用 Cygwin，架设一个能够提供软件包缓存的 HTTP 代理服务器会节省大量的网络带宽和节省大把的时间。用 Debian 的 apt-cacher-ng 就可以非常简单的搭建一个软件包代理服务器。图3-7显示的就是我在公司内网安装 Cygwin 时使用了我们公司内网的服务器 ``bj.ossxp.com`` 做为 HTTP 代理的截图，端口设置为 9999，因为这是 apt-cacher-ng 的默认端口。

.. figure:: /images/windows/cygwin-5-mirror.png
   :scale: 80

   图3-7：是否使用代理下载 Cygwin 软件包

选择一个 Cygwin 源，如图3-8所示。如果在上一个步骤选择了使用 HTTP 代理服务器，就必须选择 HTTP 协议的 Cygwin 源。

.. figure:: /images/windows/cygwin-6.png
   :scale: 80

   图3-8：选择 Cygwin 源

接下来就会从所选的 Cygwin 源下载软件包索引文件，然后显示软件包管理器界面，如图3-9所示。

.. figure:: /images/windows/cygwin-8.png
   :scale: 80

   图3-9：Cygwin 软件包管理器

Cygwin 的软件包管理器非常强大和易用（如果习惯了其界面）。软件包归类于各个分组中，点击分组前的加号就可以展开分组。在展开的 Admin 分组中，如图3-10所示（这个截图不是首次安装 Cygwin 的截图），有的软件包如 ``libattr1`` 已经安装过了，因为没有新版本而标记为“Keep”（保持）。至于没有安装过并且不准备安装的软件包则标记为 “Skip”（跳过）。

.. figure:: /images/windows/cygwin-8-expand-admin-group.png
   :scale: 80

   图3-10：Cygwin 软件包管理器展开分组

鼠标点击分组名称后面动作名称（文字“Default”），会进行软件包安装动作的切换。例如图3-11，将 Admin 分组的安装动作由“Default”（默认）切换为“Install”（安装），会看到 Admin 分组下的所有软件包都标记为安装（显示具体要安装的软件包版本号）。也可以通过鼠标点击，单独的为软件包进行安装动作的设定，可以强制重新安装、安装旧版本、或者不安装。

.. figure:: /images/windows/cygwin-8-expand-admin-group-install.png
   :scale: 80

   图3-11：Cygwin 软件包管理器展开分组

当通过软件包管理器对要安装的软件包定制完毕后，点击下一步，开始下载软件包、安装软件包和软件包后处理，直至完成安装。根据选择的软件包的多少，网络情况以及是否架设有代理服务器，首次安装 Cygwin 的时间可能从几分钟到几个小时不等。

安装 Git
-------------

默认安装的 Cygwin 没有安装 Git 软件包。如果在首次安装过程中忘记通过包管理器选择安装 Git 或其他相关软件包，可以在安装后再次运行 Cygwin 的安装程序 ``setup.exe`` 。当再次进入 Cygwin 包管理器界面时，在搜索框中输入 git。如图3-12所示。

.. figure:: /images/windows/cygwin-8-search-git.png
   :scale: 80

   图3-12：Cygwin 软件包管理器中搜索 git

从图3-12中看出在 Cygwin 中包含了很多和 Git 相关的软件包，把这些 Git 相关的软件包都安装吧，如图3-13所示。

.. figure:: /images/windows/cygwin-8-search-git-install.png
   :scale: 80

   图3-13：Cygwin 软件包管理器中安装 git

需要安装的其他软件包：

* git-completion: 提供 Git 命令自动补齐功能。安装该软件包会自动安装依赖的 bash-completion 软件包。
* openssh：SSH 客户端，提供 Git 访问 ssh 协议的版本库。
* vim：是 Git 缺省的编辑器。


Cygwin 的配置和使用
---------------------

运行 Cygwin，就会进入 shell 环境中，见到熟悉的 Linux 提示符。如图 3-14 所示。

.. figure:: /images/windows/cygwin-startup.png
   :scale: 80

   图3-14：运行 Cygwin

显示 Cygwin 中安装的软件包的版本，可以通过执行 ``cygcheck`` 命令来查看，例如查看 cygwin 软件包本身的版本：

::

  $ cygcheck -c cygwin
  Cygwin Package Information
  Package              Version        Status
  cygwin               1.7.7-1        OK

如何访问 Windows 的磁符
^^^^^^^^^^^^^^^^^^^^^^^^

刚刚接触 Cygwin 的用户遇到的头一个问题就是 Cygwin 如何访问 Windows 的各个磁盘目录，以及在 Windows 平台如何访问 Cygwin 中的目录？

执行 ``mount`` 命令，可以看到 Windows 下的盘符映射到 ``/cygdrive`` 特殊目录下。

::

  $ mount
  C:/cygwin/bin on /usr/bin type ntfs (binary,auto)
  C:/cygwin/lib on /usr/lib type ntfs (binary,auto)
  C:/cygwin on / type ntfs (binary,auto)
  C: on /cygdrive/c type ntfs (binary,posix=0,user,noumount,auto)
  D: on /cygdrive/d type ntfs (binary,posix=0,user,noumount,auto)

也就是说在 Windows 下的 ``C:\\Windows`` 目录，在 Cygwin 以路径 ``/cygdrive/c/Windows`` 进行访问。实际上 Cygwin 提供一个命令 ``cygpath`` 实现 Windows 平台和 Cygwin 之间目录名称的变换。如下：

::

  $ cygpath -u C:\\Windows
  /cygdrive/c/Windows

  $ cygpath -w ~/
  C:\cygwin\home\jiangxin\

从上面的示例也可以看出，Cygwin 下的用户主目录（即 ``/home/jiangxin/`` ）相当于 Windows 下的 ``C:\\cygwin\\home\\jiangxin\\`` 目录。

用户主目录不一致的问题
^^^^^^^^^^^^^^^^^^^^^^^^

如果其他某些软件（如 msysGit）为 Windows 设置了 HOME 环境变量，会影响到 Cygwin 中用户主目录的设置，甚至造成在 Cygwin 中不同命令有不同的用户主目录的设置。例如：Cygwin 下 Git 的用户主目录设置为 “/cygdrive/c/Documents and Settings/jiangxin”，而 SSH 客户端软件的主目录为 “/home/jiangxin”，这会造成用户的困惑。

出现这种情况，是因为 Cygwin 确定用户主目录有几个原则，依照顺序确定主目录。首先查看系统的 HOME 环境变量，其次查看 /etc/passwd 中为用户设置的主目录。有的软件遵照这个原则，而有些 Cygwin 应用如 ssh，却没有使用 HOME 环境变量而直接使用 /etc/passwd 中的的设置。要想避免在同一个 Cygwin 环境下有两个不同的用户主目录设置，可以采用下面两种方法。

* 方法1：修改 Cygwin 启动的批处理文件（如： ``C:\\cygwin\\Cygwin.bat`` ），在批处理的开头添加如下的一行，就可以清除其他软件为 Windows 引入的 HOME 环境变量。

  ::

    set HOME=

* 方法2：如果希望使用 HOME 环境变量指向的主目录，则通过手工编辑 /etc/passwd 文件，将其中用户主目录修改成 HOME 环境变量所指向的目录。

命令行补齐忽略文件大小写
^^^^^^^^^^^^^^^^^^^^^^^^^

Windows 的文件系统忽略文件名大小写，在 Cygwin 下最好对命令行补齐进行相关设置以忽略大小写，这样使用起来更方便。

编辑文件 ``~/.inputrc`` ，在其中添加设置 "set completion-ignore-case on" ，或者取消已有相关设置前面的井号注释符。修改完毕后，再重新进入 Cygwin，就可以实现文件名补齐对大小写的忽略。

忽略文件权限的可执行位
^^^^^^^^^^^^^^^^^^^^^^^^^

Linux、Unix、Mac OS X 下的可执行文件在文件权限有特殊的设置（设置文件的可执行位），Git 可以跟踪文件的可执行位，即在添加文件时会把文件的权限也记录其中。在 Windows 上，缺乏对文件可执行位的支持和需要，虽然 Cygwin 可以模拟 Linux 下的文件授权并对文件的可执行位进行支持，但一来为支持文件权限而调用 Cygwin 的 stat() 和 lstat() 函数会比 Windows 自身的 Win32 API 要慢两倍，二来对于非跨平台项目也没有必要对文件权限位进行跟踪，还有其他 Windows 下的工具及操作可能会破坏文件的可执行位，导致 Cygwin 下的 Git 认为文件的权限更改需要重新提交。通过下面的配置，可以禁止 Git 对文件权限的跟踪：

::

  $ git config --system core.fileMode false

在此模式下，当已添加到版本库中的文件其权限的可执行位改变时，该文件不会显示有改动。新增到版本库的文件，都以 100644 的权限添加（忽略可执行位），无论文件本身是否设置为可执行。

关于 Cygwin 的更多定制和帮助，参见网址： http://www.cygwin.com/cygwin-ug-net/ 。

Cygwin 下 Git 的中文支持
-------------------------

Cygwin 当前版本 1.7.x，对中文的支持非常好。无需任何配置就可以在 Cygwin 的窗口内输入中文，以及执行 ``ls`` 命令显示中文文件名。这与我记忆中的6、7年前的 Cygwin 1.5.x 完全不一样了。老版本的 Cygwin 还需要做一些工作才能在控制台输入中文和显示中文，但是最新的 Cygwin 已经完全不需要了。反倒是后面要介绍的 msysGit 的 shell 环境仍然需要做出类似（老版本 Cygwin）的改动才能够正常显示和输入中文。

Cygwin 默认使用 UTF-8 字符集，并巧妙的和 Windows 系统的字符集之间进行转换。在 Cygwin 下执行 ``locale`` 命令查看 Cygwin 下正在使用的字符集。

::

  $ locale
  LANG=C.UTF-8
  LC_CTYPE="C.UTF-8"
  LC_NUMERIC="C.UTF-8"
  LC_TIME="C.UTF-8"
  LC_COLLATE="C.UTF-8"
  LC_MONETARY="C.UTF-8"
  LC_MESSAGES="C.UTF-8"
  LC_ALL=

正因如此，Cygwin 下的 Git 对中文支持非常出色，虽然中文 Windows 本身使用 GBK 字符集，但是在 Cygwin 下 Git 的行为就如同工作在 UTF-8 字符集的 Linux 下，对中文的支持非常的好。

* 在提交时，可以在提交说明中输入中文。
* 显示提交历史，能够正常显示提交说明中的中文字符。
* 可以添加中文文件名的文件，并可以在使用 utf-8 字符集的 Linux 环境中克隆及检出。
* 可以创建带有中文字符的里程碑名称。

但是和 Linux 平台一样，在默认设置下，带有中文文件名的文件，在工作区状态输出、查看历史更改概要、以及在补丁文件中，文件名不能正确显示为中文，而是用若干8进制编码来显示中文，如下：

::

  $ git status -s
  ?? "\350\257\264\346\230\216.txt"

通过设置变量 ``core.quotepath`` 为 ``false`` ，就可以解决中文文件名在这些 Git 命令输出中的显示问题。

::

  $ git config --global core.quotepath false
  $ git status -s
  ?? 说明.txt

Cygwin 下 Git 访问 SSH 服务
----------------------------

在本书第5篇第29章介绍的公钥认证方式访问 Git 服务，是 Git 写操作最重要的服务。公钥认证方式访问 SSH 协议的 Git 服务器时无需输入口令，而且更为安全。使用公钥认证就涉及到创建公钥/私钥对，以及在 SSH 连接时选择哪一个私钥的问题（如果建立有多个私钥）。

Cygwin 下的 openssh 软件包提供的 ssh 命令和 Linux 下的没有什么区别，也提供 ssh-keygen 命令管理 SSH 公钥/私钥对。但是 Cygwin 当前的 openssh（版本号：5.7p1-1）有一个 Bug，偶尔在用 Git 克隆使用 SSH 协议的版本库时会中断，无法完成版本库克隆。如下：

::

  $ git clone git@bj.ossxp.com:ossxp/gitbook.git
  Cloning into gitbook...
  remote: Counting objects: 3486, done.
  remote: Compressing objects: 100% (1759/1759), done.
  fatal: The remote end hung up unexpectedly MiB | 3.03 MiB/s
  fatal: early EOFs:  75% (2615/3486), 13.97 MiB | 3.03 MiB/s
  fatal: index-pack failed

如果读者也遇到同样的问题，建议使用 PuTTY 提供的 plink.exe 做为 SSH 客户端，替代存在问题的 Cygwin 自带的 ssh 命令。

安装 PuTTY
^^^^^^^^^^

PuTTY 是 Windows 下一个开源软件，提供 SSH 客户端服务，还包括公钥管理相关工具。访问 PuTTY 的主页（http://www.chiark.greenend.org.uk/~sgtatham/putty/），下载并安装 PuTTY。安装完毕会发现 PuTTY 软件包包含了好几个可执行程序，对于和 Git 整合，下面几个命令会用到。

* Plink： 即 plink.exe，是命令行的 SSH 客户端，用于替代 ssh 命令。默认安装于 ``C:\\Program Files\\PuTTY\\plink.exe`` 。
* PuTTYgen ：用于管理 PuTTY 格式的私钥，也可以用于将 openssh 格式的私钥转换为 PuTTY 格式的私钥。
* Pageant ：是 SSH 认证代理，运行于后台，负责为 SSH 连接提供私钥访问服务。

PuTTY 格式的私钥
^^^^^^^^^^^^^^^^^

PuTTY 使用自定义格式的私钥文件（扩展名为 ``.ppk`` ），而不能直接使用 openssh 格式的私钥。即用 openssh 的 ssh-keygen 命令创建的私钥不能直接被 PuTTY 拿过来使用，必需经过转换。程序 PuTTYgen 可以实现私钥格式的转换。

运行 PuTTYgen 程序，如图3-15所示。

.. figure:: /images/windows/putty-keygen-1.png
   :scale: 80

   图3-15：运行 PuTTYgen 程序

PuTTYgen 既可以重新创建私钥文件，也可以通过点击加载按钮（load）读取 openssh 格式的私钥文件，从而可以将其转换为 PuTTY 格式私钥。点击加载按钮，会弹出文件选择对话框，选择 openssh 格式的私钥文件（如文件 id_rsa），如果转换成功，会显示如图3-16的界面。

.. figure:: /images/windows/putty-keygen-2.png
   :scale: 80

   图3-16：PuTTYgen 完成私钥加载

然后点击 “Save private key”（保存私钥），就可以将私钥保存为 PuTTY 的 ``.ppk`` 格式的私钥。例如将私钥保存到文件 ``~/.ssh/jiangxin-cygwin.ppk`` 中。

Git 使用 Pageant 进行公钥认证
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Git 在使用命令行工具 Plink（ ``plink.exe`` ）做为 SSH 客户端访问 SSH 协议的版本库服务器时，如何选择公钥呢？使用 Pageant 是一个非常好的选择。Pageant 是 PuTTY 软件包中为各个 PuTTY 应用提供私钥请求的代理软件，当 Plink 连接 SSH 服务器需要请求公钥认证时，Pageant 就会提供给 Plink 相应的私钥。

运行 Pageant ，启动后显示为托盘区中的一个图标，在后台运行。当使用鼠标右键单击 Pageant 的图标，就会显示弹出菜单如图3-17所示。

.. figure:: /images/windows/pageant.png
   :scale: 80

   图3-17：Pageant 的弹出菜单

点击弹出菜单中的 “Add Key”（添加私钥）按钮，弹出文件选择框，选择扩展名为 ``.ppk`` 的 PuTTY 格式的公钥，即完成了 Pageant 的私钥准备工作。

接下来，还需要对 Git 进行设置，设置 Git 使用 ``plink.exe`` 做为 SSH 客户端，而不是缺省的 ``ssh``  命令。通过设置 GIT_SSH 环境变量即可实现。

::

  $ export GIT_SSH=/cygdrive/c/Program\ Files/PuTTY/plink.exe

上面在设置 GIT_SSH 环境变量的过程中，使用了 Cygwin 格式的路径，而非 Windows 格式，这是因为 Git 是在 Cygwin 的环境中调用 ``plink.exe`` 命令的，当然要使用 Cygwin 能够理解的路径。

然后就可以用 Git 访问 SSH 协议的 Git 服务器了。运行在后台的 Pageant 会在需要的时候为 plink.exe 提供私钥访问服务。但在首次连接一个使用 SSH 协议的 Git 服务器的时候，很可能会因为远程SSH服务器的公钥没有经过确认导致 git 命令执行失败。如下所示。

::

  $ git clone git@bj.ossxp.com:ossxp/gitbook.git
  Cloning into gitbook...
  The server's host key is not cached in the registry. You
  have no guarantee that the server is the computer you
  think it is.
  The server's rsa2 key fingerprint is:
  ssh-rsa 2048 49:eb:04:30:70:ab:b3:28:42:03:19:fe:82:f8:1a:00
  Connection abandoned.
  fatal: The remote end hung up unexpectedly

这是因为首次连接一个 SSH 服务器时，要对其公钥进行确认（以防止被钓鱼），而运行于 Git 下的 ``plink.exe`` 没有机会从用户那里获取输入以建立对该SSH服务器公钥的信任，因此 Git 访问失败。解决办法非常简单，就是直接运行 ``plink.exe`` 连接一次远程 SSH 服务器，对公钥确认进行应答。如下：

::

  $ /cygdrive/c/Program\ Files/PuTTY/plink.exe git@bj.ossxp.com
  The server's host key is not cached in the registry. You
  have no guarantee that the server is the computer you
  think it is.
  The server's rsa2 key fingerprint is:
  ssh-rsa 2048 49:eb:04:30:70:ab:b3:28:42:03:19:fe:82:f8:1a:00
  If you trust this host, enter "y" to add the key to
  PuTTY's cache and carry on connecting.
  If you want to carry on connecting just once, without
  adding the key to the cache, enter "n".
  If you do not trust this host, press Return to abandon the
  connection.
  Store key in cache? (y/n)

输入 “y”，将公钥保存在信任链中，以后再次连接就不会弹出该确认应答了。当然执行 Git 命令，也就可以成功执行了。

使用自定义 SSH 脚本取代 Pageant
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

使用 Pageant 还要在每次启动 Pageant 时手动选择私钥文件，比较的麻烦。实际上可以创建一个脚本对 ``plink.exe`` 进行封装，在封装的脚本中指定私钥文件，这样就可以不必使用 Pageant 而实现公钥认证了。

例如：创建脚本 ``~/bin/ssh-jiangxin`` ，文件内容如下了：

::

  #!/bin/sh

  /cygdrive/c/Program\ Files/PuTTY/plink.exe -i \
      c:/cygwin/home/jiangxin/.ssh/jiangxin-cygwin.ppk $*

设置该脚本为可执行。

::

  $ chmod a+x ~/bin/ssh-jiangxin

通过该脚本和远程 SSH 服务器连接，使用下面的命令：

::

  $ ~/bin/ssh-jiangxin git@bj.ossxp.com
  Using username "git".
  Server refused to allocate pty
  hello jiangxin, the gitolite version here is v1.5.5-9-g4c11bd8
  the gitolite config gives you the following access:
       R          gistore-bj.ossxp.com/.*$
       R          gistore-ossxp.com/.*$
    C  R  W       ossxp/.*$
       R  W       test/repo1
       R  W       test/repo2
       R  W       test/repo3
      @R @W       test/repo4
   @C @R  W       users/jiangxin/.+$


设置 GIT_SSH 变量，使之指向新建立的脚本，然后就可以脱离 Pageant 来连接 SSH 协议的 Git 库了。

::

  $ export GIT_SSH=~/bin/ssh-jiangxin
