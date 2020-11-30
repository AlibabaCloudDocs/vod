# 安装与配置MySQL数据库

通过阅读本文，您可以了解到Linux环境下安装和配置MySQL数据库的方法。

## 操作步骤

1.  登录Linux服务器终端。

    **说明：** 本文以Ubuntu 18.04版本为例说明，其他Linux发行版本，请根据实际情况操作。

2.  更新软件源并安装wget。

    sudo apt update

    sudo apt install wget

3.  下载MySQL数据库安装包。

    wget https://dev.mysql.com/get/mysql-apt-config\_0.8.16-1\_all.deb -y

    **说明：** 如果没有安装wget，需要先执行apt install wget安装wget。

4.  使用deb包更新软件源。

    sudo dpkg -i mysql-apt-config\_0.8.16-1\_all.deb

    在弹出的对话框中选择**MySQL Server & Cluster \(Currently selected: mysql-5.7\)**，然后选择**Ok**。

    ![install_mysql_01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5363746061/p185799.png)

5.  获取软件包的所有可安装版本。

    sudo apt update

    sudo apt-cache policy mysql-server

    ```
    mysql-server:
      Installed: (none)
      Candidate: 5.7.32-1ubuntu18.04
      Version table:
      ...
    ```

    其中，**5.7.32-1ubuntu18.04**表示MySQL数据库安装版本。

6.  根据获取到的安装版本安装MySQL5.7，安装过程中需设置root用户密码并妥善保存。

    sudo apt install -f mysql-client=5.7.32-1ubuntu18.04 mysql-community-server=5.7.32-1ubuntu18.04 mysql-server=5.7.32-1ubuntu18.04

7.  配置MySQL数据库。

    1.  设置常规化安全。

        sudo mysql\_secure\_installation

        请根据提示信息设置，如下所示：

        ```
        Enter current password for root (enter for none): <Enter password>
        VALIDATE PASSWORD PLUGIN can be used to test passwords 
        and improve security. It checks the strength of password 
        and allows the users to set only those passwords which are 
        secure enough. Would you like to setup VALIDATE PASSWORD plugin? 
        
        Press y|Y for Yes, any other key for No: Y 
        
        There are three levels of password validation policy: 
        
        LOW    Length >= 8 
        MEDIUM Length >= 8, numeric, mixed case, and special characters 
        STRONG Length >= 8, numeric, mixed case, special characters and dictionary                 
        
        Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG: 1 
        Using existing password for root. 
        Estimated strength of the password: 25  
        Change the password for root ? ((Press y|Y for Yes, any other key for No) : d
        Remove anonymous users? [Y/n] Y 
        Disallow root login remotely? [Y/n] Y 
        Remove test database and access to it? [Y/n] Y 
        Reload privilege tables now? [Y/n] Y 
        ```

    2.  开启远程访问。

        1.  编辑MySQL数据库的配置文件。

            sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf

        2.  按**I**键，将bind-address的值修改为0.0.0.0。
        3.  按**Esc**键，输入:wq!保存并退出。
    3.  重启MySQL数据库服务使配置生效。

        sudo systemctl restart mysql

8.  验证MySQL数据库服务是否正常。

    1.  以root用户登录MySQL数据库。

        mysql -u root -p

    2.  在MySQL数据库交互控制台查询现有数据库。

        show databases;

        ```
        +--------------------+
        | Database           |
        +--------------------+
        | information_schema |
        | mysql              |
        | performance_schema |
        | sys                |
        +--------------------+
        5 rows in set (0.00 sec)
        ```

        如上所示，现有MySQL数据库服务正常。


