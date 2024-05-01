---
layout:     post
title:      "在 Windows 中安装 Ubuntu 虚拟机"
subtitle:   "Install Ubuntu Virtual Machine on Windows"
date:       2024-05-01 22:21:00
author:     "陈立憨"
tags:
    - Ubuntu
---

> 本文链接中包含 VMware Pro 安装包附件。建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[在 Windows 中安装 Ubuntu 虚拟机](https://flowus.cn/lihanchen/80e13e07-81d7-4e30-8a3c-dd88b98e9321)

# 一. 安装 VMware Pro

使用 VMware 安装（注意要安装 **Pro** 版！网上大把秘钥）

[](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/VMware-workstation-full-17.0.0-20800274.exe)


```
JU090-6039P-08409-8J0QH-2YR7F
```


# 二. 下载Ubuntu 22.04.2 LTS

[cn.ubuntu.com](https://cn.ubuntu.com/download/desktop)


# 三. 配置虚拟机

1. 选择你的刚才下载的 .iso 文件

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image.png)

2. 设置用户名

    **请不要使用任何中文 / Emoji，请养成习惯**

    密码不建议复杂，可设为一个空格，每次执行 `sudo` 命令时都将输入密码

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image1.png)

3. 设置存储空间

    **存储空间建议：**

    1. 只是玩一玩linux系统，则分配30GB

    2. 软件开发，50GB

    3. 学习ROS，80GB以上

    4. 深度学习、机器学习，100GB以上

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image2.png)

# 四. 在虚拟机中安装 Ubuntu22.04

1. 设置语言

    **请设置为 English！！！**

    否则将导致文件夹中出现中文名，这在未来开发中可能导致未知的错误

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image3.png)

2. Update and Software

    默认即可

3. Installation Type

    默认即可：Erase Disk and Install Ubuntu

4. 选择时区

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image4.png)

5. 设置用户名与密码

    请不要使用任何中文或 Emoji，请养成习惯 

    密码不建议复杂，可设为一个空格，每次执行 `sudo` 命令时都将输入密码

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image5.png)

6. 等待约20min后，安装成功

    ![image.png](/img/in-post/About_Ubuntu/Install-Ubuntu-Virtual-Machine-on-Windows/image6.png)

# 设置共享文件夹（选修）

实现与Windows系统共用文件

[VMware Tools灰色解决办法__Hello Spring的博客-CSDN博客](https://blog.csdn.net/wct3344142/article/details/105581607)


[VMware共享文件夹——Ubuntu20.04_邶风，的博客-CSDN博客](https://blog.csdn.net/weixin_44126785/article/details/120585921?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522168001265516782425144364%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=168001265516782425144364&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-120585921-null-null.142)


注意：每次重启虚拟机后，都需要将共享文件夹功能关闭再开启

个人觉得[微信传输助手网页版](https://filehelper.weixin.qq.com/)更好用😂