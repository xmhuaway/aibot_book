# ROS环境安装

建议`ros`安装使用`ubuntu`系统

* Ubuntu版本 16.04.5 LTS
* ROS版本 Kinetic Kame

## Ubuntu更换国内源

* 备份本地源

```bash
sudo mv /etc/apt/sources.list /etc/apt/sources.list.bk
```

* 编辑软件源，写入以下信息

```bash
sudo vim /etc/apt/sources.list
```

```bash
deb http://mirrors.aliyun.com/ubuntu/ xenial main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main
deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security universe
```



## 设置sources.list

```bash
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```

## 设置密钥

```bash
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

## 安装

```bash
sudo apt-get update
sudo apt-get install ros-kinetic-desktop-full
```

## 初始化 rosdep

```bash
sudo rosdep init
rosdep update
```
> 如果初始化失败，设置VPN重新初始化或者直接跳过该步骤

## 环境配置

```bash
echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## 构建工厂依赖

```bash
sudo apt-get install python-rosinstall python-rosinstall-generator python-wstool build-essential
```

## 验证

打开终端输入以下命令

```bash
roscore
```

如图所示，出现以下信息即安装成功

![roscore](../pic/roscore.png)
