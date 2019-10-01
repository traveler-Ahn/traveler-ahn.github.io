---
layout: post
title:  "2019/09/30 [선형대수학 #1] 주요용어 및 기본 공식"
subtitle: "2019/09/30 [선형대수학 #1] 주요용어 및 기본 공식"
categories: mathmatics
tags: LinearAlgebra
comments: true
---

- 선형대수 정리
	- 딥러닝에 필요한 선형대수 리마인드를 위한 복습
	- **[선형대수학 #1] 주요용어 및 기본 공식**
	- 거의 대부분 이곳을 [참조(선이해...후타이핑..)](https://darkpgmr.tistory.com/103?category=460967)하였습니다.

---

# [선형대수학 #1] 주요용어 및 기본 공식
- 선형대수의 핵심을 다루는 글
  - 고유값(eigen value)과 고유벡터(eigen vector)
  - 행렬의 대각화 >> 고유값 분해(eigen decomposition)
  - 행렬 분해 >> 특이값 분해(SVD, singular value decomposition)
  - 케일리-해밀턴 정리
  - 행렬식(determinant)
  - 최소자승법(least-square)과 선형 연립방정식의 풀이
  - 주성분분석(PCA, principal component analysis)



- 첫 번째 내용은 선형 대수학에 나오는 기본 용어 및 성질(정리, 공식)에 대한 단순 요약입니다.
- latext markdown 표기 [cheatsheet](https://www.codecogs.com/latex/eqneditor.php)



#### 1. 선형대수학이란?

선형대수학은  선형 함수(or 사상, 연산, 변환)에 대한 대수학으로서, 여기서 선형(linear)은 다음 관계식으로 정의된다.


$$
f(ax+by) =af(x)+bf(y) --- (1)
$$


우리가 알고있는 행렬연산, 벡터연산, 미분, 적분 등이 위 관계식을 만족하는 선형 함수(연산)에 해당된다.

또한, 대수학은 대수라는 명칭 그대로 수를 대신하여 문자를 사용해 식을 전개하여 방정식을 푸는 방법을 연구하는 수학 분야이다.



#### 2. 선형대수학 기초

해당 글을 참조해 봅시다. [http://blog.daum.net/eigenvalue/10856412](http://blog.daum.net/eigenvalue/10856412)



#### 3. 선형대수학에서 나오는 용어 및 성질

- 행렬(matrix) & 벡터(vector) 표기

$$
\begin{pmatrix}
 a_{11} & \cdots & a_{1n} \\ 
 \vdots & \ddots & \vdots \\ 
 a_{n1} & \cdots & a_{nn}
\end{pmatrix}
,
\mathbf{x} = \begin{pmatrix}
              X_{1} \\
              \vdots \\
              X_{n}
             \end{pmatrix}
(A: m \times x, \mathbf{x}: column\ vector)
$$

- 정방 행렬(square matrix)

$$
A = \begin{pmatrix}
     a_{11} & \cdots & a_{1n} \\ 
     \vdots & \ddots & \vdots \\ 
     a_{n1} & \cdots & a_{nn}
    \end{pmatrix}
$$



- 단위 행렬(identity matrix)

$$
AE = EA = A
$$

$$
E = \begin{pmatrix}
     1 & 0 \\ 
     0 & 1
    \end{pmatrix},
E = \begin{pmatrix}
     1 & 0 & 0 \\ 
     0 & 1 & 0 \\
     0 & 0 & 1
    \end{pmatrix},
\ \cdots
$$



- 전치 행렬(transpose of a matrix)

$$
\begin{matrix}
(AB)^{T}=B^{T}A^{T} \\
(A+B)^{T}=A^{T}+B^{T} \\
det(A^{T})=det(A) \\
\left \| \mathbf{x} \right \|^{2} = \mathbf{x}^{T}\mathbf{x} = \mathbf{x}\cdot\mathbf{x}
\end{matrix}
$$

$$
A=\begin{pmatrix}
    a & b & c \\
    d & e & f \\
    g & h & i
  \end{pmatrix} \rightarrow 
A^{T}=\begin{pmatrix}
        a & d & g \\
        b & e & h \\
        c & f & i
      \end{pmatrix}
$$

$$
A=\begin{pmatrix}
    a & b & c \\
    d & e & f
  \end{pmatrix}
\rightarrow 
A^{T}=\begin{pmatrix}
        a & d \\
        b & e \\
        c & f
      \end{pmatrix}, (2 \times 3 \rightarrow 3 \times 2)
$$

- 행렬식 (determinant): 정방행렬에 대해서만 정의됨

$$
A=\begin{pmatrix}
	a & b \\
	c & d 
  \end{pmatrix} \rightarrow 
det(A)=ad-bc
$$

$$
A=\begin{pmatrix}
	a & b & c \\
	d & e & f \\ 
	g & h & i
  \end{pmatrix} \rightarrow 
det(A)=a(ei-fh)-b(di-fg)+c(dh-eg)
$$

$$
det(AB)=det(A)det(B) \ (A,B: same \ size \ square \ matrix)
$$

$$
det(A^{T}) = det(A)
$$

$$
det(A^{-1})=\frac{1}{det(A)}
$$

$$
det(cA) = c^{n}det(A) \ (A: n \times n \ square \ matrix)
$$

- 대각 행렬 (diagonal matrix): 보통 정방행렬에 대해 정의

$$
D=diag(a_1,a_2,\cdots,a_n)
$$

$$
D^{k}=diag(a_{1}^{k},a_{2}^{k},\cdots,a_{n}^{k})
$$

$$
D^{-1}=diag(\frac{1}{a_1},\frac{1}{a_2},\cdots,\frac{1}{a_n})
$$

$$
D^{T}=D
$$

$$
\begin{matrix}
det(D)=a_1a_2\cdots a_n \\
diag(a_1, a_2)=\begin{pmatrix}
				 a_1 & 0 \\
				 0 & a_2
			   \end{pmatrix},
diag(a_1, a_2, a_3)=\begin{pmatrix}
                      a_1 & 0 & 0 \\
                      0 & a_2 & 0 \\
                      0 & 0 & a_3
                    \end{pmatrix}
\end{matrix}
$$

- 고유 값(eigen value), 고유벡터(eigen vector)

$$
\begin{matrix}
A\mathbf{e_{i}} = \lambda_{i}\mathbf{e_{i}} \rightarrow \lambda_{i}: eigen \ value \ of \ matrix \ A \\ \ \\
\mathbf{e_{i}}: eigen \ vector \ of \ \lambda_{i} \ of \ matrix \ A
\end{matrix}
$$

- 행렬의 대각화 : 고유값 분해(eigen decomposition)

$$
\begin{matrix}
A=PDP^{-1}=(\mathbf{e_{i}}\cdots\mathbf{e_{n}})diag(\lambda_{1},\cdots,\lambda_{n})(\mathbf{e_{i}}\cdots\mathbf{e_{n}})^{-1} \\
D: Diagonal \ matrix \ of \ eigenvalue(\lambda) \\
P: Column \ vector \ is \ eigen \ vector \\ \ \\
det(A) = det(D) = \lambda_{1}\cdots\lambda_{n} \\ \ \\
A^{k}=PD^{k}P^{-1}=Pdiag(\lambda_{1}^{k},\cdots,\lambda_{n}^{k})P^{-1}
\end{matrix}
$$

> 고유 값 분해 대각화는 모든 행렬에 대해 가능한 것이 아니라 **<u>정방행렬 A가 n개의 일차 독립(linearly independent)인 eigen vector를 가질 때</u>**만 가능하다.

- 특성 방정식(characteristic equation)

$$
\begin{matrix}
\lambda E-A : (characteristic \ matrix \ of \ A) \\ \ \\
p(\lambda)=det(\lambda E-A) :  (characteristic \ polynomial) \\ \ \\
det(\lambda E-A)=0 : (characteristic \ equation)
\end{matrix}
$$



- 케일리-해밀턴 정리(Cayley-Hamilton theorem)
- 특정 조건을 만족하는 행렬의 명칭

$$
\begin{matrix}
AA^{T} = A^{T}A = E: orthogonal \ matrix \\ \ \\
A^{T}=A:symmetric \ matrix \\ \ \\
AA^{*}=A^{*}A=E:unitary \ matrix \ (A^{*}=\overline{A^{T}}:conjugate \ transpose) \\ \ \\
A^{*}=A:Hermitian \ matrix
\end{matrix}
$$



- 특이 값 분해 (SVD)

$$
\begin{matrix}
A=U\Sigma V^{T} \ (In \ Complex\ Space \ A=U\Sigma V^{*}) \\ \ \\
A^{T}A=V(\Sigma^{T}\Sigma)V^{T} \ (eigen \ decomposition) \\ \ \\
AA^{T}=U(\Sigma\Sigma^{T})U^{T} \ (eigen \ decomposition) \\ \ \\
\Sigma=\begin{pmatrix}
		\sigma_{1} & \ \\
		           & \ddots \\
		           & \ & \sigma_{s} \\
		           & & 0
	   \end{pmatrix} \ or \\
\Sigma=\begin{pmatrix}
		\sigma_{1} & \ \\
		           & \ddots \\
		           & \ & \sigma_{s} & 0
	   \end{pmatrix} \\ \ \\
U \ Column \ vector: AA^{T} \ eigen \ vector \ (left-singular \ vectors) \\
V \ Column \ vector: A^{T}A \ eigen \ vector \ (right-singular \ vectors) \\
\Sigma: square \ root \ of \ eigen \ values \ A^{T}A, \ AA^{T} \ (singular \ values)
\end{matrix}
$$

>특이값 분해는 모든 행렬에 대해 가능하다. (정방행렬 or 직사각행렬)
>
>A: m x n, U: m x m, V: n x n, Σ: m x n



- 선형대수 첫 글은 대 부분 latex 수식 연습용인듯...OTL