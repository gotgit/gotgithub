代码评审
============

针对项目的每一次Pull Request就相当于一次代码评审，评审以讨论的形式显示在Pull Request中。在Pull Request中还看到对应的提交（一个或多个），可以直接针对提交进行代码评注。对于采用集中式协同的项目，虽然很少用到Pull Request，但同样也可以使用代码评注。代码评注会触发通知邮件给项目的开发者。

代码评注有两种形式，一种是针对整个提交的评注，另外一种是对代码的逐行评注。

提交评注
------------

透过项目的提交历史，可以看到所选分支所有的历史提交，如图4-37所示。选择其中一个提交。

.. figure:: /images/work-with-others/commit-history.png
   :scale: 100

   图4-37：gotgit项目提交历史

在查看提交的界面，除了提交日志、提交者信息之外，还显示提交所修改的文件和改动差异。在查看提交页面的最下方显示一个提交评注对话框，如图4-38所示。

.. figure:: /images/work-with-others/commit-note.png
   :scale: 100

   图4-38：添加提交评注

添加评注的同时会向项目中开发者发送一封通知邮件，提醒针对项目的某个提交有了新的评论。通知邮件如图4-39所示。

.. figure:: /images/work-with-others/commit-note-email-notify.png
   :scale: 100

   图4-39：提交评注的通知邮件


通过Web界面可以看到添加在提交下方的评注。评注者和项目的开发者还可以编辑和删除评注。如图4-40所示。

.. figure:: /images/work-with-others/commit-note-admin.png
   :scale: 100

   图4-40：提交评注

GitHub还支持Git自身提供的评注功能 [#]_ ，如图4-41所示的是提交 http://git.io/git-notes [#]_ 的评注，这个评注并非通过GitHub添加的，而是由 ``git-note`` 命令提交的评注。这种评注针对一个特定提交只能有一个，GitHub只能显示不能编辑和删除。关于如何通过命令行查看 ``git-note`` 格式的评注，参见《Git权威指南》第570页“41.5 Git评注”。

.. figure:: /images/work-with-others/commit-note-by-git-note.png
   :scale: 100

   图4-41：git-note评注


逐行评注
------------

还是以 ``gotgit/gotgit`` 版本库中的提交为例，看一下GitHub支持的逐行评注功能，即针对提交中的任意一行添加评注。浏览提交，如图4-42所示，当鼠标至于任意一行代码时，在该行代码的左侧会显示一个添加注释的图标。

.. figure:: /images/work-with-others/commit-line-note-btn.png
   :scale: 100

   图4-42：添加逐行评注按钮

点击该图标（用于添加逐行评注的图标），会显示如图4-43所示的添加逐行评注对话框。该评注对话框出现在两行代码之间，在其中写下评注。

.. figure:: /images/work-with-others/commit-line-note-form.png
   :scale: 100

   图4-43：添加逐行评注

添加评注后，项目的开发人员同样会收到邮件通知。图4-44是添加了逐行评注后的提交，在提交的最下方还可以看到之前针对整个提交的评注。

.. figure:: /images/work-with-others/commit-line-note.png
   :scale: 100

   图4-44：逐行评注和提交评注

----

.. [#] http://www.kernel.org/pub/software/scm/git/docs/git-notes.html
.. [#] 实际地址为 https://github.com/ossxp-com/gitdemo-commit-tree/commit/e80aa74
