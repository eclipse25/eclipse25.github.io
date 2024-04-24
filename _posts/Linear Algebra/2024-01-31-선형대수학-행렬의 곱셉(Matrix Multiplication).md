---
layout: post
title: "[선형대수학] 행렬의 곱셉(Matrix Multiplication)"
date: 2024-01-31 07:00:00 +0900
categories: [Linear Algebra]
tags: [Linear Algebra, Linear Algebra, Numpy]
use_math: true
---

## 행렬의 곱셉 (Matrix Multiplication)

행렬의 곱셈을 알아야하는 이유는 다음과 같다.

1. 데이터 표현: 머신러닝에서 데이터를 행렬로 표현하며, 행렬 곱셈을 사용해 데이터를 변환하고 분석한다.
2. 선형 변환 적용: 선형대수에서 행렬은 선형 변환을 나타내고, 행렬 곱셈으로 이 변환을 적용한다.
3. 신경망 연산: 신경망에서 행렬 곱셈을 통해 가중치, 입력, 바이어스를 이용한 출력 계산을 한다.
4. 최적화 알고리즘: 많은 최적화 알고리즘들이 행렬 연산을 기반으로 하며, 예를 들어 경사하강법은 행렬 미분을 사용한다.
5. 복잡도 줄이기: 행렬 곱셈은 복잡한 연산을 보다 효율적으로 만들어, 계산 복잡도를 줄인다.<br>

두 개의 행렬 $A\in \mathbb{R}^{m\times n}$, $B\in \mathbb{R}^{n\times p}$의 곱 $C = AB \in \mathbb{R}^{m\times p}$는 다음과 같이 정의된다.

$$C_{ij} = \sum_{k=1}^n A_{ik}B_{kj}$$

- $C_{ij}$ : 결과 행렬 C의 $i$번째 행과 $j$번째 열에 위치한 요소
- $A_{ik}$ : 행렬 $A$의 $i$번째 행과 $k$번째 열에 위치한 요소
- $B_{kj}$ : 행렬 $B$의 $k$번째 행과 $j$번째 열에 위치한 요소
- $\sum_{k=1}^n$ : $k = 1$ 에서 $n$까지의 합<br>

결과적으로, $C$의 각 요소는 $A$의 한 행과 $B$의 한 열의 해당하는 요소들을 곱한 값들의 합으로 구해진다.

행렬곱셈에는 다음의 3가지가 있다.

- 벡터 $\times$ 벡터
- 행렬 $\times$ 벡터
- 행렬 $\times$ 행렬

---

## 벡터 $\times$ 벡터(Vector-Vector Products)

### 내적(inner product, dot product)

두 벡터 $x, y\in \mathbb{R}^n$이 주어졌을 때 내적 $x^Ty$는 다음과 같이 정의된다.

$$
\begin{align*}
x^Ty \in \mathbb{R} = [\mbox{ }x_1\mbox{ }x_2\mbox{ }\cdots \mbox{ }x_n\mbox{ }] \begin{bmatrix}
    y_1\\
    y_2\\
    \vdots\\
    y_n
\end{bmatrix}
= \sum_{i=1}^n x_i y_i
\end{align*}
$$

$$x^Ty = y^Tx$$

- 두 벡터의 크기는 같아야 한다.
- 결과값은 하나의 실수값이 된다.

```python
import numpy as np
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])
x.dot(y)
# 32
```

### 외적(outer product)

두 개의 벡터 $x\in \mathbb{R}^m, y\in \mathbb{R}^n$이 주어졌을 때 외적 $xy^T\in \mathbb{R}^{m\times n}$는 다음과 같이 정의된다.

$$
\begin{align*}
xy^T \in \mathbb{R}^{m\times n} = \begin{bmatrix}
x_1\\
x_2\\
\vdots\\
x_m
\end{bmatrix}
[\mbox{ }y_1\mbox{ }y_2\mbox{ }\cdots \mbox{ }y_n\mbox{ }]
= \begin{bmatrix}
x_1y_1 & x_1y_2 & \cdots & x_1y_n\\
x_2y_1 & x_2y_2 & \cdots & x_2y_n\\
\vdots & \vdots & \ddots & \vdots\\
x_my_1 & x_my_2 & \cdots & x_my_n
\end{bmatrix}
\end{align*}
$$

- 결과값은 행렬이 된다.

```python
x = np.array([1, 2, 3])
y = np.array([4, 5, 6])

x = np.expand_dims(x, axis=1)
y = np.expand_dims(y, axis=0)
x.shape, y.shape
# ((3, 1), (1, 3))

x, y
#(array([[1],
#        [2],
#        [3]]),
# array([[4, 5, 6]]))

np.matmul(x,y)
#array([[ 4,  5,  6],
#       [ 8, 10, 12],
#       [12, 15, 18]])
```

행렬 $A$는 모든 열들이 동일한 벡터 $x$를 가지고 있을 때, 외적을 이용하면 간편하게 $x\mathbf{1}^T$로 나타낼 수 있다.<br>
($\mathbf{1}\in \mathbb{R}^n$는 모든 원소가 1인 $n$차원 벡터)

$$
\begin{align*}
A = \begin{bmatrix}
    \vert & \vert & & \vert\\
    x & x & \cdots & x\\
    \vert & \vert & & \vert
\end{bmatrix}
= \begin{bmatrix}
    x_1 & x_1 & \cdots & x_1\\
    x_2 & x_2 & \cdots & x_2\\
    \vdots & \vdots & \ddots & \vdots\\
    x_m & x_m & \cdots & x_m
\end{bmatrix}
= \begin{bmatrix}
    x_1\\
    x_2\\
    \vdots\\
    x_m
\end{bmatrix}
\begin{bmatrix}
    1 & 1 & \cdots & 1
\end{bmatrix}
= x\mathbf{1}^T
\end{align*}
$$

```python
# column vector
x = np.expand_dims(np.array([1, 2, 3]), axis=1)
x
#array([[1],
#       [2],
#       [3]])

ones = np.ones([1,4])
ones
#array([[1., 1., 1., 1.]])

A = np.matmul(x, ones)
A
#array([[1., 1., 1., 1.],
#       [2., 2., 2., 2.],
#       [3., 3., 3., 3.]])
```

---

## 행렬 $\times$ 벡터(Matrix-Vector Products)

행렬 $A\in \mathbb{R}^{m\times n}$와 벡터 $x\in \mathbb{R}^n$의 곱은 벡터 $y = Ax \in \mathbb{R}^m$이다.<br>
이 곱을 몇 가지 측면에서 바라볼 수 있다.

### 열벡터를 오른쪽에 곱하고($Ax$), $A$가 행의 형태로 표현되었을 때

$$
\begin{align*}
y = Ax =
\begin{bmatrix}
     \rule[.5ex]{1.7ex}{0.5pt} & a_1^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_2^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     & \vdots &\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_m^T & \rule[.5ex]{1.7ex}{0.5pt}
\end{bmatrix} x
= \begin{bmatrix}
a_1^Tx\\
a_2^Tx\\
\vdots\\
a_m^Tx
\end{bmatrix}
\end{align*}
$$

- n개의 실수가 결과로 나타나게 된다.

```python
A = np.array([
    [1,2,3],
    [4,5,6]
])
A
#array([[1, 2, 3],
#       [4, 5, 6]])

ones = np.ones([3,1])
ones
#array([[1.],
#       [1.],
#       [1.]])

np.matmul(A, ones)
#array([[ 6.],
#       [15.]])
```

### 열벡터를 오른쪽에 곱하고($Ax$), $A$가 열의 형태로 표현되었을 때

$$
\begin{align*}
y = Ax =
\begin{bmatrix}
    \vert & \vert & & \vert\\
    a_1 & a_2 & \cdots & a_n\\
    \vert & \vert & & \vert
\end{bmatrix}
\begin{bmatrix}
x_1\\
x_2\\
\vdots\\
x_n
\end{bmatrix}
= \begin{bmatrix}
\vert\\
a_1\\
\vert
\end{bmatrix} x_1 +
\begin{bmatrix}
\vert\\
a_2\\
\vert
\end{bmatrix} x_2 + \cdots +
\begin{bmatrix}
\vert\\
a_n\\
\vert
\end{bmatrix} x_n
\end{align*}
$$

```python
A = np.array([
    [1,0,1],
    [0,1,1]
])
x = np.array([
    [1],
    [2],
    [3]
])
np.matmul(A, x)
#array([[4],
#       [5]])

for i in range(A.shape[1]):
    print('a_'+str(i)+':', A[:,i], '\tx_'+str(i)+':', x[i], '\ta_'+str(i)+'*x_'+str(i)+':', A[:,i]*x[i])
#a_0: [1 0] 	x_0: [1] 	a_0*x_0: [1 0]
#a_1: [0 1] 	x_1: [2] 	a_1*x_1: [0 2]
#a_2: [1 1] 	x_2: [3] 	a_2*x_2: [3 3]
```

### 행벡터를 왼쪽에 곱하고($x^TA$), $A$가 열의 형태로 표현되었을 때

$A\in \mathbb{R}^{m\times n}$, $x\in \mathbb{R}^m$, $y\in \mathbb{R}^n$일 때, $y^T = x^TA$

$$
\begin{align*}
y^T = x^TA = x^T
\begin{bmatrix}
    \vert & \vert & & \vert\\
    a_1 & a_2 & \cdots & a_n\\
    \vert & \vert & & \vert
\end{bmatrix}
= \begin{bmatrix}
x^Ta_1 & x^Ta_2 & \cdots & x^Ta_n
\end{bmatrix}
\end{align*}
$$

### 행벡터를 왼쪽에 곱하고($x^TA$), $A$가 행의 형태로 표현되었을 때

$$
\begin{align*}
y^T =& x^TA\\
    =& \begin{bmatrix}
    x_1 & x_2 & \cdots & x_m
    \end{bmatrix}
    \begin{bmatrix}
     \rule[.5ex]{1.7ex}{0.5pt} & a_1^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_2^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     & \vdots &\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_m^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix}\\
    =& x_1 \begin{bmatrix}
        \rule[.5ex]{1.7ex}{0.5pt} & a_1^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix} + x_2 \begin{bmatrix}
        \rule[.5ex]{1.7ex}{0.5pt} & a_2^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix} + \cdots + x_n \begin{bmatrix}
        \rule[.5ex]{1.7ex}{0.5pt} & a_n^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix}
\end{align*}
$$

---

## 행렬 $\times$ 행렬(Matrix-Matrix Products)

행렬 × 행렬 연산도 여러 관점으로 접근할 수 있다.

### 일련의 벡터 × 벡터 연산으로 표현하는 경우

$A$와 $B$가 행 또는 열로 표현되었는가에 따라 두 가지 경우로 나눌 수 있다.

- $A$가 행으로 $B$가 열로 표현되었을 때

$$
\begin{align*}
C = AB = \begin{bmatrix}
     \rule[.5ex]{1.7ex}{0.5pt} & a_1^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_2^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     & \vdots &\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_m^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix}
    \begin{bmatrix}
    \vert & \vert & & \vert\\
    b_1 & b_2 & \cdots & b_p\\
    \vert & \vert & & \vert
    \end{bmatrix}
= \begin{bmatrix}
    a_1^Tb_1 & a_1^Tb_2 & \cdots & a_1^Tb_p\\
    a_2^Tb_1 & a_2^Tb_2 & \cdots & a_2^Tb_p\\
    \vdots & \vdots & \ddots & \vdots\\
    a_m^Tb_1 & a_m^Tb_2 & \cdots & a_m^Tb_p\\
\end{bmatrix}
\end{align*}
$$

$A\in \mathbb{R}^{m\times n}$, $B\in \mathbb{R}^{n\times p}$, $a_i \in \mathbb{R}^n$, $b_j \in \mathbb{R}^n$이기 때문에 내적값들이 자연스럽게 정의된다.

- $A$가 열로 $B$가 행으로 표현되었을 때

위보다는 까다롭지만 가끔씩 유용하다.

$$
\begin{align*}
C = AB =
    \begin{bmatrix}
    \vert & \vert & & \vert\\
    a_1 & a_2 & \cdots & a_n\\
    \vert & \vert & & \vert
    \end{bmatrix}
    \begin{bmatrix}
     \rule[.5ex]{1.7ex}{0.5pt} & b_1^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     \rule[.5ex]{1.7ex}{0.5pt} & b_2^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     & \vdots &\\
     \rule[.5ex]{1.7ex}{0.5pt} & b_n^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix}
= \sum_{i=1}^n a_i b_i^T
\end{align*}
$$

$AB$는 모든 $i$에 대해서 $a_i\in \mathbb{R}^m$와 $b_i\in \mathbb{R}^p$의 외적의 합이다. $a_i b_i^T$의 차원은 $m\times p$이다 ($C$의 차원과 동일).

### 일련의 행렬 × 벡터 연산으로 표현하는 경우

- $B$가 열로 표현되었을 때

$C=AB$일 때 $C$의 열들을 $A$와 $B$의 열들의 곱으로 나타낼 수 있다.

$$
\begin{align*}
C = AB =
    A \begin{bmatrix}
    \vert & \vert & & \vert\\
    b_1 & b_2 & \cdots & b_p\\
    \vert & \vert & & \vert
    \end{bmatrix}
= \begin{bmatrix}
    \vert & \vert & & \vert\\
    Ab_1 & Ab_2 & \cdots & Ab_p\\
    \vert & \vert & & \vert
    \end{bmatrix}
\end{align*}
$$

각각의 $c_i = Ab_i$는 앞에서 살펴본 행렬 $\times$ 벡터의 두 가지 관점으로 해석할 수 있다.

- $A$가 행으로 표현되었을 때

$$
\begin{align*}
C = AB =
    \begin{bmatrix}
     \rule[.5ex]{1.7ex}{0.5pt} & a_1^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_2^T & \rule[.5ex]{1.7ex}{0.5pt}\\
     & \vdots &\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_m^T & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix} B
= \begin{bmatrix}
     \rule[.5ex]{1.7ex}{0.5pt} & a_1^TB & \rule[.5ex]{1.7ex}{0.5pt}\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_2^TB & \rule[.5ex]{1.7ex}{0.5pt}\\
     & \vdots &\\
     \rule[.5ex]{1.7ex}{0.5pt} & a_m^TB & \rule[.5ex]{1.7ex}{0.5pt}
    \end{bmatrix}
\end{align*}
$$
