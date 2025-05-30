---
layout: post
title: "Dart Functions"
categories: [Dart · Flutter]
tags: [Flutter, Dart]
---

<img src="/assets/img/dart.png" alt="dart" width="500"/>

# Dart의 Functions(함수)

## Function

```dart
void sayHello(String name) {
  print("Hello $name nice to meet you!");
}
```

- `void`: 이 함수는 아무것도 반환하지 않는다. 부가적인 효과만 존재한다. 반환하면 에러가 발생한다.

```dart
String sayHello(String potato) {
  return "Hello $potato nice to meet you!";
}
```

- sayHello는 함수 이름이다.
- potato, name은 파라미터 이름이다.
- 함수 가장 앞쪽의 void, String 등은 함수의 반환형이다.

### fat arrow syntax

- 곧바로 리턴하는 간결한 문법이다.

```dart
String sayHello(String potato) => "Hello $potato nice to meet you!";
num plus(num a, num b) => a + b;
```

## named argument

- 파라미터가 여러 개일 때 유용하다.

```dart
String sayHello({String name, int age, String country}){
	return "Hello $name, you are $age, and you come from $country.";
}
void main(){
	print(sayHello(
    	age: 12,
        country: 'cuba',
        name: 'nico',   //노마드코더 맞음....
    ));

}
```

- 함수를 선언할 때 파라미터에 중괄호를 사용한다.

### null safety를 위한 방법

1. 기본값 설정

   ```dart
   String sayHello({
   String name = 'anon',
   int age = 19,
   String country = 'wakanda',
   }){
   return "Hello $name, you are $age, and you come from $country.";
   }
   ```

2. required modifier 사용

   ```dart
   String sayHello({
   required String name,
   required int age,
   required String country,
   }){
   return "Hello $name, you are $age, and you come from $country.";
   }
   ```

## Optional Positional Parameters

- 순서에 맞춰서 입력하는 파라미터이다.
- Optional: 일부 파라미터는 입력하지 않을 수도 있다.

```dart
String sayHello(String name, int age,
[String? country = 'cuba']) =>
'Hello $name, you are $age, and you come from $country.';

void main(){
	var result = sayHello('nico', 12);
    print(result);
}
```

- 함수 선언 시 []를 사용하고, 파라미터 자료형에 ?를 붙여 null일 수도 있음을 알린다.
- 초기값 설정으로 null safety를 해결한다.
- 자주 쓰지는 않는다.

## QQ Operator

- `??`: 왼쪽이 null이면 오른쪽을 반환하고, 아니면 왼쪽을 반환한다.

```dart
String capitalize name(String? name) {
	if (name != null) {
    	return name.toUpperCase();
    }
    return 'ANON';
}

String capitalize name(String? name) =>
	name != null ? name.toUpperCase() : 'ANON';

String capitalize name(String? name) =>
	name?.toUpperCase ?? 'ANON';
```

`??=`: 연산자 왼쪽의 값이 null이면 오른쪽을 할당한다.

```dart
void main(){
  String? name;
  name ??= 'apple';  // name이 null이면 'apple' 할당
}
```

- QQ operator는 Flutter에서 많이 사용된다.

## Typedef

- 자료형이 헷갈릴 때 도움이 되는 alias를 만드는 방법이다.
- 자료형 약칭을 만든다.

```dart
typedef UserInfo = Map<String, String>;

String sayHi(UserInfo userInfo){
	return "Hi ${userInfo['name']}";
}
```
