浏览托管项目
===============

GitHub的账户已经建立好了，在建立自己的项目托管之前，看看别人是怎么做的。在GitHub中搜索字符串“GotGit”，可以搜索到我建立的一个项目，项目地址是: https://github.com/gotgit/gotgit/ 。由上至下，GotGit项目首页可以分为四个区域。

* 区域一：项目概要介绍及版本库URL等。

  项目GotGit托管在组织账号 gotgit 之下 [#]_ ，并且当前有4个关注用户和2个项目分支。最下面一行显示版本库的访问地址，只显示了HTTP和Git-daemon两个协议的URL地址，这是因为当前用户对该版本库只具有只读权限，因此没有显示SSH协议的URL地址。

  .. figure:: /images/join-github/gotgit-repo-tree-1.png
     :scale: 100

     图2-10：版本库概要信息

  使用任意一种协议均可克隆该Git版本库，但要注意只有Git 1.6.6及以上版本才支持智能HTTP协议，低版本Git则无法用HTTP协议克隆GitHub上的版本库 [#]_ 。

  ::

    $ git clone https://github.com/gotgit/gotgit.git

  或者使用Git-daemon协议。

  ::

    $ git clone git://github.com/gotgit/gotgit.git


* 区域二：显示提交说明、提交用户头像、提交时间等提交信息。右侧还显示此次提交对应的提交ID、树ID，及父提交ID等。

  .. figure:: /images/join-github/gotgit-repo-tree-2.png
     :scale: 100
  
     图2-11：提交信息
  
* 区域三：目录树。每个目录和文件后面还显示最后一次变更的提交说明。

  .. figure:: /images/join-github/gotgit-repo-tree-3.png
     :scale: 100
  
     图2-12：目录树
  
* 区域四：根目录下的文件 ``README.mkd`` 格式化为HTML输出显示。

  GitHub内置了多种文本标记语言的支持，如Markdown、Textile、reStructuredText、asciidoc、Wiki等。当发现根目录下的 ``README`` 文件后，会根据其使用的标记语言类别，自动转换为HTML格式显示。

  .. figure:: /images/join-github/gotgit-repo-tree-4.png
     :scale: 100
  
     图2-13：README文件

在GitHub的页面中可以使用键盘快捷键，按下问号（?）会在弹出窗口显示当前页面可用的快捷键。

在项目的首页可以按下字母"p"，显示当前提交的父提交。图2-14就是当按下字母"p"后，切换到父提交（对照图2-11）。

.. figure:: /images/join-github/gotgit-repo-tree-parent.png
   :scale: 100

   图2-14：快捷键"p"切换到父提交

按下字母"f"，开启目录树中文件查找和过滤。图2-15就是在按下字母"f"后，当逐一输入单词"download"时的过滤效果。

.. figure:: /images/join-github/gotgit-repo-tree-filter.png
   :scale: 100

   图2-15：快捷键t开启过滤器在目录树中搜索

点击菜单中的“Commits”（提交）显示版本库GotGit的提交历史，如图2-16所示。

.. figure:: /images/join-github/gotgit-repo-commit-history.png
   :scale: 100

   图2-16：提交历史

提交历史页面也支持快捷键，按下问号（?）或者点击页面中的键盘标志会显示快捷键帮助。其中快捷键"j"和"k"用于在提交列表中向上和向下选择提交，在选中的提交按下回车键，会显示该提交包含的文件改动差异，如图2-17所示。

.. figure:: /images/join-github/gotgit-repo-commit-diff.png
   :scale: 100

   图2-17：文本文件改动差异

在文本文件的差异比较中，不但将有差异的行标识出来，还将行内具体改动的字词用特殊颜色进行了标识，不由得感叹GitHub的细致入微。

GitHub还支持对图形文件的差异比较，并提供四种比较方式。在如下地址: http://goo.gl/Gy85b [#]_ 提供了一个示例提交，尝试一下使用不同的图形文件比较方式，查看该提交对图形文件的改动。

* 默认修改前后的两幅图片左右并排显示，如图2-18所示。

  .. figure:: /images/join-github/image-diff-2-up.png
     :scale: 100
  
     图2-18：左右并排比较图形文件差异
  
* 选择交换显示比较修改前后的图片，用鼠标左右拖动进度条，可以非常直观地看到图片的差异。如图2-19所示。

  .. figure:: /images/join-github/image-diff-swipe.png
     :scale: 100
  
     图2-19：交换显示图形文件比较差异

* 还提供洋葱皮和色差比较，自己动手试试吧。

网络图是GitHub的一大特色，显示一个项目的版本库被不同用户派生（Fork）后，各个版本库的派生关系。这个网络图最早使用Flash实现的，目前已经改为HTML5实现 [#]_ 。图2-20的示例网络图来自于Gitosis项目。

.. figure:: /images/join-github/network-graph.png
   :scale: 100

   图2-20：Gitosis项目网络图

Pull Requests（拉拽请求）是派生（Fork）版本库的开发者向项目贡献提交的方法。如图2-21所示，GotGit项目目前没有未被处理的Pull Request，但是可以看到有一个已经关闭的Pull Request请求。

.. figure:: /images/join-github/gotgit-repo-pull-request.png
   :scale: 100

   图2-21：Pull Requests界面

这个Pull Request是GitHub用户agate发现了GotGit脚本中一个和ruby1.9不兼容的Bug，当我把agate派生版本库中的提交合并到GotGit版本库后，该Pull Request自动关闭。整个Pull Request的变更记录如图2-22所示。

.. figure:: /images/join-github/gotgit-repo-pull-request-detail.png
   :scale: 100

   图2-22：Pull Request的变更历史

缺陷追踪（Issue）也是GitHub工作流中一个重要的组件。GotGit项目用缺陷跟踪系统帮助维护《Git权威指南》一书的勘误，图2-23可以看到已关闭问题中有一个网友发现书的中的文字错误。

.. figure:: /images/join-github/gotgit-repo-issue.png
   :scale: 100

   图2-23：缺陷追踪

GitHub还为项目提供图像化报表分析。图2-24是GotGit项目中用到的开发语言分布图。

.. figure:: /images/join-github/gotgit-repo-graph-lang.png
   :scale: 100

   图2-24：GotGit项目开发语言分布图

图2-25是开发者对GotGit项目贡献分布图。

.. figure:: /images/join-github/gotgit-repo-graph-impact.png
   :scale: 100

   图2-25：GotGit项目贡献分布图

----

.. [#] 项目 gotgit 最早由用户 ossxp-com 创建，现已转移到组织 gotgit 账号之下。
.. [#] https://github.com/blog/809-git-dumb-http-transport-to-be-turned-off-in-90-days
.. [#] 短格式URL，实际对应于: https://github.com/cameronmcefee/Image-Diff-View-Modes/commit/8e95f70c9c47168305970e91021072673d7cdad8
.. [#] https://github.com/blog/621-bye-bye-flash-network-graph-is-now-canvas
