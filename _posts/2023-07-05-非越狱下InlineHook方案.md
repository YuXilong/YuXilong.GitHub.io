---
layout: post
title: 非越狱下InlineHook方案
date: 2023-07-05 18:40:20 +0800
tags: [iOS逆向]
categories: 逆向技术
---

使用`MachOStaticPatcher`静态修改`Mach-O`文件。

### 1、编译 & Patch

#### 1、下载`MachOStaticPatcher`

```shell
git clone https://github.com/jmpews/Dobby/tree/793b9c3bd11d7666eb8ca186e2ddea7072f92f73/Plugins/MachOStaticPatcher
```

#### 2、编译

```shell
# 编译MachOStaticPatcher
cd HookZz/Plugins/MachOStaticPatcher
mkdir build
cmake .. -DHOOKZZ_SOURCE_DIR=/path/HookZz
make -j4
```

#### 3、修改`Mach-O`文件

```shell
# 移除签名
codesign --remove-signature ./xxxx.app/

# 静态Patch 支持一次patch多个C函数地址
./MachOStaticPatcher ./xxxx.app/xxxx C函数地址1 C函数地址2

# 重命名
rm ./xxxx.app/xxxx
mv ./xxxx.app/xxxx_modified ./xxxx.app/xxxx

# 重签名
codesign --force --sign xxx ./xxxx.app/
```



### 2、MonkeyDev适配

> 修改`pack.sh`脚本内容

#### 1、修改签名部分

```shell
# "$MONKEYPARSER" install -c load -p "@executable_path/Frameworks/lib""${TARGET_NAME}""Dylib.dylib" -t "${BUILD_APP_PATH}/${APP_BINARY}"

# 修改为 optool
OPTOOL="/usr/local/bin/optool"
echo "xxxx" | sudo -S "$OPTOOL" install -c load -p "@executable_path/Frameworks/lib""${TARGET_NAME}""Dylib.dylib" -t "${BUILD_APP_PATH}/${APP_BINARY}"
```

#### 2、修改`checkApp`方法

```shell
# 注释以下代码
# if [[ $? -eq 16 ]]; then
#   	panic 1 "${VERIFY_RESULT}"
# else
#   	echo "${VERIFY_RESULT}"
# fi
```



### 3、Hook对应的C函数

> 把`InterfaceInternal.h`、`TrampolineStubRebase.cc`、`FunctionInlineReplaceExport.cc`添加到MonkeyDev工程内

```objective-c
#include "InterfaceInternal.h"

// 原始C函数
static int (*sub_1001471B8)(intptr_t L_ptr);
// 自己的C函数
static int replaced_sub_1001471B8(intptr_t L_ptr) {
  return sub_1001471B8(L_ptr);
}
CHConstructor{
  	// Hook对应的C函数
    ZzReplaceStatic((char *)"模块名称", (void *)0x1001471B8, (void *)&replaced_sub_1001471B8, (void **)&sub_1001471B8);
}
```

### 4、参考

[MachOStaticPatcher](https://github.com/jmpews/Dobby/tree/793b9c3bd11d7666eb8ca186e2ddea7072f92f73/Plugins/MachOStaticPatcher)
