# 小车机械臂控制流程


## 机械臂固件烧录

解压`myCobot固件烧录器V1.2.zip`包到任意磁盘，将`USB`连接到机械臂底部的`type-c`接口，点击 `myCobot.exe` 运行，烧录版本如下，点击`burn`烧录即可

myCobot固件烧录器V1.2.zip  [windows下载](../source/myCobot固件烧录器V1.2.zip)

![base](../pic/base.png)

`base`烧录后，还需进行`Atom`烧录，将`USB`连接到机械臂末端的`type-c`接口，重新运行`myCobot.exe`，烧录版本如下，点击`burn`烧录即可。

![atom](../pic/atom.png)


## 新建ROS工作空间

主机打开终端，输入以下命令新建ROS工作空间

```bash
mkdir -p catkin_ws/src
```

## 安装ROS机械臂控制包

创建好工作空间文件夹后，输入以下命令下载机械臂控制包

```bash
cd ~/catkin_ws/src
git clone https://github.com/kevin-zhuang/ros_arm_moveit
```

或者从[这里](../source/ros_arm_moveit.zip)下载

将下载的ROS包放在工作空间，输入以下命令编译

```bash
cd ~/catkin_ws
catkin_make
```


## 启动机械臂控制包

主机打开终端，输入以下命令启动机械臂控制包

```bash
roslaunch ros_arm_moveit mycobot_arm_moveit.launch
```

![mycobot_moveit](../pic/mycobot_moveit.png)


## 远程连接到小车

主机再打开另一个终端，输入以下命令，远程连接到小车

```bash
ssh ubuntu@小车ip
```

密码为`xmhw2015`





## 启动小车机械臂控制

连接到小车后，输入以下命令启动小车机械臂控制

```bash
roslaunch ros_arm_moveit arm_control.launch 
```

机械臂控制启动后，在`rviz`上，点击`update`，随机生成机械臂动作，确定动作后，再点击`Plan and Execute`，机械臂即可执行相应动作。
