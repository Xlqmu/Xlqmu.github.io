---
layout:     post
title:      "Ubuntu 配置 Clang 编译器"
subtitle:   "Setup Clang in Ubuntu"
date:       2024-05-02 16:47:00
author:     "陈立憨"
tags:
    - Ubuntu
    - 常用软件安装
---

> 建议使用 Flowus 阅读本文（若未失效），以获得最佳阅读体验：[Ubuntu 配置 Clang 编译器](https://flowus.cn/lihanchen/share/0c6c397c-b1a7-48b7-b49d-e3630f3a9930?code=4PP1RS)

上次更新：@2024/05/02 16:37

> 简单来说，Clang 是一个编译器，目前用来编译 C、C++、Objective-C 语言。 更进一步来说，Clang 只是一个编译器前端，其将上述的C类语言编译成一种“汇编语言（中间语言）”。接着，通过 LLVM（Low Level Virtual Machine）作为后端，将这种“汇编语言”编译成针对不同机器的二进制机器语言。  
[Clang](https://clang.llvm.org/) 在 GCC 后面发展起来的，采用了基于库式结构设计，并且与 LLVM 紧密集成。它具有非常快的编译速度和低内存占用率，并且能够提供更好的错误信息和警告。在开发过程中，特别是需要快速反馈和迭代时，Clang 相对 GCC 来说会更适合。  
[Clangd](https://clangd.llvm.org/) 是 LLVM 项目推出的 C++ 语言服务器，通过 LSP(Language Server Protocal) 协议向编辑器如 vscode/vim/emacs 提供语法补全、错误检测、跳转、格式化等等功能。

## 一. 安装 Clang

在终端中输入

```Python
sudo apt-get install clangd
sudo apt-get install clang
sudo apt-get install clang-format
```

## 二. 安装 VSCode

请前往官网下载，**不要在 Ubuntu Store 下载**，Store 中的版本被阉割，无法输入中文

[Visual Studio Code - Code Editing. Redefined](https://code.visualstudio.com/)


1. 下载 .deb 安装包

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image.png)

1. 下载完成后打开终端，依次输入如下命令

    ```Shell
    cd Downloads
    ```

    ```Shell
    sudo dpkg -i code_*
    ```

    `sudo`: 这是一个 Linux 命令，用来以超级用户（root）的身份执行后面的命令。在安装软件时通常需要超级用户权限。

    `dpkg`: 这是一个 Debian 包管理系统的命令。它可以用来安装、删除和管理 Debian 格式的软件包。在这里，它被用来安装软件包。

    `-i`: 这是 dpkg 命令的一个选项，代表 "install"，表示你要安装一个软件包。

    `code_*`: 这是一个通配符，用来匹配文件名。在这里，它会匹配以 `code_` 开头的所有文件，通配符 * 表示匹配任意字符。

    sudo 命令执行后会要求你输入密码

    请注意，输入**密码**时，屏幕上不会显示任何内容。 这称为**盲人键入**。 你**不会看到你正在键入的内容**，这是完全正常的。

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image1.png)

## 三. 配置 VSCode

此部分内容选修，若要在 VScode 中编写简单的 C++ 程序并**一键编译运行**，才需按照下属方法配置

### 3.1 安装插件

打开 VSCode 点击左边栏上方最后一项 Extensions 以进行插件安装

![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image2.png)

### 3.2 配置 Code Runner 插件

![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image3.png)

1. 勾选图中的两个选项

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image4.png)

1. 设置编译指令为 `clang`

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image5.png)

    将 `gcc`  替换为 `clang`， `g++` 替换为 `clang++`。保存

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image6.png)

1. 配置 DEBUG 编译指令（选修）

    在 `.c` 和 `.cpp` 文件的编译指令中加入 `--debug` 参数

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image7.png)

### 3.3 添加 .vscode/launch.json 文件用于 DEBUG（选修）

在当前工作目录中新建 .vscode 文件夹，再在文件夹中新建 launch.json 文件，将以下内容粘贴到文件中

```JSON
{
    "version": "0.2.0",
    "configurations": [
    {
        "type": "lldb",
        "request": "launch",
        "name": "Debug",
        "program": "${workspaceFolder}/${input:program}.exe",
        "args": [],
        "cwd": "${workspaceFolder}"
    }
    ],
    "inputs": [
    {
        "id": "program",
        "type": "promptString",
        "description": "Program name",
        "default": "test"
    }
    ],
}
```

![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image9.png)

## 四. 测试

### 4.1 编译运行测试

1. 复制下列代码到 VSCode 中

    ```C
    #include <stdio.h>
    int main() {
        printf("\n");
        printf("Congratulation! Your VSCode has been equipped with clang\n");
        printf("恭喜！你的 VSCode 已成功配置 clang 编译器\n");
        printf("\n");
        return 0;
    }
    ```

2. 点击 VSCode 右上角运行按钮，即可编译并运行代码

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image10.png)

3. 终端输出以下内容，表示成功

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image11.png)

### 4.2 DEBUG 功能测试（选修）

1. 点击 test.cpp 程序左侧的行号，打上红色的断点标识

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image12.png)

1. 进入 DEBUG 模式

    ![image.png](/img/in-post/About_Ubuntu/Setup-Clang-in-Ubuntu/image13.png)

---

- 参考文章

    [How to install clang 17 or 16 in Ubuntu](https://ubuntuhandbook.org/index.php/2023/09/how-to-install-clang-17-or-16-in-ubuntu-22-04-20-04/)


    [[VSCode插件推荐] Code Runner: 代码一键运行，支持超过40种语言](https://zhuanlan.zhihu.com/p/54861567)