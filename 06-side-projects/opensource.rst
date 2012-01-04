_github-opensource:

GitHub Open Source
===================

GitHub已成为新的开源项目大本营，而且GitHub也将其API开放，并将部分模块开源，\
借助社区的力量让GitHub变得更好。

GitHub大部分的开源项目托管在其官方账号下： https://github.com/github 。

.. _api:

API接口
-------
GitHub通过域名\ ``api.github.com``\ 提供API接口，数据以JSON格式传递。

详细的API参考手册参见网址： http://developer.github.com/ 。API手册的版本库\
地址： https://github.com/github/developer.github.com 。

.. _help-project:

官方手册
--------
GitHub官方手册参见 http://help.github.com/ ，使用 Jekyll 维护。

项目地址： https://github.com/github/help.github.com 。

.. _grit:

Grit
----
Grit是Git的Ruby封装和实现，是GitHub调用Git的接口。部分是通过封装对\ ``git``\
命令的调用实现的，部分则是纯Ruby实现。

项目地址： https://github.com/mojombo/grit 。

.. _services-project:

GitHub Services
---------------
Git版本库推送会触发服务器端\ ``post-receive``\ 钩子脚本。此项目将GitHub的\
服务器端钩子脚本开源，用户可以开发针对特定应用的钩子。GitHub还为其他GitHub\
应用提供了事件接口，如问题变更、Pull Request、维基页面修改等\ [#]_\ 。

项目地址： https://github.com/github/github-services 。

.. _hobot:

Hubot 和 Hubot Scripts
----------------------
可以把 hubot\ [#]_\ 看做是GitHub的Siri（最早出现于iPhone 4S 的智能语音助理）\
或是新浪微博上的饮水姬\ [#]_\ 。GitHub将hobot和Campfire聊天室整合，\
hobot被聊天室会话触发可以实现诸如：打开办公室的门、根据wifi使用情况列出公司中的人、\
通过公司喇叭读一段信息等等许多好玩的事情\ [#]_\ ，而实现GitHub自动化部署\
则证明 hubot 可以完成更严肃的事情，在公司工作流中扮演举足轻重的地位\ [#]_\ 。

Hobot已经开源，项目库地址：\ https://github.com/github/hubot\ 和\
https://github.com/github/hubot-scripts\ （脚本）。

.. _gollum:

Gollum
------
GitHub以Git为后端的维基系统就是由Gollum实现的。每一个维基网页对应于一个文件，\
文件格式可以是 Markdown、textile、rdoc、org、creole、mediawiki、\
reStructuredText、asciidoc、pod 等。Gollum 调用名为github-markup的Ruby gem包\
（来自于下面要介绍的 Markup 项目）完成文件到网页的格式转换。

项目地址： https://github.com/github/gollum 。

关于GitHub维基参见本书“第4.6节维基”。

.. _jekyll-project:

Jekyll
------
Jekyll 是一个简单的、支持博客的静态网站编译器。可以使用Markdown和Textile两种\
标记语言或者HTML撰写网页，并支持Liquid模版。实际上GitHub为托管项目生成静态\
网页使用的就是Jekyll。

项目地址： https://github.com/mojombo/jekyll 。

.. _linguist:

Linguist
--------
Linguist 是一个Ruby模块，GitHub使用该模块对数据文件进行语义分析，检测文件的\
语言种类，代码加亮，对二进制文件进行忽略，限制非必须的差异显示，以及生成语言\
分类图等。

项目地址： https://github.com/github/linguist 。

.. _markup:

Markup
------
GitHub通过这个ruby包对项目版本库根目录下的\ ``README``\ 文件，以及维基页面\
等文件进行解析、转换为网页显示。支持 Markdown、textile、rdoc、org、creole、\
mediawiki、reStructuredText、asciidoc、pod 等标记语言。实际上在对上述标记语言\
的解析和转换中，还依赖其他软件包，例如对于 Markdown 格式首选 Redcarpet\ [#]_\ ，\
对 textile 格式使用 RedCloth，对 reStructuredText 格式调用外部命令\
``rst2html``\ ，对 asciidoc 格式调用外部命令\ ``asciidoc``\ 等。

项目地址： https://github.com/github/markup 。

关于Markup软件包以及其他GitHub扩展的Markdown语法，参见：\
http://github.github.com/github-flavored-markdown\ 。

.. _resque:

Resque
------
Resque（发音类似 "rescue"）是一个以Redis为后端的Ruby包，用于创建和管理后台\
任务。可创建任务，将任务分配到多个队列，并在后台执行任务。

项目地址： https://github.com/defunkt/resque 。

.. _gitpad:

GitPad
------
这是一个运行于Windows下类似\ ``Notepad.exe``\ 的应用程序，安装此应用后在\
Windows下做Git提交操作会调用类似记事本（Notepad）的应用撰写提交说明。

项目地址： https://github.com/github/GitPad 。

.. _maven-plugins:

Maven Plugins
-------------
GitHub的Maven插件。

项目地址： https://github.com/github/maven-plugins 。

.. _gitignore:

Gitignore
---------
集合了针对各种语言环境的\ ``.gitignore``\ （忽略文件）模版。例如其中针对\
VisualStudio的忽略文件模版\ ``Global/VisualStudio.gitignore``\ 部分内容如下：

::

  # User-specific files
  *.suo
  *.user
  *.sln.docstates

  # Build results
  [Dd]ebug/
  [Rr]elease/

项目地址： https://github.com/github/gitignore 。

.. _media-project:

Media
-------
提供GitHub网站Logo和吉祥物 Octocat 的图片，只能在授权范围内使用。

项目地址： https://github.com/github/media 。


----

.. [#] https://github.com/blog/964-all-of-the-hooks
.. [#] http://hubot.github.com/
.. [#] http://weibo.com/u/2625288792
.. [#] http://zachholman.com/posts/why-github-hacks-on-side-projects/
.. [#] http://scottchacon.com/2011/08/31/github-flow.html#6__deploy_immediately_after_review
.. [#] Redcarpet 是对一个高效的Markdown解析器，通过对C语言的 Sundown 库封装实现。\
       项目地址：\ https://github.com/tanoku/redcarpet\ 。
