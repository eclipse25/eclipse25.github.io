---
layout: post
title: "[알고리즘] 매개변수 탐색(Binary, Parameter Search)"
categories: [CS, Algorithms]
tags: [Algorithm, Search]
use_math: true
---

## 매개변수 탐색 (Parameter Search)

최적화 문제에서 최적의 조건을 찾기 위해 사용되는 기법 중 하나이다. 특히, 알고리즘 문제 풀이에서는 주어진 조건을 만족하는 최대값이나 최소값을 찾는 문제에 자주 사용된다. **이진 탐색(Binary Search)**을 활용하여, 문제의 해답 범위를 점차 좁혀가며 최적의 값을 찾는 방식으로 진행된다. 매개변수 탐색은 주로 "결정 문제"(decision problem) 형태로 변환하여 해결한다.

### 매개변수 탐색 과정

1. **결정 문제 정의:** 원래 문제를 '특정 조건을 만족하는가?' 형태의 결정 문제로 변환한다. 예를 들어, '최대 무게 제한을 x로 했을 때, 모든 물건을 운반할 수 있는가?'와 같은 형태이다.

2. **탐색 범위 설정:** 매개변수(결정 문제의 조건)에 대한 탐색 범위를 설정한다. 이 범위는 문제에 따라 다를 수 있고, 최소값과 최대값을 기준으로 시작한다.

3. **이진 탐색 실행:** 설정한 탐색 범위 내에서 이진 탐색을 실행하여, 결정 문제의 조건을 만족하는 최적의 매개변수 값을 찾는다. 탐색 범위를 절반씩 줄여가며, 조건을 만족하는 최소값 또는 최대값을 찾아간다.

4. **최적값 확인:** 이진 탐색을 통해 결정 문제의 조건을 만족하는 매개변수의 최적값을 찾았다면, 그 값을 원래 문제의 해답으로 사용한다.

### 매개변수 탐색의 장점

- **효율성:** 결정 문제로 변환하여 이진 탐색을 사용하기 때문에, 탐색 과정이 매우 효율적이다. $O(\log n)$의 시간 복잡도를 가질 수 있다.
- **적용성:** 다양한 최적화 문제에 적용할 수 있으며, 복잡한 문제를 단순화하여 해결할 수 있다.

## 이분 탐색 & 매개변수 탐색 알고리즘 문제

- 특정 조건을 만족하도록 하는 변수의 최소값 혹은 최대값을 찾는다.
- 문제에서 주어진 조건을 따라 탐색 범위를 정하고, 이분 탐색을 이용하여 목표값을 찾는다.
- 최소값을 찾는 경우 이분 탐색의 start(left)값이, 최대값을 찾는 경우 end(right) 값이 답이 된다.
  - 작성하는 코드에 따라 달라질 수 있다.

### 백준 1654: 랜선 자르기

- 문제 설명
  - k개의 랜선들의 길이와, 이 랜선들을 잘라서 만들어야 하는 같은 길이의 랜선 수 N이 주어진다.
  - 같은 길이로 자른 후 남은 랜선들은 버린다.
  - N개를 만들 수 있는 랜선의 최대 길이를 구한다.
- 풀이
  - 랜선의 최대 길이가 될 수 있는 탐색 범위를 정한다.
  - 랜선의 최대 길이를 매개변수로, 해당 길이로 랜선을 잘랐을 때 N개가 만들어지는지 확인한다.
  - N개 이상 만들어지면 랜선을 너무 짧게 잘라서 버려지는 부분이 늘어난 것일 수 있으므로 mid값 이상으로 랜선의 길이에 대한 탐색범위를 늘리고, 만들어지지 않으면 랜선을 너무 길게 자른것이므로 mid값 아래로 길이를 줄이면서 이분탐색한다.
  - 최댓값을 구하고 있기 때문에 아래 코드에서는 right값이 답이 된다.

```python
k, n = map(int, input().split())
lines = [int(input()) for _ in range(k)]

def binary_search(arr, target):
  left, right = 1, max(arr)
  while left <= right:
    mid = (left + right) // 2

    count = 0
    for i in arr:
      count += i // mid

    if count < target:
      right = mid - 1
    else:
      left = mid + 1

  return right

print(binary_search(lines, n))
```

### 백준 2805: 나무자르기

- 문제 설명
  - 한 줄에 위치한 n개의 나무들의 높이와 필요한 만큼의 나무의 길이의 합인 m미터가 주어진다.
  - 절단기의 높이의 최대값인 h를 구한다.
  - 높이가 h보다 큰 나무는 h 위의 부분이 잘리고, 낮은 나무는 잘리지 않는다.
- 풀이
  - 절단기의 높이 h가 될 수 있는 범위를 구한다.
  - 이분 탐색을 통해, 절단기의 높이를 가정하고 그 경우 잘린 나무들의 길이 합이 m이상인지 확인한다.
  - m 이상을 만족하면 절단기를 위로 올려서 나무들을 덜 잘라도 되는 것이므로 mid값 위로 탐색범위를 조정하고, m 이상을 만족하지 않으면 절단기를 내려서 더 잘라야 하므로 mid값 아래로 탐색범위를 조정한다.

```python
import sys
n, m = map(int, sys.stdin.readline().split())
trees = list(map(int, sys.stdin.readline().split()))

def binary_search(arr, target):
  start, end = 0, max(arr)

  while start <= end:
    mid = (start + end) // 2
    sum = 0
    for i in arr:
      if i > mid:
        sum += i - mid

    if sum >= target:
      start = mid + 1
    else:
      end = mid - 1

  return end

print(binary_search(trees, m))
```

### 백준 16564: 히오스 프로게이머

- 문제설명
  - 각 레벨이 $X_i$인 캐릭터 n개와 앞으로 올릴 수 있는 레벨의 최대 총합 k가 주어진다.
  - $T = \min(X_i)$로 정의되는 팀 목표레벨 T의 최대값을 구한다.
  - 레벨을 총합 K보다 적게 올릴 수도 있다.
- 풀이
  - 팀 목표레벨은 모든 캐릭터의 레벨 중 최소값이 되므로 탐색범위에서 start값은 min(arr)으로, 최대값은 min(arr) + k으로 정한다. mid는 팀 목표레벨을 가정한 값이 된다.
  - 모든 캐릭터의 현재 레벨에서 레벨이 mid보다 낮은 경우만 mid까지의 차이를 모두 더한다.
  - 더 필요한 레벨의 합이 k보다 낮다면 목표레벨이 너무 높인 것이므로 end값을 mid아래로 낮추고, 그렇지 않다면 start값을 mid위로 올리는 방법으로 이분탐색을 수행해 최종적으로 구해지는 최대값 end를 리턴한다.

```python
import sys
n, k = map(int, sys.stdin.readline().split())
level = [int(sys.stdin.readline()) for _ in range(n)]

def target_level(arr, k):
  start, end = min(arr), min(arr) + k

  while start <= end:
    mid = (start + end) // 2
    total_needed = sum(max(mid - x, 0) for x in arr)
    if total_needed > k:
      end = mid - 1
    else:
      start = mid + 1
  return end

print(target_level(level, k))
```

### 백준 2110: 공유기 설치

- 문제 설명
  - 수직선 위에 놓여진 n개의 집의 좌표가 정렬되지 않은 상태로 주어지고, 공유기의 개수 c가 주어진다.
  - n개의 집에 c개의 공유기를 배치한다.
  - 공유기 사이의 거리들 중 최소값이 최대가 되도록 하고, 이때의 최소값을 구한다.
- 풀이
  - n개의 집의 좌표들을 순서대로 정렬한다.
  - 공유기들을 최대한 멀리 떨어뜨려야 하기 때문에 가장 앞과 뒤에 있는 집에 공유기를 배치한다.
  - 가장 앞과 뒤의 집의 좌표 차이가 공유기들 간 거리의 최대값이 되고, 최소값은 1로 지정한다.
  - 공유기들간의 최소 거리를 지정하고, 이 경우 n개의 집 사이의 거리가 이 최소거리를 만족하면서 c개의 공유기를 배치할만큼의 거리가 되는지를 확인하는 반복문을 작성한다.
    - 공유기가 배치된 마지막 위치와 공유기가 놓인 개수를 나타내는 변수를 만든다. (가장 앞에 위치한 집에 공유기를 배치하므로 마지막 위치의 초기값은 가장 앞에 위치한 집의 좌표가 된다.)
    - 다음 집들을 탐색하면서 공유기가 놓인 마지막 위치로부터 최소거리 이상인 위치에 떨어져 있는지 확인한다. 이 경우 공유기를 배치하고 마지막 위치를 갱신하며 놓인 공유기의 개수에 +1 한다.
  - 반복문이 끝난 후 놓여진 공유기의 개수가 c이상을 만족하는지 확인한다.
  - 이분 탐색을 통해 만족한다면 최소거리를 mid값 위로 늘리고, 만족하지 않는다면 mid값 아래로 줄이면서 이러한 최소거리의 최대값을 구한다.

```python
import sys
n, c = map(int, sys.stdin.readline().split())
house = [int(sys.stdin.readline()) for _ in range(n)]
house.sort()

def max_distance(arr, target):
  start, end = 1, arr[-1] - arr[0]
  while start <= end:
    mid = (start + end) // 2

    count = 1
    last = arr[0]
    for i in range(1, len(arr)):
      if arr[i] - last >= mid:
        last = arr[i]
        count += 1
    if count >= target:
      start = mid + 1
    else:
      end = mid - 1

  return end

print(max_distance(house, c))
```
