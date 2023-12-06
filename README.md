# 机械臂

- 点 `P` 在空间 `{A}` 下的坐标表示： $^{A}P = [p_x, p_y, p_z]^T$
- 基坐标系为 `{A}`，在其中有一个刚体 `M`，在 `M` 上建立坐标系 `{B}`,坐标系 `{B}` 相对于坐标系 `{A}` 的描述，即为 `M` 在坐标系 `{A}` 的位置和姿态
- $\hat{X}_B$、 $\hat{Y}_B$、 $\hat{Z}_B$ 表示坐标系 `{B}` 三个主轴方向的矢量
- `{B}` 相对于 `{A}` 的姿态，使用旋转矩阵表示
 $$ ^{A}_{B}R = \begin{pmatrix} ^{A}\hat{X}_B & ^{A}\hat{Y}_B & ^{A}\hat{Z}_B\end{pmatrix} 
 = \begin{pmatrix} 
 r_{11} & r_{12} & r_{13} \\ 
 r_{21} & r_{22} & r_{23} \\ 
 r_{31} & r_{32} & r_{33} 
 \end{pmatrix} 
 = \begin{pmatrix}
  \hat{X}_B \cdot \hat{X}_A & \hat{Y}_B \cdot \hat{X}_A & \hat{Z}_B \cdot \hat{X}_A \\ 
  \hat{X}_B \cdot \hat{Y}_A & \hat{Y}_B \cdot \hat{Y}_A & \hat{Z}_B \cdot \hat{Y}_A \\ 
  \hat{X}_B \cdot \hat{Z}_A & \hat{Y}_B \cdot \hat{Z}_A & \hat{Z}_B \cdot \hat{Z}_A 
  \end{pmatrix}$$
 其中 $r_{ij}$ 是每个矢量在参考坐标系的轴线上的投影分量。

- 欧拉角
    - 把一个旋转分解成三次绕不同的轴的旋转
        - 绕 `X` 轴为滚转 `Roll`
        - 绕 `Y` 轴为俯仰 `Pitch`
        - 绕 `Z` 轴为偏航 `Yaw`
        - 右手螺旋定则
    - 常用的旋转顺序 `ZYX`，又称 `YRP`
- 四元数：一个实部 + 三个虚部，$ q = q_0 + q_1 i + q_2 j + q_3 k$
    - 单位四元数表示空间中任意一个旋转，绕单位向量 $n = [n_x, n_y, n_z]^T$ 旋转 $\theta$ 角度，则：
    $$ q = [\cos\frac{\theta}{2}, n_x \sin\frac{\theta}{2}, n_y \sin\frac{\theta}{2}, n_z \sin\frac{\theta}{2} ]$$
    - 反解
    $$ \begin{cases} \theta = 2 \arccos q_0  \\ [n_x, n_y, n_z]^T = [q_1, q_2, q_3]^T / \sin \frac{\theta}{2} \end{cases}$$


# ROS环境

- OpenCV安装
```shell
$ git clone https://github.com/opencv/opencv.git
$ git clone https://github.com/opencvopencv_contrib.git
$ git checkout 4.8.1
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
  -D CMAKE_INSTALL_PREFIX=/usr/local/opencv481 \
  -D OPENCV_ENABLE_NONFREE=ON \
  -D OPENCV_EXTRA_MODULES_PATH=/home/ubuntu/workspace/opencv_contrib/modules \
  -D OPENCV_GENERATE_PKGCONFIG=YES \
  -D WITH_QT=ON \
  -D WITH_OPENGL=ON \
  -D WITH_CUDA=ON \
  -D BUILD_EXAMPLES=OFF \
  -D INSTALL_PYTHON_EXAMPLES=OFF \
  -D INSTALL_C_EXAMPLES=OFF ..

```