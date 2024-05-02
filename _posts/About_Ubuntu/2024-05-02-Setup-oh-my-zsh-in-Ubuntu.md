---
layout:     post
title:      "Ubuntu 中安装 oh-my-zsh"
subtitle:   "Setup oh-my-zsh in Ubuntu"
date:       2024-05-02 15:10:00
author:     "陈立憨"
tags:
    - Ubuntu
    - 常用软件安装
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[Setup oh-my-zsh](https://flowus.cn/lihanchen/share/250ffcde-d88f-4c99-a56d-bf49ac86e602?code=4PP1RS)

上次更新：@2024/02/16 17:07

[Oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh) 是一个为 zsh 提供的框架，它提供了丰富的插件、主题和配置选项，让你的终端更加个性化。

## 一. 配置 Zsh

### 1.1 安装 Zsh

```Shell
sudo apt install zsh
```

### 1.2 设置 Zsh 作为默认 Shell

```Shell
chsh -s $(which zsh)
```

> 修改后需要**注销或重启**系统才能生效。

在终端中输入 `$SHELL --version` 后，检查输出应该为 `zsh x.x.x` 

## 二. 配置 oh-my-zsh

### 2.1 安装 oh-my-zsh

```Shell
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
    
### 2.2 配置插件

此处介绍安装最常用的 `zsh-autosuggestions` 和 `zsh-syntax-highlighting`，实现 zsh 命令的自动补全和高亮显示效果

#### 2.2.1 安装插件

```Shell
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

```Shell
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

#### 2.2.2 配置插件

```Shell
sudo vim ~/.zshrc
```

将第 73 行的 `plugins=(git)` 替换为：

```Shell
plugins=( 
    git
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

vim 快捷键：`i` 键插入；更改完成后 `Esc` 退出编辑，`:wq` 保存并退出

```Shell
source ~/.zshrc
```

### 2.3 配置 ROS2 命令行补全

```Shell
sudo vim ~/.zshrc
```

```Shell
## ROS2 Humble
source /opt/ros/humble/setup.zsh

setopt no_nomatch ## In order to use command with '*'
eval "$(register-python-argcomplete3 ros2)"
eval "$(register-python-argcomplete3 colcon)"
```

```Shell
source ~/.zshrc
```