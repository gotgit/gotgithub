.. _code-comments:

代码评注
============

针对项目的每一次Pull Request就相当于一次代码评审，评审以讨论的形式显示在\
Pull Request中。

在Pull Request中还能够看到对应的提交（一个或多个），并可以直接针对提交进行\
代码评注。对于采用集中式协同的项目，即使较少使用 Pull Request，也同样可以\
使用代码评注。代码评注会触发通知邮件给项目的开发者。

代码评注有两种形式，一种是针对整个提交的评注，另外一种是对代码进行逐行评注。

.. _commit-comments:

提交评注
------------

查看项目的提交历史，从中选择一个提交，如图4-37所示。

.. figure:: /images/work-with-others/commit-history.png
   :scale: 100

   图4-37：helloworld项目提交历史

如图4-38是查看提交的界面。除了提交说明、提交者信息之外，还显示提交所修改的\
文件和改动差异。在查看提交页面的最下方显示一个提交评注对话框，可以在其中写下\
评注。评注可以使用 Markdown 语法。

.. figure:: /images/work-with-others/commit-note.png
   :scale: 100

   图4-38：添加提交评注

添加评注后，所评注的提交的作者会收到通知邮件，提醒针对自己的提交有了新的评论。\
通知邮件如图4-39所示。

.. figure:: /images/work-with-others/commit-note-email-notify.png
   :scale: 100

   图4-39：提交评注的通知邮件


通过Web界面可以看到添加在提交下方的评注，并可以撰写新的评注展开讨论。评注者\
本人或提交的作者还可以编辑甚至删除评注。如图4-40所示。

.. figure:: /images/work-with-others/commit-note-admin.png
   :scale: 100

   图4-40：提交评注

GitHub还支持Git自身提供的评注功能\ [#]_\ ，如图4-41所示的是提交\
http://git.io/git-notes\ [#]_\ 的评注，这个评注并非通过GitHub添加的，而是由\
``git-note``\ 命令提交的评注。这种评注针对一个特定提交只能有一个，GitHub只能\
显示不能编辑和删除。关于如何通过命令行查看\ ``git-note``\ 格式的评注，参见\
《Git权威指南》第570页“41.5 Git评注”。

.. figure:: /images/work-with-others/commit-note-by-git-note.png
   :scale: 100

   图4-41：git-note评注

.. _line-comments:

逐行评注
------------

还是以\ ``gotgithub/helloworld``\ 版本库中的提交为例，看一下GitHub支持的逐行\
评注功能，即针对提交中的任意一行添加评注。浏览提交，如图4-42所示，当鼠标置于\
任意一行代码时，在该行代码的左侧会显示一个添加注释的图标。

.. figure:: /images/work-with-others/commit-line-note-btn.png
   :scale: 100

   图4-42：添加逐行评注按钮

点击该图标（用于添加逐行评注的图标），会显示如图4-43所示的添加逐行评注对话框。\
该评注对话框出现在两行代码之间，在其中写下评注。

.. figure:: /images/work-with-others/commit-line-note-form.png
   :scale: 100

   图4-43：添加逐行评注

添加评注后，项目的开发人员同样会收到邮件通知。针对同一行代码的多次评论按时间\
顺序依次显示，图4-44展示了多个行间评注，其中一个评注还使用 Markdown 语法嵌入了\
一个图片。

.. figure:: /images/work-with-others/commit-line-note.png
   :scale: 100

   图4-44：逐行评注和提交评注

更有意思的评注可以围观\ ``MrMEEE/bumblebee``\ 项目的一个bug修正提交（被戏称\
一个空格引发的惨案）。地址： http://git.io/giant-bug\ [#]_\ 。

----

.. [#] http://www.kernel.org/pub/software/scm/git/docs/git-notes.html
.. [#] 即网址 https://github.com/ossxp-com/gitdemo-commit-tree/commit/e80aa74
.. [#] 即网址 https://github.com/MrMEEE/bumblebee/commit/a047be85247755cdbe0acce6
