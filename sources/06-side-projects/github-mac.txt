.. _mac:

github:mac
-----------------------

GitHub专为Mac用户开发了一款图形化客户端应用\ ``github:mac``\ ，在Mac下操作\
GitHub更简单。软件下载地址： http://mac.github.com/ 。

``github:mac`` 可以实现版本库克隆、查看历史、提交、分支管理、与GitHub同步等\
功能。图6-12展示的是提交界面，在提交界面中同时显示了变更的差异比较，用户可以\
挑选文件中的部分变更进行提交，显然这个操作要比在命令行中执行\
:command:`git add --patch`\ 或\ :command:`git commit --patch`\ 要更加直观。

.. figure:: /images/side-projects/mac-partial-commit.png
   :scale: 100

   图6-12：筛选文件中的部分更改进行提交

``github:mac``\ 和GitHub深度集成，当配置好关联的GitHub账号后，会自动在本地\
创建专用的SSH公钥/私钥对文件 :file:`~/.ssh/github_rsa` （如果该文件不存在的\
话），然后将公钥文件传递到GitHub网站并自动完成配置。新增的SSH公钥文件显示在\
GitHub网站的账号设置中，如图6-13所示：

.. figure:: /images/side-projects/mac-new-ssh-pubkey.png
   :scale: 100

   图6-13：在GitHub上自动添加的SSH公钥

同时\ ``github:mac``\ 还在本地将新生成的私钥文件添加到\ ``ssh-agent``\
认证代理中，这样一旦通过 SSH 协议连接GitHub，首先采用该公钥/私钥对进行身份\
认证。用下面的命令可以查看添加到\ ``ssh-agent``\ 中的私钥文件。

::

  $ ssh-add -l
  2048 aa:01:4f:d2:14:ba:5f:9f:8c:dc:b5:9d:44:cd:8e:18 /Users/jiangxin/.ssh/github_rsa (RSA)

这种透明的公钥认证管理非常酷，对于大多数只使用唯一一个GitHub账号的用户来说\
是非常方便的。但如果用户拥有多个GitHub账号并需要不时切换账号，这种实现却很\
糟糕，会导致认证错误。因为当\ ``ssh-agent``\ 认证代理缓存了私钥后，连接由\
文件 :file:`~/.ssh/config` 设置的 SSH 别名主机无法使用指定的公钥/私钥对进行\
认证，导致认证失败。

遇到 GitHub 账户 SSH 认证问题，可以运行下面命令清空\ ``ssh-agent``\ 缓存的私钥。

::

  $ ssh-add -d ~/.ssh/github_rsa
  Identity removed: /Users/jiangxin/.ssh/github_rsa (/Users/jiangxin/.ssh/github_rsa.pub)
