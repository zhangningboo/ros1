## 命令

- `catkin_init_workspace` :  ws/src目录下
- `catkin_create_pkg <pkg_name>`
- `rosed`: 编辑文件
- `rosmsg`
    - `rosmsg show <msg_type>`
    - `rosmsg info <msg_type>`
    - `rosmsg list`
    - `rosmsg package <pkg_name>`
    - `rosmsg packages`
    - `rosmsg <cmd> -h`
- `rossrv`
    - `rossrv show [options] <service_type>`
    - `rossrv info [options] <service_type>`
    - `rossrv list`
    - `rossrv package <package>`
    - `rossrv packages`
    - `rossrv <cmd> -h`
- `rosservice`: 服务
    - `rosservice list`
    - `rosservice args <service_name>`
    - `rosservice call <service_name> [args...]`
    - `rosservice find srv-type`
    - `rosservice info <service_name>`
    - `rosservice type <service_name>`
    - `rosservice uri <service_name>`
    - `rosservice <cmd> -h`
- `rosparam`
    - `rosparam set <param_name> <param_value>`
    - `rosparam get <param_name>`
    - `rosparam load <file>`
    - `rosparam dump <file>`
    - `rosparam delete <param_name>`
    - `rosparam list`
    - `rosparam <cmd> -h`
- `robot_state_publisher` & `joint_state_publisher`
    - `robot_state_publisher` 加载 `URDF` 中的初始参数，并获取 `/joint_states` 话题中的姿态数据，计算得出正向运动学结果，并发布到c`/tf`
    - `/joint_states` 话题的消息类型是 `sensor_msgs/JointState`
    ```shell
    $ rosmsg show sensor_msgs/JointState
    std_msgs/Header header
    uint32 seq
    time stamp
    string frame_id
    string[] name
    float64[] position  # 位置，单位：rad或m
    float64[] velocity  # 速度，单位：rad/s或m/s
    float64[] effort    # 受到的力，单位：N.m或N
    ```
    - 真实机器人中，`/joint_states` 话题是由机器人驱动负责发布
    - 仿真机器人中，通过 `joint_state_publisher` 发布虚拟节点的状态
