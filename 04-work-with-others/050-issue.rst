缺陷跟踪
===============

缺陷跟踪（Bug Tracking）是软件研发流程中重要的一环，集项目需求管理和缺陷管理于一身，通过对研发工作流的控制帮助团队建立规范的研发体系。

GitHub提供轻量级的缺陷跟踪模块，称为Issues。小巧、易用的Issues模块能与Pull Request紧密整合，是Pull Request工作流的有益补充。一个小型、管理文档和网页的项目，使用Pull Request往往就足够了。试想如果贡献者能够直接修改代码（Fork and edit this file）并通过Pull Request贡献给项目核心开发者，那么为什么还要通过Issues模块报告错误并由他人来更改呢？但是对于大型项目需要做需求管理，或者参与代码开发有难度，则非常有必要通过Issues模块启用缺陷跟踪系统，提供更多途径让贡献者参与到项目中来。

缺陷跟踪可以通过项目的管理页面开启或关闭，如图4-46所示。

.. figure:: /images/work-with-others/project-admin-features-issue.png
   :scale: 100

   图4-46：开启或关闭Issues模块

标签
--------

缺陷跟踪系统通常可用于管理多种不同类型的问题：需求、缺陷或其它，也可以通过项目不同模块、组件来为问题分类。GitHub在问题分类的实现上非常简单，通过标签（label）来为问题建立分类。

开启Issues模块后，项目的菜单中多出一个“Issues”项，点击则进入问题浏览界面，如图4-47所示。左侧的边栏是问题过滤器，由上至下分为三个部分。最上面的过滤器根据问题的所有者对问题进行筛选，默认选择所有人的问题。中间的过滤器是根据里程碑对问题进行筛选，默认未选定任何里程碑（初始也未创建任何里程碑），不对问题进行里程碑过滤。最下面的过滤器依据问题标签对问题进行筛选，初始标签尚未创建。

.. figure:: /images/work-with-others/issue-no-label.png
   :scale: 100

   图4-47：尚未定义标签

鼠标点击左侧边栏标签过滤器中的新建标签的文本框，显示如图4-48所示的新建标签界面。输入新的标签名，并为标签选择一个颜色，创建新的标签。

.. figure:: /images/work-with-others/issue-new-label.png
   :scale: 100

   图4-48：创建新标签

创建的标签显示在过滤器中，如图4-49所示。点击过滤器中的标签则对问题进行筛选，取消过滤器可以点击图中标记的“Clear active milestone and label filters”链接。

.. figure:: /images/work-with-others/issue-labels.png
   :scale: 100

   图4-49：过滤器中的标签选项

标签过滤器下方的“Manage Labels”按钮用于管理标签，下面的输入框用于创建新的标签。

里程碑
-----------

里程碑（Milestones）是项目进度管理重要工具。在传统项目管理中，里程碑对应于一个项目开发计划、一个软件版本；在敏捷项目管理中，里程碑对应于一个Sprint（冲刺）；在软件代码的版本库中则对应于一个标签（tag）或分支（branch）。

在Issues模块中的“Milestones”页面用于里程碑管理。创建新的里程碑需要输入里程碑名称和里程碑的截止时间，如图4-50所示。

.. figure:: /images/work-with-others/issue-new-milestone.png
   :scale: 100

   图4-50：创建新里程碑

创建好的里程碑以进度条形式显示在里程碑页面中，如图4-51所示定义了两个里程碑。这两个里程碑的时间跨度定义的太长，敏捷的项目管理从来不这么定义。

.. figure:: /images/work-with-others/issue-milestones.png
   :scale: 100

   图4-51：里程碑列表


Issue的生命周期
-----------------

GitHub的Issues模块非常简单，对标签和里程碑进行简单的设置后，基本上就完成了Issues模块的配置工作，接下来就是如何创建和修改Issue，完成项目的缺陷跟踪和需求管理等，这才是Issues模块的主要工作。

每个Issue都自己的生命周期，从问题的创建，到问题的指派，再到问题的解决，直至问题的关闭。图4-52就是普通贡献者身份为项目创建Issue。

.. figure:: /images/work-with-others/issue-new-by-non-member.png
   :scale: 100

   图4-52：贡献者创建问题

录入问题标题和描述后，点击“Submit new issue”按钮，完成问题创建。图4-53显示了新建立的问题，可以看出新建问题尚未设置标签。

.. figure:: /images/work-with-others/issue-created.png
   :scale: 100

   图4-53：新创建的问题尚未添加标签等

普通贡献者创建问题时只能录入问题的标题和描述，而不能设置问题的指派（谁来负责）、添加标签和设置里程碑。如果希望问题通知到特定的开发者，可以在问题描述中以“@用户名”的方式通知到该用户 [#]_ ，这也是众多社交软件通行的做法。

项目成员创建问题时，拥有更大权限，也有更多的可选项。如图4-54所示。

.. figure:: /images/work-with-others/issue-new-by-member.png
   :scale: 100

   图4-54：项目成员创建问题有更多权限

完成上述两个问题的创建后，问题浏览界面显示出新创建的两个问题，一个以项目成员身份创建的问题已经被设置了“缺陷”的标签，而另外一个问题则没有设置任何标签。如图4-55所示。

.. figure:: /images/work-with-others/issue-list.png
   :scale: 100

   图4-55：所有问题列表

以项目成员身份登录，在问题浏览界面即可为问题重新设定标签，指派负责人，设置里程碑，以及关闭问题等。如图4-56所示。

.. figure:: /images/work-with-others/issue-update.png
   :scale: 100

   图4-56：为问题添加指派、里程碑和标签

在问题浏览页面的过滤器中选择里程碑”Version4.0“，可以看到两条问题都显示出来，这是因为这两条问题都属于该里程碑。里程碑的进度条显示进度为零，这是因为里程碑所包含的全部（两个）问题都处于打开状态，尚未解决。如图4-57所示。

.. figure:: /images/work-with-others/issue-list-with-milestone.png
   :scale: 100

   图4-57：通过里程碑筛选问题

邮件通知功能是缺陷跟踪系统推动工作流的重要工具，GitHub的Issues模块也具有邮件通知功能。除了像其他缺陷跟踪系统在收到邮件通知后，访问Web界面参与问题的讨论外，还可以直接以邮件回复的功能参与到工作流中 [#]_ 。

GitHub还支持版本库提交和问题建立关联，只要提交说明中出现“#xxx”（Issue编号）字样。如果在提交说明中的问题编号前出现特定关键字，还可以关闭问题。支持的关键字有：

* fixes #xxx
* fixed #xxx
* fix #xxx
* closes #xxx
* close #xxx
* closed #xxx

下面就以 ``gotgithub/helloworld`` 版本库为例，关闭编号为“#1”的问题。

* 克隆版本库，若本地工作区尚不存在。

  ::
  
    $ git clone git@github.com:gotgithub/helloworld.git
    $ cd helloworld
 
* 在工作区中进行修改、添加文件等，然后添加至暂存区。

  ::
 
    hack, hack, hack...
    $ git add -i
    
* 提交说明中用 ``fixed #xxx`` 关键字关闭相关问题。

  ::
 
    $ git commit -m "Fixed #1: Source code for Hello world."

* 向GitHub版本库推送。

  ::

    $ git push

推送完毕后，在问题浏览界面可以看到里程碑“Version4.0”的进度已经完成了一半，即其中一个问题（#1）已经完成并关闭。如图4-58所示。

.. figure:: /images/work-with-others/issue-milestone-half-closed.png
   :scale: 100

   图4-58：关闭一个问题，里程碑完成50%

查看已经完成的问题（#1），可以看到其中关联到一个提交，该提交正是我们刚刚创建的。如图4-59所示。

.. figure:: /images/work-with-others/issue-closed-by-commit.png
   :scale: 100

   图4-59：已关闭问题中的提交链接

点击关联的提交，显示如图4-60的提交界面，出现在提交说明中的问题编号也可点击，指向缺陷追踪系统中该问题的链接。

.. figure:: /images/work-with-others/commit-link-to-issue.png
   :scale: 100

   图4-60：提交中的问题链接

Pull Requst也是Issue
--------------------------

Pull Request和Issue一样，也是一种对项目的反馈，而且是更为主动的反馈。GitHub的Issues模块将Pull Request也纳入到问题的管理之中，完美地将Pull Request整合到问题追踪的框架之中。

为了弄清二者之间的关联，首先创建一个Pull Request。以非项目成员（用户 wangsheng [#]_ ）的账号访问 ``gotgithub/helloworld`` 项目，查看文件 ``README.mkd`` ，点击“Fork and edit this file”按钮快速创建项目分支，如图4-61所示。

.. figure:: /images/work-with-others/fork-and-edit-btn-for-issue.png
   :scale: 100

   图4-61：在线编辑并创建项目分支

通过GitHub提供的在线编辑功能修改 ``README.mkd`` 文件，修改完毕后撰写提交说明，点击“Propose File Change”按钮提交。如图4-62所示。

.. figure:: /images/work-with-others/fork-and-edit-form-for-issue.png
   :scale: 100

   图4-62：在线编辑并提交

留意在提交说明中使用了“Fixed #2”关键字，以便可以通过提交关闭相应的问题。当提交修改后，GitHub会自动开启创建新的Pull Request对话框，如图4-63所示。

.. figure:: /images/work-with-others/new-pull-request-for-issue.png
   :scale: 100

   图4-63：创建Pull Request

Pull Request创建完毕后，除了在菜单项“Pull Requests”中有显示外，在“Issues”的问题浏览页面中也会显示。如图4-64所示，新建立的Pull Request的编号不是从壹开始创建，而是接着问题的编号顺序创建，所以当Pull Request出现在问题列表中时，如果不注意后面的山型的分支图标，根本意识不到这不是一个问题（Issue），而是一个Pull Request。

.. figure:: /images/work-with-others/issue-list-with-pull-request.png
   :scale: 100

   图4-64：Pull Request也显示在Issues中

显示在问题浏览界面中的Pull Request同问题一样，可以为其设置标签、指派负责人、设置里程碑。如图4-65所示。

.. figure:: /images/work-with-others/pull-request-update-as-issue.png
   :scale: 100

   图4-65：可以像更新其他Issue那样更新Pull Request

当Pull Request归类到里程碑“Version4.0”中时，在过滤器打开里程碑“Version4.0”，可以看到本来已经完成50%的进度，由于新增了一个“问题”（Pull Request），导致进度降低了。如图4-66所示。

.. figure:: /images/work-with-others/milestone-progress-with-pull-request.png
   :scale: 100

   图4-66：里程碑进度调整

点击编号为“#3”的问题（Pull Request），会进入到Pull Request页面。点击页面中的“Merge pull request”按钮实现Pull Request的合并。如图4-67所示。

.. figure:: /images/work-with-others/merge-pull-request-for-issue.png
   :scale: 100

   图4-67：在线合并Pull Request

点击“Confirm Merge”确认合并，如图4-68所示。

.. figure:: /images/work-with-others/merge-pull-request-for-issue-confirm.png
   :scale: 100

   图4-68：确认合并Pull Request

完成合并后，查看该Pull Request，可以看到该Pull Request已经关闭。如图4-69所示。

.. figure:: /images/work-with-others/pull-request-close-for-issue.png
   :scale: 100

   图4-69：Pull Request自动关闭

如果再回到问题浏览界面，能够猜到现在里程碑“Version4.0”的进度是多少么？由于编号为“#3”的Pull Request的关闭，以及该Pull Request对应的提交中同时关闭了编号为“#2”的问题，所以现在里程碑“Version4.0”关联的所有问题均已关闭，里程碑显示已关闭，即里程碑完成度为100%。

.. figure:: /images/work-with-others/milestone-closed.png
   :scale: 100

   图4-70：里程碑关闭

----

.. [#] https://github.com/blog/821-mention-somebody-they-re-notified
.. [#] https://github.com/blog/811-reply-to-comments-from-email
.. [#] 感谢王胜提供测试账号。
