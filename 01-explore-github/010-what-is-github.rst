.. _what-is-github:

==============
 什么是GitHub
==============
GitHub（网址 https://github.com/\ ）是一个面向开源及私有软件项目的托管平台，\
因为只支持Git作为唯一的版本库格式进行托管，故名GitHub。


GitHub的注册用户已经超过百万\ [#]_\ ，托管的版本库数量已超三百万，其中不乏知\
名的开源项目，如：Ruby on Rails\ [#]_\ 、Hibernate\ [#]_\ 、phpBB\ [#]_\ 、\
jQuery\ [#]_\ 、Prototype\ [#]_\ 、Homebrew\ [#]_\ 等。

GitHub于2008年4月10日正式发布\ [#]_\ ，相比始于1999年的SourceForge\ [#]_\ 和\
2005年的GoogleCode\ [#]_\ ，GitHub后来者居上。以2011年的数据从代码提交数量上\
看，GitHub已经超越其前辈\ [#]_\ ，如图1-1所示。

.. figure:: /images/explore-github/survival-of-the-forges.png
   :scale: 100

   图1-1：开源项目托管平台提交数量对照

对于一个开源项目，从开发角度讲大体上分为两类人群，一类称为核心开发团队，他们\
可以向保存源代码的版本库提交，即对源代码的修改具有最终的决定权。另外一类称为\
贡献者，他们不属于核心开发团队，虽然也能看到源代码，但无权向版本库提交修改。

.. _cvcs-model:

采用传统的集中式版本控制系统（如SVN）的开源项目，这两个群体的用户体验都不是\
太好。如图1-2所示，项目的贡献者（非核心成员）很不“高兴”，因为他们即便有修改\
源代码的能力和渴望，也不能直接向版本库提交，要想成为提交者需要一个很长的建立\
信任的过程。然而即便是核心开发团队的成员，体验也不是太好，因为凡是涉及到版本\
库的操作（检入、检出、查看日志等）都需要在联网的状态下进行，网络带宽对用户\
体验影响相当大。

.. figure:: /images/explore-github/cvcs-model.png
   :scale: 100

   图1-2：使用集中式版本控制系统

.. _dvcs-model:

Git等分布式版本控制系统的出现，彻底颠覆了原有代码管理的组织模式。使用Git，\
不再依赖唯一的、集中式的版本库，而是每个开发者本地都拥有一份完整的版本库。\
Git并不排斥集中式的使用模式，但更倾向于将集中式版本库称为共享版本库。核心\
开发团队的成员和贡献者（非核心成员）都可以从共享版本库克隆一份本地版本库，\
但只有核心团队成员才可以将自己本地版本库的提交推送到共享版本库上。\
如图1-3所示。

.. figure:: /images/explore-github/dvcs-model.png
   :scale: 100

   图1-3：使用分布式版本控制系统

使用Git做版本控制（如图1-3所示），核心开发团队非常“高兴”，因为他们和共享\
版本库之间不必一直保持连接状态，诸如查看日志、提交、创建分支等几乎全部操作\
都（脱离网络）在本地的版本库中完成。项目贡献者（非核心成员）也不再那么沮丧，\
因为版本库人人皆可更改（当然是对本地版本库而言）。稍微让贡献者感到困难的就是\
如何将自己对项目的改进被核心开发团队所了解并接纳。Git提供了多种途径，一个方法\
是先用\ ``git format-patch``\ 命令将本地提交转换为补丁文件或补丁文件序列，再\
通过邮件发送给核心开发团队。另外一个办法就是搭建一个自己专有的共享版本库，\
通过邮件创建一个拉拽请求（Pull Request），让核心团队的开发者到自己的版本库来\
抓取（Pull）。

.. _github-model:

GitHub的出现进一步推动了Git的普及，简化了版本控制的管理和操作流程，为开发者\
提供了更好的交流平台。如图1-4所示。

.. figure:: /images/explore-github/github-model.png
   :scale: 100

   图1-4：GitHub的协同模式

使用GitHub，无论是项目的核心开发团队，还是普通的项目贡献者都工作得非常“愉快”。\
创建项目变得非常轻松，创建者只需在GitHub上点击一下鼠标即可创建一个新版本库，\
通过简单的Web操作即可完成项目授权进而组建项目核心团队。在GitHub中，\
非核心团队成员参与项目也很容易。先找到自己希望参与的项目，然后只需在Web\
上点击一下鼠标即可在自己的托管空间下创建一个派生（fork）的项目，\
并对派生项目的版本库具有读写的完全权限，就好像这个项目原本就是由自己创立的\
那样。当贡献者完成开发并向自己派生的版本库推送后，可以通过GitHub的Web界面向\
项目的核心开发团队发送一个Pull Request，请求审核。项目的核心团队收到\
Pull Request后审核代码，审核通过后可以直接通过Web界面执行合并操作接纳贡献者的提交。

----

.. [#] https://github.com/blog/936-one-million
.. [#] https://github.com/rails/rails
.. [#] https://github.com/hibernate
.. [#] https://github.com/phpbb/phpbb3
.. [#] https://github.com/jquery/jquery
.. [#] https://github.com/sstephenson/prototype
.. [#] https://github.com/mxcl/homebrew
.. [#] https://github.com/blog/40-we-launched
.. [#] http://sourceforge.net/
.. [#] http://code.google.com/
.. [#] http://www.slideshare.net/sogrady/survival-of-the-forges
