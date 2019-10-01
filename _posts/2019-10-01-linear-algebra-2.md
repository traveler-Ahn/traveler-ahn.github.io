---
layout: post
title:  "2019/10/01 [선형대수학 #2] 역행렬과 행렬식"
subtitle: "2019/10/01 [선형대수학 #2] 역행렬과 행렬식"
categories: mathmatics
tags: LinearAlgebra
comments: true
---

- 선형대수 정리
	- 딥러닝에 필요한 선형대수 리마인드를 위한 복습
	- **[선형대수학 #2] 역행렬과 행렬식(determinant)**
	- 거의 대부분 이곳을 [참조(선이해...후타이핑..)](https://darkpgmr.tistory.com/104)하였습니다.

---

# [선형대수학 #2] 역행렬과 행렬식
- 선형대수학 중 역행렬과 행렬식(determinant)에 대한 내용을 주로 활용적인 측면에 초점을 맞추어 정리함
- latext markdown 표기 cheatsheet (https://www.codecogs.com/latex/eqneditor.php)



#### 1. 역행렬(Inverse Matrix)과 선형연립방정식

**1) 역행렬의 정의**

행렬 A의 역행렬은 A와 곱해서 항등행렬 E가 나오는 행렬을 A의 역행렬이라고 정의한다.


$$
AB=BA=E \ \cdots (1)
$$


위 식과 같이 A와 곱해서 E가 나오게 하는 행렬 B를 A의 역행렬이라고, 다음과 같이 표기한다.


$$
\begin{matrix}
B: Inverse \ matrix \ of \ A \\ \ \\
B = A^{-1} \ \cdots (2)
\end{matrix}
$$


**2) 역행렬의 활용**

가장 큰 활용처는 선형방정식을 풀 때 활용될 수 있다.


$$
\begin{matrix}
a_{11}x_{1}+a_{12}x_{2}+\cdots+a_{1n}x_{n}=b_{1} \\
a_{21}x_{1}+a_{22}x_{2}+\cdots+a_{2n}x_{n}=b_{2} \\
\vdots \\
a_{n1}x_{1}+a_{n2}x_{2}+\cdots+a_{nn}x_{n}=b_{n}
\end{matrix}
$$


위와 같은 x에 대한 선형 연립방정식(a, b는 상수)을 행렬로 표현하면


$$
\begin{matrix}
\begin{pmatrix}
  a_{11} & \cdots & a_{1n} \\
  \vdots & \ddots & \vdots \\
  a_{n1} & \cdots & a_{nn}
\end{pmatrix}
\begin{pmatrix}
  X_{1} \\
  \vdots \\
  X_{n}
\end{pmatrix} = 
\begin{pmatrix}
  b_{1} \\
  \vdots \\
  b_{n}
\end{pmatrix} \\ \ \\

AX = B
\end{matrix}
$$


위와 같이 매우 간단하게 표현 될 수 있다.



이제 A의 역행렬만 계산하면, 위의 연립방정식의 해는 


$$
X=A^{-1}B
$$


로 손쉽게 계산될 수 있다.



만일, A의 역행렬이 존재하지 않는 경우는, 위의 선형방정식의 해가 유일하게 결정되지 않는 경우로서 

​	(1) 해가 무수히 많거나, 

​	(2) 해가 존재하지 않는 경우이다.



**3) 역행렬의 계산**



**4) 역행렬의 성질**

역행렬은 n x n 정방행렬에 대해서만 정의되며(정방행렬이 아닌 경우도 pseudo-inverse 존재함), 역행렬은 존재할 수도 있고, 존재하지 않을 수도 있따. 하지만 만일 존재한다면 역행렬은 유일하다.

또한, 역행렬은 다음과 같은 기본 성질을 만족한다.


$$
(AB)^{-1} = B^{-1}A^{-1}
$$


즉, AB의 역행렬은 각각의 역행렬을 구한 후 순서를 바꾸어 곱한 결과와 같다.



#### 2. 행렬식(determinant)과 기하학적 활용

- 행렬식(determinant)은 딱히 정의(definition)가 없다. 그냥 어떤 특별한 계산식에 따라 행렬의 원소들을 대입하여 얻은 결과 값(수치)을 지칭한다. 즉, 주어진 행렬에 대해 계산되는 하나의 숫자 값이다. 다만, 그 결과 값이 그 행렬의 특성을 결정짓는 중요한 값이기에 특정한 이름을 붙여 determinant라고 한다.

- 행렬식(determinant) 또한 역행렬과 마찬가지로 정방행렬에 대해서만 정의된다.



**1) 행렬식 표기**

다음과 같이 det(A) 또는 행렬의 괄호를 직선으로 나타내어 표기하면 그 행렬의 행렬식임을 나타낸다.


$$
\begin{matrix}
det(A) \ or \ 
\begin{vmatrix}
  a_{11} & \cdots & a_{1n} \\
  \vdots & \ddots & \vdots \\
  a_{n1} & \cdots & a_{nn}
\end{vmatrix}
\end{matrix}
$$


**2) 행렬식의 활용**

  어떤 행렬 A의 행렬식 값 det(A) = 0이면 행렬 A는 역행렬을 갖지 않고, det(A) ≠ 0이면 A의 역행렬이 존재한다. 즉, 행렬식은 어떤 행렬의 역행렬 존재여부에 대해서 판별값 역할을 한다.



  X를  [x, y]T, [x, y, z]T 등과 같이 좌표를 나타내는 벡터라고 했을 때, 행렬 A를 X' = AX 와 같이 사용하면 행렬 A는 입력좌표 X를 X'으로 변환시켜주는 일종의 **<u>선형변환(linear transformation)</u>**으로 해석할 수 있다.



  이러한 관점에서 det(A)는 선형변환의 스케일(scale) 성분을 나타내는 값이다. 즉, 도형 P가 선형변환 A에 의해 P'으로 변환되었을 경우, 다음과 같은 수식이 성립한다.


$$
\begin{matrix}
P'=AP \\ \ \\
Area(P')=|det(A)|\times Area(P) \ \ (2-Dimension) \\ \ \\
Volume(P')=|det(A)|\times Volume(P) \ \ (3-Dimension)
\end{matrix}
$$



  또한, determinant의 부호도 중요한 의미를 갖는데, det(A) > 0이면 도형의 방향(orientation)이 보존되고 det(A) < 0이면 도형의 방향이 보존되지 않는다.



**[2-Dim ex.1]**

네 점 (1,1), (1,2), (2,2), (2,1)로 이루어진 도형 P를 2 × 2 행렬 A로 선형변환한 예

<img src="https://drive.google.com/uc?id=1hPPd4T-_wVuGdgwglFpuGT4Sf-EEkC9T">

**왼쪽그림**: A = [1 2; -1 3]라면 det(A) = 5이다. 이 때, P는 (3,2), (5,5), (6,4), (4,1)로 변환되고 변환된 도형 P'의 면적을 구해보면 5가 나온다. 즉, Area(P') = det(A)*Area(P)임을 확인할 수 있다. 또한 det(A)>0으므로 도형의 방향(시계방향, 반시계방향)이 보존됨을 확인할 수 있다.

**오른쪽그림**: A = [1 -1; -2 1]인 경우 det(A) = -1이다. 이 때, P는 (0,-1), (-1,0), (0,-2), (1,-3)으로 변환되고 면적을 구해보면 1이 나온다. 또한 도형을 이루는 점들의 방향이 반대가 된 것을 알 수 있다.



**[2-Dim ex.2]**

만일 det(A) = 0인 경우에는 어떤 결과가 나올까?

<img src="https://drive.google.com/uc?id=12eK7av3eDhmHXOe4gP8smzmyaxT9zqdu">

그림에서 det(A) = 0이면 직선(선분)으로 변환됨을 확인할 수 있다. 오른쪽 그림과 같이 좀더 복잡한 도형의 경우에도 역시 직선으로  변환된다. 직선의 면적은 0이므로 Area(P') = abs(det(A))*Area(P)는 여전히 성립함을 알 수 있다.



**[3-Dim ex1.]**

3차원 공간에서의 변환(A가 3x3 행렬)인 경우에는 면적이 부피가 되고, 직선이 평면이 되는 것 외에는 동일한 식이 성립한다.

<img src="https://drive.google.com/uc?id=1nHE6zRlz0EatKLjIg12i_kiWfJoecphG">

  행렬 A = [2,2,1;-1,1,0;3,0,1]을 통해 길이 1인 정육면체를 변환시키면 위 그림과 같이 부피가 7인 평행육면체로 변환된다 (벡터의 외적을 이용하여 실제로 부피를 계산해 보면 7이 나옴을 확인할 수 있다). 즉, 부피(P') = abs(det(A))*부피(P)가 성립함을 확인할 수 있다. 또한 det(A)<0이므로 방향이 보존되지 않아야 한다. 그림을 잘 보면 원래 도형 P를 아무리 회전시켜도 P'이 되지 않음을 확인할 수 있다.



**[3-Dim ex2.]**

3차원 공간에서 det(A) = 0인 경우의 예이다.

<img src="https://drive.google.com/uc?id=17e2koUXTf9k_Dz8ravBNmWOM5UHQevIl">

  언뜻 보면 육면체로 변환된 것 같지만 사실은 모두 xy평면(z = 0)으로 변환된 것이며 따라서 P'의 부피는 0이다. 즉, 3차원의 경우에는 det(A) = 0이면 동일 평면상의 점들로 변환됨을 알 수 있다 (또는 A에 따라서는 모든 점들이 하나의 점으로 변환될 수도 있다).



**3) 행렬식 값의 계산**

실제 행렬식 값을 계산할 필요는 없고, 컴퓨터에 맡기면 된다. 간단한 2x2, 3x3 행렬의 행렬식 계산은 다음과 같다.


$$
\begin{matrix}
\begin{vmatrix}
  a & b \\
  c & d
\end{vmatrix} = ad - bc \\ \ \\ 
\begin{vmatrix}
  a & b & c \\
  d & e & f \\
  g & h & i
\end{vmatrix} = a(ei-fh)-b(di-fg)+c(dh-eg)
\end{matrix}
$$



**4) 행렬식(determinant) 주요 성질**


$$
det(AB) = det(A)det(B)
$$


다만, 행렬식은 정방행렬일 경우에만 정의되므로 위의 식을 행렬 A, B 모두 정방행렬일 경우에만 성립한다.



기타 행렬식에 대한 주요 성질들은 다음과 같다.


$$
\begin{matrix}
det(A^{T})=det(A) \\ \ \\
det(A^{-1}) = \frac{1}{det(A)} \\ \ \\
det(PAP^{-1})=det(A) \\ \ \\
det(cA) = c^{n}det(A) (A \ is \ n\times n \ square \ matrix) \\ \ \\ \ \\
det(diag(a_{11},\cdots,a_{nn}))=
\begin{vmatrix}
  a_{11} & & 0 \\
   & \ddots & \\
  0 & & a_{nn}
\end{vmatrix} = a_{11}a_{22}\cdots a_{nn} \\ \ \\ \ \\
\begin{vmatrix}
  a_{11} & & 0 \\
  \vdots & \ddots & \\
  a_{n1} & \cdots & a_{nn}
\end{vmatrix} = a_{11}a_{22}\cdots a_{nn}
\end{matrix}
$$


  위 기타 행렬식 관련 성질들 중 대각행렬(diagonal matrix) 또는 삼각행렬 (upper/lower triangular matrix)의 행렬식 값은 대각 원소들의 곱이라는 점도 기억하면 좋다.