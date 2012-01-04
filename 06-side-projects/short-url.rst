.. _short-url:

GitHub短网址服务
===================

在“第2.2节 浏览托管项目”一节介绍图形文件差异比较时，需要给出一个网址，但\
这个网址很长。如下：

::

  https://github.com/cameronmcefee/Image-Diff-View-Modes/commit/8e95f70c9c47168305970e91021072673d7cdad8

很自然地想到了Google短网址服务，于是由上面的长网址生成出一个短小精干的网址：\
http://goo.gl/Gy85b\ ，访问该短网址会自动重定向到对应的长网址。

2011年11月，GitHub也推出了自己的短网址服务\ [#]_\ ，为GitHub自身网址提供\
短网址转换服务。GitHub短网址服务没有像Google短网址服务那样提供基于Web的图形\
化转换界面，而是需要用命令行进行网址转换。

例如对于网址 https://github.com/blog/985-git-io-github-url-shortener 的转换，\
使用\ ``curl``\ 命令如下操作。

* 将长网址转换为短网址。

  命令\ ``curl``\ 输出中的\ ``Location:``\ 语句即是转换后的短网址。

  ::

    $ curl -i http://git.io -F 'url=https://github.com/blog/985-git-io-github-url-shortener'
    ...
    HTTP/1.1 201 Created
    ...
    Location: http://git.io/help

* 查看短网址对应的原网址，同样使用\ ``curl``\ 命令。

  命令\ ``curl``\ 输出302重定向地址即为原始网址。

  ::

    $ curl -i http://git.io/help
    HTTP/1.1 302 Found
    ...
    Location: https://github.com/blog/985-git-io-github-url-shortener

为使转换的短网址更易于记忆和识别，可在\ ``curl``\ 命令中用 code 参数设定期望的\
短网址。例如下面命令将本节一开始提到的长网址转换为短网址：\
http://git.io/image-diff\ 。

::

  $ curl -i http://git.io -F \
    'url=https://github.com/cameronmcefee/Image-Diff-View-Modes/commit/8e95f70c9c47168305970e91021072673d7cdad8' \
    -F 'code=image-diff'
  ...
  HTTP/1.1 201 Created
  ...
  Location: http://git.io/image-diff


.. [#] http://git.io/help
