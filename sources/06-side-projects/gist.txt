.. _gist:

GitHub:Gist
===============
在GitHub网站的导航条上就有Gist子网站的链接： https://gist.github.com/ ，\
在本节我们就揭开其面纱。

.. figure:: /images/side-projects/gist-in-github-navbar.png
   :scale: 100

   图6-1：GitHub上的Gist链接

Gist作为一个粘贴数据的工具，就像 Pastie 网站\ [#]_\ 一样，可以很容易地将数据\
粘贴在Gist网站中，并在其他网页中引用Gist中粘贴的数据。作为GitHub的一个子网站，\
很自然地，Gist使用Git版本库对粘贴数据进行维护，这非常酷。

.. _paste:

数据的粘贴和引用
-----------------
进入Gist网站的首页，就会看到一个大大的数据粘贴对话框，如图6-2所示。

.. figure:: /images/side-projects/gist-homepage.png
   :scale: 100

   图6-2：Gist网站首页

只要提供一行简单的描述、文件名，并粘贴文件内容，即可创建一个新的粘贴。创建\
新的粘贴时，如果不指定文件名，将由系统自动指派。如图6-3所示。

.. figure:: /images/side-projects/gist-create-new.png
   :scale: 100

   图6-3：创建新的Gist

每一个新的粘贴称为一个Gist，并拥有唯一的URL。如果选择创建公开的Gist，URL中将\
使用顺序递增的ID号，如本例创建的Gist的URL地址为：\
https://gist.github.com/1202870\ 。

若选择创建私有Gist，URL中则采用20位十六进制数字的ID，例如私密Gist：\
https://gist.github.com/78d67164131ec9e08dfe\ 。需要指出的是，私有Gist的\
私密性并不像GitHub私有版本库的私密性那么强，只是其URL没有在用户Gist列表中列出，\
也不能通过Gist网站搜索到而已。如果用户知道某私密Gist的URL地址，同样可以访问、\
克隆该私密Gist，甚至创建基于该Gist创建分支（fork）。

当一个粘贴创建完毕后，会显示新建立的Gist页面，如图6-4所示。

.. figure:: /images/side-projects/gist-created.png
   :scale: 100

   图6-4：新创建的Gist

点击其中的“embed”（嵌入）按钮，就会显示一段用于嵌入其他网页的JavaScript代码，\
如图6-5所示。

.. figure:: /images/side-projects/gist-embed.png
   :scale: 100

   图6-5：显示嵌入Java


对应的嵌入JavaScript代码如下：

::

  <script src="https://gist.github.com/1202870.js?file=countdown.rb"></script>


将上面的JavaScript代码嵌入到网页（如博客\ [#]_\ ）中，即可在相应的网页中嵌入\
来自Gist的数据，并保持语法加亮等功能，如图6-6所示。

.. figure:: /images/side-projects/gist-embed-in-blog.png
   :scale: 100

   图6-6：博客中引用Gist数据

.. _git-backend-gist:

Gist背后的Git库
-----------------
创建的每一个Gist的背后都对应着一个Git版本库。例如之前创建的ID为1202870的Gist\
对应的Git版本库，可以使用两种协议进行访问：

* Git协议：\ ``git://gist.github.com/1202870.git``
* SSH协议：\ ``git@gist.github.com:1202870.git``

可以通过Git命令克隆和操作该版本库。

* 克隆该Gist对应的版本库。

  ::

    $ git clone git@gist.github.com:1202870.git
    $ cd 1202870

* 查看修改日志。每一次对Gist中文件的修改对应于一次提交。

  ::

    $ git log
    commit 993d28a1319eca314ab2e3f4c46882cf328e5ff9
    Author: GotGitHub <gotgithub@gmail.com>
    Date:   Thu Sep 15 15:41:10 2011 +0800

    commit 4dd9cfd54e1522d0b62d92dd5f705a61e3fe8778
    Author: GotGitHub <gotgithub@gmail.com>
    Date:   Thu Sep 8 00:46:50 2011 -0700


* 查看最近一次更改。

  ::
  
    $ git show HEAD
    commit 993d28a1319eca314ab2e3f4c46882cf328e5ff9
    Author: GotGitHub <gotgithub@gmail.com>
    Date:   Thu Sep 15 15:41:10 2011 +0800
    
    diff --git a/countdown.rb b/countdown.rb
    index a9d747b..9045738 100644
    --- a/countdown.rb
    +++ b/countdown.rb
    @@ -4,4 +4,8 @@
     require 'Date'
     
     days=(DateTime.new(2012,10,15)-DateTime.now).ceil
    -puts "Maybe #{days} days left."
    \ No newline at end of file
    +if days >= 0
    +  puts "Maybe #{days} days left."
    +else
    +  puts "Passed for #{days.abs} days."
    +end
    \ No newline at end of file

Gist网站并没有像GitHub网站那样对于Git版本库提供完整的、近乎复杂的操作界面和\
工作流支持，而只提供了最基本的操作界面。如图6-7所示。

.. figure:: /images/side-projects/gist-git-repo.png
   :scale: 100

   图6-7：Gist版本库简易操作界面

在这个简易的Git版本库操作界面中，左侧是版本库的简介、文件预览以及在线编辑、\
下载、加注星标\ [#]_\ 、版本库分支\ [#]_\ 等相关操作按钮。若以Gist创建者登录，\
会在右侧看到他人基于该Gist创建分支的情况，但是并不提供GitHub才有的Pull Request\
等功能。在界面的右侧还显示了Gist修订历史，和之前通过\ ``git log``\ 命令\
从Git版本库看到的一样。

.. _greasemonkey:

Greasemonkey
-----------------
Gist除了被用于粘贴数据（如代码块）并在网页中引用之外，还被用户挖掘出了新的\
应用模式，例如用作Greasemonkey脚本的维护\ [#]_\ 。

Greasemonkey\ [#]_\ 或类似插件为浏览器提供用户端JavaScript扩展功能，最早\
出现于FireFox浏览器中。其他浏览器也陆续增加了对用户端JavaScript的支持，\
如Safari的 NinjaKit\ [#]_\ 插件，IE的Trixie\ [#]_\ 插件，以及Chrome的\
Greasemetal插件\ [#]_\ 。关于如何在浏览器中安装并启用相应的插件，参照相关\
插件网站的介绍，在此不做过多叙述。

当浏览器安装了 Greasemonkey 或类似插件之后，当访问扩展名为\ ``.user.js``\
的URL时，会将该URL指向的JavaScript脚本安装在浏览器中，当访问指定的网址时会\
自动调用相应的JavaScript脚本，修改相关网页内容或添加特效等等。

我针对《Git权威指南》官网的测试网页写了一个Greasemonkey示例脚本，可以展示\
用户端JavaScript的魔法，这个用户端JavaScript脚本保存在Gist中：\
https://gist.github.com/1084591\ ，如图6-8所示。

.. figure:: /images/side-projects/gist-greasemonkey.png
   :scale: 100

   图6-8：保存Greasemonkey用户端脚本的Gist

该Greasemonkey脚本的文件名为\ ``click_more.user.js``\ ，该文件的文件头使用\
特殊的注释语句为Greasemonkey提供相关的安装和注册信息，内容如下（为方便描述\
添加了行号）：

::

  1  // ==UserScript==
  2  // @name           Click more for toggle
  3  // @namespace      gotgit
  4  // @description    Add a toogle effect at the location where anchor with a click-more css.
  5  // @include        http://www.worldhello.net/gotgit/demo*
  6  // @include        http://gotgit.github.com/gotgit/demo*
  7  // @include        http://www.ossxp.com/doc/gotgit/demo*
  8  // @require        http://code.jquery.com/jquery-1.6.2.min.js
  9  // ==/UserScript==

其中第5、6、7行三条\ `include`\ 语句限定了此用户端JavaScript脚本的应用范围，\
即只针对指定的URL（使用通配符）执行该脚本。第8行设定脚本依赖，即该脚本依赖\
jQuery，会在运行前到指定的URL地址加载jQuery脚本。

在安装该脚本前，先用浏览器访问网址\ http://www.worldhello.net/gotgit/demo.html\ ，\
看看不加载用户端JavaScript脚本时网页的模样。该网页中包含一个长长的网上书店\
列表，如图6-9所示。 

.. figure:: /images/side-projects/gist-user-js-apply-before.png
   :scale: 100

   图6-9：应用用户端JavaScript脚本前的网页内容

接下来开始安装该用户端JavaScript脚本。安装非常简单，只要点击图6-8的Gist当中\
的脚本文件对应的“raw”链接，即点击脚本文件原始内容链接\ [#]_\ 即可开启安装。\
这是因为该URL以\ ``.user.js``\ 结尾，会被Greasemonkey（或类似插件）识别并安装，\
如图6-10是Greasemonkey弹出的用户端脚本安装界面。

.. figure:: /images/side-projects/gist-user-js-install.png
   :scale: 100

   图6-10：安装用户端JavaScript脚本

用户端脚本安装完毕后，再访问同样的测试网页\
http://www.worldhello.net/gotgit/demo.html\ ，会发现网页中出现了\
一个名为“更多”的可点击链接，长长的网上书店列表不见了。如图6-11所示。

.. figure:: /images/side-projects/gist-user-js-apply-after.png
   :scale: 100

   图6-11：应用用户端JavaScript脚本后的网页内容

如果查看网页源码，会发现该网页中根本没有包含和调用任何JavaScript脚本，只是\
在页面源码中包含着一个没有任何实质输出的标签：

::

  <p><a class="click-more"></a></p>

实际上正是这个特殊的标签被Greasemonkey所加载的用户端脚本识别，为HTML网页\
添加了特效。

.. _gist-cli:

命令行操作Gist
-----------------
GitHub开发者还写了一个名为gist的命令行工具对Gist进行操作，地址见\
https://github.com/defunkt/gist\ 。

该工具使用Ruby开发，对两个特定的Git风格的配置变量进行如下设置后，即可实现在\
命令行中自动以特定用户身份登录操作Gist。

::

  $ git config --global github.user "your-github-username"
  $ git config --global github.token "your-github-token"

其中\ ``github.token``\ 中保存的是用户的API TOKEN，这在“2.1 创建GitHub账号”\
一节有过介绍。

使用gist命令行工具创建新的Gist非常简单。

* 创建包含一个文件（如\ ``script.py``\ ）的Gist，使用如下命令。

  ::
  
    $ gist script.py
  
* 创建包含多个文件的Gist，使用类似如下的命令。
  
  ::
  
    $ gist script.js notes.txt

如果对命令行操作方式感兴趣，参考gist工具网站的\ `README`\ 文件。


----

.. [#] http://pastie.org/
.. [#] http://www.worldhello.net/2011/09/14/2521.html
.. [#] 对感兴趣的Gist进行收藏，参见博客 https://github.com/blog/673-starring-gists 。
.. [#] 访问他人创建的Gist时，提供分支功能按钮。
.. [#] https://github.com/blog/302-gist-for-greasemonkey
.. [#] https://addons.mozilla.org/en-US/firefox/addon/greasemonkey/
.. [#] http://ss-o.net/safari/extension/NinjaKit.safariextz
.. [#] http://www.bhelpuri.net/Trixie/
.. [#] 版本4之后的Chrome内置了Greasemonkey类似功能，无需额外插件。
.. [#] https://gist.github.com/raw/1084591/73c3e4dfc827732241ca753fe7bb985c14c9d7ab/click_more.user.js
