---

layout: post

title: iOS Development Tips

date: 2022-11-02 15:28:20 +0800

tags: [iOS,Swift]

categories: iOS Development

---



#### `Swift`应用交叉编译

```shell
swift build -c release --arch arm64 --arch x86_64
```



#### 解决使用旧版本`Xcode`打包二进制库，`Swift`编译的问题

> `Build Setting`中`BUILD_LIBRARY_FOR_DISTRIBUTION`改为`YES`
