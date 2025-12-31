---
layout: post
title: "Dart Data Types"
categories: [Languages, Dart]
tags: [Flutter, Dart]
---

<img src="/assets/img/dart.png" alt="dart" width="500"/>

# Dart의 Data Types(자료형)

## 기본적인 자료형

```dart
void main() {
  String name = 'apple';   // 문자열은 '', "" 상관없다.
  bool alive = true;       // 불리언 타입
  int age = 20;            // 정수형
  double money = 69.99;    // 소수점을 포함하는 실수형
  num x = 12;              // num은 int와 double을 모두 포함한다.
  x = 1.1;
}
```

- integer와 double은 num 클래스를 상속받는다.
- num 자료형을 사용하면 그 숫자는 integer일 수도 있고 double일 수도 있다.

## Lists

```dart
void main() {
  var numbers = [1,2,3,4,5];        // 첫번째 방법
  List<int> numbers = [1,2,3,4,5];  // 두번째 방법
}
```

- var 또는 List<자료형>을 통해서 리스트를 만들 수 있다.
- 가능하면 var로 선언한다.

```dart
var numbers = [1,2,3,4,5];
numbers.add(1);   // 숫자 추가
numbers.first     // 첫번째 요소 반환
numbers.last      // 마지막 요소 반환
numbers.isEmpty   // 리스트가 비어있는지 반환
```

- VS Code나 DartPad에서는 List 끝을 쉼표로 하면 요소들이 세로로 포맷팅된다.
- collection-if와 collection-for을 지원한다.

### collection-if

```dart
var giveMeFive = true;
var numbers = [
  1,
  2,
  3,
  4,
  if (giveMeFive) 5,  // giveMeFive가 true면 5 추가
];
```

### collection-for

```dart
void main() {
  var oldFriends = ['apple', 'pear'];
  var newFriends = [
    'lewis',
    'ralph',
    for (var friend in oldFriends) "❤️$friend",
  ];
}
```

## Maps

- key와 value를 연결하는 객체다.
- Javascript의 object, Python의 dictionary와 유사하다.

```dart
void main() {
  var player = {
    'name': 'rabbit',
    'xp': 19.99,
    'superpower': false,
  };
}
```

- 타입: Map<String, Object> → Object=any
- var 대신 Map<String, bool>처럼 쓰는 것도 가능하다.
- Map<List<int>, bool>도 가능하다.
- Map도 클래스라서 method, property가 있다.
- Map 생성자를 사용하여 동일한 객체를 만들 수도 있다 → var gifts2 = Map();
- 특정한 형태와 의미를 가진 데이터를 다룰 때에는 Map보다 클래스를 사용하는 것을 권장한다.

## Sets

- list는 대괄호를 쓰고, set는 중괄호를 쓴다.

```dart
void main() {
  var numbers = {1, 2, 3};      // 첫번째 방법
  Set numbers = {1, 2, 3};      // 두번째 방법
  Set<int> numbers = {1, 2, 3}; // 세번째 방법
}
```

- set의 요소들은 유니크하다.
- list는 같은 요소가 여러 개 반복될 수 있지만, set은 중복을 허용하지 않는다.
- 같은 요소를 추가해도 추가되지 않는다.

---

> Dart Set → JS Set, Python Set<br>
> Dart List → JS Array, Python List
