滤波增益矩阵K的求解:

滤波方程("预测+修正"形式)
$$
\hat{X}_k = \hat{X}_{k/k-1} + K_k \widetilde{Z}_k = \hat{X}_{k/k-1} + K_k(Z_k - H_k \hat{X}_{k/k-1})
$$

状态估计误差

$$
\begin{aligned}
  \widetilde{X}_k &= X_k - \hat{X}_k = X_k - [\hat{X}_{k/k-1} + K_k(Z_k - H_k \hat{X}_{k/k-1})] \\
  &= \widetilde{X}_{k/k-1} - K_k(H_k X_k + V_k - H_k \hat{X}_{k/k-1}) = (I - K_k H_k)\widetilde{X}_{k/k-1} - K_k V_k
\end{aligned}
$$

状态估计均方误差阵
$$
\begin{aligned}
P_k &= E[\widetilde{X}_k \widetilde{X}_k^T] \\
    &= E\{[(I - K_k H_k)\widetilde{X}_{k/k-1} - K_k V_k] [(I - K_k H_k)\widetilde{X}_{k/k-1} - K_k V_k]^T\} \\
    &= (I - K_k H_k) E[\widetilde{X}_{k/k-1} \widetilde{X}_{k/k-1}^T] (I - K_k H_k)^T + K_k E[V_k V_k^T] K_k^T \\
    &= (I - K_k H_k) P_{k/k-1} (I - K_k H_k)^T + K_k R_k K_k^T
\end{aligned}
$$

---

最优估计的含义:

$$
\begin{aligned}
& E[(\widetilde{X}_k^{(1)})^2] + E[(\widetilde{X}_k^{(2)})^2] + ... + E[(\widetilde{X}_k^{(n)})^2] = min \\ 
\Longleftrightarrow &  E[\widetilde{X}_k^T \widetilde{X}_k] = min  \\
& E[\widetilde{X}_k \widetilde{X}_k^T] = 
\begin{bmatrix}
E[(\widetilde{X}_k^{(1)})^2] & E[(\widetilde{X}_k^{(1)}) (\widetilde{X}_k^{(2)})] & ... & E[(\widetilde{X}_k^{(1)}) (\widetilde{X}_k^{(n)})] \\
E[(\widetilde{X}_k^{(2)}) (\widetilde{X}_k^{(1)})] & E[(\widetilde{X}_k^{(2)})]^2 & ... & E[(\widetilde{X}_k^{(2)})] (\widetilde{X}_k^{(n)})] \\
... & ... & ... & ... \\
E[(\widetilde{X}_k^{(n)}) (\widetilde{X}_k^{(1)})] & E[(\widetilde{X}_k^{(n)})] E[(\widetilde{X}_k^{(2)}) & ... & E[(\widetilde{X}_k^{(n)})]^2 \\
\end{bmatrix} \\ 
\Longleftrightarrow &   tr(P_k) = tr(E[\widetilde{X}_k \widetilde{X}_k^T]) = min  
\end{aligned}
$$

---

$$
\begin{aligned}
P_k &= (I - K_k H_k) P_{k/k-1} (I - K_k H_k)^T + K_k R_k K_k^T \\
&= P_{k/k-1} - K_k H_k P_{k/k-1} - (K_k H_k P_{k/k-1})^T + K_k(H_k P_{k/k-1} H_k^T R_k) K_k^T \\
\Longrightarrow & tr(P_k) = tr(P_{k/k-1}) - tr(K_k H_k P_{k/k-1}) \\
  & \qquad \qquad - tr((K_k H_k P_{k/k-1})^T) + K_k(H_k P_{k/k-1} H_k^T R_k) K_k^T) \\
\Longrightarrow & \frac{d}{dK_k}[tr(P_k)] = 0 -(H_k P_{k/k-1})^T - (H_k P_{k/k-1})^T + 2K_k(H_k P_{k/k-1} H_k^T + R_k) = 0 \\
& P_{k/k-1} H_k^T = K_k(H_k P_{k/k-1} H_k^T + R_k) \\
\Longrightarrow & K_k = P_{k/k-1} H_k^T (H_k P_{k/k-1} H_k^T + R_k)^{-1}
\end{aligned}
$$

补充:
$$
\begin{aligned}
  & \frac{d}{dX}[tr(XB)] = \frac{d}{dX}[tr((XB)^T)] = B^T \\
  & \frac{d}{dX}[tr(XAX^T)] = 2XA
\end{aligned}
$$

---
方阵的迹求导验证:
$$
\begin{aligned}
  tr(XB) &= (XB)_{11} + (XB)_{22} + ... + (XB)_{nn} \\
  &= (X_{11}B_{11} + X_{12}B_{21} + ... + X_{1i}B_{i1} + ... + X_{1m}B_{m1}) + \\
  & \qquad (X_{21}B_{12} + X_{22}B_{22} + ... + X_{2i}B_{i2} + ... + X_{2m}B_{m2}) + \\
  & \qquad ... + \\
  & \qquad (X_{n1}B_{1n} + X_{n2}B_{2n} + ... + X_{ni}B_{in} + ... + X_{nm}B_{mn})
\end{aligned}
$$

$$
\frac{d}{dX}[tr(XB)] = 
\begin{bmatrix}
  B_{11} & B_{21} & ... & B_{i1} & ... & B_{m1} \\
  B_{12} & B_{22} & ... & B_{i2} & ... & B_{m2} \\
  ... & ... & ... & ... & ... & ... \\
  B_{1n} & B_{2n} & ... & B_{in} & ... & B_{mn} \\
\end{bmatrix}
= B^T
$$

补充:

定义:对矩阵X求导,求导结果排成与X尺寸相同的矩阵.

---

Kalman滤波方程:
(1) 状态一步预测
$$
\hat{X}_{k/k-1} = \Phi_{k/k-1} \hat{X}_{k-1}
$$
(2) 状态一步预测均方误差
$$
P_{k/k-1} = \Phi_{k/k-1} P_{k-1} \Phi_{k/k-1}^T + \Phi_{k-1} Q_{k-1} \Phi_{k-1}^T
$$
(3) 滤波增益
$$
K_k = P_{k/k-1} H_k^T (H_k P_{k/k-1} H_k^T + R)^{-1}
$$
(4) 状态估计
$$
\hat{X}_k = \hat{X}_{k/k-1} + K_k(Z_k - H_k \hat{X}_{k/k-1})
$$
(5) 状态估计均方误差
$$
P_k = (I - K_k H_k) P_{k/k-1}
$$