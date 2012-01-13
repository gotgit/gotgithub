.. _new-project:

创建新项目
===============

.. _new-repo:

新版本库即是新项目
----------------------

在GitHub，一个项目对应唯一的Git版本库，创建一个新的版本库就是创建一个新的项目。\
访问仪表板（Dashboard）页面，如图3-1，可以看到关注的版本库中已经有一个，\
但自己的版本库为零。在显示为零的版本库列表面板中有一个按钮“New Repository”，\
点击该按钮开始创建新版本库。

.. figure:: /images/project-hosting/new-repo-btn.png
   :scale: 100

   图3-1：版本库列表面板

新建版本库的界面如图3-2所示。

.. figure:: /images/project-hosting/new-project.png
   :scale: 100

   图3-2：创建新项目

我们为新建立的版本库命名为“helloworld”，\
相应的项目名亦为“helloworld”，创建完毕后访问项目页，提示版本库\
尚未初始化，并给出如何初始化版本库的帮助，如图3-3所示。

.. figure:: /images/project-hosting/project-uninitial.png
   :scale: 100

   图3-3：项目尚未初始化

在图3-3中可以看到访问协议增加了一个支持读写的SSH协议，访问地址为：\
``git@github.com:gotgithub/helloworld.git``\ 。注意任何GitHub用户均可使用该\
URL访问此公开版本库，但只有版本库建立者gotgithub具有读写权限，其他人\
只有只读权限。在初始化版本库之前，最好先确认是否是用正确的公钥进行认证，如下：

::

  $ ssh -T git@github.com
  Hi gotgithub! You've successfully authenticated, but GitHub does not provide shell access.

.. _init-by-clone:

版本库初始化
--------------

如果是从头创建版本库，可以采用先克隆，建立提交数据，最后再通过推送完成GitHub\
版本库的初始化。步骤如下：

* 克隆版本库。

  克隆过程会显示警告，不过这个警告可以忽略，因为GitHub创建的版本库本来就是一个\
  空白的版本库。

  ::

    $ git clone git@github.com:gotgithub/helloworld.git
    Cloning into 'helloworld'...
    warning: You appear to have cloned an empty repository.

* 创建文件\ ``README.md``\ [#]_\ 。

  下面是一段示例文字，把这段文字保存为文件\ ``README.md``\ ，该文件的内容将会\
  直接显示在项目首页中（显示效果参见后面的图3-5）。

  ::

    # 我的第一个GitHub项目

    这是项目 [helloworld](https://github.com/gotgithub/helloworld) ，
    欢迎访问。
    
    这个项目的版本库是 **Git格式** ，在 Windows、Linux、Mac OS X
    平台都有客户端工具可以访问。虽然版本库只提供Git一种格式，
    但是你还是可以用其他用其他工具访问，如 ``svn`` 和 ``hg`` 。
    
    ## 版本库地址
    
    支持三种访问协议：
    
    * HTTP协议: `https://github.com/gotgithub/helloworld.git` 。
    * Git协议: `git://github.com/gotgithub/helloworld.git` 。
    * SSH协议: `ssh://git@github.com/gotgithub/helloworld.git` 。
    
    ## 克隆版本库
    
    操作示例：
    
        $ git clone git://github.com/gotgithub/helloworld.git

  上面这段文字采用Markdown格式，您也可以使用其他支持的格式，只要确保\ ``README``\
  文件使用正确的扩展名。本书附录部分介绍了Markdown及其他GitHub支持的标记语言。\
  关于Markdown，目前我们只需知道这一个易于识别和理解的纯文本格式，可以方便的\
  转换为HTML。Markdown语法非常像我们在写邮件（纯文本）时用空行来分隔段落、\
  用星号开启列表、用缩进表示引用内容等等。

* 添加\ ``README.md``\ 文件并提交。

  ::

    $ git add README.md
    $ git commit -m "README for this project."

* 向GitHub推送，完成版本库初始化。

  ::

    $ git push origin master

然后查看GitHub上新建项目的首页。项目首页的上半部分可见版本库包含了一个新的\
提交，以及版本库目录树中包含的文件，如图3-4所示。

.. figure:: /images/project-hosting/project-pushed-head.png
   :scale: 100

   图3-4：完成推送后的项目首页上半部分

在项目首页的下半部分，会看到\ ``README.md``\ 文件被转换为HTML显示，如图3-5所示。

.. figure:: /images/project-hosting/project-pushed-tail.png
   :scale: 100

   图3-5：完成推送后的项目首页下半部分

.. _init-by-push:

从已有版本库创建
-----------------

如果在GitHub项目初始化之前，数据已经存在于本地版本库中，显然像上面那样先克隆、\
再提交、后推送的方法就不适宜了。应该采用下面的方法。

为试验新的版本库初始化方法，先把刚刚新建的测试项目“helloworld”删除，\
同时也将本地工作区中克隆的“helloworld”删除。\
警告：删除项目的操作非常危险，不可恢复，慎用。

* 点击项目首页中项目名称旁边的“Admin”按钮进入项目管理页，再点击页面最下方的\
  删除版本按钮，如图3-6所示。

  .. figure:: /images/project-hosting/project-delete.png
     :scale: 100
  
     图3-6：删除项目
  
* 然后再重建版本库“helloworld”，如本章一开始图3-2所示。

接下来使用下面的步骤完成“helloworld”版本库的初始化。

* 本地建立一个Git版本库。

  ::

    $ mkdir helloworld
    $ cd helloworld
    $ git init

* 然后在版本库中添加示例文件，如\ ``README.md``\ 文件，内容同前。

  ::

    $ git add README.md
    $ git commit -m "README for this project."

* 为版本库添加名为\ ``origin``\ 的远程版本库。

  ::

    $ git remote add origin git@github.com:gotgithub/helloworld.git

* 执行推送命令，完成GitHub版本库的初始化。注意命令行中的\ ``-u``\ 参数，在推送\
  成功后自动建立本地分支与远程版本库分支的追踪。

  ::

    $ git push -u origin master

----

.. [#] 以扩展名\ ``.md``\ ，\ ``.mkd``\ ，\ ``.mkdn``\ ，\ ``.mdown``\ ，\ ``.markdown``\
       等为结尾的文件，均以Markdown标记语言语法进行解析并显示。
