创建GitHub账号
===============

注册GitHub账号，只要点击导航条中的“Pricing and Signup”，或者点击首页中那个大大的“Plans,Pricing and Signup”按钮，即进入收费方案介绍及注册页面。

收费？不必担心，开源软件托管是GitHub的基石，对于开源项目的版本库（即非私有版本库）的托管，GitHub是免费的。在收费方案及注册页面中，最上面的就是针对于开源的免费托管方案，如图2-1所示。

.. figure:: /images/join-github/free-plan.png
   :scale: 100

   图2-1：针对开源项目（公开版本库）的免费方案

至于本页其他付费方案，将在后面的章节介绍。点击免费方案右侧的“Create a free account”按钮，就进入到注册页面，如图2-2所示。

.. figure:: /images/join-github/signup.png
   :scale: 100

   图2-2：账号注册

GitHub的注册页面非常简洁，只有登录ID，邮件地址和口令需要输入。要注意的是每个邮件地址只能注册一次。注册完毕即以新注册的账号自动登录，图2-3是以新注册的gotgithub用户登录后的首页。在首页右上方的导航条，可以看到当前登录用户的名称，如图2-3中显示为gotgithub。在登录用户名称前显示用户照片，因为尚未设置所以显示为缺省图片——GitHub吉祥物Octocat的剪影。点击导航条中的“Account Settings”，对账号进行进一步设置。

.. figure:: /images/join-github/loggedin.png
   :scale: 100

   图2-3：登录后的GitHub首页

图2-4对用户公开身份信息进行设置，所有内容均为可选项，如果填写将显示在个人页面中，并能被所有人访问。注意修改用户头像需要访问第三方头像设置网站：gravatar.com。Gravatar网站提供的头像服务是一个通用服务，可为大部分Web应用所使用。

图2-4中还显示了当前用户使用的GitHub托管方案（Free）和使用统计。因为当前注册用户选择的是免费方案，所以可用的私有版本库数量和私有空间协同者数目都是零。免费方案拥有300MB托管空间，因当前尚未创建版本库托管，所以空间占用为零。GitHub对开源软件的300MB托管空间限制并非硬性限制，可以申请扩增托管空间，如果不存在滥用情况的话。

.. figure:: /images/join-github/setting-profile.png
   :scale: 100

   图2-4：账户设置页

点击菜单中的“Account Admin”，可以更改口令、查看API Token、修改用户名，以及删除自身账号，如图2-5所示。

.. figure:: /images/join-github/setting-admin.png
   :scale: 100

   图2-5：账户管理

其中API Token是和用户口令相关的密钥，当用户口令更改时API Token也随之更改。GitHub的某些应用会使用API Token进行身份认证，从而避免直接使用用户口令造成泄露的风险。API Token若泄露的危害要远远小于口令泄露，这因为API Token不能用于登录GitHub网站等，而且一旦API Token泄露可以很容易通过更改口令的方式更换API Token。

点击菜单中的“Email Addresses”，可以添加和删除邮件地址，如图2-6所示。GitHub允许为一个账号绑定多个邮件地址，以便能够将Git版本库中的提交（提交者以 "用户名 <邮件地址>" 的格式给出）正确对应到GitHub账户。

.. figure:: /images/join-github/setting-email.png
   :scale: 100

   图2-6：邮件地址管理

GitHub为托管的Git版本库提供SSH协议支持，即用户可以用公钥认证的方式连接到GitHub的SSH服务器。下面的示例用ssh命令连接github.com的SSH服务，登录用户名为git（所有GitHub用户共享此SSH用户名，不要写成其他）。

::

  $ ssh -T git@github.com
  Permission denied (publickey).

上面的示例显示登录失败，这是因为我们尚未在GitHub账户中正确设置公钥认证。图2-7显示的是GitHub的SSH公钥设置界面。

.. figure:: /images/join-github/setting-ssh.png
   :scale: 100

   图2-7：SSH公钥管理

要想向GitHub添加SSH公钥，首先要确保正确生成了对应的公钥/私钥对。关于SSH公钥认证，在我的《Git权威指南》一书的“第29章使用SSH协议”中有详细介绍，这里仅做简要的介绍。

GitHub的SSH服务支持OpenSSH格式的公钥认证，可以通过Linux、Mac OS X、或Cygwin下的 ``ssh-keygen`` 命令创建公钥/私钥对。命令如下：

::

  $ ssh-keygen

然后根据提示在用户主目录下的 ``.ssh`` 目录中创建默认的公钥/私钥对文件，其中 ``~/.ssh/id_rsa`` 是私钥文件， ``~/.ssh/id_rsa.pub`` 是公钥文件。注意私钥文件要严加保护，不能泄露给任何人。如果在执行 ``ssh-keygen`` 命令时选择了使用口令保护私钥，私钥文件是经过加密的。至于公钥文件 ``~/.ssh/id_rsa.pub`` 则可以放心地公开给他人。

也可以用 ``ssh-keygen`` 命令以不同的名称创建多个公钥，当拥有多个GitHub账号时，非常重要。这是因为虽然一个GitHub账号允许使用多个不同的SSH公钥，但反过来，一个SSH公钥只能对应于一个GitHub账号。下面的命令在 ``~/.ssh`` 目录下创建名为 ``gotgithub`` 的私钥和名为 ``gotgithub.pub`` 的公钥文件。

::

  $ ssh-keygen -C "gotgithub@gmail.com" -f ~/.ssh/gotgithub

当生成的公钥/私钥对不在缺省位置（~/.ssh/id_rsa等）时，使用 ``ssh`` 命令连接远程主机时需要使用参数 ``-i <filename>`` 指定公钥/私钥对。或者在配置文件 ``~/.ssh/config`` 中针对相应主机进行设定。例如对于上例创建了非缺省公钥/私钥对 ``~/.ssh/gotgithub`` ，可以在 ``~/.ssh/config`` 配置文件中写入如下配置。

::

  Host github.com
    User git
    Hostname github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/gotgithub

好了，有了上面的准备，就将 :file:`~/.ssh/gotgithub.pub` 文件内容拷贝到剪切板。在命令行用下面的命令可直接将文件内容拷贝到剪切板：

::

  $ cat ~/.ssh/gotgithub.pub | pbcopy


然后将公钥文件中的内容粘贴到GitHub的SSH公钥管理的对话框中，如图2-8所示。注意整个公钥为一行，不要断行。

.. figure:: /images/join-github/setting-ssh-gotgithub.png
   :scale: 100

   图2-8：添加SSH公钥认证

设置成功后，再用 ``ssh`` 命令访问 github.com，会显示一条认证成功信息并退出。在认证成功的信息中还会显示该公钥对应的用户名。

::

  $ ssh -T git@github.com
  Hi gotgithub! You've successfully authenticated, but GitHub does not provide shell access.

如果您未能看到类似的成功信息，可以通过在 ``ssh`` 命令后面添加 ``-v`` 参数加以诊断，会在冗长的会话中看到认证所使用的公钥文件等信息。

::

  $ ssh -Tv git@github.com
  ...
  debug1: Authentications that can continue: publickey
  debug1: Next authentication method: publickey
  debug1: Offering RSA public key: /Users/jiangxin/.ssh/gotgithub
  ...
  debug1: Entering interactive session.
  Hi gotgithub! You've successfully authenticated, but GitHub does not provide shell access.
  ...

账号设置的最后一项是向GitHub提供你的求职信息。GitHub作为一个优秀程序员的聚集地，已经成为重要的IT人才招聘途径，如果你需要找工作的话，提供简历并打开“Available for hire”选项，如图2-9所示。

.. figure:: /images/join-github/setting-job.png
   :scale: 100

   图2-9：求职信息管理

