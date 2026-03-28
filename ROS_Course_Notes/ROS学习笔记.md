# ROS 学习笔记

> 本笔记跟随 B 站"机器人工匠阿杰"（张万杰）的 [机器人操作系统 ROS 快速入门教程](https://www.bilibili.com/video/BV1BP4y1o7pw/) 自主学习时编写。

---

## 一、ROS 简介

### 什么是 ROS？

类似于安卓系统，**ROS (Robot Operating System)** 将机器人程序拆散成不同的可以独立运行的模块（即节点），这种分布式的理念，大大提高了机器人程序的可移植性。

ROS 并不是真实的操作系统，它一般运行在 Linux 等其他电脑操作系统上，更像是一套机器人软件框架。

### 为什么要学习 ROS？

通过下载使用前人写好的软件包，避免重复造轮子，ROS 让构建机器人程序更加容易快速。同时通过遵循统一规范的接口标准，我们自己写的轮子也可以给别人使用，如发布到 ROS 官网和 GitHub 上。

### 如何学习 ROS？

第一步：选择合适的 Ubuntu 版本和安装对应的 ROS 版本

<img src="image/image-20241126130752846.png" alt="ROS版本对应关系" style="zoom:50%;" />

第二步：选择合适的实验对象，多实践

可以选择实体的智能小车和仿真平台。

---

## 二、Ubuntu 安装和使用

安装 Ubuntu 有两种方法，使用虚拟机和使用双系统。因为使用虚拟机安装 Ubuntu 比较简单，并且一旦出现问题可以很快的重新安装，因此我使用 VMware Workstation 17 Pro 安装 Ubuntu 20.04.1。

### 快捷键

- 打开终端的快捷键：`Ctrl + Alt + T`
- 打开终端后新打开一个分页：`Ctrl + Shift + T`
- 在终端中 `Tab` 键可以补全命令和目录名

### 终端常用命令

列出当前目录下的文件：

```bash
ls
```

创建新的目录：

```bash
mkdir <目录名>
```

改变当前目录：

```bash
cd <目录路径>
```

返回父目录：

```bash
cd ..
```

返回主文件夹：

```bash
cd ~
```

通过文本编辑器打开文件，如果文件不存在则会先创建文件再打开：

```bash
gedit <文件名>
```

执行文件中的指令序列。在 Linux 中我们经常会把一连串的指令写到 `.sh` 文件里，然后通过 `source` 命令加载运行：

```bash
source <文件名>
```

移动文件：

```bash
mv ~/Downloads/lab00 ~/Desktop/cs61a/lab
```

`mv` 命令会将 `~/Downloads/lab00` 文件夹移动到 `~/Desktop/cs61a/lab` 文件夹中。

在终端或脚本中输出文本或变量内容：

```bash
echo <选项> <字符串...>
```

以管理员权限执行命令：

```bash
sudo <指令>
```

`sudo` + 指令 = 以管理员权限执行本条指令。

### 终端程序启用脚本 ~/.bashrc

这个文件是终端程序的初始化脚本，在我们每次执行终端程序时，这个脚本文件都会被系统执行，完成一些环境变量的赋值工作。

<img src="image/image-20241203165642326.png" alt="bashrc文件示例" style="zoom:50%;" />

---

## 三、安装 ROS Noetic

### 官方安装步骤

参见 ROS Wiki：[noetic/Installation/Ubuntu](https://wiki.ros.org/noetic/Installation/Ubuntu)

---

## 四、从 ROS 社区和 GitHub 获取软件包

### ROS 应用商店 APT 源

（待补充）
