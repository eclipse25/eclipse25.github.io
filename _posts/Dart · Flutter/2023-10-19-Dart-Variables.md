---
layout: post
title: "Dart Variables"
categories: [Dart · Flutter]
tags: [Flutter, Dart]
---

<img src="/assets/img/dart.png" alt="dart" width="500"/>

# Dart의 Variables (변수)

## Main 함수

```dart
void main() {
print('Hello World!');
}
```

- 모든 Dart 프로그램의 시작점이다.
- main 함수에서 코드를 호출한다.
- main 함수가 없으면 코드를 실행할 수 없다.
- Dart는 문장 끝에 세미콜론(`;`)이 필요하다.

## 변수 선언

```dart
var name = 'apple';
```

- 타입을 구체적으로 적을 필요 없다. Dart가 알아서 타입을 추측한다.
- 업데이트할 때는 같은 자료형으로 해야 한다.
- 함수나 메소드 내부에서 지역변수로 사용한다.

```dart
String name = 'apple';
```

- 자료형을 지정해서 선언하는 것도 가능하다.
- 클래스에서 변수나 프로퍼티를 선언할 때 자주 사용된다.

## Dynamic (동적) 타입

```dart
var name;
dynamic name;
```

- 변수의 타입을 모를 때, 예를 들어 JSON 데이터를 다룰 때 사용한다.
- 선언할 때 값을 지정하지 않으면 `dynamic` 타입이 되고, `dynamic`으로 선언하는 것도 가능하다.

```dart
var name;
name = 8;
name = 'apple';
name = true; // 이렇게 타입 변경도 가능하다.
```

- 조건문 블록 안에서 다양한 메소드를 활용할 수 있다.

```dart
dynamic name;
if(name is String){
name.split(...)
}
if(name is int){
name.isEven
}
```

- `dynamic` 타입은 불가피할 때 말고는 되도록 사용하지 않는 것이 좋다.

## Nullable Variables

```dart
String? name = 'apple'; // 타입 뒤에 ?를 붙여서 표시한다.
name = null;
```

- 자료형의 메소드를 쓰려면 조건문으로 null을 제외해줘야 한다.

```dart
String? name = 'apple';
name = null;
if (name != null){
name.isNotEmpty; // 조건문 없이 메소드를 쓰면 컴파일 에러가 난다.
}
// 대신
name?.isNotEmpty
// 로 사용할 수 있다.
```

## Final Variables

```dart
void main() {
var name = 'apple';
name = 'pear'; // 가능
final name = 'apple'; // 한번 사과는 영원한 사과
}

void main() {
final String name = 'apple'; // 타입 추가도 가능하지만 불필요하다.
}
```

## Late Variables

```dart
void main(){
late final String name;
// do something, go to api
name = 'apple';
}
```

- `late`는 `var`이나 `final` 앞에 붙인다.
- 초기 데이터 없이 변수를 선언할 수 있게 해준다.
- 클래스 내의 인스턴스 변수가 `final`이면 만들면서 바로 할당해야 하고, `late final`이면 만들고 난 후에 할당해도 된다.
- 값을 넣기 전에는 접근하지 않아야 함을 알려주어 null-safety를 보장한다.
- Flutter에서 데이터 페칭을 할 때 유용하다.

## Constant Variables

```dart
const max_allowed_price = 999999;
```

- Dart의 `const`는 컴파일 타임 상수를 의미한다.
- 수정될 수 없는 것은 `final`과 동일하다.
- 컴파일 타임에 알고 있는 값이어야 한다. (API로부터 오거나, 사용자로부터 입력받는 값이 아니라, 앱스토어에 앱이 올라갈 때 이미 알고 있는 값이어야 한다.)
