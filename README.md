# ROS 机器人操作系统基础与实战

> 本-(2024-2025-1)-ME1125-01 | 2024 年秋季学期

本仓库是我在 2024 年秋季学期学习 **ROS机器人操作系统基础与实战** 课程期间完成的学习笔记和实践作业合集，基于 **ROS 1 (Noetic)**。

希望这些内容能为后续选修这门课的同学提供一些参考。

## 📖 学习资源

课堂 PPT 内容偏理论，因此我的学习笔记主要跟随 B 站 **机器人工匠阿杰**（张万杰）的视频课程自主学习时编写：

- 视频课程：[机器人操作系统 ROS 快速入门教程](https://www.bilibili.com/video/BV1BP4y1o7pw/)
- 推荐教材：《机器人操作系统 (ROS) 及仿真应用》— 张万杰

阿杰老师讲解深入浅出，非常适合 ROS 入门。

## 📂 目录结构

```
.
├── ROS_Course_Notes/                  # 学习笔记
│   ├── ROS学习笔记.md                 #   ROS 入门笔记（跟随阿杰老师视频）
│   └── image/                         #   笔记配图
│
├── ROS_Practical_Exercises_2024Fall/  # 实践作业
│   ├── README.md                      #   作业说明文档（含运行效果展示）
│   ├── images/                        #   截图与 GIF 演示
│   └── src/                           #   ROS 工作空间源码
│       ├── use_topic/                 #     作业1：自定义 msg 的 Topic 通信
│       ├── use_serv/                  #     作业2：自定义 srv 的 Service 调用
│       ├── joy_turtle/                #     作业3：手柄控制仿真小乌龟
│       ├── change_pen_turtle/         #     作业4：Service 切换小乌龟轨迹样式
│       ├── my_urdf/                   #     作业5：三自由度带夹爪机械臂 URDF
│       ├── my_moveit/                 #     作业6：MoveIt 运动规划
│       ├── use_turtlebot3/            #     大作业1：TurtleBot3 建图与导航
│       ├── catch_fruits/              #     大作业2：机械臂抓取水果
│       ├── learning_tf2_1/            #     TF2 坐标变换学习
│       └── jaka/                      #     JAKA 机械臂驱动包
└── .gitignore
```

## 🔧 环境配置

| 项目 | 版本 / 工具 |
|------|------------|
| 操作系统 | Ubuntu 20.04 (VMware Workstation 17 Pro) |
| ROS 版本 | ROS Noetic |
| 仿真工具 | Gazebo、RViz、MoveIt |
| 硬件（大作业2） | JAKA MiniCobo 机械臂、USB 摄像头、Arduino 夹爪 |

## 📋 作业列表

详细说明请查看 [实践作业文档](ROS_Practical_Exercises_2024Fall/README.md)。

| # | 作业 | 关键知识点 | 源码包 |
|---|------|-----------|--------|
| 1 | 自定义 msg 的 Topic 通信 | Topic、Publisher/Subscriber、自定义消息 | `use_topic` |
| 2 | 自定义 srv 的 Service 调用 | Service、Server/Client、自定义服务 | `use_serv` |
| 3 | 手柄控制仿真小乌龟 | joy_node、Twist 消息、turtlesim | `joy_turtle` |
| 4 | Service 切换小乌龟轨迹样式 | Service 客户端、set_pen | `change_pen_turtle` |
| 5 | 三自由度带夹爪机械臂 URDF | URDF/Xacro、RViz、Gazebo 仿真 | `my_urdf` |
| 6 | MoveIt 运动规划 | MoveIt Setup Assistant、运动规划 | `my_moveit` |
| 大1 | TurtleBot3 建图与导航 | gmapping、AMCL、move_base、SLAM | `use_turtlebot3` |
| 大2 | 机械臂抓取水果 | OpenCV、JAKA 驱动、坐标标定 | `catch_fruits` |