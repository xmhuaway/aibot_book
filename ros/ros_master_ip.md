# ROS 主从机设置

* 主机`IP`设置，编辑`.bashrc`文件，在文件末尾添加以下内容

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

* 从机`IP`设置（一般为小车），编辑`.bashrc`文件，在文件末尾添加以下内容

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