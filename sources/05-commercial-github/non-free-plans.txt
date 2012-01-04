.. _github-plans:

GitHub收费方案
===============

访问网址 https://github.com/plans 可以看到GitHub提供的不同的服务方案列表。

.. figure:: /images/commercial-products/available-plans.png
   :scale: 100

   图5-1：GitHub服务方案列表

图5-1中显示了GitHub的三类（8种）服务方案：

* 第一类是免费方案。免费用户账号可以创建任意数量的开放式项目（版本库），并且\
  可以为开放式项目设置任意数量的协同者。
* 第二类是需要付费的个人账号方案。付费的个人账号允许托管私有版本库，即可以\
  创建只有自己及指定的私有协同者才能够访问的版本库，而其他人不能访问。根据允许\
  创建的私有版本库数量及私有版本库协同者数量，提供了三种收费标准（7美元/月、\
  12美元/月 和 22美元/月）。
* 第三类是需要付费的组织账号方案。使用付费的组织账号，可以突破私有项目的\
  协同者数量限制，并使用更易管理的团队（Team）对项目进行授权。关于如何通过\
  团队配置授权参见“4.3. 组织和团队”。组织账号的付费标准较个人账号更高\
  （有25美元/月、50美元/月、100美元/月 和 200美元/月），但同时也可以创建更多\
  的私有版本库和拥有更大的托管空间。

用户可以随时升级或降级自己在GitHub上的服务方案。点击菜单中的“Account Settings”\
可以看到当前所选方案，如图5-2所示。

.. figure:: /images/commercial-products/plan-status.png
   :scale: 100

   图5-2：用户所选方案及状态

点击图5-2中的“Change plan”按钮，进入到更换GitHub服务方案页面，如图5-3所示。

.. figure:: /images/commercial-products/change-plan.png
   :scale: 100

   图5-3：更换方案

选择适合的收费方案并付款后，即可完成服务方案的升级。

当 gotgithub 用户升级为付费账号后，创建新版本库时就可以通过新的选项创建\
私有版本库了。即在创建版本库时，如果不选择默认的“Anyone”，而是选择\
“Only the people I specify”可以创建私有版本库，如图5-4所示。

.. figure:: /images/commercial-products/new-private-repository.png
   :scale: 100

   图5-4：创建私有版本库

通过版本库的管理界面，可以随时将版本库的状态在公开和私有之间切换，如图5-5所示。

.. figure:: /images/commercial-products/private-repos-settings.png
   :scale: 100

   图5-5：私有版本库管理界面

付费账号的公开版本库没有协同者数量上的限制，但是私有版本库却存在协同者数量上\
的限制。如图5-6所示，当私有版本库的协同者数量超出所选GitHub付费方案的限额后，\
会显示“OVERLIMIT”的警告，不过超出限额的协同者依然可以操作私有版本库。

.. figure:: /images/commercial-products/add-private-collaborators.png
   :scale: 100

   图5-6：添加私有协同者

组织是一类特殊的不能登录的用户账号。如果要对组织账号进行配置，需要先以组织\
所有者的用户账号登录，再通过切换上下文的方式访问组织账号。图5-7就是以\
gotgithub用户账号登录后，切换到 GotGitOrg 组织账号的管理界面。

.. figure:: /images/commercial-products/org-plan-status.png
   :scale: 100

   图5-7：团队账号的所选方案及状态

在图5-7所示的组织账号管理界面中显示了组织账号当前的GitHub方案，点击其中的\
“Change plan”按钮，显示如图5-8所示界面，可对组织账号的GitHub方案进行升级或降级。

.. figure:: /images/commercial-products/org-change-plan.png
   :scale: 100

   图5-8：团队账号更换方案

为组织账号选择一个付费方案后，就可以在组织的账号下创建私有版本库，并以团队\
方式管理该私有版本库的授权。图5-9就是一个私有版本库\ ``GotGitOrg/NonPublicRepo``\
的设置界面。

.. figure:: /images/commercial-products/org-private-repo-settings.png
   :scale: 100

   图5-9：团队的私有版本库设置
