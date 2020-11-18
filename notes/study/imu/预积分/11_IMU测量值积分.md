IMU的真实值为$w,a$,测量值为$\widetilde{w}, \widetilde{a}$,则有:

$$
\begin{aligned}
  & \widetilde{b}^b = w^b + b^g + n^g \\
  & \widetilde{a}^b = q_{bw}(a^w + g^w) + b^a + n^a
\end{aligned}
$$

上标g表示gyro,a表示acc,w表示在世界坐标系world,b表示imu机体坐标系body.

PVQ对时间的倒数可写成:

$$
\begin{aligned}
  & \dot{p}_{wb_t} = v^w_t \\
  & \dot{v}^w_t = a^w_t \\
  & \dot{q}_{wb_t} = q_{wb_t} \otimes 
    \begin{bmatrix}
      0 \\
      \frac{1}{2} w^{b_t}
    \end{bmatrix} ??
\end{aligned} 
$$

---

从第i时刻的PVQ对IMU的测量值进行积分得到第j时刻的PVQ:

$$
\begin{aligned}
  & p_{wb_j} = p_{wb_i} + v^w_i \Delta t + \int\int_{t \in [i,j]} (q_{wb_t}a^{b_t} - g^w) \delta t^2 \\
  & v^w_j = v^w_i + \int_{t \in [i,j]} (q_{wb_t}a^{b_t} - g^w) \delta t \\
  & q_{wb_j} = \int_{t \in [i,j]} q_{wb_t} \otimes 
    \begin{bmatrix} 
      0 \\ \frac{1}{2} w^{b_t}
    \end{bmatrix} \delta t
\end{aligned}
$$

问题: 每次$q_{wb_t}$优化更新后,都需要重新进行积分,运算量较大.

高频采样;

---

IMU预积分

一个公式转换,就可以将积分模型转为预积分模型:
$$
q_{wb_t} = q_{wb_i} \otimes q_{b_i b_t}
$$

PVQ公式中的积分项则变成相对于第i时刻的姿态,而不是相对于世界坐标系的姿态:

$$
\begin{aligned}
  & p_{wb_j} = p{wb_i} + v^w_i \delta t - \frac{1}{2} g^w \Delta t^2 + q_{wb_i} \int \int_{t \in [i,j]}(q_{b_ib_t}) \delta t^2 \\
  & v^w_j = v^w_i - g^w \Delta t + q_{wb_i} \int_{t \in [i,j]} (q_{b_ib_t} a^{b_t}) \delta t  \\
  & q_{wb_j} = q_{wb_i} \int_{t \in [i,j]} q_{b_ib_t} \otimes 
    \begin{bmatrix}
      0 \\ \frac{1}{2} w^{b_t}
    \end{bmatrix} \delta t
\end{aligned}
$$

---
预积分量

预积分量仅仅跟IMU测量值有关,它将一段时间内的IMU数据直接积分起来就得到了预积分量:

$$
\begin{aligned}
  & \alpha_{b_ib_j} = \int \int_{t \in [i,j]} (q_{b_i b_t} a^{b_t}) \delta t^2 \\
  & \beta_{b_i b_j} = \int_{t \in [i,j]}(q_{b_i b_t} a^{b_t}) \delta t \\
  & q_{b_i b_j} = \int_{t \in [i,j]} q_{b_i b_t} \otimes 
    \begin{bmatrix}
      0 \\ \frac{1}{2} w^{b_t}
    \end{bmatrix} \delta t
\end{aligned}
$$

重新整理PVQ的积分公式,有:
$$
\begin{bmatrix}
  p_{wb_j} \\ v^w_j \\ q_{wb_j} \\ b^a_j \\ b^g_j
\end{bmatrix} =
\begin{bmatrix}
  p_{wb_i} + w^w_i \Delta t - \frac{1}{2} g^w \Delta t^2 + q_{wb_i} \beta_{b_i b_j} \\
  v^w_i - g^w \Delta t + q_{wb_i} \beta_{b_i b_j} \\ 
  q_{wb_i} q_{b_i b_j} \\
  b^a_i \\ b^g_i 
\end{bmatrix}
$$

