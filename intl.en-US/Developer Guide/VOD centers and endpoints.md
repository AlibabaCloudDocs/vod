# VOD centers and endpoints

ApsaraVideo VOD provides access in a number of regions around the world. Each endpoint corresponds to a storage region. You cannot call resources across storage regions. This topic describes the API regions that correspond to service regions, API region IDs, endpoints \(domain names\), supported storage regions, and storage region IDs.

## Overview

-   The **API region ID** corresponds to the RegionId parameter in API operations or SDKs.
-   The **Storage region ID** corresponds to the region ID in the StorageLocation request parameter.
-   When you upload a media file, you can specify the storage address in the StorageLocation parameter to upload the file to the specified storage region. You can view the storage addresses on the [Storage](https://vod.console.aliyun.com/?spm=5176.12818093.0.2.6ed816d0ZyFwPz#/storage/list) page in the ApsaraVideo VOD console. For more information, see [Manage VOD resources](/intl.en-US/User Guide/Global settings/Manage VOD resources.md).
-   Each service region supports storage only in the corresponding storage region. Users in the Shanghai service region who have specified China \(Beijing\) as the storage region can continue to call API operations in Shanghai. You can view the region list in the upper left corner of the console.

## API regions and storage regions

|Service region|API region|API region ID|Endpoint \(Domain name\)|Storage region|Storage region ID|
|--------------|----------|-------------|------------------------|--------------|-----------------|
|Shanghai|China \(Shanghai\)|cn-shanghai|vod.cn-shanghai.aliyuncs.com|China \(Shanghai\)|cn-shanghai|
|Beijing|China \(Beijing\)|cn-beijing|vod.cn-beijing.aliyuncs.com|China \(Beijing\)|cn-beijing|
|Shenzhen|China \(Shenzhen\)|cn-shenzhen|vod.cn-shenzhen.aliyuncs.com|China \(Shenzhen\)|cn-shenzhen|
|Singapore|Singapore|ap-southeast-1|vod.ap-southeast-1.aliyuncs.com|Singapore|ap-southeast-1|
|Indonesia|Indonesia \(Jakarta\)|ap-southeast-5|vod.ap-southeast-5.aliyuncs.com|Indonesia \(Jakarta\)|ap-southeast-5|
|India|India \(Mumbai\)|ap-south-1|vod.ap-south-1.aliyuncs.com|India \(Mumbai\)|ap-south-1|
|Germany|Germany \(Frankfurt\)|eu-central-1|vod.eu-central-1.aliyuncs.com|Germany \(Frankfurt\)|eu-central-1|
|Japan|Japan \(Tokyo\)|ap-northeast-1|vod.ap-northeast-1.aliyuncs.com|Japan \(Tokyo\)|ap-northeast-1|

