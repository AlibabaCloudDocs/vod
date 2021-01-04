# Installation

This topic describes the prerequisites and procedure of installing ApsaraVideo VOD SDK for C/C++.

## Prerequisites

**Note:** A Linux server is prepared. Windows servers are not supported.

-   CMake is installed. It is a third-party compiler. We recommend that you install CMake 2.6.0 or later. Example:

    ```
    yum install cmake
    ```

    For more information, visit [Download CMake](https://cmake.org/download/?spm=a2c4g.11186623.2.21.5dda52d4UiTtyc). Example:

    ```
    ./configure
    make
    make install
    ```

-   libcurl is installed. libcurl is used to troubleshoot network connection issues. We recommend that you install libcurl 7.29.0 or later. Example:

    ```
    yum install libcurl-devel
    ```

    For more information, visit [Download libcurl](https://curl.haxx.se/download.html?spm=a2c4g.11186623.2.22.5dda52d4Lxvb8R). Example:

    ```
    ./configure
    make
    make install
    ```

-   libuuid is installed. libuuid is used to generate universally unique identifiers \(UUIDs\). Example:

    ```
    yum install libuuid-devel
    ```

-   The Apache Portable Runtime \(APR\) is installed. Example:

    ```
    yum install apr-devel
    ```

    For more information, visit [Download APR](https://apr.apache.org/download.cgi?spm=a2c4g.11186623.2.23.5dda52d4ZIM0i2&file=download.cgi). Example:

    ```
    ./configure
    make
    make install
    ```

-   APR-util is installed. APR-util is used to manage memory usage and cross-platform issues. Example:

    ```
    yum install apr-util
    ```

    For more information, visit [Download APR-util](https://apr.apache.org/download.cgi?spm=a2c4g.11186623.2.24.5dda52d4bygO9h&file=download.cgi). Example:

    ```
    // You must specify the --with-apr option when you install APR-util.
    ./configure --with-apr=/your/apr/install/path
    make
    make install
    ```

-   Mini-XML is installed. Mini-XML is used to parse data that is returned in the XML format. Example:

    ```
    yum install mxml mxml-devel
    ```

    For more information, visit [Download Mini-XML](https://www.msweet.org/mxml/?spm=a2c4g.11186623.2.25.5dda52d42wQFlq). Example:

    ```
    ./configure
    make
    make install
    ```

-   JsonCpp is installed. JsonCpp is used to parse data that is returned in the JSON format. Example:

    ```
    yum install jsoncpp-devel
    ```

    For more information, visit [Download JsonCpp](https://github.com/open-source-parsers/jsoncpp?spm=a2c4g.11186623.2.26.5dda52d4zyUacn). Example:

    ```
    ./configure
    make
    make install
    ```

-   Before you use upload SDKs for C/C++, you must download and install Object Storage Service \(OSS\) SDK for C. For more information, see [Installation](https://help.aliyun.com/document_detail/32132.html?spm=a2c4g.11186623.2.27.5dda52d4bv7REl).

    **Note:** If some dependent libraries of OSS are installed, you do not need to install them again.


## Install the SDK

1.  Download the SDK

    For more information, see [Release notes of the upload SDK for C or C++](/intl.en-US/SDK Downloads/shortvideo-sdk-history/Upload SDK for C_C++.md).

    **Note:** Server SDKs for C/C++ and upload SDKs for C/C++ are of the same version.

2.  Install the SDK
    -   Decompress the downloaded SDK package.
    -   Go to the SDK installation directory. Then, compile and install the SDK. Example:

        ```
        cmake .
        make
        make install
        ```


