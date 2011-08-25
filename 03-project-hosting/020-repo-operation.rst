操作版本库
===============

强制推送
----------

细心的读者可能从图3-4已经看出，显示的提交者并非gotgithub用户，而是一个名为ossxp-com的用户，这是因为GitHub是通过提交中的邮件地址来对应到GitHub用户的。看看提交说明：

::

  $ git log --pretty=fuller
  commit a00f4dda9f72d1f71eed6b6269dd7327951446f1
  Author:     Jiang Xin <worldhello.net@gmail.com>
  AuthorDate: Thu Aug 11 16:31:39 2011 +0800
  Commit:     Jiang Xin <worldhello.net@gmail.com>
  CommitDate: Thu Aug 11 16:31:39 2011 +0800

      README for this project.

原来提交用户设置的邮件地址并非gotgithub用户设置的邮件地址。补救办法就是对此提交进行修改，然后强制推送到GitHub。

* 重新设置 ``user.name`` 和 ``user.email`` 配置变量。

  因为gotgithub是一个测试用的临时用户，我并不希望影响我在本地其他项目的提交，因此下面的设置命令没有使用 ``--global`` 参数，只对本地版本库进行设置。

  ::

    $ git config user.name "Jiang Xin"
    $ git config user.email "gotgithub@gmail.com"

* 执行Git修补提交命令。

  注意使用 ``--reset-author`` 会将提交信息中的属性 ``Author`` 连同 ``AuthorDate`` 一并修改，否则只修改 ``Commit`` 和 ``CommitDate`` 。参数 ``-C HEAD`` 维持提交说明不变。

  ::

    $ git commit --amend --reset-author -C HEAD

* 查看提交日志，发现提交者信息和作者信息都已经更改。

  ::

    $ git log --pretty=fuller
    commit f172c51a111d558130028c7e9c3e81b60196d512
    Author:     Jiang Xin <gotgithub@gmail.com>
    AuthorDate: Thu Aug 11 18:23:56 2011 +0800
    Commit:     Jiang Xin <gotgithub@gmail.com>
    CommitDate: Thu Aug 11 18:23:56 2011 +0800
    
        README for this project.

* 直接推送会报错。

  ::

    $ git push
    To git@github.com:gotgithub/helloworld.git
     ! [rejected]        master -> master (non-fast-forward)
    error: failed to push some refs to 'git@github.com:gotgithub/helloworld.git'
    To prevent you from losing history, non-fast-forward updates were rejected
    Merge the remote changes (e.g. 'git pull') before pushing again.  See the
    'Note about fast-forwards' section of 'git push --help' for details.

* 使用强制推送。

  对于此例，我们显然不需要向上面命令错误信息中提示那样先执行 ``git pull`` 合并上游版本库再推送，而是选择强制推送。

  ::

    $ git push -f
    Counting objects: 3, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 597 bytes, done.
    Total 3 (delta 0), reused 2 (delta 0)
    To git@github.com:gotgithub/helloworld.git
     + a00f4dd...f172c51 master -> master (forced update)

完成强制推送后，再查看GitHub项目页面，会发现提交者已经显示为gotgithub用户。如图3-7所示。

.. figure:: /images/project-hosting/force-push.png
   :scale: 100

   图3-7：强制更新后，提交者已更改

新建分支
---------

现在版本库中只有一个默认分支 ``master`` ，如果希望在GitHub版本库中再创建分支，可以采用如下方法：

* 本地版本库中建立分支 ``mybranch1`` 。

  创建分支有多种方法，最为便捷的就是 ``git checkout -b`` 命令，同时完成分支创建和分支切换。

  ::

    $ git checkout -b mybranch1
    Switched to a new branch 'mybranch1'

* 为了易于识别，添加一个新文件 ``hello1`` ，并提交。    

  ::

    $ touch hello1
    $ git add hello1
    $ git commit -m "add hello1 for mark."
    [mybranch1 73e586f] add hello1 for mark.
     0 files changed, 0 insertions(+), 0 deletions(-)
     create mode 100644 hello1

* 通过推送命令，将本地分支 ``mybranch1`` 推送到GitHub远程版本库，完成在GitHub上的新分支创建。

  ::

    $ git push -u origin mybranch1
    Counting objects: 4, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 280 bytes, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To git@github.com:gotgithub/helloworld.git
     * [new branch]      mybranch1 -> mybranch1
    Branch mybranch1 set up to track remote branch mybranch1 from origin.

在GitHub上查看版本库，会看到新增了一个分支 ``mybranch1`` ，不过默认分支仍为 ``master`` ，如图3-8所示。

.. figure:: /images/project-hosting/new-branch.png
   :scale: 100

   图3-8：版本库新增了一个分支

设置默认分支
---------------

如果希望版本库的默认分支为 ``mybranch1`` ，点击项目名称旁边的”Admin“按钮，修改项目的默认分支，如图3-9所示。

.. figure:: /images/project-hosting/set-default-branch.png
   :scale: 100

   图3-9：设置缺省分支

设置了GitHub默认分支后，如果再从GitHub克隆版本库，本地克隆后版本库的默认分支也将改变。

::

  $ git clone git@github.com:gotgithub/helloworld.git helloworld-nb
  Cloning into helloworld-nb...
  remote: Counting objects: 6, done.
  remote: Compressing objects: 100% (4/4), done.
  remote: Total 6 (delta 0), reused 6 (delta 0)
  Receiving objects: 100% (6/6), 845 bytes, done.
  $ cd helloworld-nb
  $ git branch
  * mybranch1

之所以本地缺省分支不再是 ``master`` ，是因为远程（GitHub）版本库中的特殊引用 ``HEAD`` 指向 ``mybranch1`` 分支。这可以从下面命令看出。

::

  $ git branch -r
    origin/HEAD -> origin/mybranch1
    origin/master
    origin/mybranch1

也可以从 ``git ls-remote`` 命令看出引用 ``HEAD`` 和 ``refs/heads/mybranch1`` 指向同一个对象的哈希值。

::

  $ git ls-remote
  From git@github.com:gotgithub/helloworld.git
  73e586f46f5a4a476e415f248714e595ddbe2f7f        HEAD
  f172c51a111d558130028c7e9c3e81b60196d512        refs/heads/master
  73e586f46f5a4a476e415f248714e595ddbe2f7f        refs/heads/mybranch1

删除分支
---------------

删除本地版本库的分支 ``mybranch1`` ，用如下命令：

::

  $ git branch -d mybranch1
  error: Cannot delete the branch 'mybranch1' which you are currently on.

错误信息显示不能删除当前工作分支。因此先切换到其他分支，例如从GitHub版本库中取出 ``master`` 分支并切换。  

::

  $ git checkout -b master origin/master

可以看出新的工作分支为 ``master`` 分支。

::

  $ git branch
  * master
    mybranch1

现在删除 ``mybanch1`` 分支。之所以使用 ``-D`` 参数，而非 ``-d`` 参数，是因为为了防止 ``mybranch1`` 的提交丢失，Git缺省禁止删除尚未合并的分支。

::
 
  $ git branch -D mybranch1
  Deleted branch mybranch1 (was 73e586f).

现在只是本地分支被删除了，远程GitHub服务器上的 ``mybranch1`` 分支尚在。删除远程GitHub版本库中的分支就不能使用 ``git branch`` 命令而，而是要使用 ``git push`` 命令，不过在使用推送分支命令时要使用一个特殊的引用表达式（冒号前为空）。如下：

::

  $ git push origin :mybranch1
  remote: error: refusing to delete the current branch: refs/heads/mybranch1
  To git@github.com:gotgithub/helloworld.git
   ! [remote rejected] mybranch1 (deletion of the current branch prohibited)
  error: failed to push some refs to 'git@github.com:gotgithub/helloworld.git'

为什么删除远程分支出错了呢？是因为没有使用强制推送么？

实际上即使使用强制推送也会遇到上面的错误。GitHub发现要删除的 ``mybranch1`` 分支是版本库的缺省分支，因而禁止删除。重新访问GitHub的项目管理页面，将缺省分支设置回 ``master`` 分支，参照图3-9。然后再执行上述命令，即可成功删除分支。

::

  $ git push origin :mybranch1
  To git@github.com:gotgithub/helloworld.git
   - [deleted]         mybranch1

执行 ``git ls-remote`` 命令可以看到GitHub远程分支已删除。

::

  $ git ls-remote git@github.com:gotgithub/helloworld.git
  f172c51a111d558130028c7e9c3e81b60196d512        HEAD
  f172c51a111d558130028c7e9c3e81b60196d512        refs/heads/master

里程碑管理
------------

里程碑管理和分支管理极其类似。

* 先在本地创建一个新提交。

  ::

    $ touch hello1
    $ git add hello1
    $ git commit -m "add hello1 for mark."

* 本地创建里程碑 ``mytag1`` 、 ``mytag2`` 和 ``mytag3`` 。

  ::

    $ git tag -m "Tag on initial commit" mytag1 HEAD^
    $ git tag -m "Tag on new commit"     mytag2
    $ git tag mytag3

* 查看新建立的里程碑。

  ::

    $ git tag -l -n1
    mytag1          Tag on initial commit
    mytag2          Tag on new commit
    mytag3          add hello1 for mark.

* 将本地里程碑推送到GitHub远程版本库。

  ::

    $ git push origin refs/tags/*
    Counting objects: 6, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (4/4), done.
    Writing objects: 100% (5/5), 564 bytes, done.
    Total 5 (delta 0), reused 2 (delta 0)
    To git@github.github.com:gotgithub/helloworld.git
     * [new tag]         mytag1 -> mytag1
     * [new tag]         mytag2 -> mytag2
     * [new tag]         mytag3 -> mytag3

* 删除本地里程碑。

  ::

    $ git tag -d mytag3
    Deleted tag 'mytag3' (was de60c49)

* 删除GitHub远程版本库中的里程碑。

  ::

    $ git push origin :mytag3
    To git@github.github.com:gotgithub/helloworld.git
     - [deleted]         mytag3

此时查看GitHub上的项目页，会看到已有两个里程碑，如图3-10所示。

.. figure:: /images/project-hosting/tags-list.png
   :scale: 100

   图3-10：里程碑列表


