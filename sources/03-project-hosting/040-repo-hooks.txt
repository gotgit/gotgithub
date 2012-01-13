.. _hooks:

版本库钩子扩展
==================

通过钩子扩展，GitHub托管的版本库可以和外部应用实现整合。整合的接口完全开放，\
开发者可以访问GitHub的开源项目 `github/github-services`_ 开发新的应用整合脚本。\
目前GitHub已经支持超过50个外部应用的整合，在这里恕不一一列举，仅以\
``helloworld``\ 项目为例，介绍几个常见应用的整合。

.. _github/github-services: https://github.com/github/github-services

.. _mail-notify-hook:

邮件通知功能
--------------

配置邮件通知，可以实现新提交推送至版本库时，发送通知邮件。在版本库的管理界面，\
选择“Service Hooks”中的Email进入邮件通知配置界面，如图3-15所示。配置界面很简单，\
写上邮件地址，选择激活即可。为了便于整个团队都能收到通知邮件，可以将收件地址\
设置为一个邮件列表。如果选择“Send From Author”，邮件的发件者显示为提交者的\
邮件地址，否则发件者为\ ``noreply@github.com``\ 。

.. figure:: /images/project-hosting/hooks-email.png
   :scale: 100

   图3-15：邮件通知功能配置

邮件通知配置生效后，当有新提交推送到版本库时，会发出通知邮件，如图3-16所示。

.. figure:: /images/project-hosting/mail-in-gg.png
   :scale: 100

   图3-16：提交触发邮件通知

.. _redmine-hook:

和Redmine整合
---------------

Redmine是一个开源的项目管理平台，用于项目的需求管理和缺陷跟踪。Redmine可以和\
多种版本库（包括Git）整合，可以直接通过Web界面浏览Git提交，还实现了提交和问题\
的关联。

Redmine需要周期性地扫描版本库，以便更新内置数据库及建立提交和问题的关联。\
通常是以计划任务（crontab）的方式实现版本库的周期性扫描，这导致Redmine中\
版本库更新会存在一定的延迟。GitHub提供的Redmine整合的钩子脚本能够在GitHub\
版本库更新后，通过WebService触发Redmine主动扫描Git版本库获取更新。

GitHub提供的Redmine整合的配置界面如图3-17所示。

.. figure:: /images/project-hosting/hooks-redmine.png
   :scale: 100

   图3-17：与Redmine整合

图3-17中的地址是Redmine部署的URL地址，项目ID是Redmine中的相关项目（如果不填写\
则更新所有项目），而“Api Key”并非GitHub项目中配置的Api Key，而是Redmine中为\
版本库更新配置的全局Api Key。相应的Redmine配置界面如图3-18所示。

.. figure:: /images/project-hosting/redmine-api-key.png
   :scale: 100

   图3-18：Redmine中的API Key配置

