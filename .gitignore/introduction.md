## Convex optimization

### Introduction

### 目录

- 什么是凸优化
  - 为什么要使用凸优化
  - 凸函数的定义
  - 凸函数的性质
- 常见的凸函数 
  - 一些凸函数列表
  - 两种特殊的凸优化
    - 最小二乘
    - 线性规划
- 范数逼近
[TOC]


<div STYLE="page-break-after: always;" ></div>


### 什么是凸优化

一个优化问题一般可以写成下式：
$$
\begin{equation}\begin{split} 
minimize \quad f_0(x)\\
subject\quad to \quad f_i(x)\\ b_i,  i =1,...,m 
\end{split}
\end{equation}
$$

$f_0(x)$会有各种各样的形式，当$f_0(x)$是一个凸函数的时候，就把这类问题称作是凸优化问题。**在凸优化的问题中，局部最优值一定是全局最优值**。

#### 为什么要使用凸优化
General optimization problem
- Very <font color=#0099ff>difficult </font>to solve
- Methods involve some compromise, e.g., very long computation time, or not always find the solution

Exceptions: certain problem classes can be solved efficiently are reliably
- <font color = #0099ff>Least-squares</font> problem
- <font color = #0099ff>Linear programming</font> problems
- <font color = #ff0000>Convex optimization</font> problems

#### 凸函数的定义

对任意的$x,y \in R^n$ , 对 $\alpha >0$, 有下式：
$$
f(\alpha x+ (1- \alpha )y) \le \alpha f(x) + (1- \alpha)f(y)
\tag{0}
$$
则称$f(x)$是一个凸函数。

一些感性认识：

![512px-ConvexFunction.svg](C:\Users\LEI\Documents\ST\512px-ConvexFunction.svg.png) 

#### 凸函数的性质

**一阶性质**：

假设$f$可微，则函数$f$是凸函数的充要条件是**dom** $f$是凸集，且有下式成立：
$$
f(y) \ge f(x) + f'(x)(y-x)
\tag{1}
$$
感性认识:

![1538031749789](C:\Users\LEI\AppData\Local\Temp\1538031749789.png)

对过一点$(x, f(x))$,斜率为$f'(x)$的直线来说，其方程是$y  - f(x) = f'(x)(x- y)$ , 而凸函数的一阶性质指出凸函数$f(y)$应该是在这条线之上。

证明：

注意到(1)式中有一阶项$f'(x)$, 联系求导公式 ,所以把(0)式变形，有：
$$
\begin{eqnarray*}
f(\alpha x + y - \alpha y) &\le& \alpha f(x) + f(y) -  \alpha f(y)  \\
f(y + \alpha (x - y)) -f(y) &\le& \alpha f(x) - \alpha f(y)  \\
\cfrac{f(y + \alpha (x - y)) - f(y)}{\alpha} &\leqslant& f(x) - f(y)  \\
\cfrac{f(y + \alpha (x - y)) - f(y)}{\alpha (x - y)} (x - y) &\leqslant& f(x) - f(y)
\end{eqnarray*}
$$
联系式
$$
f'(x) = \lim_{\Delta x \to 0} \cfrac{f(x + \Delta x)-f(x)}{\Delta x}
$$

令$\alpha \to 0 $，可得(1)式。

**二阶性质**
假设f二阶可微，**dom** f是凸集， 则有：
$$
f''(x) \geqslant 0
$$
证明：
把$f(y)$在$x$点泰勒展开有：
$$
f(y) = f(x) + f'(x)(y-x) + \frac{1}{2}f''(x)(y-x)^2 + H.O.G
$$
由一阶性质有：
$$
f(y) \geqslant f(x) + f'(x)(y-x)
$$
所以：
$$
\frac{1}{2}f''(x)(y-x)^2 + H.O.G \geqslant 0 \\
f''(x)(y-x)^2 + \frac{H.O.G}{(y-x)^2} \geqslant 0 \\
f''(x) \geqslant 0
$$



### 常见的凸函数
#### 例子
- **指数函数**，对任意的 $ a \in R$，函数$e^{ax}$在$R$上是凸的。
- **幂函数**， 当$a \ge 1$或者 $a \le 0$的时候，$x^a$在正实数域内是凸函数， 当$0 \le a \e 1 $时，$x^a$在正实数域是凹函数。
- **绝对值幂函数**，当$p \ge 1$，$ |x|^p$是凸函数。
- **对数函数** ，$-log x$在正实数域内是凸函数
- **负熵**， $xlogx$ 在正实数域内是凸函数。
  一些在$R^n$上的例子：
- **范数**， $R^n$上的任意范数都是凸函数。
- **最大值范数**， $f(x)=max{x_1, ..., x_n}$在$R^n$上是凸的。
- **几何平均**， $f(x) = (\prod_{i=1}^n x_i)^{1/n}$在正实数域上是凸的。

#### 两种常用的凸优化
##### 最小二乘：
最小二乘以一类优化问题，它没有约束条件，目标函数的若干项的和，如下：
$$
minimize \quad f(x) = \|Ax - b \|_2^2
$$
其中$A \in R^{m \times n}$ 是参数矩阵, $x \in R^n$是要解的变量，最小二乘有解析解：
$$
\begin{eqnarray*}
f(x) &=& \| Ax - b \|_2^2 \\
	 &=& (Ax-b)^T(Ax-b)  \\
	 &=& x^TA^TAx - 2x^TA^Tb + b^Tb
\end{eqnarray*}
\tag{2}
$$
补充两个矩阵求导公式：
$$
\frac{\part b^Tx}{\part x} = b \\
\frac{\part x^TAx}{\part x} = (A + A^T)x
$$
对(2)是求导，令其等于0：
$$
\Delta f(x) = 2A^TAx- 2A^Tb = 0 \\
A^TAx=A^Tb
$$
当$A$的列向量是独立的时候，此时有唯一解 $x = (A^TA)^{-1}A^Tb$
注意到$A^TA$需要求逆，$A^TA \in R^{n \times n }$, $rank(A^TA) \le 、min( n,m )$, 所以如果 $m < n $ , 那$A^TA$ 肯定就没法求逆，这个时候没有解析解。另外，当n特别大的时候, $A^TA $会变得非常大，矩阵求逆的复杂度是O(n^3)，时间上可能也没法接受。这种时候一般用其他的方式来比如**梯度下降**来求解。


**最小二乘和最大似然**
假定我们的模型和上面一致，加入误差，如下：
$$
f(x) = Ax + \epsilon
$$
**假定误差服从分布 $\epsilon \sim N(0, \sigma ^ 2)$** , 那么就有 f(x) \sim N(Ax ,  \sigma ^ 2), 由最大似然估计，有：
$$
\begin{eqnarray*}
L(x) &=& ln \prod_{i=1}^n \frac{1}{\sigma \sqrt{2\pi}} exp(- \frac{1}{2}(\frac{f(x_i) - Ax_i}{\sigma})^2 ) \\
	 &=& \frac{1}{2\sigma ^2}\sum_{i=1}{n}(f(x_i) - Ax_i)^2- nln\sigma \sqrt{2 \pi}
\end{eqnarray*}
$$
求上式最大，等价于求下式最小：
$$
\sum_{i=1}{n}(f(x_i) - Ax_i)^2  \\ 
\| f(x) - Ax \|_2^2
$$
此时，最大似然和最小二乘的解等价。

**最小二乘的两种变形**

- 加权版本：  
  $$
  \sum_{i=1}^{k}w_k(a_i^Tx-b_i)^2
  $$

- 

$$
\sum_{i=1}^{k}w_k(a_i^Tx-b_i)^2 + \lambda \sum_{i=1}^nx_i^2
$$

![1538125004329](C:\Users\LEI\AppData\Local\Temp\1538125004329.png)

一般来说，参数的值越小，对应一个越光滑的函数，也即更简单的函数，因此不容易发生过拟合。

##### 线性规划



### 范数逼近

假定有线性模型 
$$
y =Ax+\sigma
$$
y是测量值，$\sigma$是未知的测量的误差。**假设\sigma在 || . ||下很小**，那么对x一个合理的猜测是
$$
\hat x = argmin_x ||Ax-y||
$$
假设$Ax-y = (r_1, ..., r_m)$,在不同的范数下面目标函数有不同的形式：

l2范数：
$$
minimize \quad ||Ax-b||_2^2 = r_1^2 + r_2^2+ ...+r_m^2
$$
l_{\infty}范数：
$$
minimize \quad || Ax- b||_\infty = max\{ |r_1|, |r_2|, ..., |r_m| \}
$$
$l1$范数：
$$
minimize \quad ||Ax-b||_1 = |r_1|+ |r_2|+ ...+ |r_m|
$$
不同形式的范数度量了对误差r的接受程度。虽然总体来讲都是希望误差尽可能的小，但是对不同的范数对不同范围的误差接受程度是不一样的。

比较l1范数和l2范数，对l1范数，其罚函数（度量函数）是$\phi _1(\sigma)= |u|$ , 对l2范数，其罚函数是$phi _2(\sigma) = x^2$.

![abs](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/Absolute_value.svg/350px-Absolute_value.svg.png)

![二次函数](http://www2.edu-ctr.pref.okayama.jp/math/image/10206a.jpg)

当$\sigma = 1$, 这两个函数给出同样的惩罚，当$\sigma$ 很小的时候，$\phi _1$ 比 $\phi _2$ 给出了大的惩罚(一个是$|\sigma |$， 一个是$\sigma ^2$), 而当$ \sigma $比较大的时候，$\phi _2$会给出远比$\phi _1$大的惩罚，所以到最后的分布上就是，$l1$范数逼近会让最后的误差分布趋向于有非常多0或者非常小的残差；而$l2$范数的倾向于有较少的比较大的误差。

![1538123494694](C:\Users\LEI\AppData\Local\Temp\1538123494694.png)

### Reference

[1] convex optimization book
