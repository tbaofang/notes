Kalman滤波方程的推导

**随机系统状态空间模型**:
$$
\begin{aligned}
  & X_k = \Phi_{k/k-1} X_{k-1} + \Gamma_{k-1}W_{k-1} \\
  & Z_k = H_kX_k + V_k
\end{aligned}
$$

关于噪声的基本假设

$$
\begin{aligned}
  & E[W_k] = 0, E[W_k W_j^T] = Q_k \delta_{kj} \\
  & E[V_k] = 0, E[V_k V_j^T] = R_k \delta_{kj} \\
  & E[W_k V_j^T] = 0 \\
  & Q_k \geq 0, R_k > 0 \qquad or \qquad (Q_k > 0, R_k > 0)
\end{aligned}
$$

补充:
白噪声:从信息的角度,不同时刻的信号不相关,相同时刻的信号是高斯或均匀分布,白噪声分为高斯白噪声和均匀白噪声. 只有高斯白噪声的线性组合还是高斯白噪声.

---

一些必备的记号介绍:
假设已知k-1时刻的**状态估计**/**状态估计误差**/**状态估计的均方差阵**:
$$
\hat{X}_{k-1}, \widetilde{X}_{k-1}=X_{k-1} - \hat{X}_{k-1}, P_{k-1} = E[\widetilde{X}_{k-1} \widetilde{X}_{k-1}^T]
$$

(补充:1.只有高斯分布,知道均值(一阶矩),方差(二阶矩),分布的密度函数也是知道的;2.卡尔曼滤波最终虑出的结果是分布的均值)

状态一步预测:$\hat{X}_{k/k-1} = \Phi_{k/k-1} \hat{X}_{k-1}$

一步预测误差:

$$
\begin{aligned}
  \widetilde{X}_{k/k-1} &= X_k - \hat{X}_{k/k-1} = (\Phi_{k/k-1} X_{k-1} + \Gamma_{k-1} W_{k-1}) - \Phi_{k/k-1} \hat{X}_{k-1} \\
  &= \Phi_{k/k-1}(X_{k-1} - \hat{X}_{k-1}) + \Gamma_{k-1} W_{k-1} = \Phi_{k/k-1} \widetilde{X}_{k-1} + \Gamma_{k-1} W_{k-1} 
\end{aligned}
$$

预测均方误差阵:

$$
\begin{aligned}
  P_{k/k-1} &= E[\widetilde{X}_{k/k-1} \widetilde{X}^T_{k/k-1}] \\
  &= E[(\Phi_{k/k-1} \widetilde{X}_{k-1} + \Gamma_{k-1} W_{k-1})(\Phi_{k/k-1} \widetilde{X}_{k-1} + \Gamma_{k-1} W_{k-1})^T] \\
  &= \Phi_{k/k-1} E[\widetilde{X}_{k-1} \widetilde{X}^T_{k-1}] \Phi^T_{k/k-1} + \Gamma_{k-1} E[W_{k-1} W^T_{k-1}] \Gamma^T_{k-1} \\
  &= \Phi_{k/k-1} P_{k-1} \Phi^T_{k/k-1} + \Gamma_{k/k-1} Q_{k-1} \Gamma^T_{k/k-1}
\end{aligned}
$$

其中,$\Phi_{k/k-1} \widetilde{X}_{k-1}(\Gamma_{k-1} W_{k-1})^T = 0, \Gamma_{k-1} W_{k-1}(\Gamma_{k/k-1} \widetilde{X}_{k-1})^T = 0$,理由是从物理的角度解释$\widetilde{X}_{k-1}$是k-1时刻的状态估计误差,$W_{k-1}$是k-1时刻到k时刻的白噪声,从时序上这两个量是不相关的.(??) 


---

量测一步预测:$\hat{Z}_{k/k-1} = H_k \hat{X}_{k/k-1}$

一步预测误差:
$$
\begin{aligned}
  \widetilde{Z}_{k/k-1} &= Z_k -\hat{Z}_{k/k-1} = (H_k X_k + V_k)-H_k \hat{X}_{k/k-1} \\
  &= H_k \widetilde{X}_{k/k-1} + V_k
\end{aligned}
$$

预测均方差阵:
$$
\begin{aligned}
  P_{ZZ,k/k-1} &= E(\widetilde{Z}_{k/k-1} \widetilde{Z}^T_{k/k-1}) \\
  &= E[(H_k \widetilde{X}_{k/k-1}+V_k)(H_k \widetilde{X}_{k/k-1}+V_k)^T] \\
  &= H_k E[\widetilde{X}_{k/k-1}\widetilde{X}_{k/k-1}^T] H_k^T + E[V_k V_k^T] \\
  &= H_k P_{k/k-1} H_k^T + R_k
\end{aligned}
$$

预测协方差:
$$
\begin{aligned}
  P_{XZ,k/k-1} &= E[\widetilde{X}_{k/k-1} \widetilde{Z}_{k/k-1}^T] \\
  &= E[\widetilde{X}_{k/k-1} (H_k \widetilde{X}_{k/k-1} + V_k)^T]\\
  &= P_{k/k-1} H_k^T
\end{aligned}
$$

---

