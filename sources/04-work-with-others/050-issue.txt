.. _issues:

缺陷跟踪
===============

缺陷跟踪（Bug Tracking）是软件研发流程中重要的一环，集项目需求管理和缺陷管理\
于一身，通过对研发工作流的控制帮助团队建立规范的研发体系。GitHub提供轻量级的\
缺陷跟踪模块，称为Issues。小巧、易用的Issues模块能与Pull Request紧密整合，\
是Pull Request工作流的有益补充。

一个小型、管理文档和网页的项目，使用Pull Request往往就足够了。试想如果贡献者\
能够直接修改代码（Fork and edit this file）并通过Pull Request贡献给项目核心\
开发者，那么为什么还要通过Issues模块报告错误并由他人来更改呢？但是对于大型\
项目需要做需求管理，或者参与代码开发有难度，则非常有必要通过Issues模块启用\
缺陷跟踪系统，提供更多途径让贡献者参与到项目中来。

缺陷跟踪可以通过项目的管理页面开启或关闭，如图4-45所示。

.. figure:: /images/issues/project-admin-features-issue.png
   :scale: 100

   图4-45：开启或关闭Issues模块

.. _labels:

标签
--------

缺陷跟踪系统通常可用于管理多种不同类型的问题：需求、缺陷或其它，也可以通过\
项目不同模块、组件来为问题分类。GitHub在问题分类的实现上非常简单，通过标签\
（label）来为问题建立分类。

开启Issues模块后，项目的菜单中多出一个“Issues”项，点击则进入问题浏览界面，\
如图4-46所示。左侧的边栏是问题过滤器，由上至下分为三个部分。最上面的过滤器\
根据问题的所有者对问题进行筛选，默认选择所有人的问题。中间的过滤器是根据\
里程碑对问题进行筛选，默认未选定任何里程碑（初始尚未创建任何里程碑），不对\
问题进行里程碑过滤。最下面的过滤器依据问题标签对问题进行筛选，初始标签尚未\
创建。

.. figure:: /images/issues/issue-no-label.png
   :scale: 100

   图4-46：尚未定义标签

鼠标点击左侧边栏标签过滤器中的新建标签的文本框，显示如图4-47所示的新建标签\
界面。输入新的标签名，并为标签选择一个颜色，创建新的标签。

.. figure:: /images/issues/issue-new-label.png
   :scale: 100

   图4-47：创建新标签

创建的标签显示在过滤器中，如图4-48所示。点击过滤器中的标签则对问题进行筛选，\
取消过滤器可以点击图中标记的“Clear active milestone and label filters”链接。

.. figure:: /images/issues/issue-labels.png
   :scale: 100

   图4-48：过滤器中的标签选项

标签过滤器下方的“Manage Labels”按钮用于管理标签，下面的输入框用于创建新的标签。

.. _milestone:

里程碑
-----------

里程碑（Milestones）是项目进度管理的重要工具。在传统项目管理中，里程碑对应\
于一个项目开发计划、一个软件版本；在敏捷项目管理中，里程碑对应于一个Sprint\
（冲刺）；在软件代码的版本库中则对应于一个标签（tag）或分支（branch）。

在Issues模块中的“Milestones”页面用于里程碑管理。创建新的里程碑需要输入里程碑\
名称和里程碑的截止时间，如图4-49所示。

.. figure:: /images/issues/issue-new-milestone.png
   :scale: 100

   图4-49：创建新里程碑

创建的里程碑以进度条形式显示在里程碑页面中，如图4-50所示定义了两个里程碑。\
这两个里程碑的时间跨度定义的太长，敏捷的项目管理从来不这么定义。

.. figure:: /images/issues/issue-milestones.png
   :scale: 100

   图4-50：里程碑列表

.. _lifecycle:

Issue的生命周期
-----------------

GitHub的Issues模块非常简单，对标签和里程碑进行简单的设置后，基本上就完成了\
Issues模块的配置工作，接下来就是如何创建和修改Issue，完成项目的缺陷跟踪和\
需求管理等，这才是Issues模块的主要工作。

每个Issue都有自己的生命周期，从问题的创建，到问题的指派，再到问题的解决，\
直至问题的关闭。图4-51就是以普通贡献者身份为项目创建Issue。

.. figure:: /images/issues/issue-new-by-non-member.png
   :scale: 100

   图4-51：以普通贡献者身份创建问题

录入问题标题和描述后，点击“Submit new issue”按钮，完成问题创建。图4-52显示了\
新建立的问题，可以看出新建问题尚未设置标签。

.. figure:: /images/issues/issue-created.png
   :scale: 100

   图4-52：新创建的问题尚未添加标签等

普通贡献者创建问题时只能录入问题的标题和描述，而不能设置问题的指派\
（谁来负责）、添加标签和设置里程碑。如果希望问题通知到特定的开发者，\
可以在问题描述中以“@用户名”的方式通知到该用户\ [#]_\ ，这也是众多社交\
软件通行的做法。

项目成员创建问题时，拥有更大权限，也有更多的可选项。如图4-53所示。

.. figure:: /images/issues/issue-new-by-member.png
   :scale: 100

   图4-53：以项目成员身份创建问题

完成上述两个问题的创建后，问题浏览界面显示新创建的两个问题，一个以项目成员\
身份创建的问题已经被设置了“缺陷”的标签，而另外一个问题则没有设置任何标签。\
如图4-54所示。

.. figure:: /images/issues/issue-list.png
   :scale: 100

   图4-54：所有问题列表

以项目成员身份登录，在问题浏览界面即可为问题重新设定标签，指派负责人，设置\
里程碑，以及关闭问题等。如图4-55所示。

.. figure:: /images/issues/issue-update.png
   :scale: 100

   图4-55：为问题添加指派、里程碑和标签

在问题浏览页面的过滤器中选择里程碑”Version 4.0“，可以看到两条问题都显示出来，\
这是因为这两条问题都属于该里程碑。里程碑的进度条显示进度为零，这是因为里程碑\
所包含的全部（两个）问题都处于打开状态，尚未解决。如图4-56所示。

.. figure:: /images/issues/issue-list-with-milestone.png
   :scale: 100

   图4-56：通过里程碑筛选问题

邮件通知功能是缺陷跟踪系统推动工作流的重要工具，GitHub的Issues模块也具有邮件\
通知功能。除了像其他缺陷跟踪系统在收到邮件通知后，访问Web界面参与问题的讨论外，\
还可以直接以邮件回复的功能参与到工作流中\ [#]_\ 。

GitHub还支持版本库提交和问题建立关联，只要提交说明中出现“#xxx”（Issue编号）\
字样。如果在提交说明中的问题编号前出现特定关键字，还可以关闭问题。支持的关键字有：

* fixes #xxx
* fixed #xxx
* fix #xxx
* closes #xxx
* close #xxx
* closed #xxx

下面就以\ ``gotgithub/helloworld``\ 版本库为例，关闭编号为“#1”的问题。

* 克隆版本库，若本地工作区尚不存在。

  ::
  
    $ git clone git@github.com:gotgithub/helloworld.git
    $ cd helloworld

* 编辑文件\ `src/main.c`\ ，改正“问题#1”发现的文字错误。

  ::

    $ vi src/main.c
    $ git diff
    diff --git a/src/main.c b/src/main.c
    index 3daf9fe..f974b49 100644
    --- a/src/main.c
    +++ b/src/main.c
    @@ -19,7 +19,7 @@ int usage(int code)
                "            say hello to the world.\n\n"
                "    hello -v, --version\n"
                "            show version.\n\n"
    -           "    hello -h, -help\n"
    +           "    hello -h, --help\n"
                "            this help screen.\n\n"), _VERSION);
         return code;
     }


* 将修改添加至暂存区。

  ::
 
    $ git add -u
    
* 提交，并在提交说明中用\ ``fixed #xxx``\ 关键字关闭相关问题。

  ::
 
    $ git commit -m "Fixed #1: -help should be --help."

* 向GitHub版本库推送。

  ::

    $ git push

推送完毕后，在问题浏览界面可以看到里程碑“Version 4.0”的进度已经完成了一半，\
即其中一个问题（#1）已经完成并关闭。如图4-57所示。

.. figure:: /images/issues/issue-milestone-half-closed.png
   :scale: 100

   图4-57：关闭一个问题，里程碑完成50%

查看已经完成的问题（#1），可以看到其中关联到一个提交，该提交正是我们刚刚创建的。\
如图4-58所示。

.. figure:: /images/issues/issue-closed-by-commit.png
   :scale: 100

   图4-58：已关闭问题中的提交链接

点击关联的提交，显示如图4-59的提交界面，出现在提交说明中的问题编号也可点击，\
指向缺陷追踪系统中该问题的链接。

.. figure:: /images/issues/commit-link-to-issue.png
   :scale: 100

   图4-59：提交中的问题链接

.. _pull-request-as-issue:

Pull Requst也是Issue
--------------------------

Pull Request和Issue一样，也是一种对项目的反馈，而且是更为主动的反馈。GitHub的\
Issues模块将Pull Request也纳入到问题的管理之中，完美地将Pull Request整合到问题\
追踪的框架之中。

为了弄清二者之间的关联，首先创建一个Pull Request。

以非项目成员（如用户 omnidroid）的账号访问\ ``gotgithub/helloworld``\ 项目，\
查看文件\ ``src/Makefile``\ ，点击“Fork and edit this file”按钮快速创建派生\
项目，如图4-60所示。

.. figure:: /images/issues/fork-and-edit-btn-for-issue.png
   :scale: 100

   图4-60：在线编辑并创建派生项目

通过GitHub提供的在线编辑功能修改\ ``src/Makefile``\ 文件，修改完毕后撰写提交\
说明，点击“Propose File Change”按钮提交。如图4-61所示。

.. figure:: /images/issues/fork-and-edit-form-for-issue.png
   :scale: 100

   图4-61：在线编辑并提交

在提交说明中特意使用了“Fixed #2”关键字，以便该提交被上游版本库接纳后能够关闭关联的问题。

当完成提交后，GitHub会自动开启创建新的Pull Request对话框，如图4-62所示。

.. figure:: /images/issues/new-pull-request-for-issue.png
   :scale: 100

   图4-62：创建Pull Request

Pull Request创建完毕后，除了在菜单项“Pull Requests”中有显示外，在“Issues”的\
问题浏览页面中也会显示。如图4-63所示，新建立的Pull Request的编号不是从壹开始\
创建，而是接着问题的编号顺序创建，所以当Pull Request出现在问题列表中时，\
如果不注意后面的山型的分支图标，根本意识不到这不是一个普通的问题（Issue），\
而是一个Pull Request。

.. figure:: /images/issues/issue-list-with-pull-request.png
   :scale: 100

   图4-63：Pull Request也显示在Issues中

显示在问题浏览界面中的Pull Request和问题一样，可以为其设置标签、指派负责人、\
设置里程碑。如图4-64所示。

.. figure:: /images/issues/pull-request-update-as-issue.png
   :scale: 100

   图4-64：可以像更新其他Issue那样更新Pull Request

当Pull Request归类到里程碑“Version 4.0”中时，在过滤器打开里程碑“Version 4.0”，\
可以看到本来已经完成50%的进度，由于新增了一个“问题”（Pull Request），导致\
进度降低了。如图4-65所示。

.. figure:: /images/issues/milestone-progress-with-pull-request.png
   :scale: 100

   图4-65：里程碑进度调整

点击编号为“#3”的问题（Pull Request），会进入到Pull Request页面。点击页面中的\
“Merge pull request”按钮实现Pull Request的合并。如图4-66所示。

.. figure:: /images/issues/merge-pull-request-for-issue.png
   :scale: 100

   图4-66：在线合并Pull Request

点击“Confirm Merge”确认合并，如图4-67所示。

.. figure:: /images/issues/merge-pull-request-for-issue-confirm.png
   :scale: 100

   图4-67：确认合并Pull Request

完成合并后，查看该Pull Request，可以看到该Pull Request已经关闭。如图4-68所示。

.. figure:: /images/issues/pull-request-close-for-issue.png
   :scale: 100

   图4-68：Pull Request自动关闭

如果再回到问题浏览界面，能够猜到现在里程碑“Version 4.0”的进度是多少么？

由于关闭了编号为“#3”的Pull Request，以及所合并的Pull Request中对应提交的提交\
说明的指令同时关闭了编号为“#2”的问题，所以现在里程碑“Version 4.0”关联的所有\
问题均已关闭。里程碑也显示已关闭，即里程碑完成度为100%。

.. figure:: /images/issues/milestone-closed.png
   :scale: 100

   图4-69：里程碑关闭

----

.. [#] https://github.com/blog/821-mention-somebody-they-re-notified
.. [#] https://github.com/blog/811-reply-to-comments-from-email
