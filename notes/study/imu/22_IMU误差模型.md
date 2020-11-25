MEMS陀螺仪误差修正模型

$$
\begin{aligned}
  \begin{bmatrix}
    G_x \\ G_y \\ G_z
  \end{bmatrix} = 
  \begin{bmatrix}
    g_{x0} \\ g_{y0} \\ g_{z0}
  \end{bmatrix} +
  \begin{bmatrix}
    S_{gx} & K_{gx1} & K_{gx2} \\
    K_{gy1} & S_{ky} & K_{gy2} \\
    K_{gz1} & K_{gz2} & S_{kz}
  \end{bmatrix} \cdot 
  \begin{bmatrix}
    g_x \\ g_y \\ g_z
  \end{bmatrix}
\end{aligned}
$$

陀螺零偏: $g_{x0}, g_{y0}, g_{z0}$
标度因素: $S_{gx}, S_{gy}, S_{kz}$
安装误差: $K_{gx1}, K_{gx2}, K_{gy1}, K_{gy2}, K_{gz1}, K_{gz2}$


MEMS加速度计误差修正模型

$$
\begin{aligned}
  \begin{bmatrix}
    A_x \\ A_y \\ A_z
  \end{bmatrix} = 
  \begin{bmatrix}
    a_{x0} \\ a_{y0} \\ a_{z0}
  \end{bmatrix} +
  \begin{bmatrix}
    S_{ax} & K_{ax1} & K_{ax2} \\
    K_{ay1} & S_{ay} & K_{ay2} \\
    K_{az1} & K_{az2} & S_{az}
  \end{bmatrix} \cdot 
  \begin{bmatrix}
    a_x \\ a_y \\ a_z
  \end{bmatrix}
\end{aligned}
$$

陀螺零偏: $a_{x0}, a_{y0}, a_{z0}$
标度因素: $S_{ax}, S_{ay}, S_{az}$
安装误差: $K_{ax1}, K_{ax2}, K_{ay1}, K_{ay2}, K_{az1}, K_{az2}$

---
加速度计标定:

六面法标定:

---
陀螺仪标定:

MEMS陀螺仪采用速率标定方式. 将MEMS IMU固定于三轴转台的平台上,通过给定固定速率值测量其对应输出的方式进行实验.具体步骤如下:

- https://www.bilibili.com/video/BV1Vs411k7NG?from=search&seid=15197424126110122027
