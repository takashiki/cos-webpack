Qcloud Cos Webpack Plugin
====================

> 上传 Webpack Assets 至 腾讯云 COS

## 前提

需要 Node 版本在 v4.0 以上，COS V4 以上（APPID 为 125 开头）

## 安装

```sh
npm i -D cos-webpack
```

## 使用方法

支持的配置项:

+ `secretId` COS SecretId
+ `secretKey` COS SecretKey
+ `bucket` COS 存储对象名称，格式为对象名称加应用 ID，如：`bucket-1250000000`
+ `region` COS 存储地域，参见[官方文档](https://cloud.tencent.com/document/product/436/6224)
+ `path` 存储路径， 默认为 `[hash]`，也可以指定 hash 长度，如: `[hash:8]`
+ `exclude` 可选，排除特定文件，正则表达式，如: `/index\.html$/`
+ `include` 可选，指定要上传的文件，正则表达式，如: `/app\.js$/`
+ `batch` 可选，批量上传文件并发数，默认 20

***注: Webpack 的 `output.publicPath` 要指向 COS（或自定义的）域名地址***

```js
// 引入
const CosPlugin = require('cos-webpack');

// 配置 Plugin
const cosPlugin = new CosPlugin({
  secretId: 'my-secret-id',
  secretKey: 'my-secret-key',
  bucket: 'my-125000000',
  region: 'ap-chengdu',
  path: '[hash]/'
});

// Webpack 的配置
module.exports = {
 output: {
    // 此处为 COS 访问域名(bucket-1250000000.file.myqcloud.com) 加上 path([hash]/)
    publicPath: "http://bucket-1250000000.file.myqcloud.com/[hash]/"
    // ...
 },
 plugins: [
   cosPlugin
   // ...
 ]
 // ...
}
```

## 声明

本项目大部分代码来自：[https://github.com/lyfeyaj/qn-webpack](https://github.com/lyfeyaj/qn-webpack)
