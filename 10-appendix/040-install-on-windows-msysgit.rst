Windows 下安装和使用 Git（msysGit篇）
=====================================

运行在 Cygwin 下的 Git 不是直接使用 Windows 的系统调用，而是通过二传手 ``cygwin1.dll`` 来进行，虽然 Cygwin 的 git 命令能够在 Windows 下的 ``cmd.exe`` 命令窗口中运行的非常好，但 Cygwin 下的 Git 并不能看作是 Windows 下的原生程序。相比 Cygwin 下的 Git，msysGit 是原生的 Windows 程序，msysGit 下运行的 Git 直接通过 Windows 的系统调用运行。

msysGit 的名字前面的四个字母来源于 MSYS 项目。MSYS 项目源自于 MinGW（Minimalist GNU for Windows，最简GNU工具集），通过增加了一个 bash 提供的shell 环境以及其他相关工具软件，组成了一个最简系统（Minimal SYStem），简称 MSYS。利用 MinGW 提供的工具，以及 Git 针对 MinGW 的一个分支版本，在 Windows 平台为 Git 编译出一个原生应用，接合 MSYS 就组成了 msysGit。

安装 msysGit
-------------

安装 msysGit 非常简单，访问 msysGit 的项目主页（http://code.google.com/p/msysgit/），下载 msysGit。最简单的方式是下载名为 ``Git-<VERSION>-preview<DATE>.exe`` 的软件包，如： ``Git-1.7.3.1-preview20101002.exe`` 。如果有时间和耐心，喜欢观察 Git 是如何在 Windows 上是编译为原生应用的，也可以下载带 ``msysGit-fullinstall-`` 前缀的软件包。

点击下载的安装程序（如 ``Git-1.7.3.1-preview20101002.exe`` ），开始安装，如图3-18。

.. figure:: /images/windows/msysgit-1.png
   :scale: 80

   图3-18：启动 msysGit 安装

默认安装到 ``C:\\Program Files\\Git`` 目录中。

.. figure:: /images/windows/msysgit-3.png
   :scale: 80

   图3-19：选择 msysGit 的安装目录

在安装过程中会询问是否修改环境变量，如图3-20。默认选择“Use Git Bash Only”，即只在 msysGit 提供的 shell 环境（类似 Cygwin）中使用 Git，不修改环境变量。注意如果选择最后一项，会将 msysGit 所有的可执行程序全部加入 Windows 的 PATH 路径中，有的命令会覆盖 Windows 相同文件名的程序（如 find.exe 和 sort.exe）。而且如果选择最后一项，还会为 Windows 添加 HOME 环境变量，如果安装有 Cygwin，Cygwin 会受到 msysGit 引入的 HOME 环境变量的影响（参见前面 3.3.3 节的相关讨论）。

.. figure:: /images/windows/msysgit-6.png
   :scale: 80

   图3-20：是否修改系统的环境变量

还会询问换行符的转换方式，使用默认设置就好。参见图3-21。关于换行符转换，参见本书第8篇相关章节。

.. figure:: /images/windows/msysgit-8.png
   :scale: 80

   图3-21：换行符转换方式

根据提示，完成 msysGit 的安装。

msysGit 的配置和使用
---------------------

完成 msysGit 的安装后，点击 Git Bash 图标，启动 msysGit，如图3-22。会发现 Git Bash 的界面和 Cygwin 的非常相像。

.. figure:: /images/windows/msysgit-startup.png
   :scale: 80

   图3-22：启动 Git Bash

如何访问 Windows 的磁符
^^^^^^^^^^^^^^^^^^^^^^^^

在 msysGit 下访问 Windows 的各个盘符，要比 Cygwin 简单，直接通过 "``/c``" 即可访问 Windows 的 C: 盘，用 "``/d``" 访问 Windows 的 D: 盘。

::

  $ ls -ld /c/Windows
  drwxr-xr-x  233 jiangxin Administ        0 Jan 31 00:44 /c/Windows

至于 msysGit 的根目录，实际上就是 msysGit 安装的目录，如：“C:\\Program Files\\Git”。

命令行补齐和忽略文件大小写
^^^^^^^^^^^^^^^^^^^^^^^^^^

msysGit 缺省已经安装了 Git 的命令补齐功能，并且在对文件名命令补齐时忽略大小写。这是因为 msysGit 已经在配置文件 ``/etc/inputrc`` 中包含了下列的设置:

::

  set completion-ignore-case on

msysGit shell 环境的中文支持
--------------------------------

在介绍 Cygwin 的章节中曾经提到过，msysGit 的 shell 环境的中文支持相当于老版本的 Cygwin，需要配置才能够实现录入中文和显示中文。

中文录入问题
^^^^^^^^^^^^^

缺省安装的 msysGit 的 shell 环境无法输入中文。为了能在 shell 界面中输入中文，需要修改配置文件 ``/etc/inputrc`` ，增加或修改相关配置如下：

::

  # disable/enable 8bit input
  set meta-flag on
  set input-meta on
  set output-meta on
  set convert-meta off

关闭 Git Bash 再重启，就可以在 msysGit 的 shell 环境中输入中文了。

::

  $ echo 您好
  您好

分页器中文输出问题
^^^^^^^^^^^^^^^^^^^

当对 ``/etc/inputrc`` 进行正确的配置之后，能够在 shell 下输入中文，但是执行下面的命令会显示乱码。这显然是 ``less`` 分页器命令导致的问题。

::

  $ echo 您好 | less
  <C4><FA><BA><C3>

通过管道符调用分页器命令 ``less`` 后，原本的中文输出变成了乱码显示。这将会导致 Git 很多命令的输出都会出现中文乱码问题，因为 Git 大量的使用 ``less`` 命令做为分页器。之所以 ``less`` 命令出现乱码，是因为该命令没有把中文当作正常的字符，可以通过设置 LESSCHARSET 环境变量，将 utf-8 编码字符视为正规字符显示，则中文就能正常显示了。下面的操作，可以在 ``less`` 分页器中正常显示中文。

::

  $ export LESSCHARSET=utf-8
  $ echo 您好 | less
  您好  

编辑配置文件 ``/etc/profile`` ，将对环境变量 LESSCHARSET 的设置加入其中，以便 msysGit 的 shell 环境一启动即加载。

::

  declare -x LESSCHARSET=utf-8

ls 命令对中文文件名的显示
^^^^^^^^^^^^^^^^^^^^^^^^^^

最常用的显示目录和文件名列表的命令 ``ls`` 对中文文件名的显示有问题。下面的命令创建了一个中文文件名的文件，显示文件内容中的中文没有问题，但是显示文件名本身会显示为一串问号。

::

  $ echo 您好 > 您好.txt

  $ cat \*.txt
  您好

  $ ls \*.txt
  ????.txt

实际上只要在 ``ls`` 命令后添加参数 ``--show-control-chars`` 即可正确显示中文。

::

  $ ls --show-control-chars *.txt
  您好.txt

为方便起见，可以为 ``ls`` 命令设置一个别名，这样就不必在输入 ``ls`` 命令时输入长长的参数了。

::

  $ alias ls="ls --show-control-chars"

  $ ls \*.txt
  您好.txt

将上面的 alias 命令添加到配置文件 ``/etc/profile`` 中，实现在每次运行 Git Bash 时自动加载。

msysGit 中 Git 的中文支持
--------------------------------

非常遗憾的是 msysGit 中的 Git 对中文支持没有 Cygwin 中的 Git 做的那么好，msysGit 中的 Git 对中文支持的程度，就相当于前面讨论过的 Linux 使用了 GBK 字符集时 Git 的情况。

* 未经配置的 msysGit 提交时，如果在提交说明中输入中文，从 Linux 平台或其他 UTF-8 字符集平台上查看提交说明显示乱码。
* 同样从 Linux 平台或者其他使用 UTF-8 字符集平台进行的提交，若提交说明包含中文，在未经配置的 msysGit 中也显示乱码。
* 如果使用 msysGit 向版本库中添加带有中文文件名的文件，在 Linux（或其他 utf-8）平台检出文件名显示为乱码。反之亦然。
* 不能创建带有中文字符的引用（里程碑、分支等）。

如果希望版本库中出现使用中文文件名的文件，最好不要使用 msysGit，而是使用 Cygwin 下的 Git。而如果只是想在提交说明中使用中文，经过一定的设置 msysGit 还是可以实现的。

为了解决提交说明显示乱码问题，msysGit 要为 Git 设置参数 i18n.logOutputEncoding，将提交说明的输出编码设置为 gbk。

::

  $ git config --system i18n.logOutputEncoding gbk

Git 在提交时并不会对提交说明进行从 GBK 字符集到 UTF-8 的转换，但是可以在提交说明中标注所使用的字符集，因此在非 UTF-8 字符集的平台录入中文，需要用下面指令设置录入提交说明的字符集，以便在 commit 对象中嵌入正确的编码说明。为了使 msysGit 提交时输入的中文说明能够在 Linux 或其他使用 UTF-8 编码的平台中正确显示，还必须对参数 i18n.commitEncoding 设置。

::

  $ git config --system i18n.commitEncoding gbk


同样，为了能够让带有中文文件名的文件，在工作区状态输出、查看历史更改概要、以及在补丁文件中，能够正常显示，要为 Git 配置 core.quotepath 变量，将其设置为 false。但是要注意在 msysGit 中添加中文文件名的文件，只能在 msysGit 环境中正确显示，而在其他环境（Linux, Mac OS X, Cygwin）中文件名会出现乱码。

::

  $ git config --system core.quotepath false
  $ git status -s
  ?? 说明.txt

注意：如果同时安装了 Cygwin 和 msysGit（可能配置了相同的用户主目录），或者因为中文支持问题而需要单独为 TortoiseGit 准备一套 msysGit 时，为了保证不同的 msysGit 之间，以及和 Cygwin 之间的配置不会互相影响，而在配置 Git 环境时使用 ``--system`` 参数。这是因为不同的 msysGit 安装以及 Cygwin 有着不同的系统配置文件，但是用户级配置文件位置却可能重合。

使用 SSH 协议
------------------

msysGit 软件包包含的 ssh 命令和 Linux 下的没有什么区别，也提供 ssh-keygen 命令管理 SSH 公钥/私钥对。在使用 msysGit 的 ssh 命令时，没有遇到 Cygwin 中的 ssh 命令（版本号：5.7p1-1）不稳定的问题，即 msysGit 下的 ssh 命令可以非常稳定的工作。

如果需要和 Windows 有更好的整合，希望使用图形化工具管理公钥，也可以使用 PuTTY 提供的 plink.exe 做为 SSH 客户端。关于如何使用 PuTTY 可以参见 3.3.5 节 Cygwin 和 PuTTY 整合的相关内容。

TortoiseGit 的安装和使用
-------------------------

TortoiseGit 提供了 Git 和 Windows 资源管理器的整合，提供了 Git 的图形化操作界面。像其他 Tortoise 系列产品（TortoiseCVS, TortoiseSVN）一样，Git 工作区的目录和文件的图标附加了标识版本控制状态的图像，可以非常直观的看到哪些文件被更改了需要提交。通过对右键菜单的扩展，可以非常方便的在资源管理器中操作 Git 版本库。

TortoiseGit 是对 msysGit 命令行的封装，因此需要先安装 msysGit。安装 TortoiseGit 非常简单，访问网站 http://code.google.com/p/tortoisegit/ ，下载安装包，然后根据提示完成安装。

安装过程中会询问要使用的 SSH 客户端，如图3-23。缺省使用内置的 TortoisePLink（来自 PuTTY 项目）做为 SSH 客户端。

.. figure:: /images/windows/tgit-3.png
   :scale: 80

   图3-23：启动 Git Bash

TortoisePLink 和 TortoiseGit 的整合性更好，可以直接通过对话框设置 SSH 私钥（PuTTY格式），而无需再到字符界面去配置 SSH 私钥和其他配置文件。如果安装过程中选择了 OpenSSH，可以在安装完毕之后，通过 TortoiseGit 的设置对话框重新选择 TortoisePLink 做为缺省 SSH 客户端程序，如图3-24。

.. figure:: /images/windows/tgit-settings-network-plink.png
   :scale: 80

   图3-24：配置缺省 SSH 客户端

当配置使用 TortoisePLink 做为缺省 SSH 客户端时，在执行克隆操作时，在操作界面中可以选择一个 PuTTY 格式的私钥文件进行认证，如图3-25。

.. figure:: /images/windows/tgit-clone.png
   :scale: 80

   图3-25：克隆操作选择 PuTTY 格式私钥文件

如果连接一个服务器的 SSH 私钥需要更换，可以通过 Git 远程服务器配置界面对私钥文件进行重新设置。如图3-26。

.. figure:: /images/windows/tgit-settings-remote.png
   :scale: 80

   图3-26：更换连接远程 SSH 服务器的私钥

如果安装有多个 msysGit 拷贝，也可以通过 TortoiseGit 的配置界面进行选择，如图3-27。

.. figure:: /images/windows/tgit-settings-general.png
   :scale: 80

   图3-27：配置 msysGit 的可执行程序位置

TortoiseGit 的中文支持
-------------------------

TortoiseGit 虽然在底层调用了 msysGit，但是 TortoiseGit 的中文支持和 msysGit 有区别，甚至前面介绍 msysGit 中文支持时所进行的配制会破坏 TortoiseGit。

TortoiseGit 在提交时，会将提交说明转换为 UTF-8 字符集，因此无须对 i18n.commitEncoding 变量进行设置。相反，如果设置了 i18n.commitEncoding 为 gbk 或其他，则在提交对象中会包含错误的编码设置，有可能为提交说明的显示带来麻烦。

TortoiseGit 在显示提交说明时，认为所有的提交说明都是 UTF-8 编码，会转换为合适的 Windows 本地字符集显示，而无须设置 i18n.logOutputEncoding 变量。因为当前版本的 TortoiseGit 没有对提交对象中的 encoding 设置进行检查，因此使用 GBK 字符集的提交说明中的中文不能正常显示。

因此，如果需要同时使用 msysGit 的文字界面 Git Bash 以及 TortoiseGit，并需要在提交说明中使用中文，可以安装两套 msysGit，并确保 TortoiseGit 关联的 msysGit 没有对 i18n.commitEncoding 进行设置。

TortoiseGit 对使用中文命名的文件和目录的支持和 msysGit 一样，都存在缺陷，因此应当避免在 msysGit 和 TortoiseGit 中添加用中文命名的文件和目录，如果确实需要，可以使用 Cygwin。

