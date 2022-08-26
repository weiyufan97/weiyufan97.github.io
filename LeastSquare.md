最小二乘法是一种基本的线性回归方法，现总结其矩阵形式的推导。

##### 优化目标

$\mathop{min}\limits_{\mathbf{x}}f(\mathbf{x})={||\mathbf{Ax-B||}_2^2}$

##### 第一步： l2范式展开

$$
\begin{aligned}
f(\mathbf{x}) &= \mathbf{{(Ax-B)^T(Ax-B)}} \\
&= {\mathbf{x^TA^TAx-B^TAx-x^TA^TB+B^TB}}  \\
&= {\mathbf{x^TA^TAx-2B^TAx+B^TB}}
\end{aligned}
$$

注意，这里中间两项由于结果都是标量且形式上互为转置，那么必然相等，因此合并为一项。

##### 第二步：求偏导得到最小值点

首先列出要用到的对向量求偏导的公式：
$$
\begin{aligned}
\frac{\partial{\mathbf{(c^T\beta)}}}{\partial{\mathbf{\beta}}} = 
{\mathbf{c}}
\end{aligned}
$$

$$
\begin{aligned}
\frac{\partial{\mathbf{({\beta}^TV{\beta})}}}{\partial{\mathbf{\beta}}} &= \mathbf{(V+V^T)\beta} \\
&= \mathbf{2V\beta}\quad\text{(V对称)}
\end{aligned}
$$

根据公式，可立即得到：
$$
\begin{aligned}
\frac{\partial{f(\mathbf{x})}}{\partial{\mathbf{x}}} &= \frac{\partial{\mathbf{(x^TA^TAx-2B^TAx+B^TB)}}}{\partial{\mathbf{x}}} \\
&= \mathbf{2A^TAx-2{(B^TA)}^T} \\
&= \mathbf{2A^TAx-2{A^TB}}
\end{aligned}
$$
令$\frac{\partial{f(\mathbf{x})}}{\partial{\mathbf{x}}}=0$得到：
$$
\mathbf{2A^TAx-2{A^TB}} = 0 \\
\mathbf{x} = \mathbf{{(A^TA)}^{-1}A^TB}
$$


因此，当$\mathbf{{A^TA}}$的逆存在时，可以解得极值点$\mathbf{x}$

易证明海森矩阵$\frac{\partial^2f(\mathbf{x})}{\partial{x}\partial{x}}$为正定矩阵，因此$\mathbf{x}$为极小值点。

##### 举例

假如观测点为(0, 6)、(1, 0)、(2, 0)，欲拟合形式为$y = x_0 + x_1t$的直线（变量为t，参数为$x_0, x_1$）

那么$\mathbf{A}$为
$$
\left[
\begin{matrix}
1 & 0 \\
1 & 1 \\
1 & 2
\end{matrix}
\right]
$$
$\mathbf{x}$为
$$
\left[
\begin{matrix}
x_0 \\
x_1
\end{matrix}
\right]
$$
$\mathbf{B}$为
$$
\left[
\begin{matrix}
6 \\
0 \\
0
\end{matrix}
\right]
$$
使用此结论代入求得
$$
\begin{aligned}
\mathbf{x} = \left[
\begin{matrix}
5 \\
-3
\end{matrix}
\right]
\end{aligned}
$$
所以拟合直线为$y = 5 + -3t$