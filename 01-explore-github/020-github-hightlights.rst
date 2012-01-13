.. _github-hightlights:

GitHub亮点
===============

是什么让GitHub如此成功？GitHub有什么魔力？

1. 只用Git。

   GitHub只支持Git格式的版本库托管，而不像其他开源项目托管平台还对CVS、SVN、\
   Hg等格式的版本库进行托管。GitHub的哲学很简单，既然Git是最好的版本控制系统\
   之一（对于很多喜欢Git和GitHub的人没有之一），没有必要为兼顾其他版本控制\
   系统而牺牲Git某些独有特性。因此没有支持其他版本控制系统的历史负担，\
   是GitHub成功的要素之一。

   只用Git并不是说GitHub完全无视其他版本控制系统的使用者，相反，GitHub面向\
   SVN（Subversion）用户和Hg（Mercurial）用户开发了接口，让这些用户可以使用\
   SVN或Hg的客户端工具访问Git版本库。

2. 对Git的完整支持。

   相比其他开源项目托管平台，GitHub对Git版本库提供了完整的协议支持，支持HTTP\
   智能协议、Git-daemon、SSH协议。相比只支持HTTP协议的GoogleCode，GitHub\
   通过SSH协议可以实现版本库访问的无口令认证\ [#]_\ 。

3. 无处不在的Git。

   除了在版本库托管上使用Git，Git还被GitHub应用到更多领域。维基使用Git，\
   可以通过克隆维基所在的版本库，离线修改维基；在线粘贴数据的Gist网站\ [#]_\
   使用Git，记录变更历史；以及在Jekyll应用的帮助下，用Git版本库维护个人网站\
   和博客等。

4. 在线编辑文件。

   GitHub提供了在线编辑文件的功能，不熟悉Git的用户也可以直接通过浏览器修改\
   版本库里的文件。

5. 社交编程。

   将社交网络引入项目托管平台是GitHub的创举。用户可以关注项目、关注其他用户\
   进而了解项目和开发者动态。项目的派生（Fork）和拉拽请求（Pull Request）\
   构成GitHub最独具一格的工作模式。对提交代码的逐行评注及Pull Request构成了\
   GitHub特色的代码审核。

6. 商业上的成功。

   GitHub通过私有版本库托管、面向企业的版本库托管和项目管理平台、人员招聘等\
   付费服务获得了商业上的成功，这种成功使得GitHub不必以页面中嵌入广告的方式\
   维持运营，最大的受益者还是用户。

7. 关注细节。

   GitHub网站采用了Ruby on Rails架构，在Web设计中运用了大量的JavaScript、\
   AJAX、HTML5等技术，支持对使用Markdown等标记语言的内容进行渲染和显示等。\
   关注细节使得GitHub成为了项目托管领域的后起之秀。

----

.. [#] 实际上使用HTTP协议也可以免口令输入。即通过文件\ ``~/.netrc``\ 写入\
       HTTP认证的明文口令。具体文件格式参见\ ``ftp``\ 命令MAN手册中相关介绍。
.. [#] https://gist.github.com/
