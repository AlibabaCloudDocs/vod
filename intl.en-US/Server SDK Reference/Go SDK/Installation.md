# Installation

This topic describes the prerequisites for installing ApsaraVideo VOD SDK for Go. It also describes how to install and update ApsaraVideo VOD SDK for Go.

## Prerequisites

**Go 1.7** or later is installed. For more information, visit [Go](https://golang.org/dl/?spm=a2c4g.11186623.2.16.44f4ed6eekesoC).

## Install the SDK

-   You can run the `go get` command to install the SDK. Example:

    ```
    go get -u github.com/aliyun/alibaba-cloud-sdk-go/sdk
    ```

    **Note:**

    -   When you run the preceding command to install the SDK, no prompts are displayed. If timeout occurs during installation, run the command again.
    -   If the subdirectory src/github.com/aliyun/alibaba-cloud-sdk-go/services/vod is displayed in the directory that stores the GOPATH file, the SDK is installed.
-   You can also run the `glide` command to install the SDK. Example:

    ```
    glide get github.com/aliyun/alibaba-cloud-sdk-go
    ```


## Update the SDK

If new features or new API operations are unavailable in the current SDK, update the SDK to the latest version. For more information, see [Install the SDK](#section_p3e_rug_ila).

## Example:

For more information about the sample code and related reference, see [Initialization](/intl.en-US/Server SDK Reference/Go SDK/Initialization.md).

