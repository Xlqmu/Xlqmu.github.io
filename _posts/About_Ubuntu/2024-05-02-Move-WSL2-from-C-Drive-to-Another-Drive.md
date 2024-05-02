---
layout:     post
title:      "将 WSL2 从 C 盘迁移至其他盘"
subtitle:   "Move WSL2 from C Drive to Another Drive"
date:       2024-05-02 13:45:00
author:     "陈立憨"
tags:
- Ubuntu
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[将 WSL2 从 C 盘迁移至其他盘](https://flowus.cn/lihanchen/share/df854215-9f18-40b9-a361-1d0d7dd4844e?code=4PP1RS)

# Step1 关闭要迁移的虚拟机

查看虚拟机状态，并关闭要迁移的虚拟机

```Shell
wsl -l -v
```

![image.png](/img/in-post/About_Ubuntu/Move-WSL2-from-C-Drive-to-Another-Drive/image.png)

可以看到第二个虚拟机正在运行，我们将其关闭

```Shell
wsl --shutdown Ubuntu-22.04
```

# Step2 迁移WSL2

首先在对应的盘创建好新的WLS2的目录： `D:\WSL2Ubuntu22.04LTS`

以及WLS2的备份目录（用于存放临时导出后的文件）： `D:\WSL_UBUNTU_BACKUP`

1. 导出虚拟机到D盘的某个位置

    ```Shell
    wsl --export Ubuntu-22.04 D:\WSL_UBUNTU_BACKUP\WSL2Ubuntu22.04.bak
    ```

1. 注销要迁移的WSL

    ```Shell
    wsl --unregister Ubuntu-22.04
    ```

1. 导入虚拟机到指定位置，并设置WSL版本为2

    ```Shell
    wsl --import Ubuntu-22.04 D:\WSL2Ubuntu22.04LTS D:\WSL_UBUNTU_BACKUP\WSL2Ubuntu22.04.bak --version 2
    ```

---

- 参考博客

    [WSL_03 WSL2 从C盘迁移到D盘_wsl迁移到d盘_LiQiang33的博客-CSDN博客](https://blog.csdn.net/qq_44776065/article/details/128331835)