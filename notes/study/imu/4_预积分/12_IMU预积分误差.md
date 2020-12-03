预积分误差

定义:一段时间内IMU构建的预积分量作为测量值,对两时刻之间的状态量进行约束.

$$
\begin{bmatrix}
  r_p \\ r_q \\ r_v \\ r_{ba} \\ r_{bg}
\end{bmatrix}_{15 \times 1} =
\begin{bmatrix}
  q_{b_i w}(p_{wb_j} - p_{wb_i} - v^w_i \Delta t + \frac{1}{2} g^w \Delta t^2) - \alpha_{b_i b_j} \\
  2[q_{b_j b_i} \otimes (q_{b_iw} \otimes q_{wb_j})]_{xyz} \\
  q_{b_iw}(v^w_j - v^w_i + g^w \Delta t) - \beta_{b_i b_j} \\ 
  b^a_j - b^a_i \\ 
  b^g_j - b^g_i
\end{bmatrix}
$$

上面误差中的位移/速度/偏置都是直接相减得到.
第二项是关于四元素的旋转误差,其中$[\cdot]_{xyz}$表示只取四元素的虚部$(x,y,z)$组成的三维向量.

---



