公钥认证管理
================

开发者向GitHub版本库写入最常用的是SSH协议，因为SSH协议使用公钥认证，可以实现无口令访问，而若使用HTTPS协议每次身份认证时都需要提供口令。使用SSH公钥认证，就涉及到公钥的管理。

用户级公钥管理
---------------

开发者可能会从不止一台电脑访问GitHub中的版本库（用SSH协议），因不同的电脑有不同的公钥/私钥对，这就需要为GitHub账号添加多个公钥。点击账号设置中的“SSH Public Keys”进入SSH公钥管理界面，如图3-11所示。

.. figure:: /images/project-hosting/ssh-public-keys.png
   :scale: 100

   图3-11：SSH多公钥管理

如图3-11，在创建gotgithub账号一开始，就添加了名为“My Mac OS X”的公钥，显然这是为苹果电脑准备的。图中正在添加的名为“Key on Windows”是为Windows环境下使用SSH协议访问GitHub准备的公钥。

当添加了新的公钥后，无论是从哪台电脑（苹果或PC）用SSH协议访问版本库时都拥有相同授权，即都是以gotgithub账号身份来访问。

项目级公钥管理
------------------

多增加一个用户级别的公钥，就意味着可以从另外一台电脑访问该用户所有版本库。但有时只希望从某台电脑上向某一个版本库“写入”，其他版本库则不可写，这可以通过设置版本库级别的公钥认证实现。

以项目管理者（创建者）身份登录GitHub，例如以gotgithub用户身份访问 ``gotgithub/helloworld`` 版本库，进入到项目的管理页面，选择菜单中的“Deploy Keys”，即可设置项目级别公钥。如图3-12所示。

.. figure:: /images/project-hosting/deploy-keys.png
   :scale: 100

   图3-12：项目级公钥管理


