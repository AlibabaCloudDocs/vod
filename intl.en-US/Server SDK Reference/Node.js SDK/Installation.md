# Installation

This topic describes the prerequisites for installing ApsaraVideo VOD SDK for Node.js. It also describes how to install and update ApsaraVideo VOD SDK for Node.js.

## Prerequisites

One of the following Node.js packages is installed. For more information, visit [Node.js](https://nodejs.org/zh-cn/download/).

-   Node.js 4.x
-   Node.js 6.x

You can run the `node-v` command to check the Node.js version.

## Install the SDK

We recommend that you use `npm` to install dependent modules for Node.js. For more information, visit [nmp](https://www.npmjs.com/get-npm?spm=a2c4g.11186623.2.14.50883aadN0np3R). All Alibaba Cloud SDKs for Node.js are stored in the `@alicloud` directory.

-   Assume that ApsaraVideo VOD SDK for Node.js is downloaded to the /path/to/aliyun-openapi-Node.js-sdk directory. If you develop an application based on the SDK core library, run the following command to install the `@alicloud/pop-core` module. Example:

    ```
    npm install @alicloud/pop-core --save
    ```

-   The `--save` option in this command writes the module to the package.json file of the application as a dependent module.

## Update the SDK

If new features are unavailable in the current SDK, update the SDK to the latest version. Example:

```
npm install @alicloud/pop-core --save
```

