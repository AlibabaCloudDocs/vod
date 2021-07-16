# HTTP回调鉴权

点播服务支持在HTTP（含HTTPS）回调时增加特定签名头，供回调消息接收服务端进行签名认证，以防止非法或无效请求。本文为您介绍HTTP回调鉴权的参数、规则和注意事项。

## 鉴权参数

在回调HTTP头部增加的具体鉴权参数如下：

|字段|描述|
|--|--|
|X-VOD-TIMESTAMP|UNIX时间戳，整形正数，固定长度10，1970年1月1日以来的秒数，表示回调请求发起时间。|
|X-VOD-SIGNATURE|签名字符串，为32位MD5值，详细说明见下文签名算法。|

## 签名算法

X-VOD-SIGNATURE的计算依赖如下字段：

|字段|示例|描述|
|--|--|--|
|回调URL|https://www.example.com/your/callback|用户设置的回调地址。|
|X-VOD-TIMESTAMP|1519375990|UNIX时间戳，整形正数，固定长度10，1970年1月1日以来的秒数，表示回调请求发起时间。|
|PrivateKey|test123|用户预设的签名Key。|

将上述三个字段进行拼接，字段中间以竖线（\|）分割，后计算MD5值，即：

```
MD5Content = 回调URL|X-VOD-TIMESTAMP|PrivateKey
X-VOD-SIGNATURE = md5sum(MD5Content)
```

X-VOD-SIGNATURE字段计算方法示例如下：

```
X-VOD-SIGNATURE = md5sum(https://www.example.com/your/callback|1519375990|test123) = c72b60894140fa98920f1279219b****
```

## 回调消息接收服务端校验规则

-   回调消息接收端将回调所设置的回调URI、X-VOD-TIMESTAMP取值、PrivateKey字符串拼接后，进行MD5值计算，得到加密串，再将加密串与X-VOD-SIGNATURE字段进行对比，如果不一致，则请求非法。
-   回调消息接收端获取当前时间，与回调请求所带的X-VOD-TIMESTAMP字段时间相减，如果超过服务端所设定的指定时间（如5分钟，由服务端自行定义），则认为该请求无效。

    **说明：** 由于时间设置等问题，时间差值可能会有误差，服务端可自行决定是否进行该校验。


## PrivateKey切换

客户在切换PrivateKey时，为保证回调功能不受影响，消息接收服务端需要兼容新旧两个PrivateKey的平滑切换，即在一段时间内兼容新旧两个PrivateKey的鉴权，由服务方完成。

建议操作顺序如下：

1.  用户定义新的PrivateKey。
2.  用户升级回调消息接收服务端，兼容新、旧两个PrivateKey的鉴权。
3.  在点播控制台将PrivateKey更新成最新。
4.  观察一段时间后，回调消息接收服务端去掉对原来PrivateKey的兼容。
5.  切换完成。

## 其他注意事项

-   回调鉴权是否开启由用户决定（建议开启）。一旦设置了PrivateKey，则回调时会携带所有鉴权相关内容，供回调消息接收服务端进行鉴权使用，即设置PrivateKey不会影响原有功能，具体是否校验由用户决定。
-   未设置PrivateKey的用户不会受任何影响。

