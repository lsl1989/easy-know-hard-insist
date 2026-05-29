---
id: linear-no-1
title: 基础知识 （1）
---
## 线性代数基础知识 （1）

### 行列式

什么是行列式？

矩阵A 的行列式记为det(A)
$$
\left|
\begin{matrix}
 a_{11} & a_{12} \\
 a_{21} & a_{22} \\
\end{matrix}
\right|
or
 \left|
\begin{matrix}
 1      & 2      & \cdots & 4      \\
 7      & 6      & \cdots & 5      \\
 \vdots & \vdots & \ddots & \vdots \\
 8      & 9      & \cdots & 0      \\
\end{matrix}
\right|
$$

### 行列式的三种定义方式

1. 行列式
$
\left|
\begin{matrix}
 a_{11} & a_{12} \\
 a_{21} & a_{22} \\
\end{matrix}
\right|
$
可以看做是以这两个二维向量$(a_{11}, a_{12})$和$(a_{21}, a_{22})$为临边的平行四边形的面积。
将这个结论推广: **n阶行列式是由n维向量组成的,其结果为以这n个向量为邻边的n维图形的体积**
2. 逆序数定义法

> 理解什么是逆序数,
> 设A为一个有n个数字的有序集（n>1），其中所有数字各不相同。
> 如果存在正整数i, j使得1 ≤ i ＜ j ≤ n而且A[i] ＞ A[j]，则`<A[i], A[j]>`这一个有序对称为A的一个逆序对，也称作逆序。逆序对的数量称作逆序数。
> 例如：数组`<2,3,8,6,1>`的逆序对为：`<2,1>` `<3,1>` `<8,1>` `<8,6>` `<6,1>`共5个逆序对。
> -- 来自[维基百科](https://zh.wikipedia.org/wiki/%E9%80%86%E5%BA%8F%E5%AF%B9)

n(n>2)阶行列式
$$
\left|\begin{matrix}
a_{11} & a_{12} & \cdots & a_{1n}  \\
a_{21} & a_{22} & \cdots & a_{2n}  \\
\vdots & \vdots & \ddots & \vdots   \\
a_{n1} & a_{n2} & \cdots & a_{nn}  \\
\end{matrix}\right|
= \Sigma_{j1, j2, \cdots, jn}(-1)^{\tau(j1, j2, \cdots, jn)}a_{1j_1}a_{2j_2} \cdots a{nj_n}
$$

3. 行列式的值等于行列式的某行(列)元素分别乘其相对应的代数余子式后再求和,其核心思想是降阶

### 行列式基本性质

* 行列式 D 按行按列转置，记为  $D^T$, 行列式与转制后的行列式值相等， 即$D = D^T$
  * 即行列式中，所有对行生效的性质，对列也同样生效
$$
\left|
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{matrix}
\right|
=
\left|
\begin{matrix}
1 & 4 & 7 \\
2 & 5 & 8 \\
3 & 6 & 9 \\
\end{matrix}
\right|
$$
* 行列式的某一行乘以系数k，等于行列式的值乘以该系数k
  * 推论 若行列式某一行全为0，则行列式的值等于0
$$
\left|
\begin{matrix}
1 & 2 & 3 \\
4k & 5k & 6k \\
7 & 8 & 9 \\
\end{matrix}
\right|
=
k\left|
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{matrix}
\right|
$$
* 行列式若某一行的元素都是两数之和，则行列式可按改行拆为两个行列式之和，（即改行换为两行，其他各行保持不变）
$$
\left|
\begin{matrix}
1 & 2 & 3 \\
4 + 3 & 5 + 7 & 6 + 2 \\
7 & 8 & 9 \\
\end{matrix}
\right|
=
\left|\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{matrix}\right| +
\left|\begin{matrix}
1 & 2 & 3 \\
3 & 7 & 2 \\
7 & 8 & 9 \\
\end{matrix}\right|
$$
* 行列式两行互换，行列式变号（乘以-1）
$$
\left|
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{matrix}
\right|
=
-\left|
\begin{matrix}
4 & 5 & 6 \\
1 & 2 & 3 \\
7 & 8 & 9 \\
\end{matrix}
\right|
$$
* 行列式两行相同，则行列式等于0
  * 若行列式中有两行成比例，则该行列式也等于0 （同性质2可一同推导出）
$$
\left|
\begin{matrix}
1 & 2 & 3 \\
1k & 2k & 3k \\
7 & 8 & 9 \\
\end{matrix}
\right|
= k
\left|
\begin{matrix}
1 & 2 & 3 \\
1 & 2 & 3 \\
7 & 8 & 9 \\
\end{matrix}
\right|
=0
$$
* 将行列式的某一行乘以一个系数后加到另一行对应的元素中，行列式不变。（通常用此法将一个行列式转为倒三角形，然后将对角线的元素相乘得到行列式的值）

$$
\left|
\begin{matrix}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9 \\
\end{matrix}
\right| =
\left|
\begin{matrix}
1 & 2 & 3 \\
4 + 1k & 5 + 2k & 6 + 3k \\
7 & 8 & 9 \\
\end{matrix}
\right|
$$
例: 利用该性质计算行列式的值
>
> 1. 通常思路是从上到下从左到右将行列式变换为倒三角行列式
> 2. 可以先将左上角的数转为1， 然后下面每一行先减去第一行乘以一个数N,将每一行第一列数转为0
> 3. 同上面的步骤用第二行第二列的数将第二行之后的每一行的第二列转为0
> 4. 重复操作直至行列式变为倒三角行列式，即对角线下面的所有数都是0，利用倒三角行列式的值等于对角线数的乘积得到行列式的值
$$
\begin{aligned}
\left|\begin{matrix}
3 & 4 & 2 & 9 \\
1 & 0 & 1 & 7 \\
5 & 6 & 1 & 8 \\
2 & 2 & 8 & 9 \\
\end{matrix}\right|
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
3 & 4 & 2 & 9 \\
5 & 6 & 1 & 8 \\
2 & 2 & 8 & 9 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
3 - 1 *3 & 4 - 0* 3 & 2 - 1*3 & 9 - 7* 3 \\
5 & 6 & 1 & 8 \\
2 & 2 & 8 & 9 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & -1 & -12 \\
5 & 6 & 1 & 8 \\
2 & 2 & 8 & 9 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & -1 & -12 \\
5 - 1*5 & 6- 0* 5 & 1 - 1 *5 & 8 - 7* 5 \\
2 - 1 *2 & 2 - 0* 2 & 8 - 1 *2 & 9 - 7* 2 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & 2 & 9 \\
0 & 6 & -4 & -27 \\
0 & 2 & 6 & -5 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & 2 & 9 \\
0 & 6 - 4 *6/4 & -4 - 2* 6/4 & -27 - 9*6/4\\
0 & 2 - 4 /2 & 6 - 2/2 & -5 - 9/2 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & 2 & 9 \\
0 & 0 & -7 & -81/2 \\
0 & 0 & 5 & -19/2 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & 2 & 9 \\
0 & 0 & -7 & -81/2 \\
0 & 0 & 5 +(-7)/5 & -19/2 + (-81/2) / 5 \\
\end{matrix}\right| \\
&=
-\left|\begin{matrix}
1 & 0 & 1 & 7 \\
0 & 4 & 2 & 9 \\
0 & 0 & -7 & -81/2 \\
0 & 0 & 0 & -176 / 10\\
\end{matrix}\right| \\
&=
-(1* 4 *(-7)* (-176/ 10)) \\
&=-4928 / 10
\end{aligned}
$$
