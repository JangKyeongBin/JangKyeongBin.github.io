---
title : "슈트라센 알고리즘"
layout : single
categories : 
 - jekyll
 - minimal-mistakes
tags :
 - github pages
 - jekyll
 - minimal-mistakes
use_math : true
date : "2020-04-08 17:00"
---

### 슈트라센 알고리즘

---

$$
A=\begin{bmatrix}
A_{1,1}&A_{1,2}\\
A_{2,1}&A_{2,2}
\end{bmatrix},
B=\begin{bmatrix}
B_{1,1}&B_{1,2}\\
B_{2,1}&B_{2,2}
\end{bmatrix},
 C=\begin{bmatrix}
C_{1,1}&C_{1,2}\\
C_{2,1}&C_{2,2}
\end{bmatrix}
$$

위와 같이 세개의 행렬이 있다.

A행렬과 B행렬을 곱해 C행렬을 구하고자 할 때 

우리는 아래와 같은 방법을 이용했다.


$$
C_{1,1}= A_{1,1} B_{1,1} + A_{1,2} B_{2,1}\\
C_{1,2}= A_{1,1} B_{1,2} + A_{1,2} B_{2,2}\\
C_{2,1}= A_{2,1} B_{1,1} + A_{2,2} B_{2,1}\\
C_{2,2}= A_{2,1} B_{1,2} + A_{2,2} B_{2,2}
$$

이 때,
$$
A_{i,j},B_{i,j},C_{i,j}\in F^{2^n\times2^n}
$$


이러한 방법은 단순한 2x2 행렬에서는 문제 없겠지만 n이 커질수록 계산시간은 비약적으로 증가한다.

이를 해결하고자 슈트라센은 슈트라센 알고리즘이란걸 만들었다고 한다.

#### '행렬을 쪼개서 계산하다' 라는게 기본 아이디어다.





$$
\begin{align}
M_1 &=(A_{1,1}+A_{2,2})(B_{1,1}+B_{2,2})\\
M_2 &= (A_{2,1}+A_{2,2})B_{1,1}\\
M_3 &= A_{1,1}(B_{1,2}-B_{2,2})\\
M_4 &= A_{2,2}(B_{2,1}-B_{1,1})\\
M_5 &= (A_{1,1}+A_{1,2})B_{2,2}\\
M_6 &= (A_{2,1}-A_{1,1})(B_{1,1}+B_{1,2})\\
M_7 & = (A_{1,2}-A_{2,2})(B_{2,1}+B_{2,2})\\
\end{align}
$$



$$
\begin{align}
M_{k}를& C_{i,j}에 대해 바꿔주면\\
C_{1,1}=&M_1 + M_4 - M_5 + M_7\\
C_{1,2}=&M_3 + M_5 \\
C_{2,1}=&M_2 + M_4\\
C_{2,2}=&M_1 - M_2 + M_3 + M_6\\

\end{align}
$$





증명

$$
\begin{align}
C_1&= -P_2+P_4+P_5+P_6\\
&=(-A_1B_4-A_2B_4)+P_4+(A_1B_1+A_1B_4+A_4B_1+A_4B_4)+P_6\\
&=-A_2B_4+(A_4B_3-A_4B_1)+A_1B_1+A_4B_1+A_4B_4+P_6\\
&=-A_2B_4+A_4B_3+A_1B_1+A_4B_4+(A_2B_3+A_2A_4-A_4B_3-A_4B_4)\\
&=A_1B_1+A_2B_3\\
\\
C_2&=P_1+P_2\\
&=(A_1B_2-A_1B_4)+(A_1B_4+A_2B_4)\\
&=A_1B_2+A_2B_4\\
\\
C_3 &= P_3+P_4\\
&=(A_3B_1+A_4B_1)+(A_4B_3-A_4B_1)\\
&=A_3B_1+A_4B_3\\
\\
C_4&=P_1-P_3+P_5+P_7\\
&=(A_1B_2-A_1B_4)-P_3+(A_1B_1+A_1B_4+A_4B_1+A_4B_4)+P_7\\
&=A_1B_2-A_3B_1+A_1B_1+A_4B_4+(A_3B_1+A_3B_2-A_1B_1-A_1B_2)\\
&=A_3B_2+A_4B_4\\
\end{align}
$$

이 과정을 재귀적으로 반복할 경우 총 ![{\displaystyle 7\cdot n^{\log _{2}7}-6\cdot n^{2}}](https://wikimedia.org/api/rest_v1/media/math/render/svg/586e85e6ba93daf1db18e144da90a79af278e9a9)번의 연산이 필요하다

슈트라센 알고리즘은 속도에 비해 수치 안정성이 떨어지는 것으로 알려져 있다. 두 행렬 *A*와 *B*를 곱한 결과를 C라 할 때, 실제 오차인 ![{\displaystyle 27n^{2}u\lVert A\rVert \lVert B\rVert +O(u^{2})}](https://wikimedia.org/api/rest_v1/media/math/render/svg/892fed34761231c6ae447382f89caa717b376a46)보다 작음이 알려져 있다. 이는 일반적인 행렬 곱셈보다 더 큰 오차이다.