---
layout:     post
title:      "在 WSL2 下连接 Livox 雷达"
subtitle:   "Connect Livox Lidar under WSL2"
date:       2024-05-02 13:55:00
author:     "陈立憨"
tags:
    - Ubuntu
    - WSL2
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[在 WSL2 下连接 Livox 雷达](https://flowus.cn/lihanchen/share/b32e10e4-b223-452e-8291-5303df318c31?code=4PP1RS)

## 一. Windows 中 设置

### 配置 Livox 雷达

进入 Windows 控制面板 → 网络和 Internet → 网络和共享中心

```
控制面板\网络和 Internet\网络和共享中心
```

找到 Livox 雷达的以太网连接

![image.png](/img/in-post/About_Ubuntu/Connect-Livox-Lidar-under-WSL2/image.png)

设置本机 Livox 的 ip

![image.png](/img/in-post/About_Ubuntu/Connect-Livox-Lidar-under-WSL2/image1.png)

### 配置镜像模式网络

可以在 `.wslconfig` 文件中的 `[wsl2]` 下设置 `networkingMode=mirrored`，以启用镜像模式网络。 启用此功能会将 WSL 更改为全新的网络体系结构，其目的是**将 Windows 上的网络接口“镜像”到 Linux 中**，以添加新的网络功能并提高兼容性。

以下是启用此模式的当前优势：

- IPv6 支持

- 使用 localhost 地址 `127.0.0.1` 从 Linux 内部连接到 Windows 服务器

- 改进了 VPN 的网络兼容性

- 多播支持

- 直接从局域网 (LAN) 连接到 WSL

在用户目录 `%USERPROFILE%` 下面创建一个配置文件 `.wslconfig`，写入以下内容：

```C
networkingMode=bridged
vmSwitch=WSLBridge
ipv6=true
dnsTunneling=true
firewall=true
autoProxy=true
```

```Shell
[experimental]
networkingMode=mirrored
dnsTunneling=true
firewall=true
autoProxy=true
```

以管理员身份运行 Windows PowerShell ，输入

```PowerShell
Set-NetFirewallHyperVVMSetting -Name ‘{40E0AC32-46A5-438A-A0B2-2B479E8F2E90}’ -DefaultInboundAction Allow
```

重启 WSL2

```Shell
wsl --shutdown
```

## 二. 在 WSL2 中设置

### 2.1 Livox 驱动安装

这里以 mid360 为例

1. 安装 [Livox SDK2](https://github.com/Livox-SDK/Livox-SDK2)

    ```Shell
    sudo apt install cmake
    ```

    ```Shell
    git clone https://github.com/Livox-SDK/Livox-SDK2.git
    cd ./Livox-SDK2/
    mkdir build
    cd build
    cmake .. && make -j
    sudo make install
    ```

1. 安装 [Livox ROS Driver 2](https://github.com/Livox-SDK/livox_ros_driver2)

    ```Shell
    git clone https://github.com/Livox-SDK/livox_ros_driver2.git ws_livox/src/livox_ros_driver2
    ```

    ```Shell
    cd ws_livox/src/livox_ros_driver2
    source /opt/ros/humble/setup.sh
    ./build.sh humble
    ```

    为了便于启动驱动，可以设置每次启动终端时，自动 source livox_ros_driver2 的工作空间。**注意替换 `WHERE_YOU_GIT_CLONE`**

    ```Shell
    echo '## livox_ros_driver2' >> ~/.bashrc
    echo 'source source /WHERE_YOU_GIT_CLONE/ws_livox/install/setup.bash' >> ~/.bashrc
    ```

### 2.2 在 livox_ros_driver2 中配置 config

- **修改 `cmd_data_ip`, `push_msg_ip` 和 `imu_data_ip`** ，是你的 主机 ip 

    修改为 `192.168.1.50`

- **修改 `lidar_configs` 中的 `ip`**，是 livox 雷达的静态 ip

    修改为 `192.168.1.1XX` （ `XX` 为 Livox 雷达机身上 `SN 码` 的最后两位数字)

- 修改后如下：

    ```json
    {
        "lidar_summary_info" : {
        "lidar_type": 8
        },
        "MID360": {
        "lidar_net_info" : {
            "cmd_data_port": 56100,
            "push_msg_port": 56200,
            "point_data_port": 56300,
            "imu_data_port": 56400,
            "log_data_port": 56500
        },
        "host_net_info" : {
            "cmd_data_ip" : "192.168.1.50",
            "cmd_data_port": 56101,
            "push_msg_ip": "192.168.1.50",
            "push_msg_port": 56201,
            "point_data_ip": "192.168.1.50",
            "point_data_port": 56301,
            "imu_data_ip" : "192.168.1.50",
            "imu_data_port": 56401,
            "log_data_ip" : "",
            "log_data_port": 56501
        }
        },
        "lidar_configs" : [
        {
            "ip" : "192.168.1.146",
            "pcl_data_type" : 1,
            "pattern_mode" : 0,
            "extrinsic_parameter" : {
            "roll": 0.0,
            "pitch": 0.0,
            "yaw": 0.0,
            "x": 0,
            "y": 0,
            "z": 0
            }
        }
        ]
    }
    ```

- 修改完成后不要忘记再次编译！

## 三. 测试
1. 在 Windows cmd 中可以看到 livox 雷达的连接情况

    ![在 Windows cmd 中可以看到 livox 雷达的连接情况](/img/in-post/About_Ubuntu/Connect-Livox-Lidar-under-WSL2/image2.png)

2. 进入 WSL2 ，可以看到相同的 Livox 雷达连接情况

    ![进入 WSL2 ，可以看到相同的 Livox 雷达连接情况](/img/in-post/About_Ubuntu/Connect-Livox-Lidar-under-WSL2/image3.png)

3. 输入下面这串命令，就可以看到 Livox 的点云啦

    ```Shell
    ros2 launch livox_ros_driver2 rviz_MID360_launch.py
    ```

    ![运行成功，显示点云消息已发布](/img/in-post/About_Ubuntu/Connect-Livox-Lidar-under-WSL2/image4.png)

    ![Rviz2 中查看点云](/img/in-post/About_Ubuntu/Connect-Livox-Lidar-under-WSL2/image5.png)

---

- 参考文章：[WSL2 网络的最终解决方案](https://zhuanlan.zhihu.com/p/593263088)