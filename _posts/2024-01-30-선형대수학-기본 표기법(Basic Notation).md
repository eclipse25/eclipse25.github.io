---
layout: post
title: "선형대수학 - 기본 표기법(Basic Notation)"
categories: [선형대수학]
tags: [선형대수학, 머신러닝, 딥러닝]
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

- $A \in \mathbb{R}^{m\times n}$ : $m$개의 행과 $n$개의 열을 가진 행렬을 의미한다.
- $x \in \mathbb{R}^n$ : $n$개의 원소를 가진 벡터를 의미한다.

  - $n$차원 벡터는 $n$개의 행과 1개의 열을 가진 행렬로 생각할 수도 있고 이것을 열벡터(column vector)로 부르기도 한다.
  - 행벡터(row vector)를 표현하려면, $x^T$($T$는 transpose를 의미)로 쓴다.

- $x_i$ : 벡터 $x$의 $i$번째 원소를 의미한다.

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

- $a_{ij}$(또는 $A_{ij}, A_{i,j}$) : 행렬 $A$의 $i$번째 행, $j$번째 열에 있는 원소를 의미한다.

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

- $a_j$ 혹은 $A_{:,j}$ : $A$의 $j$번째 열을 의미한다.

  $$
  \begin{align*}
  A = \begin{bmatrix}
      \vert & \vert & & \vert\\
      a_1 & a_2 & \cdots & a_n\\
      \vert & \vert & & \vert
  \end{bmatrix}
  \end{align*}
  $$

- $a_i^T$ 혹은 $A_{i,:}$ : $A$의 $i$번째 행을 의미한다.

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
