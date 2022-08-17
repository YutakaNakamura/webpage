---
title: "数学的基礎知識"
metaTitle: "PMSM"
metaDescription: "This is the meta description motor page"
---

ここではPMSMの制御理論に密接に関連する数学的基礎知識を説明する。  

# 準備中

# 微分演算子とラプラス変換
$f(t)$のラプラス変換を$F(s)$とするとき、
$f(t)$に作用する微分演算子$\frac{d}{dt}$は、$F(s)$と$s$の積に対応する。
$$
\begin{CD}
   f(t) @>\frac{d}{dt}>> \frac{d}{dt}f(t) \\
@V\mathcal{L}VV @VV\mathcal{L}V \\
   F(s) @>s>> sF(s)
\end{CD}
$$
以後、特別な理由が無い限り$\frac{d}{dt}$も$s$と表記する。  
混在するが、作用する関数の引数や定義域を考えれば両者の区別は自明である。

# 2次元実数空間と複素数の対応

$$
\bm{I}=
\begin{pmatrix}
1 & 0 \\
0 & 1 \\
\end{pmatrix}
$$
$$
\bm{J}=
\begin{pmatrix}
0 & -1 \\
1 & 0 \\
\end{pmatrix}
$$
と定義する。  
複素数$x + jy \in \mathbb{C}$に$x\bm{I}+y\bm{J}$を対応させると、複素数における和と積は行列における和と積に対応する。即ち、演算として同系となる。
$$
\begin{CD}
\mathbb{R}^2 \ni A @>x\bm{I}+y\bm{J}>> B \in \mathbb{R}^2\\
@VVV @VVV \\
\mathbb{C} \ni  z @>x + jy>> w \in \mathbb{C}
\end{CD}
$$
この性質を利用すると、モータ制御に頻出する$\bm{I}$と$\bm{J}$による演算は、一旦複素数に置き換えて、複素数の上で演算し、最後に$\mathbb{R}^2$に戻すことで計算が簡単になる。

### 例
$$
\begin{pmatrix}
\cos \theta & - \sin \theta \\
\sin \theta & \cos \theta \\
\end{pmatrix}
s
\begin{pmatrix}
x \\
y \\
\end{pmatrix}
\rightarrow
e^{j\theta}sz
$$
$$
e^{j\theta}sz = se^{j\theta}z + j\omega e^{j\theta}z
$$
$$
se^{j\theta}z + j\omega e^{j\theta}z \rightarrow 
( s\bm{I} + \omega \bm{J} )
\begin{pmatrix}
\cos \theta & - \sin \theta \\
\sin \theta & \cos \theta \\
\end{pmatrix}
\begin{pmatrix}
x \\
y \\
\end{pmatrix}
$$
また、複素数体の元は可換であるため、$\bm{I}$と$\bm{J}$を用いて表現すれば、計算コストが低くなる。

### 例
$$
\begin{pmatrix}
a & - b \\
b & a \\
\end{pmatrix}
\begin{pmatrix}
c & - d \\
d & c \\
\end{pmatrix}
\begin{pmatrix}
x \\
y \\
\end{pmatrix}
=
\begin{pmatrix}
c & - d \\
d & c \\
\end{pmatrix}
\begin{pmatrix}
a & - b \\
b & a \\
\end{pmatrix}
\begin{pmatrix}
x \\
y \\
\end{pmatrix}
$$

# 同相・鏡相信号を用いた回転処理
主に扱うのは$\mathbb{R}^2$の信号であるが、回転の写像がある場合には$\mathbb{C}^2$で考えると簡単になる事がある。

ここで、ユニタリ行列
$$
\bm{U} \coloneqq 
\frac{1}{\sqrt{2}}\begin{pmatrix}
1 & - j \\
1 & j \\
\end{pmatrix}
$$
を考える。

いま、$\mathbb{R}^2 \rightarrow \mathbb{C}^2$の写像と制限して考えれば、この行列は$\mathbb{C}$上に、元と、元の複素共役が射影される変換である。

<!-- 説明用の絵 -->

$$
\begin{pmatrix}
u_1 \\
u_2 \\
\end{pmatrix}
=\bm{u} \in \mathbb{R}^2
$$
$$
\begin{pmatrix}
u_p \\
u_n \\
\end{pmatrix}
= \bm{u_{pn}} = \bm{U} \bm{u} = 
\frac{1}{\sqrt{2}}
\begin{pmatrix}
u_1 + ju_2 \\
u_1 - ju_2 \\
\end{pmatrix}
$$

このとき、$u_p$を$\bm{u}$の正相成分、$u_n$を$\bm{u}$の逆相成分と呼ぶ。

$$
\begin{CD}
\mathbb{R}^2 \ni \bm{u} @>f>> \bm{y} \in \mathbb{R}^2\\
@VV\bm{U}V @AA{}^t\!\bm{U}A \\
\mathbb{C}^2 \ni  \bm{u_{pn}} @>g>> \bm{y_{pn}} \in \mathbb{C}^2
\end{CD}
$$