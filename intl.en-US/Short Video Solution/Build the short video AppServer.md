# Build the short video AppServer

The short video AppServer is used to exchange data between the short video application and ApsaraVideo VOD, process business logic, and manage operations data. This topic describes how to build the short video AppServer.

-   An Alibaba Cloud account is created. Real-name verification is complete for the Alibaba Cloud account. For more information, see [t12832.md\#]().
-   Elastic Compute Service \(ECS\) is activated. An ECS instance is configured. For more information, see [Activate and configure ECS](/intl.en-US/Short Video Solution/Activate and configure ECS.md).
-   Java Development Kit \(JDK\) 8 is installed on the ECS instance. For more information, see [t1989721.md\#section\_hzq\_5v9\_ffy]().
-   MySQL 5.7 is installed on the ECS instance. For more information, see [Install and configure a MySQL database](). When you publish your short video service to the production environment, we recommend that you use ApsaraDB RDS. For more information, visit [the buy page of ApsaraDB RDS](https://rds-buy.aliyun.com/nextBuy/rds#/create/rds/mysql).
-   ApsaraVideo VOD is activated. For more information, see [Activate and configure ApsaraVideo VOD](/intl.en-US/Short Video Solution/Activate and configure ApsaraVideo VOD.md).

## Procedure

1.  Download the ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226.zip package, which contains the source code of the short video AppServer and console. For more information, see the "Download the short video demo" section of the [SDK download](/intl.en-US/SDK Downloads/SDK download.md) topic.

2.  Run the following command to upload the source code package to the ECS instance. In this example, the source code package ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226.zip is in the current directory. The username that is used to log on to the ECS instance is root. The IP address is 10.10.10.101. The upload path is /root/workspace/.

    scp ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226.zip root@10.10.10.101:/root/workspace/

3.  Log on to the ECS instance. Then, decompress the source code package.

    cd /root/workapace

    unzip ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226.zip

    **Note:** If the unzip tool is not installed, run the apt install unzip command to install the unzip tool.

4.  Initialize and configure a database.

    **Note:** You can create a self-managed database for your music files.

    -   Make sure that the query results that are returned by the database use the data structure defined by ApsaraVideo VOD. Otherwise, ApsaraVideo VOD cannot obtain music data from the database.
    -   If your database uses a custom data structure, modify the downloaded demo code so that ApsaraVideo VOD supports this data structure.
    1.  Create a database named voddemo.

        cd /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/sql

        mysqladmin -u root -p create voddemo

    2.  Create a table and an administrator account.

        mysql -u root -p voddemo < ./appserver\_create\_table.sql

        **Note:** In addition to a table creation statement, the appserver\_create\_table.sql script contains an INSERT INTO statement that is used to create a console administrator account. The username of the account is admin, and the password is 123456. After you build the short video console, you can use the account to log on to the short video console as an administrator.

    3.  Modify the case check rule for the database.

        1.  Edit the profile of the database.

            vim /etc/mysql/mysql.conf.d/mysqld.cnf

        2.  Press the **I** key and add `lower_case_table_names=1` to the end of the profile.
        3.  Press the **Esc** key and enter :wq!to save the profile and exit.
        4.  Restart the database so that the configuration can take effect.

            service mysql restart

    4.  Configure the IP address of the database.

        1.  Edit the profile in the source code directory.

            vim /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/src/main/resources/application.properties

        2.  Press the **I** key. Then, edit the profile. The following code shows you how to edit the profile:

            ```
            spring.datasource.url = jdbc:mysql://IP address of the database (127.0.0.1):3306/Name of the database (voddemo)?useSSL=false&useUnicode=true&characterEncoding=UTF-8
            spring.datasource.username = The username that is used to log on to the database, for example, root.
            spring.datasource.password = The password that is used to log on to the database.
            ```

            **Note:**

            -   If both the database and the AppServer are run on the ECS instance, set the IP address of the database to 127.0.0.1. Otherwise, set the IP address of the database to that of the server where the database is run.
            -   A database named voddemo is being initialized.
        3.  Press the **Esc** key and enter :wq!to save the profile and exit.
5.  Configure a RAM role. For more information about RAM roles, see [Overview](/intl.en-US/Developer Guide/Access authorization/Overview.md).

    1.  Log on to the [Resource Access Management \(RAM\) console](https://ram.console.aliyun.com/overview).

        **Note:** Log on to the RAM console by using an Alibaba Cloud account.

    2.  In the left-side navigation pane, click **RAM Roles**. On the page that appears, click **Create RAM Role**.

    3.  In the Create RAM Role panel, set the **Trusted entity type** parameter to **Alibaba Cloud Account** and click **Next**.

    4.  Enter a role name in the **RAM Role Name** field, set the Select Trusted Alibaba Cloud Account parameter to **Current Alibaba Cloud Account**, and then click **OK**. In this example, set the name of the RAM role to alivc-demo-role.

    5.  Click **Add Permissions to RAM Role**. The Add Permissions panel appears.

    6.  Click the **AliyunVODFullAccess** system policy and then **OK**, as shown in the following figure.

        ![server_config_01](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9443947061/p185551.png)

    7.  On the **RAM Roles** page, click the name of the created RAM role alivc-demo-role to view the Alibaba Cloud Resource Name \(ARN\) of the RAM role. We recommend that you store the name and ARN of the RAM role to a file on your PC for subsequent use.

    8.  On the **RAM Roles** page, click the name of the created RAM role alivc-demo-role. On the details page of the RAM role, click the Trust Policy Management tab. On the **Trust Policy Management** tab, click **Edit Trust Policy**. In the Edit Trust Policy panel, modify the trust policy based on the following code:

        ```
        {
            "Statement": [
                {
                    "Action": "sts:AssumeRole", 
                    "Effect": "Allow", 
                    "Principal": {
                        "Service": [
                            "ecs.aliyuncs.com"
                        ]
                    }
                }
            ], 
            "Version": "1"
        }
        ```

        The trust policy indicates that the RAM role is a service role, which can be assigned to the trusted Alibaba Cloud service ECS. If you do not modify the trust policy, you cannot assign the RAM role to the ECS instance.

        The ID of the ECS instance must be specified in the `["Instance ID"]` format.

    9.  Assign the RAM role to the ECS instance.

        Call the [AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md) operation that is provided by ECS in OpenAPI Explorer. For more information, see [OpenAPI Explorer](https://next.api.aliyun.com/api/Ecs/2014-05-26/AttachInstanceRamRole).

        **Note:**

        -   RegionId: the ID of the region where the ECS instance resides, such as the China \(Shanghai\) region. You can go to the ECS console to obtain the region ID of the instance.
        -   RamRoleName: the name of the RAM role. In this example, the name of the RAM role is alivc-demo-role.
        -   InstanceIds: the ID of the ECS instance. You can go to the [ECS console](https://ecs.console.aliyun.com/#/home) to view the ID of the instance. You must enter the instance ID in the format of an array, for example, \["i-bp135jrddxxf9tgo\*\*\*\*"\]. In this example, only one ECS instance is involved. You can also specify the IDs of multiple ECS instances to which you want to assign the RAM role based on your business requirements.
        Click **Submit Request**. After the call succeeds, a success response is displayed on the Debugging Result tab on the right part of the page.

    10. Run the following command on the ECS instance to check whether the RAM role is assigned to the ECS instance:

        curl http://100.100.100.200/latest/meta-data/ram/security-credentials/alivc-demo-role

        If the output contains the following Security Token Service \(STS\) authorization information, the RAM role is assigned to the ECS instance:

        ```
        {
        "AccessKeyId" : "STS.XXXXXXXXXXXX",
        "AccessKeySecret" : "XXXXXXXXXXXXXXXX",
        "Expiration" : "2020-11-20T14:33:31Z",
        "SecurityToken" : "XXXXXXXXXXXXXXXXXXXXXX",
        "LastUpdated" : "2020-11-20T08:33:31Z",
        "Code" : "Success"
        }
        ```

        **Note:** You can assign only one RAM role to an ECS instance. To change the RAM role, call the [DetachInstanceRamRole](/intl.en-US/API Reference/Instances/DetachInstanceRamRole.md) operation in [OpenAPI Explorer](https://next.api.aliyun.com/api/Ecs/2014-05-26/AttachInstanceRamRole?tab=DEBUG) to remove the RAM role from the ECS instance. Then, call the [AttachInstanceRamRole](/intl.en-US/API Reference/Instances/AttachInstanceRamRole.md) operation to assign a new RAM role to the ECS instance.

    11. Configure the information about RAM.

        1.  Edit the profile in the source code directory.

            vim /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/src/main/resources/application.properties

        2.  Press the **I** key. Then, edit the profile. The following code shows you how to edit the profile:

            ![server_config_03](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9443947061/p185636.png)

            **Note:**

            -   REGION\_CN\_HANGZHOU: the region where your ApsaraVideo VOD service is activated. For example, cn-shanghai indicates the China \(Shanghai\) region.
            -   roleArn: the ARN of the RAM role that is obtained from the RAM console.
            -   roleSessionName: the name of the session that uses a temporary token. You can customize the session name as needed.
            -   roleName: the name of the RAM role that is obtained from the RAM console. In this example, the name of the RAM role is alivc-demo-role.
        3.  Press the **Esc** key and enter :wq!to save the profile and exit.
6.  Configure the information about ApsaraVideo VOD.

    1.  Edit the profile in the source code directory.

        vim /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/src/main/resources/application.properties

    2.  Press the **I** key. Then, edit the profile. The following code shows you how to edit the profile:

        ![server_config_04](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9443947061/p185707.png)

        |Parameter|Required|Description|
        |---------|--------|-----------|
        |TEMPLATEGROUP\_ID|Yes|The ID of the transcoding template group. You can obtain the ID from the [Transcode](https://vod.console.aliyun.com/settings/transcode/list#/settings/transcode/list) page in the ApsaraVideo VOD console.|
        |LONGVIDEO\_TRANSCODE\_TEMPLATEGROUP\_ID|No|The ID of the transcoding template group that is used to review long videos after they are released.|
        |TAB\_TEMPLATEGROUP\_ID|No|The ID of the Narrowband HD™ transcoding template group. To recommend Narrowband HD™-transcoded videos in your short video console, you must set this parameter. Otherwise, an error occurs when you recommend Narrowband HD™-transcoded videos.|
        |DOMAIN\_NAME|Yes|The address of the ECS instance. In this example, the address is http://10.10.10.101:8080/.|
        |AVATAR\_DOMAIN\_NAME|No|The address of the profile pictures, which is the address of static resources on the ECS instance. In this example, the address is http://10.10.10.101:8080/resource/.|
        |AVATAR\_URL|No|An array of profile picture names, such as 1.png,2.png. **Note:** Store the profile pictures 1.png and 2.png in the /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/src/main/webapp/resource directory. If you do not configure the profile picture feature, users cannot use profile pictures on mobile clients. Other features are not affected. |
        |VOD\_REGIONID|Yes|The ID of the region where ApsaraVideo VOD is activated. In this example, set the parameter to cn-shanghai.|
        |OPEN\_API\_URL|No|The URL that is used to connect to the DMH platform of Taihe Music Group. For more information, visit [DMH](http://cp.dmhmusic.com/). **Note:** The DMH platform of Taihe Music Group offers online music resources for short videos. The DMH platform provides tens of thousands of high-quality songs of various genres and is authorized to delegate the copyright of the songs. You can access music resources by using SDKs or API operations. The DMH platform charges you fees for online music resources based on the number of calls. For more information, you can contact DMH sales manager Han Xuan by email or phone. The email address is hanxuan@taihe.com. The mobile number is 18610319065. |
        |Q\_SOURCE|No|
        |CALLBACK\_PRIVETEKEY|Yes|The key that is used for callback authentication. You can obtain the key from the [Callback](https://vod.console.aliyun.com/settings/transcode/list#/settings/callback) page in the ApsaraVideo VOD console.|
        |CALLBACK\_NAME|Yes|The callback URL, in the format of http://Public IP address of the ECS instance:8080/vodcallback/callback. In this example, the callback URL is http://10.10.10.101:8080/vodcallback/callback.|
        |AUDIT\_SETTINGS\_FLAG|Yes|Specifies whether to review videos before the videos are released. Default value: on. Valid values:         -   **on**: Review videos before the videos are released.
        -   **off**: Review videos after the videos are released. |
        |auth\_key|No|The configurations for live streaming. If you do not set the parameters, the **no data found** message appears on the live streaming page. The current edition of the short video AppServer does not provide the source code of live streaming. To use the live streaming feature, submit a ticket to apply for the source code of the preview edition.|
        |live\_domain|No|
        |package\_name|Yes|The names of valid packages that are allowed by the interceptor. Separate multiple package names with commas \(,\). Default value: IOS,ANDROID,TEST,com.aliyun.apsara.svideo,com.aliyun.apsaravideo,com.aliyun.solution.longvideo. **Note:**

        -   com.aliyun.apsara.svideo is the name of the package that is used in this example for Android.
        -   If you use a bundle ID that has been registered, the short video client for iOS cannot connect to the AppServer. You must customize a bundle ID, such as com.<Company name\>.<Project name\>. The bundle ID is used to calculate the signature for the short video client for iOS. You must contain the bundle ID in the value of the package\_name parameter to ensure normal access.
        -   The interceptor allows only the mobile applications that have the specified valid packages to access the AppServer. When other mobile applications try to access the AppServer, the request fails with an error, for example, Request failed:forbidden \(403\). |

    3.  Press the **Esc** key and enter :wq!to save the profile and exit.

7.  Run the service.

    1.  Compile and package the files.

        cd /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226

        mvn clean package -Dmaven.test.skip=true

        **Note:**

        -   If Maven is not installed, run the apt install maven command to install it.
        -   The packaging duration depends on the bandwidth and performance of the ECS instance. In this example, the duration of the first packaging is around 30 minutes.
        After the packaging is complete, the sdk-api-0.0.1-SNAPSHOT.jar file is generated in the /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/target/ directory.

    2.  Deploy the JAR package and start the service.

        cd /root/workspace/ApsaraVideo\_QuVideo\_v1.4.0\_Server\_20191226/target

        nohup java -jar sdk-api-0.0.1-SNAPSHOT.jar &

        **Note:**

        -   When the command is run, the nohub command is triggered. Press the Enter key to run the program in the background.
        -   After the command is run, the log file nohup.out is generated in the current directory. You can run the cat nohup.out command to view the log. If the log contains `start success`, the service is started.
        -   The ECS instance that you purchase may have limited idle memory. If you want to repackage and deploy the source code of the AppServer, run the jps command to query the process ID \(PID\) of the current JAR program. Then, run the kill -9 JAR program PID command to stop the program. After that, you can repackage and deploy the source code. Otherwise, the packaging may fail due to insufficient memory.

