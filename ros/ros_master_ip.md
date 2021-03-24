# ROS 主从机设置

## PC或者虚拟机从机IP设置

* 从机`IP`设置

    编辑`.bashrc`文件
    ```bash
    vim ~/.bashrc
    ```

    在文件末尾添加以下内容

    ```bash
    export ROS_HOSTNAME=从机IP
    export ROS_MASTER_URI=192.168.30.1:11311
    export ROS_IP=从机IP
    ```

    添加完成后

    ```bash
    source ~/.bashrc
    ```


## 小车主机IP设置

* 连接**小车底盘**

    PC连接小车AP，名称为`AIBot_base_xxxx`，密码为`12345678`
    连接到小车底盘后，ssh远程连接，密码为`aibot1234`
    ```bash
    ssh pi@192.168.30.1
    ```

* 主机`IP`设置

    编辑`.bashrc`文件
    ```bash
    vim ~/.bashrc
    ```

    在文件末尾添加以下内容

    ```bash
    export ROS_HOSTNAME=192.168.30.1
    export ROS_MASTER_URI=192.168.30.1:11311
    export ROS_IP=192.168.30.1
    ```

    添加完成后

    ```bash
    source ~/.bashrc
    ```