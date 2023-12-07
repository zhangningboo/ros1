### 使用方法

- 测试
```shell
$ roslaunch joint_state_demo xarm_states_cpp.launch
```
- 启动仿真
```shell
$ roslaunch robot_module display.launch
```
- 控制
```shell
$ rosrun joint_state_demo joint_states_pub.py
$ rosrun joint_state_demo gripper_open_close.py
$ rosrun joint_state_demo jixiebi_gripper.py
$ rosrun joint_state_demo urdf_state_publisher_fuzaweizhi.py
```