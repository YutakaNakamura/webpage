---
title: "PMSMのトルク発生式"
metaTitle: "PMSM"
metaDescription: "This is the meta description motor page"
---

ここではPMSMのトルク発生式について、発生原理を考慮し導出する。

# 準備中

# マグネットトルク
マグネットトルクを考慮するには、磁場中の電流に働く力を考える。

# リラクタンストルク
リラクタンストルクを考慮するには、電磁エネルギー変換を考える。

# PMSMのトルク発生式
PMSMのトルクは、次のように表せる。
$$
\tau = 
N_p\begin{vmatrix}\bm{\phi}_{dq} \bm{i}_{dq} \end{vmatrix} = 
N_p\begin{vmatrix}
\phi_d & i_d \\
\phi_q & i_q \\
 \end{vmatrix} =
N_p( \phi_d i_q - \phi_q i_d )
\tag{1} $$ 
IPMSMでは
$$
\tau = 
N_p( \phi_d i_q - \phi_q i_d ) =
N_p( (\phi + L_d i_d)i_q - L_q i_q i_d ) =
N_p( \phi i_q + (Ld - Lq)i_di_q )
\tag{2} $$
となる。

