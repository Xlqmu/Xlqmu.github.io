---
layout:     post
title:      "robot_upstart自启动任务"
subtitle:   "Robot upstart Starts a task"
date:       2025-01-20 11:14:00
author:     "Xlqmu"
tags:
    - TOOLS
---

上次更新：@2025/01/20 11:15

## 一. 前提
1. 在比赛的时候可能没有太多的时间让我们去一步一步地去启动,或许可能很多人选择将启动命令
写成sh脚本然后用bashrc来启动,但是这样的做法不够优雅,而且对于python文件(如launch
 file)不能很好的启动,简单来说,robot_upstart提供了一个方法来实现ros节点的启动以及进程守护
2. 好的工具会使工作很便捷

## 二. 安装软件包
``` bash
sudo apt-get install ros-humble-robot-upstart
```

## 三. 如何实现节点的自启动

设置自启动(这里以 galaxy camera 的自启动为例)
``` bash
ros2 run robot_upstart install 
--job galaxy_camera_driver 
--setup /home/dji/rm_vision/install/setup.bash 
galaxy_camera/launch/galaxy_camera.launch.py
``` 
>参数含义：


**--job** 是要保存的service的名称

**--setup** 是设置当前工作空间下的环境

然后在后面跟上相关功能包的名称(不知道的话可以用colcon list来查看当下工作空间下的功能包)
随之后面跟上启动文件的相对路径

## 四. 设置service与进程守护

``` bash
sudo systemctl daemon-reload
sudo systemctl start galaxy_camera_driver
```

## 五. 设置开机自启动(貌似这一步是多余的)

>sudo systemctl enable galaxy_camera_driver

## 六. 调试日志

如果报错or出现奇怪的状况,可以查看相应的日至排查问题

>journalctl -u galaxy_camera_driver