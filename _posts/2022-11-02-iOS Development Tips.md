---

layout: post

title: iOS Development Tips

date: 2022-11-18 14:18:20 +0800

tags: [iOS,Swift]

categories: iOS Development

---



### `Swift`应用交叉编译

```shell
swift build -c release --arch arm64 --arch x86_64
```



### 解决使用旧版本`Xcode`打包二进制库，`Swift`编译的问题

> `Build Setting`中`BUILD_LIBRARY_FOR_DISTRIBUTION`改为`YES`



### 使用`xcrun atos`解析crash日志

```shell
xcrun atos -o xxx.app.dSYM/Contents/Resources/DWARF/xxx -arch arm64 -l 模块基地址 模块内内存地址
```

