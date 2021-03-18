# 小车机械臂控制流程

小车机械臂配合`PC`主机(ROS环境)一起使用

## PC安装ROS

[ros ubuntu安装](ros_install.md)


## 机械臂固件烧录

解压`myCobot固件烧录器V1.2.zip`包到任意磁盘，将`USB`连接到机械臂底部的`type-c`接口，点击 `myCobot.exe` 运行，烧录版本如下，点击`burn`烧录即可

![base](../pic/base.png)



`base`烧录后，还需进行`Atom`烧录，将`USB`连接到机械臂末端的`type-c`接口，重新运行`myCobot.exe`，烧录版本如下，点击`burn`烧录即可。

![atom](../pic/atom.png)





## ROS主从机设置

主机`IP`设置，编辑`.bashrc`文件，在文件末尾添加以下内容

```bash
vim ~/.bashrc
export ROS_HOSTNAME=主机IP
export ROS_MASTER_URI=主机IP:11311
export ROS_IP=主机IP
```

添加完成后

```bash
source ~/.bashrc
```



从机`IP`设置，编辑`.bashrc`文件，在文件末尾添加以下内容

```bash
vim ~/.bashrc
export ROS_HOSTNAME=192.168.20.253 #从机IP
export ROS_MASTER_URI=主机IP:11311
export ROS_IP=192.168.20.253 #从机IP
```

添加完成后

```bash
source ~/.bashrc
```





## 主机PC安装ROS机械臂控制包

```bash
git clone https://github.com/kevin-zhuang/ros_arm_moveit
```

将下载的ROS包放在工作空间，编译。





## 启动主机ROS机械臂控制包

```bash
roslaunch ros_arm_moveit mycobot_arm_moveit.launch
```

![mycobot_moveit](../pic/mycobot_moveit.png)





## 远程连接到小车

```bash
ssh ubuntu@192.168.20.253
```

密码为`xmhw2015`





## 启动小车机械臂控制

```bash
roslaunch ros_arm_moveit arm_control.launch 
```

机械臂控制启动后，在`rviz`上，点击`update`，随机生成机械臂动作，确定动作后，再点击`Plan and Execute`，机械臂即可执行相应动作。
