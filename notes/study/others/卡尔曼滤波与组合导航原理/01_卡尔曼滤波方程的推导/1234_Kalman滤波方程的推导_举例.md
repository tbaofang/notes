举例:
线性定常系统: $ \qquad
\begin{cases}
  X_k = \Phi X_{k-1} + W_{k-1}\\
  Z_k = X_k + V_k
\end{cases}
$

滤波方程:
$$
\begin{cases}
  \widetilde{X}_{k/k-1} = \phi \hat{X}_{k-1} & \text{(1)}\\
  P_{k/k-1} = \phi^2 P_{k-1} + Q & \text{(2)} \\
  K_k = \frac{P_{k/k-1}}{P_{k/k-1} + R} = \frac{\phi^2 P_{k-1} + Q}{\phi^2 P_{k-1} + Q + R} & \text{(3)} \\
  \hat{X}_k = \hat{X}_{k/k-1} K_k(Z_k - \hat{X}_{k/k-1}) = (1-K_k) \hat{X}_{k/k-1} + K_k Z_k & \text{(4)} \\ 
  P_k = (1-K_k)P_{k/k-1} = (1-\frac{P_{k/k-1}}{P_{k/k-1} + R}) P_{k/k-1} = R K_k &\text{(5)}
\end{cases}
$$

分析:
1. 如果 $Q$矩阵增大(预测误差变大),$K_k$增大;
2. 如果 $R$矩阵增大(量测误差变大),$K_k$减小.

---

带确定输入的Kalman滤波:

状态空间模型:

$$
\begin{cases}
  X_k = \Phi_{k/k-1} X_{k-1} + B_{k-1} u_{k-1} + \Gamma_{k-1} W_{k-1} \\
  Z_k = H_k X_k + Y_k + V_k
\end{cases}
$$

滤波方程:
$$
\begin{cases}
  \hat{X}_{k/k-1} = \Phi_{k/k-1} \hat{X}_{k-1} + B_{k-1} u_{k-1} \\ 
  P_{k/k-1} = \Phi_{k/k-1} P_{k-1} \Phi_{k/k-1}^T + \Gamma_{k-1} Q_{k-1} \Gamma_{k-1}^T \\
  K_k = P_{k/k-1} H_k^T (H_k P_{k/k-1} H_k^T + T_k)^{-1} \\
  \hat{X}_k = \hat{X}_{k/k-1} + K_k(Z_k - Y_k - H_k \hat{X}_{k/k-1})\\
  P_k = (I - K_k H_k) P_{k/k-1}
\end{cases}
$$

其中$Z_k - Y_k = H_k X_k + V_k $