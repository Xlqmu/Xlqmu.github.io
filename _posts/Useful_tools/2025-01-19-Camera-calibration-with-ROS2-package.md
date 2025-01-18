---
layout:     post
title:      "相机标定"
subtitle:   "Camera calibration with ros2 package"
date:       2025-01-19 01:40:00
author:     "Xlqmu"
tags:
    - TOOLS
---

上次更新：@2025/01/19 06:11

## 一.前提

1. 系统版本：ubuntu 22.04 LTS
2. ros2 版本：humble
3. 相机类型：galaxy
4. 标定类型：单目相机标定
5. 标定板：已知尺寸的大棋盘格。本教程使用 8x11 棋盘，方格大小为 15 毫米。校准使用棋盘的内部顶点，因此“8x11”棋盘使用内部顶点参数“7x10”

## 二.依赖安装

``` shell
sudo apt install ros-humble-camera-calibration-parsers

sudo apt install ros-humble-camera-info-manager

sudo apt install ros-humble-launch-testing-ament-cmake
```
在主目录git clone
``` shell
git clone -b <ros2-distro> git@github.com:ros-perception/image_pipeline.git
```
## 三.驱动相机节点

``` shell
https://github.com/Aurora-UJS/rm_vision_ros2_galaxy_camera
cd rm_vision_ros2_galaxy_camera
colcon build --symlink-install
ros2 launch galaxy galaxy_camera.launch.py
```

查看是否启动相机节点,确保有image_raw的topic被发布
``` shell
ros2 topic list
ros2 topic hz /camera/image_raw
```
## 四.驱动相机标定节点

``` shell
ros2 run camera_calibration cameracalibrator --size 7x10 --square 0.015 image:=/image_raw camera:=/camera
```
**一堆参数**
``` shell
Camera Name:

-c, --camera_name
        name of the camera to appear in the calibration file


Chessboard Options:

You must specify one or more chessboards as pairs of --size and--square options.

  -p PATTERN, --pattern=PATTERN
                    calibration pattern to detect - 'chessboard','circles', 'acircles','charuco'
  -s SIZE, --size=SIZE
                    chessboard size as NxM, counting interior corners (e.g. a standard chessboard is 7x7)
  -q SQUARE, --square=SQUARE
                    chessboard square size in meters

# size与square两个参数是必须的

ROS Communication Options:

 --approximate=APPROXIMATE
                    allow specified slop (in seconds) when pairing images from unsynchronized stereo cameras
# 这个参数似乎是为多相机联合标定的参数
 --no-service-check
                    disable check for set_camera_info services at startup
# 后面这些参数不太需要
Calibration Optimizer Options:

 --fix-principal-point
                    fix the principal point at the image center
 --fix-aspect-ratio
                    enforce focal lengths (fx, fy) are equal
 --zero-tangent-dist
                    set tangential distortion coefficients (p1, p2) to
                    zero
 -k NUM_COEFFS, --k-coefficients=NUM_COEFFS
                    number of radial distortion coefficients to use (up to
                    6, default 2)
 --disable_calib_cb_fast_check
                    uses the CALIB_CB_FAST_CHECK flag for findChessboardCorners

    This will open a calibration window which highlight the checkerboard.
```
不断地移动标定板,是的GUI界面的几个条子都绿了,同时第一个按钮亮了的话就可以结束标定了,然后按save即可保存数据

## 参考博客

[Nav2 Camera Calibration](https://docs.nav2.org/tutorials/docs/camera_calibration.html)