随机系统状态空间模型:
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
白噪声:从信息的角度,不同时刻的信号不相关,相同时刻的信号是高斯或均匀分布,白噪声分为高斯白噪声和均匀白噪声.

---

一些必备的记号介绍:
假设已知k-1时刻的状态估计/状态估计误差/状态估计的均方差阵:
$$
\hat{X}_{k-1}, \widetilde{X}_{k-1}=X_{k-1} - \hat{X}_{k-1}, P_{k-1} = E[\widetilde{X}_{k-1} \widetilde{X}_{k-1}^T]
$$

(补充:1.只有高斯分布,知道均值(一阶矩),方差(二阶矩),分布的密度函数也是知道的;2.卡尔曼滤波最终虑出的结果是分布的均值)

状态一步预测:$\hat{X}_{k/k-1} = \Gamma_{k/k-1} \hat{X}_{k-1}$

一步预测误差:

预测均方误差阵:


其中,$\Phi_{k/k-1} \widetilde{X}_{k-1}(\Gamma_{k-1} W_{k-1})^T = 0, \Gamma_{k-1} W_{k-1}(\Gamma_{k/k-1} \widetilde{X}_{k-1})^T = 0$,理由是k-1之前时刻的状态与k-1时刻的状态独立.(??)