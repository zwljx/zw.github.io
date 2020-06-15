---
title: linux_one
date: 2020-06-15 11:59:46
tags: [Linux]
categories: [Linux]
meta:
  header: [title, author, category,date,wordcount]
---
## 后台运行

<!-- more -->

`nohup [command] &`
该命令启动的后台进程可能会被杀掉，解决办法是写在一个脚本里面，示例如下：
```
#!/bin/bash

BUILD_ID=dontKillMe

nohup [command] &
```

执行该脚本