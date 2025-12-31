---
layout: post
title: "[선형대수학] 기본 표기법(Basic Notation)"
categories: [CS, Math, Linear Algebra]
tags: [Math, Linear Algebra, ML, Numpy]
use_math: true
---

# 머신러닝을 위한 선형대수학

## 선형대수학의 기본 개념들

- **벡터(Vector)**: 숫자의 배열로 표현되며, 일반적으로 소문자와 굵은 글씨체로 표기한다. 예를 들어, **v**.

- **행렬(Matrix)**: 숫자의 2차원 배열로, 대문자와 굵은 글씨체로 표기한다. 예를 들어, **A**.

- **행렬의 곱셈**: 두 행렬 **A**와 **B**의 곱셈은 **AB**로 표현하며, 이는 행렬의 각 행과 열의 내적으로 계산된다.

- **전치 행렬(Transpose)**: 행렬의 행과 열을 바꾼 것으로, 예를 들어 행렬 **A**의 전치는 **A<sup>T</sup>**로 표현한다.

- **단위 행렬(Identity Matrix)**: 대각선 상의 모든 원소가 1이고, 나머지 원소가 0인 정사각 행렬로, **I**로 표기한다.

- **역행렬(Inverse Matrix)**: 행렬 **A**의 역행렬은 **A<sup>-1</sup>**로 표기하며, **AA<sup>-1</sup> = I**를 만족한다.

- **벡터의 내적(Inner Product)**: 두 벡터 **v**와 **w**의 내적은 **v**와 **w**의 각 성분의 곱의 합으로, **v<sup>T</sup>w**로 표기한다.

- **벡터의 노름(Vector Norm)**: 벡터의 크기를 나타내며, **\|\|v\|\|**로 표기한다. L2 노름은 벡터의 각 요소의 제곱 합의 제곱근으로 계산된다.

## 기본 표기법 (Basic Notation)

- $A \in \mathbb{R}^{m\times n}$ : $m$개의 행과 $n$개의 열을 가진 행렬
- $x \in \mathbb{R}^n$ : $n$개의 원소를 가진 벡터

  - $n$차원 벡터는 $n$개의 행과 1개의 열을 가진 행렬로 생각할 수도 있고 이것을 열벡터(column vector)로 부르기도 한다.
  - 행벡터(row vector)를 표현하려면, $x^T$($T$는 transpose를 의미)로 쓴다.

- $x_i$ : 벡터 $x$의 $i$번째 원소

  $$
  \begin{align*}
  x = \begin{bmatrix}
  x_1\\
  x_2\\
  \vdots\\
  x_n
  \end{bmatrix}
  \end{align*}
  $$

- $a_{ij}$(또는 $A_{ij}, A_{i,j}$) : 행렬 $A$의 $i$번째 행, $j$번째 열에 있는 원소

  $$
  \begin{align*}
  A = \begin{bmatrix}
  a*{11} & a*{12} & \cdots & a*{1n}\\
  a*{21} & a*{22} & \cdots & a*{2n}\\
  \vdots & \vdots & \ddots & \vdots\\
  a*{m1} & a*{m2} & \cdots & a\_{mn}
  \end{bmatrix}
  \end{align*}
  $$

- $a_j$ 혹은 $A_{:,j}$ : $A$의 $j$번째 열

  $$
  \begin{align*}
  A = \begin{bmatrix}
      \vert & \vert & & \vert\\
      a_1 & a_2 & \cdots & a_n\\
      \vert & \vert & & \vert
  \end{bmatrix}
  \end{align*}
  $$

- $a_i^T$ 혹은 $A_{i,:}$ : $A$의 $i$번째 행

  $$
  \begin{align*}
  A = \begin{bmatrix}
      \rule[.5ex]{1.7ex}{0.5pt} & a_1^T & \rule[.5ex]{1.7ex}{0.5pt}\\
      \rule[.5ex]{1.7ex}{0.5pt} & a_2^T & \rule[.5ex]{1.7ex}{0.5pt}\\
      & \vdots &\\
      \rule[.5ex]{1.7ex}{0.5pt} & a_m^T & \rule[.5ex]{1.7ex}{0.5pt}
  \end{bmatrix}
  \end{align*}
  $$

---

## NumPy (Numerical Python)

NumPy는 파이썬에서 다차원 배열을 다루고 계산하는데 특화되어 있는 라이브러리이다<br>
효율적인 데이터 구조와 다양한 수학적 함수와 연산을 제공해서 수치 계산 작업을 단순하게 만들어준다.<br>

**주요 특징:**

1. **다차원 배열 (Numpy Array):** 다차원 배열을 다루기 위한 강력한 도구를 제공하며, 이러한 배열은 행렬과 유사한 구조를 가지고 있다.

2. **효율성:** NumPy 배열은 내부적으로 저수준 언어(C)로 작성된 루틴을 사용하여 빠른 연산을 제공하므로 대용량 데이터 처리에 이상적이다.

3. **수학적 함수와 연산:** 다양한 수학적 함수와 연산을 제공하여 선형 대수, 통계, 푸리에 변환 등 다양한 계산 작업을 지원한다.

4. **데이터 분석과 과학적 연구:** NumPy는 데이터 분석, 머신 러닝, 과학적 연구 등 다양한 분야에서 널리 사용되며 데이터 처리 작업에 필수적이다.

이런 이유로 선형대수학, 행렬 계산을 프로그래밍으로 구현할 때 numpy를 사용한다.

### Python에서의 벡터와 행렬 표현 방법

Python에서 벡터는 일반적으로 숫자의 리스트로 표현된다. 예를 들어, 다음과 같은 벡터가 있다.

```python
[10.5, 5.2, 3.25, 7.0]
```

`numpy` 라이브러리를 사용하면 이 리스트를 `ndarray` 객체로 변환할 수 있다. `numpy`는 다차원 배열을 쉽게 처리할 수 있게 해준다.

```python
import numpy as np
x = np.array([10.5, 5.2, 3.25, 7.0])
```

x의 shape를 쿼리하면 배열의 차원과 길이를 알 수 있다.

```python
x.shape
# (4,)
```

특정 인덱스의 요소에 접근하려면, 인덱스를 사용한다.

```python
i = 2
x[i]
# 3.25
```

하나의 차원을 추가하여 벡터를 2차원 배열로 만들 수도 있다. 이 경우 벡터는 열 벡터로 확장된다

```python
x_2dims = np.expand_dims(x, axis=1)
x_2dims
#array([[10.5 ],
#       [ 5.2 ],
#       [ 3.25],
#       [ 7.  ]])
```

2차원 배열의 특정 요소에 접근하려면, 다음과 같이 한다.

```python
x_2dims[0]      # array([10.5])
x_2dims[0][0]   # 10.5
x_2dims[0, 0]   # 10.5
```

`x_2dims`의 shape는 이제 다음과 같다.

```python
x_2dims.shape
# (4, 1)
```

행렬은 2차원 배열로 표현된다. 예를 들어, 다음과 같은 행렬 A를 만들 수 있다.

```python
A = np.array([
    [10, 20, 30],
    [40, 50, 60]
])
A
# array([[10, 20, 30],
#       [40, 50, 60]])
```

A의 shape를 쿼리하면 행과 열의 수를 알 수 있다.

```python
A.shape
# (2, 3)
```

특정 행이나 열의 요소에 접근하려면 인덱스를 사용한다.

```python
i = 0
j = 2
A[i, j]
# 30
```

열 벡터를 얻으려면 슬라이싱을 사용한다.

```python
j = 1
A[:, j]
# array([20, 50])
```

행 벡터도 같은 방법으로 얻는다.

```python
i = 1
A[i, :]
# array([40, 50, 60])
```
