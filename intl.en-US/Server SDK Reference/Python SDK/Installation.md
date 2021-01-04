# Installation

This topic describes the prerequisites, request commands, and instructions for installing the Python SDK, so that you can access the ApsaraVideo VOD service without complicated programming.

## Prerequisites

-   Python 2.7 or later is installed. You can go to the [Python official website](https://www.python.org/?spm=a2c4g.11186623.2.15.285b7d4eSeGrKF) to obtain the required version.
-   Pip is installed. For more information about how to install pip, see the [pip official website](https://pip.pypa.io/en/stable/installing/?spm=a2c4g.11186623.2.16.285b7d4ejMAbI5).

## Install the SDK

Example:

```
pip install aliyun-python-sdk-core
pip install aliyun-python-sdk-vod
```

**Note:**

-   If you are using Python 3.x, replace `pip install aliyun-python-sdk-core` with `pip install aliyun-python-sdk-core-v3`. If you have installed different versions, you can run the pip3 command.
-   If the system prompts for insufficient permissions during installation, add `sudo` before the command.

## Update the SDK

If new operations or new features of existing operations are unavailable in the current SDK, update the SDK to the latest version. Example:

```
pip install --upgrade aliyun-python-sdk-vod
```

## Uninstall the SDK

Use pip to uninstall the SDK. Example:

```
pip uninstall aliyun-python-sdk-core
pip uninstall aliyun-python-sdk-vod
```

