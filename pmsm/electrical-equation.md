---
title: "PMSMの電圧方程式"
metaTitle: "PMSM"
metaDescription: "This is the meta description motor page"
---

ここではPMSMの電圧方程式について解説する。  

# 準備中

# uvw軸の電圧方程式
uvw軸の電圧方程式は、
$$
\bm{v_{uvw}} = R \bm{i_{uvw}} + s \bm{\phi_{all}} \tag{1}
$$
となる。

# αβ軸の電圧方程式
αβ軸上の電圧方程式は3相モデルに対して
$$
\bm{S}=\sqrt{\frac{2}{3}}\begin{pmatrix}
1 & -\frac{1}{2} & -\frac{1}{2} \\
0 & \frac{\sqrt{3}}{2} & -\frac{\sqrt{3}}{2} \\
\end{pmatrix}
$$

を作用させ、

$$
\begin{pmatrix}
v_{\alpha}\\
v_{\beta}\\
\end{pmatrix}
= \bm{v_{\alpha\beta}} = \bm{S} \bm{v_{uvw}}
$$
$$
\begin{pmatrix}
i_{\alpha}\\
i_{\beta}\\
\end{pmatrix}
= \bm{i_{\alpha\beta}} = \bm{S} \bm{i_{uvw}}
$$

$$
\bm{v_{\alpha\beta}} = R \bm{i_{\alpha\beta}} + s\bm{I} (L_i \bm{I} + L_m \bm{Q}(\theta)) \bm{i_{\alpha\beta}} + s\bm{I} \bm{u}(\theta) \begin{pmatrix}\phi\\ 0\\ \end{pmatrix} \tag{2}
$$
を得る。

# γδ軸の電圧方程式
γδ軸上の電圧方程式は回転行列
$$
\bm{R}=\begin{pmatrix}
\cos \theta & - \sin \theta \\
\sin \theta & \cos \theta \\
\end{pmatrix}
$$
を作用させると、
$$
\bm{v_{\gamma\delta}} = R \bm{i_{\gamma\delta}} + ( s\bm{I} + \omega_\gamma \bm{J} ) (L_i \bm{I} + L_m \bm{Q}(\theta_\gamma)) \bm{i_{\gamma\delta}} + ( s\bm{I} + \omega_\gamma \bm{J} ) \bm{u}(\theta_\gamma) \begin{pmatrix}\phi\\ 0\\ \end{pmatrix} \tag{3}
$$
を得る。

# dq軸の電圧方程式
dq軸上の電圧方程式は
$$
\bm{v_{dq}} = R \bm{i_{dq}} + ( s\bm{I} + \omega \bm{J} ) \begin{pmatrix} L_d & 0 \\ 0 & L_q \\ \end{pmatrix} \bm{i_{dq}} + ( s\bm{I} + \omega \bm{J} )\begin{pmatrix}\phi\\ 0\\ \end{pmatrix} \tag{4}
$$
を得る。