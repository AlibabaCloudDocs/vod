# 创建RAM用户并授权

使用RAM用户可以帮助您有效避免AccessKey或者密码泄露导致的安全问题。本文为您介绍如何创建一个RAM用户，并设置相应的权限。

如果您之前没有使用过阿里云控制台，需要先开通服务。

1.  登录[RAM控制台](https://ram.console.aliyun.com/overview)。

2.  单击左侧导航栏**用户**，进入用户管理页面，单击页面中的**创建用户**。

    ![用户管理](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3355793061/p177869.png)

3.  勾选**编程访问**，单击**确定**。

    ![创建用户](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0112204061/p177870.png)

    单击**确定**后会弹出手机验证窗口，完成验证码验证后，自动生成该RAM用户的AccessKey。

    ![生成AK](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1112204061/p177876.png)

4.  单击用户信息右侧的**复制**，保存用户登录名称、登录密码、AK对（AccessKey ID、AccessKey Secret）等用户信息。

    **说明：** 请保存用户信息并妥善保管，用于后续的访问。

5.  返回用户管理界面，这里显示一个名为vod的账号已创建。

    创建完成之后，该RAM用户还是没有任何权限。

6.  单击用户信息右侧的**添加权限**。

    ![添加权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1112204061/p177877.png)

7.  选择授权范围，在选择权限下输入框输入`vod`，选择筛选出的权限策略，单击**确定**。

    ![添加权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1112204061/p177879.png)

    授权策略的定义，请参见[系统授权策略](/intl.zh-CN/开发指南/账号和授权/概述.md)。

8.  授权完成之后如果该账号需要控制台登录等权限，也可以单击用户名称，在认证管理页面来完成操作。

    ![修改权限](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6758634061/p177889.png)


