# 小车SLAM流程

## PC安装ROS

[ros ubuntu安装](ros_install.md)

## 小车连接到本地WIFI网络

* PC连接本地WIFI网络并查看本地IP

    ```bash
    ifconfig
    ```

    如图所示，`ip`为`192.168.20.121`
    ![ifconfig](../pic/ifconfig.png)

* PC连接小车AP

    小车开机后，会生成一个AP，名称为`aibot_xxx`，PC主机连接到小车wifi，密码为`12345678`。

* SSH远程连接小车

    打开终端，使用`SSH`连接到小车系统，密码为`xmhw2015`
    
    ```bash
    ssh pi@192.168.30.1
    ```

* 添加本地WIFI

    输入以下命令，编辑`wpa_supplicant.conf`文件
    
    ```bash
    sudo vim /etc/wpa_supplicant/wpa_supplicant.conf 
    ```

    添加本地`WIFI`信息到文件，如

    ```bash
    network={
        ssid="wifi名称"
        psk="wifi密码"
        key_mgmt=WPA-PSK
    }
    ```

    `ESC`退出，输入`:wq`保存

    输入以下命令，编辑`dhcpcd.conf`文件

    ```bash
    sudo vim /etc/dhcpcd.conf
    ```

    根据PC连接的网络信息，添加IP固定地址

    ```bash
    interface wlan0
    static ip_address=192.168.20.xxx/24
    static routers=192.168.20.1 
    static domain_name_servers=218.85.157.99
    ```
    >ip一般设置为200以外的网段比较不冲突，如`192.168.20.237`

    `ESC`退出，输入`:wq`保存


* 禁用AP

    ```bash
    sh ~/Documents/shcmd/disableAP.sh
    ```

* 重启小车

    终端输入

    ```bash
    sudo reboot
    ```

## 设置PC、小车主从机模式


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

从机`IP`设置（一般为小车），编辑`.bashrc`文件，在文件末尾添加以下内容

```bash
vim ~/.bashrc
export ROS_HOSTNAME=从机IP
export ROS_MASTER_URI=主机IP:11311
export ROS_IP=从机IP
```

添加完成后

```bash
source ~/.bashrc
```

## 建图

* 启动PC节点
    
    在PC端开启终端，输入以下内容，启动建图节点
    
    ```bash
    roslaunch navigation_demo slam.launch
    ```

* 远程连接小车

    使用`SSH`连接到小车，密码为`xmhw2015`

    ```bash
    ssh pi@192.168.20.237
    ```

    >根据实际情况，选择实际的IP地址，如果实际设置小车的IP地址为`192.168.1.251`，那么上面的`192.168.20.237`则改为`192.168.1.251`


* 启动小车节点

    ```bash
    roslaunch linorobot car_slam.launch
    ```

* 启动键盘控制

    在PC端开启终端，输入以下内容

    ```bash
    rosrun teleop_twist_keyboard teleop_twist_keyboard.py
    ```

    ```bash
   u    i    o
   j    k    l
   m    ,    .
   ...
   q/z : increase/decrease max speeds by 10%
   w/x : increase/decrease only linear speed by 10%
   e/c : increase/decrease only angular speed by 10%
    ```
    按照提示,降低控制的线速度(按键x)为0.2左右,角速度(按键c)为0.5左右.

    之后进行小车的控制（前进`i`,后退`，`,原地左转`j`,原地右转`l`）

    效果如下图
    ![slam](../pic/slam.png)

    ![slam](../pic/slam2.png)

* 保存地图

    PC端打开一个终端,输入以下命令

    ```bash
    rosrun  map_server map_saver -f map_name
    ```
    >其中map_name为保存地图的名称

    保存后有2个文件,分别是 `.pgm`和`.yaml`文件.打开文件管理器即可看到.
    ![map](../pic/map.png)

    如果出现无法建图或者导航,可能是时间同步问题，可以参照视频time.mp4做相应处理.
