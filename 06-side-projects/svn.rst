.. _svn-github:

用SVN操作GitHub
=================
2008年4月1日，GitHub宣布推出基于SVN的SVNHub网站，后证实这是一个愚人节玩笑\ [#]_\ 。\
2010年愚人节，类似消息再起，可这一次不再是玩笑\ [#]_\ 。即对于GitHub上的\
每一个Git版本库，现在都可以用SVN命令进行操作。更酷的是 SVN 版本库使用的是\
和 Git 版本库同样的地址\ [#]_\ 。

例如用下面的 Git 命令访问本书的 Git 版本库，显示版本库包含的引用。其中分支\
``master``\ 用于维护书稿，分支\ ``gh-pages``\ 保存书稿编译后的 HTML 网页用于\
在 GitHub 上显示。

::

  $ git ls-remote --heads https://github.com/gotgit/gotgithub
  ce5d3dda9b9ce8ec90def1da10181a094bea152f        refs/heads/gh-pages
  c4d370b1b0bafb103de14e104ca18b8c31d80add        refs/heads/master

如果使用 SVN 命令访问相同的版本库地址，Git 服务器变身为一个 SVN 服务器，\
将Git的引用对应为 SVN 风格的分支。如下：

::

  $ svn ls https://github.com/gotgit/gotgithub
  branches/
  trunk/
  $ svn ls https://github.com/gotgit/gotgithub/branches
  gh-pages/

SVN 支持部分检出，下面命令将整个主线\ ``trunk``\ （相当于 Git 版本库的\
``master``\ 分支）检出。

::

  $ svn checkout https://github.com/gotgit/gotgithub/trunk gotgithub
  A    gotgithub/Makefile
  A    gotgithub/README.rst
  ...
  Checked out revision 30.

还可以使用 SVN 命令创建分支，即相当于在 Git 版本库中创建新的引用。测试发现\
GitHub 尚不支持 SVN 远程拷贝创建分支，需要通过本地拷贝再提交的方式创建新分支。\
操作如下：

1. 为避免检出版本库所有分支过于耗时，在检出时使用\ ``--depth=empty``\ 参数。

   ::

     $ svn checkout --depth=empty \
       https://github.com/gotgit/gotgithub gotgithub-branches
     Checked out revision 30.

2. 进入到检出目录中，更新出\ ``trunk``\ 和\ ``branches``\ 两个顶级目录。

   ::

     $ cd gotgithub-branches
     $ svn up --depth=empty trunk branches
     A    trunk
     Updated to revision 30.
     A    branches
     Updated to revision 30.

3. 通过拷贝从主线\ ``trunk``\ 创建分支\ ``branches/svn-github``\ 。

   ::

     $ svn cp trunk branches/svn-github
     A         branches/svn-github
     $ svn st
     A  +    branches/svn-github

4. 提交完成分支创建。

   ::

     $ svn ci -m "create branch svn-github from trunk"
     Authentication realm: <https://github.com:443> GitHub
     Username: gotgithub
     Password for 'gotgithub':
     Adding         branches/svn-github
     
     Committed revision 31.

5. 用 Git 命令可以看到服务器上创建了一个新的同名引用，并且指向和\ ``master``\ 一致。

   ::

     $ git ls-remote --heads https://github.com/gotgit/gotgithub
     ce5d3dda9b9ce8ec90def1da10181a094bea152f        refs/heads/gh-pages
     c4d370b1b0bafb103de14e104ca18b8c31d80add        refs/heads/master
     c4d370b1b0bafb103de14e104ca18b8c31d80add        refs/heads/svn-github

下面尝试一下用 SVN 命令在新创建的分支\ ``svn-github``\ 中提交。

1. 进入到之前检出完整主线\ ``trunk``\ 的\ ``gotgithub``\ 目录，并将工作区切换\
   为分支\ ``branches/svn-github``\ 。

   ::

     $ cd ../gotgithub
     $ svn switch https://github.com/gotgit/gotgithub/branches/svn-github
     At revision 31.

2. 修改文件，查看工作区状态。

   ::

     $ svn st
     M       06-side-projects/040-svn.rst

3. 用 SVN 提交。

   ::

     $ svn ci -m "GitHub svn client support improved. Refs: http://git.io/svn"
     Sending        06-side-projects/040-svn.rst
     Transmitting file data .
     Committed revision 32.

4. 同样查看 Git 版本库的更新，会发现\ ``svn-github``\ 分支的指向已和\
   ``master``\ 不同。

   ::

     $ git ls-remote --heads https://github.com/gotgit/gotgithub
     ce5d3dda9b9ce8ec90def1da10181a094bea152f        refs/heads/gh-pages
     c4d370b1b0bafb103de14e104ca18b8c31d80add        refs/heads/master
     64b80cb5331e28fdfb896e2ab3085779bf6ca019        refs/heads/svn-github

----

.. [#] https://github.com/blog/31-back-to-subversion
.. [#] https://github.com/blog/626-announcing-svn-support
.. [#] https://github.com/blog/966-improved-subversion-client-support
