# Create and grant permissions to a RAM user

You can use RAM users to avoid security risks caused by AccessKey pair and password leaks. This topic describes how to create a RAM user and grant permissions to the user.

Resource Access Management \(RAM\) is activated.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/overview).

2.  In the left-side navigation pane, click **Users**. On the Users page, click **Create User**.

    ![Users](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7198039061/p177869.png)

3.  Select **Programmatic Access** and click **OK**.

    ![Create User](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7198039061/p177870.png)

    ![ ](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8046201161/p177876.png)

4.  Click **Copy** in the Actions column corresponding to the RAM user to save the user logon name, logon password, and AccessKey pair.

    **Note:** We recommend that you keep the user information confidential for future access purposes.

5.  Go back to the Users page. The RAM user you created appears in the user list.

    When the RAM user is created, it does not have any permissions.

6.  Click **Add Permissions** in the Actions column corresponding to the RAM user.

    ![Add Permissions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8046201161/p177877.png)

7.  Select the permissions to grant. In the field below Select Policy, enter `vod`. Select the policies that are filtered out and click **OK**.

    ![Add Permissions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8046201161/p177879.png)

    For the definition of system policies, see the "System policies" section in [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md).

8.  If the RAM user requires permissions such as the console logon permission, you can click the User Logon Name and enable console logon on the Authentication tab.

    ![Modify permissions](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9046201161/p177889.png)


