---
layout: post
title: "[선형대수학] 행렬의 종류와 벡터 공간(Type and Vector Space)"
date: 2024-01-31 07:30:00 +0900
categories: [CS, Math, Linear Algebra]
tags: [Math, Linear Algebra, ML, Numpy]
use_math: true
---

## 행렬의 종류(Type of Matrices)

### 정방행렬(square matrix)

- 행과 열의 개수가 동일한 행렬

  $$
  \begin{bmatrix}
    5 & 9 & 2 \\
    3 & 5 & 7 \\
    8 & 1 & 6
  \end{bmatrix}
  $$

### 상삼각행렬(upper triangular matrix)

- 정방행렬이며 주대각선 아래 원소들이 모두 0인 행렬

  $$
  \begin{bmatrix}
    3 & 8 & 2 \\
    0 & 5 & 7 \\
    0 & 0 & 6
  \end{bmatrix}
  $$

### 하삼각행렬(lower triangular matrix)

- 정방행렬이며 주대각선 위 원소들이 모두 0인 행렬

  $$
  \begin{bmatrix}
    3 & 0 & 0 \\
    3 & 9 & 0 \\
    5 & 1 & 6
  \end{bmatrix}
  $$

### 대각행렬(diagonal matrix)

- 정방행렬이며 주대각선 제외 모든 원소가 0인 행렬

  $$
  \begin{bmatrix}
    4 & 0 & 0 \\
    0 & 5 & 0 \\
    0 & 0 & 6
  \end{bmatrix}
  $$

  - NumPy's `diag` 함수를 사용해서 대각행렬을 생성할 수 있다.

    ```python
    np.diag([4, 5, 6])
    #array([[4, 0, 0],
    #       [0, 5, 0],
    #       [0, 0, 6]])
    ```

### 단위행렬(identity matrix)

- 대각행렬이며 주대각선 원소들이 모두 1. $I$로 표시한다.

  $$
  \begin{bmatrix}
    1 & 0 & 0 \\
    0 & 1 & 0 \\
    0 & 0 & 1
  \end{bmatrix}
  $$

  - 모든 $A\in \mathbb{R}^{m\times n}$에 대해
    $$AI = A = IA$$
  - Numpy의 `eye` 함수를 사용하면 원하는 크기의 단위행렬을 생성할 수 있다.

  ```python
  np.eye(3)
  #array([[1., 0., 0.],
  #       [0., 1., 0.],
  #       [0., 0., 1.]])
  ```

### 역행렬(The Inverse)

- 정방행렬 $A\in \mathbb{R}^{n\times n}$의 역행렬 $A^{-1}$은 다음을 만족하는 정방행렬($\in \mathbb{R}^{n\times n}$)이다.

$$A^{-1}A = I = AA^{-1}$$

- $A$의 역행렬이 존재할 때, $A$를 **_invertible_** 또는 **_non-singular_**하다고 말한다.

  - $A$의 역행렬이 존재하기 위해선 $A$는 full rank여야 한다.(선형독립 글 참고)
  - $(A^{-1})^{-1} = A$
  - $(AB)^{-1} = B^{-1}A^{-1}$
  - $(A^{-1})^T = (A^T)^{-1}$

    ```python
    A = np.array([
        [1, 2],
        [3, 4],
    ])
    LA.inv(A)
    #array([[-2. ,  1. ],
    #       [ 1.5, -0.5]])

    LA.inv(LA.inv(A))
    #array([[1., 2.],
    #       [3., 4.]])
    ```

- $A$의 역행렬이 존재할 때,

  - $Ax = b$
  - $x = A^{-1}b$

### 직교행렬(Orthogonal Matrices)

- $x^Ty=0$가 성립하는 두 벡터 $x, y \in \mathbb{R}^n$를 직교(orthogonal)라고 하고 $\|x\|_2 = 1$인 벡터 $x\in \mathbb{R}^n$를 정규화(normalized)된 벡터라고 부른다.

- 모든 열들이 서로 직교이고 정규화된 정방행렬 $U\in \mathbb{R}^{n\times n}$를 직교행렬이라고 부른다. 따라서 다음이 성립한다.

  - $U^TU = I$
  - $UU^T = I$
  - $U^{-1} = U^T$
  - $\|Ux\|_2 = \|x\|_2$ for any $x\in \mathbb{R}^{n}$
  - $\|Ux\|_2 = \big((Ux)^T(Ux)\big)^{1/2} = \big(x^TU^TUx\big)^{1/2} = (x^Tx)^{1/2} = \|x\|_2$

- 예시 직교행렬 : 두 열 벡터는 서로 직교하며, 또한 정규화되어 있다.

  $$
  Q = \begin{bmatrix}
  \frac{1}{\sqrt{2}} & \frac{1}{\sqrt{2}} \\
  \frac{1}{\sqrt{2}} & -\frac{1}{\sqrt{2}}
  \end{bmatrix}
  $$

---

## 벡터 공간(Vector Space)

### 벡터의 생성(span)

- 벡터의 집합($\{x_1,x_2,\ldots,x_n\}$)에 대한 생성(span)은 이 벡터들의 모든 선형 결합으로 이루어진 집합이다.
- 주어진 벡터들을 사용하여 생성할 수 있는 모든 벡터의 집합을 의미한다.
- 기하학적으로는, 이 벡터들이 이루는 공간을 생각할 수 있다.

$$\mathrm{span}(\{x_1,x_2,\ldots,x_n\}) = \left\{ v : v = \sum_{i=1}^n\alpha_i x_i, \alpha_i \in \mathbb{R} \right\}$$

### 행렬의 치역(range)

- 행렬 $A\in \mathbb{R}^{m\times n}$의 치역 $\mathcal{R}(A)$는 A의 모든 열들에 대한 생성(span)이다.
- 행렬 $A$에 의해 생성될 수 있는 모든 벡터의 집합으로, $A$를 곱하여 얻을 수 있는 벡터 공간을 의미한다.

$$\mathcal{R}(A) = \{ v\in \mathbb{R}^m : v = Ax, x\in \mathbb{R}^n\}$$

### 영공간(nullspace)

- 행렬 $A\in \mathbb{R}^{m\times n}$의 영공간(nullspace) $\mathcal{N}(A)$는 $A$와 곱해졌을 때 0이 되는 모든 벡터들의 집합이다.
- $A$에 의해 "소멸"되는 모든 벡터의 집합이다. 이는 $A$가 특정 방향으로의 정보를 "잃어버린다"는 것을 의미한다.
  $$\mathcal{N}(A) = \{x\in \mathbb{R}^n : Ax = 0\}$$

중요한 성질:
$$\{w : w = u + v, u\in \mathcal{R}(A^T), v \in \mathcal{N}(A)\} = \mathbb{R}^n ~\mathrm{and}~ \mathcal{R}(A^T) \cap \mathcal{N}(A) = \{0\}$$

#### 직교여공간(orthogonal complements)

- $\mathcal{R}(A^T)$와 $\mathcal{N}(A)$를 직교여공간(orthogonal complements)이라고 부르고 $\mathcal{R}(A^T) = \mathcal{N}(A)^\perp$라고 표시한다.
- 하나의 공간이 다른 공간의 직교여집합이라는 것을 의미한다.
- 이 성질은 $\mathbb{R}^n$ 공간을 $\mathcal{R}(A^T)$와 $\mathcal{N}(A)$ 두 부분으로 나눈다는 것을 의미한다.
- 하나는 $A^T$의 치역(즉, $A$의 행 벡터들에 대한 생성)이고, 다른 하나는 $A$의 영공간인데, 이 두 공간은 서로 직교하며, 모든 벡터 $w$는 이 두 공간의 요소들의 합으로 표현될 수 있다.

### 투영(projection)

- 벡터의 투영은 하나의 벡터를 다른 벡터나 벡터 공간 위에 "옮겨 놓는" 연산을 의미한다.
- 특히, $\mathcal{R}(A)$ 위로 벡터 $y\in \mathbb{R}^m$의 투영은 $y$를 행렬 $A$의 치역(열 공간) 위에 가장 가깝게 매핑하는 벡터 $v$를 찾는 과정이다.
- $\mathcal{R}(A)$위로 벡터 $y\in \mathbb{R}^m$의 투영(projection)은 다음과 같이 표현된다.

$$\mathrm{Proj}(y;A) = \mathop{\mathrm{argmin}}_{v\in \mathcal{R}(A)} \| v - y \|_2 = A(A^TA)^{-1}A^Ty$$

#### $U^TU = I$인 정방행렬 $U$는 $UU^T = I$임을 보이기

- $U^TU = I$인 정방행렬이라는 것은 $U$가 정규직교행렬(orthonormal matrix)임을 의미한다. 여기서 $I$는 단위행렬(identity matrix)이고, 이 조건을 만족하는 $U$는 다음과 같은 성질을 가진다:

  - 정의: 모든 열 벡터가 서로 직교하며 각 벡터의 크기가 1인 행렬이다.
  - 성질: $U^TU = I$인 경우, $U$의 역행렬은 $U$의 전치행렬과 같다. 즉, $U^{-1} = U^T$이다.

$U^TU = I$에서 $UU^T = I$임을 보이는 과정

- **$U$의 치역은 전체 공간** : $U^TU = I$이면, $U$는 전체 공간 $\mathbb{R}^n$에서 $\mathbb{R}^n$으로의 정규직교 변환을 나타낸다. 이는 $U$가 공간의 모든 벡터를 변환한 후에도 원래 공간을 완전히 커버한다는 것을 의미한다.
- **투영의 정의에 의한 결과** : 임의의 벡터 $y$에 대해 $\mathrm{Proj}(y;U) = y$이어야 한다. $U$의 열 벡터들이 정규직교 기저를 형성하기 때문에, $U$에 의한 $y$의 투영은 $y$ 자신이어야 한다.
  - 정규직교 기저 : 벡터 공간에서의 기저 중에서 모든 기저 벡터가 서로 직교(orthogonal)하며 각 벡터의 크기(norm)가 1인(normalized) 경우
- **수학적 결과** : 모든 $y$에 대해 $U(U^TU)^{-1}U^Ty = y$이므로, $U(U^TU)^{-1}U^T = I$이 된다. 여기서 $U^TU = I$이므로, $(U^TU)^{-1} = I^{-1} = I$이다. 따라서, $UU^T = I$이 된다.

이 과정은 $U$가 정규직교행렬일 때, $U$에 의한 투영이 원래 벡터를 변형시키지 않고, $U$와 $U^T$의 곱이 단위행렬이 됨을 보여준다. 이는 $U$가 공간을 회전시키거나 반사시킬 수 있지만, 벡터의 길이나 공간의 각도를 변화시키지 않는다는 것을 의미한다.
