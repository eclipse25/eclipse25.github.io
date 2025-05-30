---
layout: post
title: "Dart Classes"
categories: [Dart · Flutter]
tags: [Flutter, Dart]
---

<img src="/assets/img/dart.png" alt="dart" width="500"/>

# Dart의 Classes (클래스)

## Class

- Flutter에서는 모든 게 클래스다.
- 프로퍼티를 선언할 때는 타입을 사용해서 정의한다. 함수 내에서 변수를 정의할 때에는 var을 사용하고 타입을 명시할 필요가 없지만, 클래스에서는 타입을 꼭 명시해야 한다.

```dart
class Player{
String name = 'nico';
int xp = 1500;
}
void main(){
var player = Player(); //new 붙일 필요 없음
}
```

- variable의 modifier

```dart
class Player{
String name = 'nico';
int xp = 1500;
}
void main(){
var player = Player(); //new 붙일 필요 없음
print(player.name); // -> nico
player.name = 'lala';
 print(player.name); // -> lala
}
```

- 수정을 못하게 하려면 final을 붙인다.

```dart
class Player{
final String name = 'nico';
int xp = 1500;
}
```

## Class안에서의 method

```dart
class Player{
final String name = 'nico';
int xp = 1500;

    void sayHello(){
    	print("Hi my name is $name");
    }

}
```

- `$this.name`을 쓰지 않고 `$name`을 쓴다.
- `this`를 써도 괜찮지만, 아래의 경우가 아니면 권장되지 않는다.
- `void sayHello()` 내에 name이라는 이름이 같은 변수가 또 있는 경우, `sayHello()`의 name 말고 클래스의 name을 쓰려면 `$this.name` 또는 `${this.name}`을 써줘야 한다.

## Constructor

- constructor: 클래스 바깥에서 값을 받아서 클래스를 생성한다.
- 첫 번째 방법

```dart
class Player{
late final String name; // late는 class에서 유용
late int xp;

    Player(String name, int xp){
    	this.name = name;
        this.xp = xp;
    }

    void sayHello(){
    	print("Hi my name is $name");
    }

}
void main(){
var player = Player("nico", 1500);
player.sayHello();

}
```

- 두번째 방법

```dart
class Player{
final String name; // late 필요 없음
int xp;

    Player(this.name, this.xp);  // positional

    void sayHello(){
    	print("Hi my name is $name");
    }

}
void main(){
var player = Player("nico", 1500); // positional
player.sayHello();

}
```

## Named Constructor Parameters

- 너무 많은 positional argument가 있으면 혼란스럽다.
- named argument로 만든다.

```dart
class Player{
final String name; // late 필요 없음
int xp;
String team;
int age;

    Player({            // {} 붙여줌 => named argument
    required this.name, // required 붙여줌 =>null safety
    required this.xp,
    required this.team,
    required this.age,
    });

    void sayHello(){
    	print("Hi my name is $name");
    }

}
void main(){
var player = Player(
name = "nico",
xp = 1200,
team = 'blue',
age = 21,
);
 player.sayHello();

}
```

## Named Constructors

```dart
class Player{
final String name, team;
 int xp, age;

    Player({
    required this.name,
    required this.xp,
    required this.team,
    required this.age,
    });

    Player.createBluePlayer({
    	required String name,
        required int age,
    })	:	this.age = age;
            this.name = name;
            this.team = 'blue';
            this.xp = 0;

    Player.createRedPlayer(String name, int age)		:	this.age = age;
            this.name = name;
            this.team = 'blue';
            this.xp = 0;

    void sayHello(){
    	print("Hi my name is $name");
    }

}
void main(){
var player.createBluePlayer = Player(
name = "nico",
age = 21, // named
);
 var player.createRedPlayer = Player(
"nico",
21, // positional
);
}
```

### Named Constructor의 syntactic sugar(편의 문법)

✅ Named parameters

- 일반적인 방법

```dart
Player.createBlue({
required String name,
required int xp
}) : this.name = name,
this.xp = xp,
this.team = 'blue';
```

- 간소화된 방법(dart는 간소화된 방법을 추천)

```dart
Player.createRed({
required this.name,
required this.xp,
this.team = 'red',
});

```

✅ positional parameters

- 일반적인 방법

```dart
Player.createRed(String name, int xp)
: this.name = name,
this.xp = xp,
this.team = 'red';
```

- 간소화된 방법

```dart
Player.createRed(this.name, this.xp, [this.team = 'red']);
```

✍ API에서 Jason Format 등으로 데이터를 받을 때 Flutter Dart Class로 바꿔야 한다.

```dart
class Player {
final String name;
int xp;
String team;

    Player.fromJson(Map<String, dynamic> playerJson)
    	:	name = playerJson['name'],
    		xp = playerJson['xp'],
            team = playerJson['team'];

    void sayHello(){
    	print("Hi my name is $name");
    }

}
void main(){
var apiData = [
{
"name" : "nico",
"team" : "red",
"xp": 0,
},
{
"name" : "lynn",
"team" : "red",
"xp": 0,
},
{
"name" : "dal",
"team" : "red",
"xp": 0,
},
]

    apiData.forEach({playerJson} {
    	var player = Player.fromJson(playerJson);
        player.sayHello();
    })

}
```

## Cascade Notation

- Cascade Notation은 객체의 여러 속성을 연속적으로 설정할 수 있게 한다.

```dart
class Player {
String name;
int xp;
String team;

    Player({required this.name, required this.xp, required this.team});

    void sayHello(){
    	print("Hi my name is $name");
    }

}

//✅ 기존 코드(nico 정보수정)
void main(){
var nico = Player(name: 'nico', xp: 1200, team: 'red');
nico.name = 'las';
nico.xp = 120000;
nico.team = 'blue';
}
//✅ Cascade Notation 코드(nico 정보수정)
void main(){
var nico = Player(name: 'nico', xp: 1200, team: 'red')
..name = 'las'
..xp = 120000
..team = 'blue'
..sayHello();
}
```

## Enums

- Enum은 Flutter에서 굉장히 많이 사용된다.
- 실수를 방지하는 데 도움을 준다.

```dart
enum Team = {red, blue}

class Player {
String name;
int xp;
Team team; // 더이상 String이 아님
}
void main(){
var nico = Player(name: 'nico', xp: 1200, team: Team.red)
 ..name = 'las'
..xp = 120000
..team = Team.blue // 'blue' → Team.blue
..sayHello();
}
```

## Abstract Classes

- 추상화 클래스로는 객체를 생성할 수 없다.
- 다른 클래스들이 직접 구현해야 하는 메소드들을 모아놓은 블루프린트다.
- 이를 상속받는 모든 클래스가 특정 메소드를 구현하도록 강제한다.

```dart
abstract class Human {
void walk();
}
class Coach extends Human {
void walk(){
print('The Coach is walking');
}
}
```

- Flutter에서 많이 쓰이지는 않지만 유용하다.

## Inheritance ★

- 상속을 하고 `super`를 이용해 부모 클래스의 생성자를 호출할 수 있다.
- `@override`를 이용해 부모 클래스의 객체를 받아올 수 있다.
- `extends` 키워드 사용

```dart
class Human {
final String name;
Human({required this.name}); // named
void sayHello(){
print("Hi my name is $name");
}
}

enum Team = {blue, red}

class Player extends Human { // Human class 상속
final Team team;
Player({
required this.team,
required String name,
}) : super(name: name); // super로 부모클래스와 상호작용
@override // Human에서 온 sayHello를 대체
void sayHello(){
super.sayHello();
print('and I Play for ${team}');
}
}

void main(){
var player = Player(team: Team.red, name: 'nico');
}
```

## Mixins

- 생성자가 없는 클래스다.
- Flutter에서 많이 사용된다.
- 클래스에 속성과 메소드를 추가할 때 사용한다.
- with 키워드를 사용한다.

```dart
class Strong {
final double strengthLevel = 1500.99;
}
class QuickRunner {
void runQuick(){
print("ruuuuuuuuuun!");
}
}
class Human with Strong, QuickRunner {
final String name;
Human({required this.name}); // named
void sayHello(){
print("Hi my name is $name");
}
}
```
