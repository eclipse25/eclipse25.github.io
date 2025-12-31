---
layout: post
title: "[선형대수학] 행렬의 연산(Operations)"
date: 2024-01-31 08:00:00 +0900
categories: [CS, Math, Linear Algebra]
tags: [Math, Linear Algebra, ML, Numpy]
use_math: true
---

## 행렬의 연산(Operations)

### 전치(Transpose)

- 행렬을 전치한다는 것은 그 행렬을 뒤집는 것이다.
- 행렬 $A\in \mathbb{R}^{m\times n}$이 주어졌을 때 그것의 전치행렬은 $A^T \in \mathbb{R}^{n\times m}$으로 표시하고 각 원소는 다음과 같이 주어진다.

$$\left( A^T \right)_{ij} = A_{ji}$$

$$
$ A^T =
\begin{bmatrix}
  1 & 2 & 3 \\
  4 & 5 & 6
\end{bmatrix}^T =
\begin{bmatrix}
  1 & 4 \\
  2 & 5 \\
  3 & 6
\end{bmatrix}$
$$

- 다음의 성질들이 성립한다.

  - $(A^T)^T = A$
  - $\left(AB\right)^T = B^TA^T$
  - $(A + B)^T = A^T + B^T$

- Numpy의 `T` 속성(attribute)을 사용해서 전치행렬을 구할 수 있다.

```python
A = np.array([
[1,2,3],
[4,5,6]
])

A.T
#array([[1, 4],
#       [2, 5],
#       [3, 6]])

A.T.T
#array([[1, 2, 3],
#       [4, 5, 6]])

B = np.array([[1,2], [4, 5], [6, 7]])
B
#array([[1, 2],
#       [4, 5],
#       [6, 7]])

np.matmul(A, B).T
#array([[27, 60],
#       [33, 75]])

np.matmul(B.T, A.T)
#array([[27, 60],
#       [33, 75]])

B = np.array([[1,2,3], [4, 5, 6]])
(A + B).T
#array([[ 2,  8],
#       [ 4, 10],
#       [ 6, 12]])

A.T + B.T
#array([[ 2,  8],
#       [ 4, 10],
#       [ 6, 12]])
```

### 대칭행렬(Symmetic Matrices)

- 정방행렬 $A$가 $A^T$와 동일할 때 $A$는 대칭행렬이다.
- $A = -A^T$일 때는 반대칭(anti-symmetric)행렬이다.
- $AA^T$는 항상 대칭행렬이다.
- $A + A^T$는 대칭, $A - A^T$는 반대칭이다.

$$A = \frac{1}{2}(A+A^T)+\frac{1}{2}(A-A^T)$$

```python
np.matmul(A, A.T)
#array([[14, 32],
#       [32, 77]])

np.matmul(A.T, A)
#array([[17, 22, 27],
#       [22, 29, 36],
#       [27, 36, 45]])
```

### 대각합(Trace)

- 대각합(Trace)은 정사각(정방) 행렬에서 주 대각선에 위치한 요소들의 합을 말한다.
  - 주 대각선이란 행렬의 왼쪽 위에서 오른쪽 아래로 이어지는 대각선을 의미한다.
- 정방행렬 $A\in \mathbb{R}^{n\times n}$의 대각합은 $\mathrm{tr}(A)$ 또는 $\mathrm{tr}A$로 표시하고 그 값은 $\sum_{i=1}^n A_{ii}$이다.<br>

대각합은 다음과 같은 성질을 가진다.

- For $A\in \mathbb{R}^{n\times n}$, $\mathrm{tr}A = \mathrm{tr}A^T$
- For $A,B\in \mathbb{R}^{n\times n}$, $\mathrm{tr}(A+B) = \mathrm{tr}A + \mathrm{tr}B$
- For $A\in \mathbb{R}^{n\times n}, t\in\mathbb{R}$, $\mathrm{tr}(tA) = t\,\mathrm{tr}A$
- For $A, B$ such that $AB$ is square, $\mathrm{tr}AB = \mathrm{tr}BA$
- For $A, B, C$ such that $ABC$ is square, $\mathrm{tr}ABC = \mathrm{tr}BCA = \mathrm{tr}CAB$, and so on for the product of more matrices

```python
A = np.array([
        [100, 200, 300],
        [ 10,  20,  30],
        [  1,   2,   3],
    ])
np.trace(A)
#123
```

### Norms

- 벡터의 norm은 벡터의 길이를 말한다.
- $l_2$ norm (Euclidean norm)은 다음과 같이 정의된다.

$$\left \Vert x \right \|_2 = \sqrt{\sum_{i=1}^n{x_i}^2}$$

- $\left \Vert x \right \|_2^2 = x^Tx$이다.

```python
import numpy.linalg as LA
LA.norm(np.array([3, 4]))
#5.0
```

- $l_p$ norm

  $$\left \Vert x \right \|_p = \left(\sum_{i=1}^n|{x_i}|^p\right)^{1/p}$$

- Frobenius norm

  - 행렬의 크기를 측정하는 방법 중 하나이다.
  - 행렬의 모든 요소의 제곱들의 합의 제곱근으로 계산된다.
  - 행렬의 모든 요소를 개별적으로 고려하기 때문에, 행렬 내의 모든 요소의 크기를 종합적으로 파악할 수 있는 척도를 제공한다.
  - 행렬 차이의 '거리'를 측정하는 데에도 사용되며, 예를 들어 머신러닝에서 두 행렬 간의 차이를 비교할 때 사용될 수 있는데, 행렬이나 벡터 간의 유사도를 평가하는 데 유용하다.

  $$\left \Vert A \right \|_F = \sqrt{\sum_{i=1}^m\sum_{j=1}^n A_{ij}^2} = \sqrt{\mathrm{tr}(A^TA)}$$

  - 특수한 경우: $A$가 벡터 $x$일 때

  $$
  $\begin{align}
  \left \Vert A \right \|_F  &= \left \Vert x \right \|_F = \left \Vert x \right \|_2\\
  \mathrm{tr}(A^TA) &= \mathrm{tr}(x^Tx) = x^Tx\\
  \left \Vert A \right \|_F^2 &= \mathrm{tr}(A^TA)
  \end{align}
  $
  $$

  ```python
  A = np.array([
          [100, 200, 300],
          [ 10,  20,  30],
          [  1,   2,   3],
      ])

  LA.norm(A)
  #376.0505285197722

  np.trace(A.T.dot(A))**0.5
  #376.0505285197722
  ```
