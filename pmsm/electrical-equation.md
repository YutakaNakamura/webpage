---
title: "PMSMの電圧方程式"
metaTitle: "PMSM"
metaDescription: "This is the meta description motor page"
---

ここではPMSMの電圧方程式について解説する。  

# 準備中
簡単のために、まずは固定子のみの電気的特性を考察する。後に回転子込みの電気的特性を導く。

# 固定子の電圧方程式
ここでは固定子の電気的構造を考える。  
$v$、$i$、$\phi$をそれぞれ電圧、電流、磁束として、抵抗とインダクタを直列に接続したR-L負荷の電圧方程式は次式となる。
$$
\begin{aligned}
v &= Ri + sLi \\
  &= Ri + s\phi
\end{aligned}
$$
固定子では、3相巻線として3対のR-Lが、Y結線もしくはΔ結線で接続される。以後、簡単のためY結線とする。

主磁束を$\phi_{L}$、漏れ磁束を$\phi_{l}$、各々に対応するインダクタンスを$L$、$l$とする。このとき短絡する磁束を考慮する。
$$
\begin{aligned}
v &= Ri + s(\phi_{L} + \phi_{l}) \\
  &= Ri + s(L + l)i
\end{aligned}
$$

このとき$\bm{\phi}$を鎖交磁束とし、固定子の電圧方程式は次式となる。
$$
\begin{aligned}
\bm{v} &= R \bm{i} + s \bm{\phi} \\

\begin{pmatrix}
v_u\\
v_v\\
v_w\\
\end{pmatrix} 
&= R 
\begin{pmatrix}
i_u\\
i_v\\
i_w\\
\end{pmatrix}
 + s 
\begin{pmatrix}
\phi_u\\
\phi_v\\
\phi_w\\
\end{pmatrix}
\end{aligned}
\tag{1} 
$$

$$
\begin{aligned}
\begin{pmatrix}
\phi_u\\
\phi_v\\
\phi_w\\
\end{pmatrix} 
&= \begin{pmatrix}
\cos{(0)} (\phi_{Lu} + \phi_{lu}) & \cos{(\frac{2\pi}{3})} \phi_{Lv} & \cos{(\frac{-2\pi}{3})} \phi_{Lw} \\
\cos{(\frac{-2\pi}{3})} \phi_{Lu}  & \cos{(0)} (\phi_{Lv} + \phi_{lv}) & \cos{(\frac{2\pi}{3})} \phi_{Lw} \\
\cos{(\frac{2\pi}{3})} \phi_{Lu} & \cos{(\frac{-2\pi}{3})} \phi_{Lv} & \cos{(0)} (\phi_{Lw} + \phi_{lw})
\end{pmatrix} \\
&= \begin{pmatrix}
\phi_{Lu} + \phi_{lu} & -\frac{1}{2} \phi_{Lv} & -\frac{1}{2} \phi_{Lw} \\
-\frac{1}{2} \phi_{Lu} & \phi_{Lv} + \phi_{lv} & -\frac{1}{2} \phi_{Lw} \\
-\frac{1}{2} \phi_{Lu} & -\frac{1}{2} \phi_{Lv} & \phi_{Lw} + \phi_{lw}
\end{pmatrix} \\
&= \begin{pmatrix}
L_u + l_u & -\frac{1}{2}L_v & -\frac{1}{2} L_w \\
-\frac{1}{2} L_u & L_v + l_v & -\frac{1}{2} L_w \\
-\frac{1}{2} L_u & -\frac{1}{2} L_v & L_w + l_w
\end{pmatrix}
\begin{pmatrix}
i_u\\
i_v\\
i_w\\
\end{pmatrix} \\
&= \begin{pmatrix}
L & M & M \\
M & L & M \\
M & M & L
\end{pmatrix}
\begin{pmatrix}
i_u\\
i_v\\
i_w\\
\end{pmatrix}\\

\bm{\phi} &= \bm{L} \bm{i}  
\end{aligned}
$$

$$
\bm{v} = R \bm{i} + s \bm{L} \bm{i}  
\tag{2} 
$$


### 補足
- $s\bm{L}\bm{i}$は、$\frac{d}{dt}(\bm{L}\bm{i})$である事に注意する。
- 回転子の有無によりLの値が変化する。磁気経路内にある物体の透磁率に依存する。  
透磁率は空気、珪素鋼板でそれぞれ$1.25 \times 10^{-6}$[H/m]、$5.0 \times 10^{-3}$[H/m]程度と異なる。  
よってこのセクションのLは、以後出現する回転子を含むPMSMのモデルに含まれたLとは値が異なる事に注意する。

# SPMSMの電圧方程式
SPMSMは回転子にリラクタンス(磁気抵抗)の変動が存在しないモータである。  
合計の磁束$\bm{\phi_{all,uvw}}$とは、固定子反作用磁束$\bm{\phi_{i,uvw}}$と回転子の永久磁束により発生する磁束$\bm{\phi_{m,uvw}}$の和となる。
$$
\begin{equation}
\begin{split}
\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \bm{\phi_{all,uvw}}\\
\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \bm{\phi_{i,uvw}} + s \bm{\phi_{m,uvw}}\\

\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \begin{pmatrix}
L & M & M \\
M & L & M \\
M & M & L
\end{pmatrix}
\bm{i_{uvw}}
+ s \Phi
\begin{pmatrix}
\cos{(\theta)}\\
\cos{(\theta + \frac{2\pi}{3})}\\
\cos{(\theta - \frac{2\pi}{3})}\\
\end{pmatrix}\\

\end{split}
\end{equation}
$$

# IPMSMの電圧方程式
IPMSMは回転子にリラクタンス(磁気抵抗)の変動が存在するモータである。
回転子の形状の対称性から、リラクタンスの変動は$2\theta$の関数となる。  

合計の磁束$\bm{\phi_{all,uvw}}$とは、固定子反作用磁束$\bm{\phi_{i,uvw}}$と回転子の永久磁束により発生する磁束$\bm{\phi_{m,uvw}}$の和となる。
$$
\begin{equation}
\begin{split}
\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \bm{\phi_{all,uvw}}\\
\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \bm{\phi_{i,uvw}} + s \bm{\phi_{m,uvw}}\\

\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \begin{pmatrix}
L(2\theta) & M(2\theta) & M(2\theta) \\
M(2\theta) & L(2\theta) & M(2\theta) \\
M(2\theta) & M(2\theta) & L(2\theta)
\end{pmatrix}
\bm{i_{uvw}}
+ s \Phi
\begin{pmatrix}
\cos{(\theta)}\\
\cos{(\theta + \frac{2\pi}{3})}\\
\cos{(\theta - \frac{2\pi}{3})}\\
\end{pmatrix}\\

\end{split}
\end{equation}
$$

# uvw軸の電圧方程式
uvw軸の電圧方程式は、
$$
\begin{equation}
\begin{split}

\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \bm{\phi_{all}} \\
\bm{v_{uvw}} &= R \bm{i_{uvw}} + s \bm{\phi_{i,uvw}} + s \bm{\phi_{m,uvw}}

\end{split}
\end{equation}
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
\begin{pmatrix}
\phi_{\alpha}\\
\phi_{\beta}\\
\end{pmatrix}
= \bm{\phi_{\alpha\beta}} = \bm{S} \bm{\phi_{uvw}}
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