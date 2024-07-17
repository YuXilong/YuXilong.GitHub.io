---
layout: post

title: iOS中Flutter应用逆向方法

date: 2024-07-17 16:32:21 +0800

tags: [iOS,Flutter, 逆向]

categories: 逆向记录
---

### 安装`reflutter`

> 参考地址：[reFlutter](https://github.com/Impact-I/reFlutter)

```shell
pip3 install reflutter
```

### 使用

```shell
# 重打包 完成后重签名后安装到iOS设备上即可
reflutter xxx.ipa
```

### 使用`Charles`抓包

Charles监听端口设置为`8083`即可

### 查看dump出的dart文件

重签名安装后将iOS设备连接到Mac上，可在macOS的控制台看到iOS设备的实时日志。

增加过滤条件`Current working dir:`即可。

例如：

```shell
/private/var/mobile/Containers/Data/Application/<UUID>/dump.dart
```





