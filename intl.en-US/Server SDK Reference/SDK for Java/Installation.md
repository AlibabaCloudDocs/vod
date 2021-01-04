# Installation

This topic describes how to install ApsaraVideo VOD SDK for Java and provides sample code for the required Maven repository and JAR file dependencies.

## Prerequisites

JDK 6 or later is installed.

## Install the SDK

Add the Maven repository and JAR file dependencies.

1.  Add the Maven repository.

    ```
        <repositories>
          <repository>
            <id>sonatype-nexus-staging</id>
            <name>Sonatype Nexus Staging</name>
            <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
            <releases>
                <enabled>true</enabled>
            </releases>
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
          </repository>
        </repositories>
    ```

2.  Add JAR file dependencies.

    ```
      <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.1</version>
      </dependency>
      <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-vod</artifactId>
        <version>2.15.11</version>
      </dependency>
      <dependency>
        <groupId>com.google.code.gson</groupId>
        <artifactId>gson</artifactId>
        <version>2.8.2</version>
      </dependency>
    ```

    **Note:**

    -   The version of the `aliyun-java-sdk-core` SDK is 4.4.5 or later.
    -   For more information about the latest version of the `aliyun-java-sdk-vod` SDK, see the `Version` column of the first table in [Release notes of server operation SDKs](/intl.en-US/SDK Downloads/Server SDK release notes.md).

