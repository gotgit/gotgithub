.. _github-enterprise:

GitHub企业版
===========================
出于隐私或法律原因而不能将代码托管到第三方平台的企业，可能希望在企业内部架设\
专有的GitHub服务，能做到么？答案就是GitHub企业版（GitHub Enterprise）。

网址：\ https://enterprise.github.com/\ 。

GitHub企业版搭建在企业本地网络中，因此企业拥有对版本库和项目完整的控制权限。\
GitHub企业版包含了GitHub上所有的好东西：提交历史、代码浏览、比较视图、\
Pull Requests、问题追踪、维基、Gists、组织和团队管理、强大的API，和漂亮的界面，\
因此会使用GitHub就会使用GitHub企业版。此外企业版还增加了对LDAP和CAS支持功能，\
以便和企业现有的认证系统整合等等\ [#]_\ 。

GitHub企业版不像它的前身GitHub:FI\ [#]_\ 那样通过下载软件包进行安装和部署，\
而是提供基于虚拟机的解决方案。即GitHub企业版以OVF虚拟机文件格式发布，可以运行\
在多种虚拟机平台，如：VMWare、VirtualBox、Oracle VM、\
Red Hat Enterprise Virtualization和IBM POWER。\
使用OVF格式让GitHub企业版的部署更加轻松。

GitHub企业版根据用户数量收取年费，入门级的价格为20用户每年5,000美金。如果用户数\
少，建议采用付费的GitHub托管账号。购买更多用户许可，访问GitHub企业版网站，\
那儿有一个报价生成器，如图5-10所示。

.. figure:: /images/commercial-products/github-enterprise-pricing.png
   :scale: 100

   图5-10：GitHub企业版报价生成器

----

.. [#] https://github.com/blog/978-introducing-github-enterprise
.. [#] GitHub:FI是GitHub Firewall Install的缩写，含义为在企业的防火墙内部架设\
       GitHub服务，现已升级为GitHub Enterprise。
