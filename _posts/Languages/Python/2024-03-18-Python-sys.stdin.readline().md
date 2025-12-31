---
layout: post
title: "Python 입출력, sys.stdin.readline()"
categories: [Languages, Python]
tags: [Python]
---

### 입력

입력받기

```python
n = input()
```

좀 더 빠르게 입력받기

```python
import sys
n = sys.stdin.readline()
```

한 줄에 공백을 구분자로 정수 입력이 2개인 경우

```python
a, b = map(int, input().split())

import sys
a, b = map(int, sys.stdin.readline().split())
```

한 줄에 공백을 구분자로 여러 정수 입력을 받아 리스트에 넣기

```python
li = list(map(int, input().split()))

import sys
li = list(map(int, sys.stdin.readline().split()))
```

### 출력

한 줄에 공백을 구분자로 여러 값 출력

```python
for i in range(len(list)):
    print(list[i], end = " ")    #end 매개변수의 초깃값은 줄바꿈(\n)이다.
print("\n")                      #보통 마지막에 줄바꿈을 해주어야 정답처리된다.
```

- 그런데 이 방법은 마지막 원소 뒤에 공백이 추가된 후 줄바꿈 되는 문제점이 있다

```python
for i in range(len(my_list) - 1):
    print(my_list[i], end=" ")
print(my_list[-1])
```

```python
my_list = [1, 2, 3, 4, 5]
print(" ".join(map(str, my_list))) #문자열로 처리
```

### sys.stdin.readline()

`sys.stdin.readline()`은 사용자 입력을 받을 때 주로 사용된다. 이 코드를 스크립트로 실행하고 사용자 입력을 기다리는 경우, 사용자가 입력을 마친 후 엔터 키를 누르면 입력된 문자열 끝에 `개행 문자(\n)`가 추가된다.

```python
import sys
i_str = sys.stdin.readline()
print(i_str)
print(i_str[:-1])
```

따라서, i_str[:-1]을 사용하면 실제로는 문자열의 마지막 글자가 아니라 이 개행 문자를 제거하는 것이 된다.

#### sys.stdin.readline().split()

`split()` 함수는 기본적으로 공백 문자(스페이스, 탭, 개행 문자 등)를 기준으로 문자열을 분리하여 리스트로 반환한다. 따라서, 사용자 입력에서 엔터를 치면 입력의 끝에 들어가는 `개행 문자(\n)`도 `split()`에 의해 기준으로 사용되어, 입력 문자열을 분리하는 데 사용된다. 이 과정에서 개행 문자는 자동으로 제거된다.

- `input()`은 내부적으로 `sys.stdin.readline()`을 호출하여 입력을 받고, 추가로 개행 문자를 제거하는 작업(strip)을 수행해 입력된 문자열의 마지막에 있는 개행 문자(\n)를 제거하고 반환한다. 이 추가 작업으로 인해 `input()`은 `sys.stdin.readline()`보다 느려진다.
- 또한 `input()`은 Python 레벨에서 정의된 함수로, 호출 시 약간의 오버헤드가 발생하지만 `sys.stdin.readline()`은 더 직접적으로 C 라이브러리를 호출하여 처리한다.
