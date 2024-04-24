---
layout: post
title: "[선형대수학] 선형독립(Linear Independence)"
date: 2024-01-31 09:00:00 +0900
categories: [Linear Algebra]
tags: [Linear Algebra, ML, Numpy]
use_math: true
---

## 선형독립(Linear Independence)

- 벡터 공간에서 벡터 집합에 대한 개념으로, 어떤 벡터도 그 집합에 속한 다른 벡터들의 선형 조합으로 표현될 수 없을 때, 그 벡터들은 선형독립이라고 한다.
- 벡터 집합 {$v_1, v_2, \ldots, v_n$}에 대해 다음과 같은 식이 오직 $c_1 = c_2 = \ldots = c_n = 0$일 때만 성립할 경우를 말한다.

  $$
  c_1v_1 + c_2v_2 + \ldots + c_nv_n = 0
  $$

  여기서 $c_1, c_2, \ldots, c_n$은 스칼라 계수이다.<br>
  이 조건을 만족하지 않고 어떤 스칼라 계수가 0이 아닌 값을 가짐으로써 위 식이 성립한다면, 그 벡터들은 선형 종속(Linearly Dependent)이다.

```python
A = np.array([
        [1, 4, 2],
        [2, 1, -3],
        [3, 5, -1],
    ])

# 위 행렬 A의 열들의 집합은 종속이다.
# 행렬 A의 세 번째 열이 첫 번째 열과 두 번째 열의 선형 조합으로 표현될 수 있다.

A[:, 2] == -2*A[:, 0] + A[:, 1]
#array([ True,  True,  True])
```

## Rank

랭크는 행렬의 행 벡터들 또는 열 벡터들 중에서 선형독립인 벡터들의 최대 개수로 정의되며, 행렬이나 선형 변환의 **차원**을 나타내는 데 사용된다.
행렬 $A$가 주어졌을 때, $A$의 랭크는 $A$의 열 벡터들 또는 행 벡터들 중 선형독립인 벡터들의 최대 집합의 크기와 같다고 볼 수 있다.
행렬의 랭크는 그 행렬을 통해 변환될 때, 이미지(변환된 공간)의 차원을 나타내며, 선형 시스템이 얼마나 **큰** 공간을 차지하고 있는지를 알려준다.<br>
랭크는 행렬이 역행렬을 가지는지 여부를 결정하는 데에도 중요한 역할을 한다.
$m \times n$행렬 $A$의 랭크가 $m$이고 $m = n$일 경우, $A$는 전체 랭크(full rank)를 가지며, 이는 역행렬이 존재한다는 것을 의미한다.
랭크가 행렬의 열 또는 행의 수보다 작다면, 행렬은 특정 차원에서 선형 종속 관계를 가지고 있음을 나타낸다. 이러한 경우, 행렬은 **랭크 결핍**(rank-deficient)이라고 불린다.<br>

- Column rank: 행렬 $A\in \mathbb{R}^{m\times n}$의 열들의 부분집합 중에서 가장 큰 선형독립인 집합의 크기
- Row rank: 행렬 $A\in \mathbb{R}^{m\times n}$의 행들의 부분집합 중에서 가장 큰 선형독립인 집합의 크기
- 모든 행렬의 column rank와 row rank는 동일하다. 따라서 단순히 $\mathrm{rank}(A)$로 표시한다.

다음의 성질들이 성립한다.

- For $A\in \mathbb{R}^{m\times n}$, $\mathrm{rank}(A) \leq \min(m, n)$. If $\mathrm{rank}(A) = \min(m, n)$, then $A$ is said to be **_full rank_**.
- For $A\in \mathbb{R}^{m\times n}$, $\mathrm{rank}(A) = \mathrm{rank}(A^T)$.
- For $A\in \mathbb{R}^{m\times n}, B\in \mathbb{R}^{n\times p}$, $\mathrm{rank}(AB) \leq \min(\mathrm{rank}(A), \mathrm{rank}(B))$.
- For $A, B\in \mathbb{R}^{m\times n}$, $\mathrm{rank}(A+B) \leq \mathrm{rank}(A) + \mathrm{rank}(B)$.

1. **_Full Rank_**:

   - 만약 $ A $가 $ \mathbb{R}^{m \times n} $에 속하는 행렬이라면, $ A $의 랭크는 $ m $과 $ n $중 작은 값 이하가 된다. 이는 행렬의 랭크가 그 행렬의 행 또는 열의 최대 개수를 초과할 수 없음을 의미한다.
   - 만약 $ \mathrm{rank}(A) = \min(m, n) $이면, 행렬 $ A $를 **_full rank_**라고 한다. 이는 $ A $의 모든 행 또는 열이 선형독립임을 나타낸다.

2. **행렬과 그 전치 행렬의 랭크**:

   - 행렬 $ A $가 $ \mathbb{R}^{m \times n} $에 속하면, $ A $의 랭크는 그 전치 행렬 $ A^T $의 랭크와 같다. 이는 행렬과 그 전치 행렬이 같은 수의 선형독립 행 또는 열을 가짐을 의미한다.

3. **두 행렬의 곱의 랭크**:

   - 만약 $ A $가 $ \mathbb{R}^{m \times n} $에 속하고, $ B $가 $ \mathbb{R}^{n \times p} $에 속하는 행렬이라면, $ AB $의 랭크는 $ \min(\mathrm{rank}(A), \mathrm{rank}(B)) $ 이하가 된다. 이는 두 행렬 중 하나라도 랭크가 낮으면, 그 곱의 랭크도 그만큼 제한됨을 나타낸다.

4. **두 행렬의 합의 랭크**:
   - $ A, B $가 $ \mathbb{R}^{m \times n} $에 속하는 행렬들일 때, $A + B $의 랭크는 $ \mathrm{rank}(A) + \mathrm{rank}(B)$이하가 된다. 이는 두 행렬을 더할 때, 랭크가 각각의 랭크 합보다 클 수 없음을 의미한다.

```python
A = np.array([
        [1, 4, 2],
        [2, 1, -3],
        [3, 5, -1],
    ])

LA.matrix_rank(A)
#2
# ->세 번째 열은 첫 번째와 두 번째 열의 선형 조합으로 표현될 수 있다.
# 첫번째와 두번째 열 벡터는 서로 선형독립인 관계를 가지며, 행렬 A의 랭크가 2임을 나타낸다.
```
