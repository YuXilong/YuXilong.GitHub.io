---
layout: post
title: 非越狱下InlineHook方案
date: 2023-07-05 18:40:20 +0800
tags: [iOS逆向]
categories: 逆向技术
---



### 静态Patch Mach-O文件

#### 1、下载`MachOStaticPatcher`

```shell
git clone https://github.com/jmpews/Dobby/tree/793b9c3bd11d7666eb8ca186e2ddea7072f92f73/Plugins/MachOStaticPatcher
```

#### 2、编译

```shell
cd HookZz/Plugins/MachOStaticPatcher

mkdir build

cmake .. -DHOOKZZ_SOURCE_DIR=/path/HookZz

make -j4
```

