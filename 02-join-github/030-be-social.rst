社交网络
===============

社交网络的一大特征就是用户间的相互关注，从而形成朋友圈或媒体圈，实现便捷的信息分享和传播。GitHub支持项目级别及用户级别的关注。

关注一个项目很简单，只需点击项目名称右侧的“Watch”按钮。

.. figure:: /images/join-github/watch-project.png
   :scale: 100

   图2-26：项目的关注按钮

添加对项目的关注后，在“Dashboard”（仪表板）页面的左侧会显示关注项目的最新动态，右侧会列表显示关注的项目。如图2-27所示。

.. figure:: /images/join-github/dashboard-with-watched-prj.png
   :scale: 100

   图2-27：关注项目在仪表板页的显示

GitHub还可以关注用户。访问 https://github.com/mojombo 可以看到mojombo（GitHub创始者之一）的用户页，关注他只需点击图2-28中的“Follow”按钮。从mojombo的用户页还可以看到majombo关注的开发者，可以以此扩大GitHub朋友圈。

.. figure:: /images/join-github/github-mojombo.png
   :scale: 100

   图2-28：mojombo的用户页

GitHub仪表板页面，有一个“RSS Feed”链接，如图2-29所示。点击该链接可以使用RSS客户端（如Google Reader）订阅，实现无需登录GitHub即可访问所关注的项目和人的动态。

.. figure:: /images/join-github/rss-feed.png
   :scale: 100

   图2-29：RSS Feed

RSS中可能包括隐私信息，如私有版本库的更新信息，那么RSS订阅是如何保护个人隐私呢？难道需要口令认证么？查看一下RSS订阅的URL，你会看到类似如下格式的URL地址：

::

  https://github.com/gotgithub.private.atom?token=7fa3febca074046415a6308a3f673a4a

原来RSS订阅用到了API Token，既保护了隐私，又不怕密码泄露。关于API Token参见本章第一节的相关介绍。
