.. _fork-and-pull-request:

Fork + Pull模式
====================

参与GitHub中的项目开发，最常用和推荐的首选方式是“Fork + Pull”模式。在\
“Fork + Pull”模式下，项目参与者不必向项目创建者申请提交权限，而是在自己的托管\
空间下建立项目的派生（Fork）。

如果一个开源项目派生出另外的项目，通常意味着项目的分裂和开发团队的削弱，\
而GitHub中的项目派生则不会，而且正好相反，GitHub中的项目派生是项目壮大的体现。\
所有的派生项目都会有链接指向原始项目，派生项目没有独立的缺陷追踪系统（ISSUE），\
而是必须利用创建者本人的项目中的缺陷追踪系统。至于在派生项目中创建的提交，\
可以非常方便地利用GitHub的Pull Request工具向原始项目的维护者发送Pull Request。

下面以GotGit版本库为例，介绍如何利用GitHub提供的Fork和Pull Request工具实现工作协同。

.. _fork:

版本库派生
------------------

GotGit版本库\ [#]_\ 用于维护《Git权威指南》一书的官网和勘误，下面演示的勘误表\
修改是由王胜\ [#]_\ 通过GitHub之外的一个缺陷追踪平台报告的\ [#]_\ 。\
他在报告中，甚至直接用GNU diff格式告诉我该如何修改。

下面就以用户gotgithub身份，访问版本库 https://github.com/gotgit/gotgit/ ，\
添加新的勘误。如图4-1所示，gotgit项目在之前的示例中已经被我们关注但尚未Fork。

.. figure:: /images/work-with-others/gotgit-repo-before-fork.png
   :scale: 100

   图4-1：原gotgit项目

点击项目名称右侧的Fork按钮，便在gotgithub用户自己的托管空间下创建项目派生，\
派生项目版本库出现在版本库列表中，如图4-2。

.. figure:: /images/work-with-others/gotgit-in-repo-list.png
   :scale: 100

   图4-2：gotgithub用户的项目列表

访问派生后的版本库，会发现和派生前的几乎相同，除了没有缺陷跟踪（ISSUE），\
以及标识了该项目派生之前的原路径等。如图4-3所示。

.. figure:: /images/work-with-others/gotgit-repo-forked.png
   :scale: 100

   图4-3：派生的gotgit项目

现在gotgithub用户就在本地派生的版本库中提交。

* 克隆 gotgithub/gotgit 版本库。

  ::

    $ git clone git@github.com:gotgithub/gotgit.git
    $ cd gotgit

* 为了向问题的发现者致敬，并经王胜同意，以他的身份进行提交。

  ::

    $ git config user.name "Wang Sheng"
    $ git config user.email wangsheng@ossxp.com

* 编辑\ ``errata.mkd``\ 文件\ [#]_\ ，录入新发现的书中的文字错误。

  ::

    $ vi errata.mkd

* 对\ ``error.mkd``\ 的改动如下：

  ::

    $ git diff
    diff --git a/errata.mkd b/errata.mkd
    index b0b68fb..29e40cf 100644
    --- a/errata.mkd
    +++ b/errata.mkd
    @@ -14,5 +14,6 @@
     |     66 | 倒数第11行                | Author（提交者）             |  Author（作者）              | [Github#2](http://github.com/gotgit/gotgit/issues/2)    |
     |    144 | 第1行                     | \`$ **git rev-parse  A^{tree}  A:**  | $ **git rev-parse  A^{tree}  A:**              | [#153](http://redmine.ossxp.com/redmine/issues/153)  |
     |    218 | 第8行                     | 况下，Gits标识出合并冲突，           | 况下，Git标识出合并冲突，                      | [#159](http://redmine.ossxp.com/redmine/issues/159)  |
    +|    369 | 第21行                    | 但 `-i` 参数仅当对一个项执行时才有效。 | 但 `-i` 参数仅当对一个项目执行时才有效。     | [Github#3](http://github.com/gotgit/gotgit/issues/3)    |
     |    516 | 倒数第15行                | **oldtag="cat"**             | **oldtag=\`cat\`**           | [#151](http://redmine.ossxp.com/redmine/issues/151)  |

* 提交修改。至于提交说明中出现的编号，是为了和缺陷跟踪系统关联，会在后面章节介绍。

  ::

    $ git add -u
    $ git commit -m "Fixed #3: should be 项目, not 项."

* 推送提交到GitHub。

  ::

    $ git push

访问GitHub上的派生项目页面，会看到以用户whangsheng在\ ``master``\ 分支\ [#]_\
创建的提交。如图4-4所示。

.. figure:: /images/work-with-others/gotgit-new-commit.png
   :scale: 100

   图4-4：派生版本库中的新提交

.. _pull-request:

Pull Request
------------------

那么如何能够让gotgit原始项目的创建者知道这个派生项目及新的提交呢？GitHub提供的\
工具就是“Pull Request”。注意到图4-3右上方“Pull Request”按钮了么？点击该按钮进入\
Pull Request创建界面。

在弹出的Pull Request创建界面中，点击菜单中的“Commits”，查看所包含的提交。如图4-5所示。

.. figure:: /images/work-with-others/pull-request-form-commit.png
   :scale: 100

   图4-5：Pull Request包含的提交

点击菜单中的“Files Changed”，查看所包含的提交。如图4-6所示。

.. figure:: /images/work-with-others/pull-request-form-file.png
   :scale: 100

   图4-6：Pull Request包含的改动差异

点击菜单中的“Preview Discussion”，填写Pull Request的标题和内容，完成Pull Request\
的创建。如图4-7所示。

.. figure:: /images/work-with-others/pull-request-form-discuss.png
   :scale: 100

   图4-7：Pull Request的提交界面

当Pull Request发出后，项目gotgit的开发者会收到通知邮件，如图4-8所示。

.. figure:: /images/work-with-others/pull-request-email.png
   :scale: 100

   图4-8：Pull Request的通知邮件

点击邮件中的URL链接，以项目gotgit的开发者（如ossxp-com）身份登录，看到如图4-9\
的视图。之所以看到有两个用户参与到此Pull Request，是因为Pull Request创建者和\
提交的作者是不同的用户。图4-9下方的表单可以向Pull Request追加评论，或者关闭此\
Pull Request。

.. figure:: /images/work-with-others/pull-request-owner-view.png
   :scale: 100

   图4-9：Pull Request接收者视图

GitHub如果检测到Pull Request中包含的提交可以直接合并，会显示自动合并的提示信息，\
点击图4-9中提示信息中的自动合并按钮，显示图4-10的自动合并对话框。

.. figure:: /images/work-with-others/pull-request-auto-merge.png
   :scale: 100

   图4-10：Pull Request的通知邮件

点击“Confirm Merge”按钮即完成Pull Request中所含提交的自动合并。自动合并完成后，\
Pull Request页面下方会以评论的形式出现相关提示，并自动关闭Pull Request。\
如图4-11所示。

.. figure:: /images/work-with-others/pull-request-closed.png
   :scale: 100

   图4-11：Pull Request关闭

.. _merge-by-hands:

手工合并
------------

Pull Request提供的自动合并显示在提交日志中是什么样子的呢？以用户ossxp-com\
身份检出版本库，会看到用户wangsheng的提交已经合并到版本库中。

::

  $ git clone git@github.com:gotgit/gotgit.git
  $ cd gotgit
  $ git log --graph -3
  *   commit 6c1f1ee152629fd2f8d00ebe92c27a32d068d756
  |\  Merge: 00c6c4b 7ecdfe7
  | | Author: OpenSourceXpress <worldhello.net@gmail.com>
  | | Date:   Tue Aug 16 01:23:47 2011 -0700
  | | 
  | |     Merge pull request #4 from gotgithub/master
  | |     
  | |     Find a typo in the book
  | |   
  | * commit 7ecdfe7451412cfb2e65bb47c12cf2162e21c841
  |/  Author: Wang Sheng <wangsheng@ossxp.com>
  |   Date:   Tue Aug 16 10:17:53 2011 +0800
  |   
  |       Fixed #3: should be 项目, not 项.
  |  
  * commit 00c6c4bfab9824bd967440902ce87440f9e87852
  | Author: Jiang Xin <worldhello.net@gmail.com>
  | Date:   Wed Aug 3 11:50:31 2011 +0800
  | 
  |     Change font color for stronger text from red to brown.

可以看出GitHub的自动合并产生了一个合并提交，类似执行\ ``git merge --no-ff``\
命令。也就是说即使用户wangsheng的提交是一个“快进式提交”（基于gotgit/gotgit\
版本库最新提交所做的提交），也要产生一个合并提交。

可能有人并不喜欢这种用\ ``--no-ff``\ 参数的非标准的合并方式，因为这种合并产生\
了一个多余的提交，可能增加代码评审的负担。若要取消GitHub的自动合并也很简单，\
因为Git无所不能：

::

  $ git reset --hard HEAD^  # 回退一个提交，即回退到当前提交的第一个父提交
  $ git rev-parse HEAD      # 检查是否正确的回退
  00c6c4bfab9824bd967440902ce87440f9e87852
  $ git push -f             # 强制推送回退的 master 分支

下面就演示一下当收到他人的Pull Request后，该如何手动合并。实际上在很多情况下，\
Pull Request所含提交有可能造成合并冲突，那样的话GitHub不再、也不能提供自动合并\
功能，就必须采用手工合并的方式。

* 将Pull Request发出者的派生版本库添加为一个新的源。

  例如收到来自gotgithub用户的Pull Request，不妨以gotgithub为名添加新的源。

  ::

    $ git remote add gotgithub https://github.com/gotgithub/gotgit.git

* 此时版本库中有两个源，一个克隆时自动建立的origin，另外一个就是新增加的gotgithub。

  ::

    $ git remote -v
    gotgithub       https://github.com/gotgithub/gotgit.git (fetch)
    gotgithub       https://github.com/gotgithub/gotgit.git (push)
    origin  git@github.com:gotgit/gotgit.git (fetch)
    origin  git@github.com:gotgit/gotgit.git (push)

* 获取远程版本库gotgithub的分支和提交。

  ::

    $ git fetch gotgithub
    From https://github.com/gotgithub/gotgit
     * [new branch]      gh-pages   -> gotgithub/gh-pages
     * [new branch]      master     -> gotgithub/master

* 现在除了本地分支\ ``master``\ 外，还有若干远程分支，如下：

  ::

    $ git branch -a
    * master
      remotes/gotgithub/gh-pages
      remotes/gotgithub/master
      remotes/origin/HEAD -> origin/master
      remotes/origin/gh-pages
      remotes/origin/master


* 将远程分支\ ``remotes/gotgithub/master``\ （可简写为\ ``gotgithub/master``\ ）\
  合并到当前分支中。

  ::

    $ git merge gotgithub/master
    Updating 00c6c4b..7ecdfe7
    Fast-forward
     errata.mkd |    1 +
     1 files changed, 1 insertions(+), 0 deletions(-)

* 查看提交说明，看到此次合并没有产生不必要的合并提交。

  ::

    $ git log --graph -2
    * commit 7ecdfe7451412cfb2e65bb47c12cf2162e21c841
    | Author: Wang Sheng <wangsheng@ossxp.com>
    | Date:   Tue Aug 16 10:17:53 2011 +0800
    | 
    |     Fixed #3: should be 项目, not 项.
    |  
    * commit 00c6c4bfab9824bd967440902ce87440f9e87852
    | Author: Jiang Xin <worldhello.net@gmail.com>
    | Date:   Wed Aug 3 11:50:31 2011 +0800
    | 
    |     Change font color for stronger text from red to brown.

* 将合并推送到GitHub版本库中。

  ::

    $ git push

.. _online-edit:

在线编辑
---------

GitHub提供了在线编辑功能，这样可以无需克隆版本库、无需使用Git即可完成对版本库\
中文件的修改，甚至可以在你的iPad甚至iPhone上完成对文件的修改。

以gotgithub账户身份登录GitHub，访问之前派生而来的版本库gotgithub/gotgit\
中的文件，例如文件\ ``errata.md``\ [#]_\ ，会看到其中一个“Edit this file”\
的按钮，如图4-12所示。


.. figure:: /images/work-with-others/edit-this-file-btn.png
   :scale: 100

   图4-12：浏览自己版本库中文件

点击图4-12中的“Edit this file”按钮，开始在线编辑文件\ ``errata.md``\ ，\
编辑器还支持语法加亮，如图4-13所示。

.. figure:: /images/work-with-others/edit-this-file-form.png
   :scale: 100

   图4-13：编辑文件

.. _quick-fork-edit-pull-request:

简化的 Fork + Pull Request
--------------------------------

到目前，我们已经了解了GitHub的三大武器：Fork、Pull Request和在线编辑。对于\
最常用的“Fork + Pull Request”操作，GitHub还提供了一个快捷模式。即GitHub对于\
无权更改的他人版本库中的文件，提供了一个类似在线编辑的按钮，名为\
“Fork and edit this file”按钮，自动完成版本库派生和在线编辑，即将三大武器一勺烩。

访问他人版本库（尚未在自己空间派生）中的文件，例如访问下面地址：\
http://git.io/hello-world-makefile\ [#]_\ 。显示他人（ossxp-com）版本库\
``hello-world``\ 中的\ ``src/Makefile``\ 文件，如图4-14所示。

.. figure:: /images/work-with-others/fork-and-edit-btn.png
   :scale: 100

   图4-14：浏览他人版本库中文件

点击图4-14中的“Fork and edit this file”按钮，会自动在自己托管空间创建派生\
版本库，并开始在线编辑文件\ ``src/Makefile``\ ，如图4-15所示。

.. figure:: /images/work-with-others/fork-and-edit-form.png
   :scale: 100

   图4-15：派生并编辑文件

文件修改完毕，点击“Propose File Change”按钮，会将改动作提交到派生的版本库中，\
并马上开启一个新的Pull Request。如图4-16所示。

.. figure:: /images/work-with-others/fork-and-edit-pull-request.png
   :scale: 100

   图4-16：编辑完毕自动开启Pull Request

点击“Send pull request”按钮完成Pull Request的创建。如果仔细查看图4-16，会发现\
Pull Request所包含的修改发生在\ ``gotgithub/hello-world``\ 派生版本库中的\
``patch-1``\ 分支中，并非通常的\ ``master``\ 分支。

原版本库\ ``ossxp-com/hello-world``\ 的开发者会收到一封邮件，通知有新的\
Pull Request，如下所示（前四行为信头）：

::

  From: GotGitHub <reply+i-...@reply.github.com>
  Date: 2011/12/17
  Subject: [hello-world] Bugfix: build target when version.h changed.  (#1)
  To: Jiang Xin <worldhello.net@gmail.com>


  Without this fix, when version changed only version.h update, target rebuild needs a second `make`.

  You can merge this Pull Request by running:

   git pull https://github.com/gotgithub/hello-world patch-1

  Or you can view, comment on it, or merge it online at:

   https://github.com/ossxp-com/hello-world/pull/1

  -- Commit Summary --

  * Bugfix: build target when version.h changed.

  -- File Changes --

  M src/Makefile (3)

  -- Patch Links --

   https://github.com/ossxp-com/hello-world/pull/1.patch
   https://github.com/ossxp-com/hello-world/pull/1.diff

  ---
  Reply to this email directly or view it on GitHub:
  https://github.com/ossxp-com/hello-world/pull/1

版本库\ ``ossxp-com/hello-world``\ 的管理员既可以通过GitHub提供的图形化界面\
完成对 Pull Request 的审核和合并，也可以在命令行下完成。正如邮件中所述若使用\
命令行，操作如下：

::

  $ git pull https://github.com/gotgithub/hello-world patch-1


----

.. [#] https://github.com/gotgit/gotgit/
.. [#] https://github.com/wangsheng/
.. [#] http://redmine.ossxp.com/redmine/issues/161
.. [#] 版本库 gotgit/gotgit 已将勘误文件重命名为\ ``errata.md``\ 。
.. [#] 版本库 gotgit/gotgit 原\ ``master``\ 分支内容已转移至\ ``gh-pages``\
       分支，通过GitHub提供的网站部署机制完成网页的编译和部署。
.. [#] 版本库 gotgit/gotgit 已重构。分支\ ``gh-pages``\ 中文件\ ``errata.md``\
       文件来自于原\ ``master``\ 分支的\ ``errata.mkd``\ 文件，地址：\
       https://github.com/gotgithub/gotgit/blob/gh-pages/errata.md 。
.. [#] 即地址 https://github.com/ossxp-com/hello-world/blob/master/src/Makefile 。
