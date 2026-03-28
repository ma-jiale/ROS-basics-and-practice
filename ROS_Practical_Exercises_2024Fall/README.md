# ROS 机器人操作系统基础与实战 — 实践作业

> 本-(2024-2025-1)-ME1125-01 | Ubuntu 20.04 + ROS Noetic

## 作业1：自定义 msg 的 Topic 发送和接收

作业1的源代码存放在 `use_topic` 软件包中，具体内容是创建了两个节点 `talker.py` 和 `listener.py`，`talker.py` 发布 `chatter` 话题并持续在话题中发送消息，`listener.py` 节点订阅该话题接收消息并打印在终端上。

我自定义了一个 `MyInfo.msg` 的 msg 文件存放在软件包中的 `msg` 文件夹中，其中内容如下：

```
string my_name
int32 age
```

为了自定义消息可以生成和发送，需要修改 `CMakeLists.txt` 文件：

添加 `message_generation` 依赖项：

```cmake
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation # 添加message_generation依赖项
)
```

添加在编译时生成 `msg` 文件夹里的消息的代码和生成附加的消息：

```cmake
# 在编译时生成 'msg' 文件夹里的消息
add_message_files(
  FILES
  MyInfo.msg
)
# 生成附加的消息，并在此处列出所有依赖项
generate_messages(
  DEPENDENCIES
  std_msgs
)
```

修改 `package.xml` 文件，添加 `message_generation` 编译和运行时的依赖：

```xml
<build_depend>message_generation</build_depend> 
<exec_depend>message_runtime</exec_depend>
```

具体的 `talker.py` 节点和 `listener.py` 节点的实现请参看代码文件。

运行 `hw1.launch` 文件实现效果如下：

![Topic通信运行效果](images/image-20241231194423271.png)

在 rqt_graph 中的节点图：

![rqt_graph节点图](images/image-20241231194542751.png)

## 作业2：自定义 srv 的 Service 服务和调用

作业2的源代码存放在 `use_serv` 软件包中，具体内容是创建了 `add_two_ints_client.py` 和 `add_two_ints_server.py` 节点。`add_two_ints_server.py` 提供一个 `add_two_ints` 的服务，作用是接受客户端传过来的两个整型，求它们的和并返回。`add_two_ints_client.py` 节点接受两个命令行参数，将它们解释为整型通过 `add_two_ints` 服务传输给服务端节点并获取返回的值打印在终端上。

我定义了一个 `AddTwoInts.srv` 的 srv 文件存放在软件包中的 `srv` 文件夹中，其中内容如下：

```
int64 a
int64 b
---
int64 sum
```

`---` 前为请求内容，`---` 后为返回内容。

为了自定义服务可以生成和发送，需要修改 `CMakeLists.txt` 文件：

添加 `message_generation` 依赖项，添加在编译时生成 `srv` 文件夹里的服务的代码和生成附加的服务：

```cmake
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
)

# Generate services in the 'srv' folder
add_service_files(
  FILES
  AddTwoInts.srv
)

# Generate added messages and services with any dependencies listed here
generate_messages(
  DEPENDENCIES
  std_msgs
)
```

也需要修改 `package.xml` 文件，添加 `message_generation` 编译和运行时的依赖：

```xml
<build_depend>message_generation</build_depend> 
<exec_depend>message_runtime</exec_depend>
```

具体服务端和客户端的实现请看代码。

先运行 `add_two_ints_server.py` 节点，再添加命令行参数（为要相加的两个数）运行 `add_two_ints_client.py`，实现效果如下：

![Service客户端运行效果](images/image-20250105213235212.png)

![Service服务端运行效果](images/image-20250105213202622.png)

## 作业3：使用手柄控制仿真小乌龟运动

作业3的源代码存放在 `joy_turtle` 软件包中，具体内容是创建了 `use_joy_ctr_turtle.py` 节点，其作用是订阅 `joy_node` 节点向 `/joy` 话题发送的手柄数据，使用手柄数据向 `/turtle1/cmd_vel` 话题发送 `Twist` 消息来控制小乌龟运动。

`joy_node` 节点的作用是读取连接在系统中的手柄（一般为 `/dev/input/js0`）的数据并通过 `/joy` 话题发送，`turtlesim_node` 监听 `/turtle1/cmd_vel` 话题，向此话题发送 `Twist` 消息可以控制小乌龟移动。

`use_joy_ctr_turtle.py` 节点实现请看代码。

运行 `hw3.launch` 文件实现效果如下：

![手柄控制小乌龟](images/joy_turtle.gif)

## 作业4：使用 Service 切换改变小乌龟的轨迹颜色和粗细

作业4的源代码存放在 `change_pen_turtle` 软件包中，具体内容是创建了 `set_turtle_client.py` 节点，其作用是接受命令行的 `r g b width` 四个参数，通过调用 `/turtle1/set_pen` 服务发送轨迹的参数信息（具体可以查看 `srv` 文件夹下的 `SetPen.srv`）。`turtlesim_node` 节点收到服务的请求后将改变小乌龟的运行轨迹。

`/turtle1/set_pen` 服务是 `turtlesim_node` 节点提供的服务，可以更改小乌龟运行轨迹。

`set_turtle_client.py` 节点实现请看代码。

运行 `hw4.launch` 文件和 `set_turtle_client.py` 实现效果如下：

先运行 `hw4.launch` 文件：

![hw4.launch运行效果](images/image-20250107094639369.png)

使用 R=240 G=10 B=10 width=10 命令行参数运行 `set_turtle_client.py` 改变轨迹的颜色和线宽：

![改变轨迹后效果](images/image-20250107094948158.png)

## 作业5：绘制三自由度带夹爪机械臂的 URDF 并实现控制与仿真

标准化机器人描述格式（URDF）是一种用于描述机器人、其部分结构、关节、自由度等的 XML 格式文件。通过使用机器人的 URDF 文件，在 ROS 中仿真机器人或者帮助机器人开发者简化他们的日常工作。

机械臂参考图如下：

![机械臂参考图](images/image-20250107095233383.png)

我绘制的机械臂的 URDF 文件保存在 `my_urdf` 软件包的 `urdf` 目录下。在定义了基本的 link 和 joint 前提下，为了能实现在 RViz 中的控制以及在 Gazebo 的仿真，我又为其添加了 color、collision、transmission、inertial 等参数，并添加了 Gazebo 插件。

### 5.1 在 RViz 中控制机械臂

运行 `hw5.launch` 文件效果如下：

![RViz中控制机械臂](images/my_urdf_rivz.gif)

### 5.2 在 Gazebo 进行机械臂仿真

运行 `hw5.5.launch` 文件效果如下：

![Gazebo仿真界面](images/image-20250107101100422.png)

运行下列命令可以控制 Gazebo 仿真环境下的机械臂：

```bash
# 控制夹爪开启
rostopic pub  /r2d2_gripper_controller/command std_msgs/Float64MultiArray "layout:
  dim:
  - label: ''
    size: 3
    stride: 1
  data_offset: 0
data: [0, 0.5, 0.5]"
```

![夹爪开启](images/my_urdf_gazobo_1.gif)

```bash
# 控制夹爪关闭
rostopic pub  /r2d2_gripper_controller/command std_msgs/Float64MultiArray "layout:
  dim:
  - label: ''
    size: 3
    stride: 1
  data_offset: 0
data: [0, 0, 0]"
```

![夹爪关闭](images/my_urdf_gazobo.gif)

```bash
# 控制关节运动
rostopic pub /r2d2_link1_controller/command std_msgs/Float64 "data: -0.707"
rostopic pub /r2d2_link2_controller/command std_msgs/Float64 "data: 0.5"
```

## 作业6：实现 URDF 绘制的机械臂的 MoveIt 规划

作业6的实现思路是使用 MoveIt 配置助手生成 MoveIt 配置文件，然后运行 MoveIt 配置文件 `launch` 目录下的 `demo.launch` 文件。

使用 MoveIt 配置助手生成 MoveIt 配置文件的细节可以参照这篇文章：[MoveIt入门之——使用MoveIt配置助手生成MoveIt配置文件](https://blog.csdn.net/weixin_41995979/article/details/81515711)

我的机械臂的 MoveIt 配置文件存放在 `my_moveit` 软件包中，运行 `demo.launch` 文件效果如下：

规划关节规划组：

![MoveIt关节规划](images/my_urdf_moveit1.gif)

规划夹爪规划组：

![MoveIt夹爪规划](images/my_urdf_moveit2.gif)

## 大作业1：使用虚拟 TurtleBot3 机器人

大作业1的源代码存放在 `use_turtlebot3` 软件包中。

以下子任务均需要先运行 TurtleBot3 机器人 Gazebo 仿真环境：

```bash
export TURTLEBOT3_MODEL=waffle
roslaunch turtlebot3_gazebo turtlebot3_world.launch
```

### 1.1 手柄控制机器人移动

主要的实现思路是启动 `joy_node` 节点接收游戏手柄数据并向 `/joy` 话题发送手柄数据，运行 `turtlebot3_world.launch` 文件启动 TurtleBot3 虚拟仿真环境，运行 `use_joy_ctr_turtlebot3.py` 节点订阅 `/joy` 话题接收手柄数据并发送 `Twist` 消息到 `/cmd_vel` 话题控制机器人底盘运动。

设置环境变量 `export TURTLEBOT3_MODEL=waffle`，运行 `joy_bot.launch` 效果如下：

![手柄控制TurtleBot3](images/turtlebot1.gif)

### 1.2 手柄控制机器人完成环境建图

主要的实现思路是在 1.1 手柄控制机器人移动的基础上，运行 gmapping 的 SLAM 节点和 RViz（用于可视化）。注意为了确保能正确收到 map 数据，需要确保机器人的 TF 树完整，典型的 TF frames 结构如下：

![TF树结构](images/image-20250107112823405.png)

如果 TF 树不完整，需要手动发布 TF 变换，如何手动发布静态 TF 变换可以参照软件包内代码。

运行 `my_mapping.launch` 效果如下：

![建图过程](images/turtlebot2.gif)

运行 `rosrun map_server map_saver -f <保存路径>` 命令保存地图：

![保存地图命令](images/image-20250107144300655.png)

在指定的目录下会生成两个地图文件：

![地图文件](images/image-20250107144430606.png)

![地图预览](images/image-20250107144527385.png)

### 1.3 实现机器人导航

主要的实现思路是使用 `map_server` 节点发布 1.2 中保存的地图数据到 ROS 中，然后使用 AMCL 软件包实现机器人的自主定位，使用 move_base 软件包实现机器人的实时路径规划和导航。

基本的原理图如下：

![move_base原理图](http://wiki.ros.org/move_base?action=AttachFile&do=get&target=overview_tf_small.png)

运行 `my_mapping.launch` 文件。

给机器人一个大致的初始定位：

![初始定位](images/movebase_1.gif)

实现机器人的实时路径规划和导航：

![路径规划导航](images/movebase_2.gif)

move_base 算法可以实现实时路径规划和导航，如果遇到地图中没有的障碍物会重新规划路线并导航：

![动态避障导航](images/movebase_3.gif)

### 1.4 利用虚拟机器人实现简易碰撞式扫地机器人功能

主要实现思路是读取激光雷达数据，当机器人靠近障碍物时减速并转向。

激光雷达数据可以通过订阅 `/scan` 话题接收，控制机器人底盘移动可以通过向 `/cmd_vel` 话题发送 `Twist` 消息实现。

运行 `clean_robot.py` 节点，实现效果如下：

![扫地机器人效果](images/clean_robot.gif)

## 大作业2：机械臂抓取水果

作业细节要求如下：

![大作业2要求](images/image-20250107153735571.png)

大作业2的源代码存放在 `catch_fruits` 软件包中：

- `usb_cam_gripper.launch` — 连接相机和使用 Arduino 控制的夹爪舵机
- `robot_start.launch` — 连接机械臂
- `find_fruits.launch` — 读取网格位置，检测水果的位置（在哪个格子里）并通过 `fruits_position` 话题发送
- `catch.launch` — 订阅 `fruits_position` 话题获取水果的位置并抓取放到指定位置
- `tag.py` — 标定网格的位置并存储

实现效果视频：[抓个橘子：基于 ROS 和 OpenCV 的 JAKA 机械臂抓取任务设计](https://www.bilibili.com/video/BV1WZrUYXExB/)