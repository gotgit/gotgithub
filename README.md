这是一本关于GitHub的书，在线阅读请访问： <http://www.worldhello.net/gotgithub> 。

动笔写GitHub不是因为我对其了解，恰恰是对其太不了解。在我写的 [《Git权威指南》][gotgit] 一书中，涉及到GitHub的只有区区三页纸，这显然回答不了读者对于GitHub的诸多疑问。

这本书采用Creative Commons协议发布，并托管在GitHub上，意味着您可以免费阅读并可以用GitHub特有的方式参与本书的维护。

## 如何离线阅读

项目 [gotgit/gotgithub](https://github.com/gotgit/gotgithub) 的版本库中的 ``gh-pages`` 分支保存着本书编译后的页面，意味着您只要下载版本库并检出 ``gh-pages`` 分支即可在本地浏览。

* 克隆版本库。

        $ git clone git://github.com/gotgit/gotgithub.git

* 检出 ``gh-pages`` 分支。

        $ cd gotgithub
        $ git checkout gh-pages

* 用浏览器打开 ``index.html`` 即可离线阅读。

因分支 ``gh-pages`` 的提交历史可能会周期性删除或压缩合并，为避免执行 ``git pull`` 更新分支时造成困惑，请对本地版本库进行如下设置。

    $ git config --add remote.origin.fetch +refs/heads/gh-pages:refs/heads/gh-pages

## 如何编译

### 预备

* Python, docutils

    本书使用 [reStructuredText](http://docutils.sourceforge.net/rst.html) 格式撰写，格式解析依赖 Python 和 docutils 包。

* Sphinx

    用 [Sphinx](http://sphinx.pocoo.org/) 工具进行编译。编译前先确认已经安装 Python、docutils 及 sphinx。

* ImageMagick 及 Inkscape

    本书图片矢量图采用 [Inkscape](http://inkscape.org/) 绘制，位图处理采用 [GIMP](http://www.gimp.org/) 。上述格式图片在网页显示需要格式转换，格式转换需用到 ImageMagick 和 Inkscape。

* Git

    不解释。

### 克隆版本库（本书书稿及图片）

本书用两个版本库维护：

* 书稿版本库：

    https://github.com/gotgit/gotgithub/

* 图片版本库：

    https://github.com/gotgit/gotgithub-graphics/


本书的图片版本库以子模组形式关联到书稿版本库，运行下面命令执行克隆：

* 若尚未克隆书稿版本库，先克隆书稿版本库。

        $ git clone git://github.com/gotgit/gotgithub.git
        $ cd gotgithub

* 默认检出 ``master`` 分支。如果当前非 ``master`` 分支，执行下面命令检出分支。

        $ git checkout master

* 通过子模组更新命令克隆子模组版本库（即保存图片的版本库）并检出。

      $ git submodule init
      $ git submodule update

### 编译书稿

确保安装了 Sphinx、ImageMagick、Inkscape。编译本书使用命令：

    $ make html

编译后的网页位于 ``_build/html`` 目录下。

更多的格式输出参见下面的命令输出：

    $ make

## 如何贡献

请采用GitHub方式贡献。

* 创建派生项目。即 Fork。
* 修改您觉得不满意的地方。修改后推送到您创建的分支版本库中。
* 通过 GitHub 向我发送 Pull Request。

[gotgit]: http://www.worldhello.net/gotgit/ "Got Git"

-- 蒋鑫, <http://weibo.com/gotgit/>
