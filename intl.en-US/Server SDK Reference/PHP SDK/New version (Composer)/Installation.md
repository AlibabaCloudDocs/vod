# Installation

This topic describes the prerequisites for installing ApsaraVideo VOD SDK for PHP and the new features of ApsaraVideo VOD SDK for PHP. It also describes how to install and update the SDK.

## Overview

Alibaba Cloud SDK for PHP is a development kit that enables quick access to Alibaba Cloud services. The [Alibaba Cloud Client for PHP](https://github.com/aliyun/openapi-sdk-php-client/blob/master/README.md?spm=a2c4g.11186623.2.15.37214fefIN79m1&file=README.md) provides underlying support.

**Note:** Alibaba Cloud SDK for PHP in the new version is different from that in the old version in terms of installation and use. For more information, see the following sections and [Alibaba Cloud SDK for PHP](https://github.com/aliyun/openapi-sdk-php?spm=a2c4g.11186623.2.20.37214fefzEIChA).

## Prerequisites

-   Requirements
    -   PHP 5.5.0 or later is used.

        **Note:** You can run the `php -v` command to view the current PHP version. If you need to install PHP, visit the [PHP official website](https://www.php.net/downloads.php?spm=a2c4g.11186623.2.21.37214fefaLqcbQ).

    -   [Composer](https://getcomposer.org/?spm=a2c4g.11186623.2.22.37214fefX2WurK) is used and the `composer dump-autoload --optimize` command is executed.
    -   If you use an RsaKeyPair client that is supported only on the Alibaba Cloud Japan site, [OpenSSL PHP](https://www.php.net/manual/zh/book.openssl.php?spm=a2c4g.11186623.2.23.37214fef2ok1h1) is enabled.
-   Suggestions
    -   [cURL](https://www.php.net/manual/zh/book.curl.php?spm=a2c4g.11186623.2.24.37214fefwS7Ang) 7.16.2 or later is used.
    -   [OPcache](https://www.php.net/manual/zh/book.opcache.php?spm=a2c4g.11186623.2.25.37214fefPwcdms) is used.
    -   Do not use [Xdebug](http://xdebug.org/?spm=a2c4g.11186623.2.26.37214fefYsKytE) in the production environment.

## Install the SDK

Install Alibaba Cloud SDK for PHP by using one of the following methods:

-   Use Composer to install Alibaba Cloud SDK for PHP. This method is recommended.

    Composer is a dependency manager for PHP. For more information about how to install Composer, configure autoloading, and follow other best practices for defining dependencies, see [getcomposer.org](https://getcomposer.org/?spm=a2c4g.11186623.2.27.37214fefb9N8gX).

    1.  Install dependencies.
        1.  If Composer is installed on your system, run the following command in your project directory to install Alibaba Cloud SDK for PHP as a dependency. Example:

            ```
            composer require alibabacloud/sdk
            ```

            If Composer is not installed, [globally install Composer](https://getcomposer.org/doc/00-intro.md?spm=a2c4g.11186623.2.28.37214fefMTZb1y#globally). For Windows users, download and run [Composer-Setup.exe](https://getcomposer.org/Composer-Setup.exe?spm=a2c4g.11186623.2.29.37214fefOhF9j1&file=Composer-Setup.exe). Example:

            ```
            curl -sS https://getcomposer.org/installer | php
            ```

            **Note:** If HTTPS is not supported, run the `curl http://getcomposer.org/installer | php` command. For more information, see [Composer Download](https://getcomposer.org/download/?spm=a2c4g.11186623.2.30.37214fefOhF9j1).

        2.  Run a Composer command to install Alibaba Cloud SDK for PHP of the latest version as a dependency. Example:

            ```
            php -d memory_limit=-1 composer.phar require alibabacloud/sdk
            ```

            **Note:** If the installation fails due to network issues, change the address of the Composer image.

    2.  Add the autoloader to the PHP script. Example:

        ```
        <? php
        require __DIR__ . '/vendor/autoload.php';
        ```

        **Note:** To use Alibaba Cloud SDK for PHP in a script, include an autoloader in the script.

-   Download and use a ZIP file.

    If Composer is unavailable, you can download a ZIP file that contains all classes and dependencies.

    Download the [SDK](https://aliyunsdk-pages.alicdn.com/php-sdk/sdk.zip?spm=a2c4g.11186623.2.31.37214) file, decompress it in a specified directory of the project, and then include the autoloader in your script. Example:

    ```
    <? php
    require __DIR__ . '/vendor/autoload.php';
    ```


## Update the SDK

If new operations or new features of existing operations are unavailable in the current SDK version, upgrade the SDK to the latest version. Example:

```
php -d memory_limit=-1 composer.phar require alibabacloud/sdk
```

