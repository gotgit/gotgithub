共享版本库
===============

除了独具特色的“Fork + Pull”的分布式工作模式，GitHub同样支持传统的集中式协同工作模式。

版本库授权
-----------------

GitHub可以通过多种途径为版本库授权，让版本库成为多人共享的版本库，从而让项目管理者围绕项目创建一个核心开发团队。下面以gotgithub账号下的helloworld版本库为例，介绍如何设置版本库的多人共享。

进入 ``gotgithub/helloworld`` 项目的管理界面，点击左侧导航条中的“Collaborators”，可以查看及添加项目的合作者，如图4-17所示。

.. figure:: /images/work-with-others/collaborators.png
   :scale: 100

   图4-17：添加项目合作者

图4-17为项目添加了两个合作者：ossxp-com和jiangxin。添加到项目当中的合作者会收到通知邮件，告知已经被加入到相应的项目当中。当新加入的项目合作者，如jiangxin，登录GitHub，在仪表板的版本库列表中会看到源自gotgithub用户的版本库，如图4-18所示。

.. figure:: /images/work-with-others/prj-list-of-collab.png
   :scale: 100

   图4-18：合作者项目列表

从图4-18可以看出GitHub用户jiangxin自己创建的项目托管在自己的空间下，而作为合作者参与的项目仍然托管在原创建者（gotgithub）的空间下，这一点明显和项目分支（Fork）不同。图4-19是以jiangxin登录GitHub访问 ``gotgithub/helloworld`` 的界面。

.. figure:: /images/work-with-others/jx-helloworld.png
   :scale: 100

   图4-19：以合作者身份访问项目

用户jiangxin对版本库 ``gotgithub/helloworld`` 拥有写入权限。和 ``gotgithub`` 用户稍有区别的是没有管理员权限。

与传统集中式工作模式的异同
--------------------------------

传统的集中式版本控制系统，如CVS、SVN，所有用户都访问同一个版本库。采用集中式工作模式的GitHub用户同样也是访问同一版本库。

对于由用户gotgithub创建的 ``helloworld`` 版本库，添加了合作者ossxp-com和jiangxin，三个人克隆版本库使用如下命令。

* 用户 gotgithub 克隆版本库。

  ::

    gotgithub$ git clone https://gotgithub@github.com/gotgithub/helloworld.git

* 用户 ossxp-com 克隆版本库。

  ::

    ossxp-com$ git clone https://ossxp-com@github.com/gotgithub/helloworld.git

* 用户 jiangxin 克隆版本库。

  ::

    jiangxin$ git clone https://jiangxin@github.com/gotgithub/helloworld.git

传统集中式版本控制系统，所有的提交历史数据都在唯一的版本库中，各个提交是顺序进行的。为了防止多用户在提交时相互覆盖，集中式版本控制系统发明了很多方法。有的采用编辑锁的形式（如VSS），更改文件前对文件锁定，其他人禁止对文件进行访问（甚至无法读取），完成修改并提交后，文件解锁。有的如SVN，允许多人同时编辑同一文件，但只有先进行提交的才能成功，后提交的会遇到“过时”错误，必须先获取版本库中的新增提交并和本地修改进行合并。即传统集中式版本控制系统，提交时必须和唯一的版本库所在的服务器保持连接，而且提交有可能会失败。

对于如Git这样的分布式版本控制系统，提交总是会成功，这是因为提交并不涉及和共享服务器的交互，是针对本地克隆版本库进行的本地操作。采用集中式的工作模式，共享版本库作为各个用户各自本地版本库数据交换、沟通的媒介，只有在本地克隆版本库需要和共享版本库同步的时候才要和服务器建立连接，例如将本地所做的一个或多个提交推送到共享服务器，或者将服务器上新的提交获取到本地克隆版本库。

实际上无论采用分布式还是集中式的工作模式，Git都好像工作在一个独立的分支上（克隆即分支），即使共享版本库和本地克隆版本库的分支名都叫做 ``master`` 。如图4-20，三个用户克隆 ``gitgithub/helloworld`` 版本库后，各自在本地执行了一次或多册提交。


.. figure:: /images/work-with-others/helloworld-commit.png
   :scale: 100

   图4-20：在本地版本库中的提交

三个用户各自的提交都会非常顺利，但是一旦决定将本地提交推送到共享服务器时就可能遇到麻烦。用户 gotgithub 先执行推送，会非常顺利。

::

  gotgithub$ git push

而其他人就没有这么幸运了。Git的推送操作正如SVN等集中式版本控制系统的提交操作那样，先执行者成功，后执行者糟糕（要解决冲突，自动或手动）。

合并后推送
---------------

当用户gotgithub完成推送后，共享版本库以及三个用户的本地版本库如图4-21所示。其中共享版本库变得和gotgithub用户的本地版本库相一致。

.. figure:: /images/work-with-others/helloworld-push.png
   :scale: 100

   图4-21：用户gotgithub完成推送

此时如果用户ossxp-com执行推送，会遇到错误：非快进式推送。

::

  ossxp-com$ git push
  To https://ossxp-com@github.com/gotgithub/helloworld.git
   ! [rejected]        master -> master (non-fast-forward)
  error: failed to push some refs to 'https://ossxp-com@github.com/gotgithub/helloworld.git'
  To prevent you from losing history, non-fast-forward updates were rejected
  Merge the remote changes (e.g. 'git pull') before pushing again.  See the
  'Note about fast-forwards' section of 'git push --help' for details.

GitHub并不对强制推送进行限制，但是用户ossxp-com不要用 ``git push -f`` 命令强制推送，因为那样会覆盖掉共享版本库中用户gotgithub的推送，正确的做法是获取共享版本库中新提交，并在本地版本库中和本地提交合并。过程如图4-22所示。

.. figure:: /images/work-with-others/helloworld-fetch-merge.png
   :scale: 100

   图4-22：合并操作示意图

图4-22是一个分节动作，实际上用户ossxp-com只需执行一条命令，即完成所有的操作：

::

  ossxp-com$ git pull

如果一切顺利，合并后共享版本库以及三个开发者各自本地版本库的示意图如图4-23所示。

.. figure:: /images/work-with-others/helloworld-merged.png
   :scale: 100

   图4-23：用户ossxp-com完成合并的示意图

但是合并操作并不总是会成功，如果自动合并失败，会在暂存区对合并前后文件进行标识，工作区进入冲突解决状态，在冲突解决完成之前不能提交。冲突解决Git支持和多种命令行及图形工具的整合，只需执行如下命令，即可调用已安装工具进行冲突解决。

::

  ossxp-com$ git mergetool

冲突解决完毕，执行提交。

::

  ossxp-com$ git commit

如果在冲突解决过程把本地文件搞得一团糟，随时可以取消合并操作，让本地版本库的 ``master`` 分支退回到合并之前的状态，操作如下：

::

  ossxp-com$ git reset --hard

这时用户ossxp-com的本地版本库示意如图4-24所示。

.. figure:: /images/work-with-others/helloworld-merged-canceled.png
   :scale: 100

   图4-24：取消合并后版本库示意图

取消合并操作后，分支 ``master`` 回退到合并之前，而分支 ``origin/master`` 则由于 ``git fetch`` 操作而变得和共享版本库当前 ``master`` 分支一样。若要再次开始合并操作，执行：

::

  ossxp-com$ git merge origin/master

无论是自动合并还是手工合并，完成合并后的版本库示意图都如图4-23所示。用户ossxp-com若要将本地合并后的提交同步到共享服务器，还是执行推送操作。

::

  ossxp-com$ git push

完成推送后的版本库示意图如图4-25所示。

.. figure:: /images/work-with-others/helloworld-merged-pushed.png
   :scale: 100

   图4-25：合并后推送

合并还是变基
---------------

合并会产生除了合并双方（或多方）所有提交外的一个新提交，这一方面会增加代码审核的负担，另一方面本地多个提交混杂一起与远程分支合并可能会比本地提交逐一迁移式合并更加困难。因此在特定情况下，变基是取代合并的一个选择。

图4-26展示用户jiangxin若采用合并和变基两种不同方案时本地版本库 ``master`` 分支的情况。图的左侧是合并，右侧是变基。

.. figure:: /images/work-with-others/helloworld-merged-vs-rebase.png
   :scale: 100

   图4-26：合并和变基结果比较

用户jiangxin采用变基操作，执行命令如下：

* 获取远程版本库的提交到本地的远程分支。

  ::

    jiangxin$ git fetch origin

* 执行变基操作，将本地 ``master`` 分支的提交变基到新的远程分支中。

  ::

    jiangxin$ git rebase origin/master

如果一切顺利，变基后的本地版本库正如图4-26右侧示意的那样。向远程版本库推送，执行命令：

::

  $ git push

如果希望在执行 ``git pull`` 时自动使用 ``git rebase`` 取代默认的 ``git merge`` 操作，可以进行如下设置：

::

  $ git config branch.master.rebase true

如果希望本地所有克隆版本库在执行 ``git pull`` 时都改变默认行为，将变基作为首选，则如下设置全局变量。

::

  $ git config --global branch.autosetuprebase true

