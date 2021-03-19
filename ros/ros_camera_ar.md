# 摄像头识别

## 启动主机节点

主机打开终端，输入以下命令,打开可视化识别

```bash
roslaunch arm_navigation camera_ar.launch
```

## 远程连接小车

主机再打开另一个终端，输入以下命令，远程连接到小车

```bash
ssh ubuntu@小车ip
```

密码为`xmhw2015`

连接小车后启动摄像头识别节点

```bash
roslaunch arm_navigation aibot_arm_cam.launch 
```

## 放置标签

将标签放在摄像头可视范围内，可以看到标签被识别

![camera_ar](../pic/camera_ar.png)

## 查看识别信息

主机打开终端，输入以下命令查看识别信息

```bash
rostopic echo /visualization_marker
```

识别信息如图所示

![camera_ar_info](../pic/camera_ar_info.png)
