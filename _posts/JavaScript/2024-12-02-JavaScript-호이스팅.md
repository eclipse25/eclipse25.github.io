---
layout: post
title: "JavaScript 호이스팅"
categories: [JavaScript]
tags: [JavaScript, Frontend]
---

## JavaScript 호이스팅(Hoisting)

<br>

### 호이스팅(Hoisting)이란?

호이스팅이란 자바스크립트에서 **변수나 함수의 선언이 실제 코드상의 위치와 상관없이 가장 위로 끌어올려져 처리되는 현상**을 말한다.  

실제 코드가 위로 이동하는 것이 아니라, 자바스크립트 엔진이 코드를 실행하기 전에 먼저 선언 부분을 읽고 메모리에 저장하는 것이다.


<br>

### 변수 호이스팅

자바스크립트에서 변수 선언은 보통 `var`, `let`, `const`로 한다.

<br>

#### var로 선언한 변수의 호이스팅

`var`로 선언한 변수는 **선언만** 호이스팅된다.   
초기화 값은 함께 올라가지 않는다.

```javascript
console.log(myVar); // undefined
var myVar = 10;
```

위 코드의 실행 순서를 실제 자바스크립트가 바라보는 관점에서 다시 쓰면 다음과 같다.

```javascript
var myVar; // 선언은 호이스팅됨 (초기화는 안됨)

console.log(myVar); // undefined
myVar = 10;
```

즉, 변수 선언(`var myVar;`)만 코드의 최상단으로 옮겨진 것처럼 동작한다.  
아직 값을 넣지 않았기 때문에 콘솔에서는 `undefined`로 출력된다.

<br>

#### let과 const 변수의 호이스팅

`let`과 `const`도 선언만 호이스팅이 된다.  
하지만 **Temporal Dead Zone(TDZ)** 이라는 특수한 영역 때문에 **초기화되기 전에 접근하면 에러가 발생한다.**

```javascript
console.log(myLet); // ReferenceError 발생
let myLet = 10;
```

자바스크립트가 내부적으로 바라보는 관점에서 다시 쓰면 다음과 같다.

```javascript
let myLet; // 선언은 호이스팅되었지만, 접근 불가능한 영역(TDZ)에 있음

console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
myLet = 10;
```

<br>

#### TDZ(Temporal Dead Zone, 일시적 사각 지대)

**let이나 const로 선언된 변수가 선언된 시점부터 초기화(값이 할당)되기 전까지의 구간**

- JavaScript에서 ES6부터 도입된 개념   
- 이 구간에서 변수를 사용하려고 하면 ReferenceError가 발생한다.  
- 변수를 선언 전에 사용하는 실수를 방지하기 위해 도입되었다.  

그럼 `var`은 왜 에러가 발생하지 않는가?

- 자바스크립트가 처음 만들어졌을 때 설계된 `var`은 변수를 미리 정의하지 않더라도 유연하게 처리하도록 설계되어, 선언만 된 상태에서 초기화되지 않은 변수는 자바스크립트가 `undefined`라는 기본값을 넣어줬다.
- 시간이 지나면서 자바스크립트가 더욱 복잡하고 큰 규모의 애플리케이션에 사용되기 시작하고 `var`로 인한 문제가 많이 발생하자 ES6에서 `let`과 `const`를 도입하면서는 초기화 전에 변수에 접근하면 에러가 발생되도록 했다.

<br>

**정리**
- `var`는 초기화 전에 접근 가능하며 `undefined` 반환
- `let`, `const`는 초기화 전에 접근 불가능하며 ReferenceError 발생

<br>

### 함수 호이스팅

함수 호이스팅은 **함수 선언식(Function Declaration)** 에만 적용된다.  
선언과 초기화가 모두 호이스팅되기 때문에 함수 선언 전에도 호출할 수 있다.

```javascript
myFunc(); // 정상적으로 'Hello!' 출력

function myFunc() {
    console.log('Hello!');
}
```

실제 자바스크립트 엔진의 관점에서는  

```javascript
function myFunc() { // 선언과 초기화 모두 호이스팅됨
    console.log('Hello');
}

myFunc(); // 정상적으로 'Hello' 출력
```

<br>

#### 함수 표현식과 화살표 함수에서 호이스팅

함수 표현식이나 화살표 함수는 변수와 같이 선언만 호이스팅된다.  
초기화 전에 호출하면 에러 발생

```javascript
myFuncExpr(); // TypeError: myFuncExpr is not a function

var myFuncExpr = function() {
    console.log('Hi!');
};
```

실제 자바스크립트 엔진의 관점

```javascript
var myFuncExpr; // 선언만 호이스팅

myFuncExpr(); // TypeError: myFuncExpr is not a function

myFuncExpr = function() {
    console.log('Hi!');
};
```

**정리**
- 함수 선언식 → 선언, 초기화 모두 호이스팅됨 (미리 호출 가능)
- 함수 표현식 및 화살표 함수 → 선언만 호이스팅됨 (초기화 전 호출 시 에러)

<br>

## 전체 호이스팅 정리

| 항목 | 선언 호이스팅 | 초기화 호이스팅 | 초기화 전 접근 시 |
|------|---------------|-----------------|------------------|
| var | O | X | undefined |
| let, const | O | X | ReferenceError |
| 함수 선언식 | O | O | 정상 작동 |
| 함수 표현식, 화살표 함수 | O | X | TypeError |

