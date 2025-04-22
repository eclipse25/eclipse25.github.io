---
layout: post
title: "JavaScript 자료형"
categories: [JavaScript]
tags: [JavaScript, Frontend]
---

## **JavaScript 자료형**

<br>

JavaScript의 자료형은 크게 **기본형(Primitive Type)** 과 **참조형(Reference Type)** 으로 나뉜다.

<br>

- **기본형(Primitive Type)**: 값 자체를 저장하며, 변경이 불가능(Immutable)함  
- **참조형(Reference Type)**: 값이 아니라 참조값(주소)을 저장하며, 값 변경이 가능(Mutable)함  
- 기본형은 **값 자체를 변수에 저장**하지만, 참조형은 **메모리 주소(참조값)를 저장**함  
- 기본형은 연산할 때 새로운 값을 생성하지만, 참조형은 직접 값이 변경됨  
- 기본형은 스택(Stack), 참조형은 힙(Heap)에 저장됨  

<br>

### **1. 기본형 (Primitive Type)**

| 자료형   | 설명            | 예제            |
|---------|----------------|----------------|
| `number`  | 숫자형 (정수, 실수) | `let a = 42;` `let b = 3.14;` |
| `bigint`  | 큰 정수형 (ES11+) | `let c = 1234567890123456789n;` |
| `string`  | 문자열 | `let d = "JavaScript";` |
| `boolean` | 논리형 (true/false) | `let e = true;` |
| `undefined` | 값이 정의되지 않음 | `let f;` |
| `null` | 값이 없음을 명시적으로 지정 | `let g = null;` |
| `symbol` | 유일한 값 생성 (ES6+) | `let h = Symbol("id");` |

- **불변(Immutable)**: 값이 변경될 수 없으며, 연산 시 새로운 값이 생성됨  
- `typeof` 연산자를 사용하면 자료형을 확인할 수 있음  

```javascript
console.log(typeof 42);        // "number"
console.log(typeof "hello");   // "string"
console.log(typeof true);      // "boolean"
console.log(typeof undefined); // "undefined"
console.log(typeof null);      // "object" (버그지만 유지됨)
console.log(typeof Symbol());  // "symbol"
console.log(typeof 10n);       // "bigint"
```

<br>

### **2. 참조형 (Reference Type)**

| 자료형   | 설명                      | 예제                         |
|---------|--------------------------|-----------------------------|
| `object` | 객체 (key-value 저장) | `let obj = { name: "Alice", age: 25 };` |
| `array`  | 배열 (리스트 구조) | `let arr = [1, 2, 3];` |
| `function` | 함수도 객체의 한 종류 | `function foo() { return 42; }` |
| `date` | 날짜 및 시간 객체 | `let now = new Date();` |
| `regexp` | 정규 표현식 객체 | `let regex = /ab+c/;` |

- **가변(Mutable)**: 값 변경 가능하며, 동일한 객체의 상태를 수정할 수 있음  
- `=` 연산자로 복사하면 같은 객체를 참조  
- `Object.assign()`이나 `structuredClone()`을 사용하면 별도의 객체를 생성  

```javascript
let a = { name: "Alice" };
let b = a;
b.name = "Bob";
console.log(a.name); // "Bob" → 원본 객체도 변경됨 (같은 참조값 공유)
```

<br>

### **3. 메모리 저장 방식**

| 구분   | 기본형 (Primitive Type) | 참조형 (Reference Type) |
|--------|------------------------|------------------------|
| 저장 방식 | 값 자체 저장          | 참조(메모리 주소) 저장 |
| 값 변경 여부 | 변경 불가 (새 값 생성) | 변경 가능 (같은 객체 수정) |
| 연산 가능 여부 | 연산 시 새 값 반환 | 연산 시 기존 객체 변경 |
| 메모리 할당 | 스택(Stack)         | 힙(Heap) |

- `number`, `string`, `boolean` 등은 **불변 객체**로 값 변경 시 새로운 객체 생성  
- `object`, `array`, `function`은 **가변 객체**로 값을 변경해도 같은 객체 유지  

<br>

### **4. 함수 호출 시 차이**

- **기본형(Primitive Type)**: 함수 호출 시 값이 복사되어 전달되므로, 원본 변수는 변경되지 않음  
- **참조형(Reference Type)**: 함수 호출 시 참조값이 전달되므로, 내부에서 값을 변경하면 원본 데이터도 변경됨  

```javascript
// 참조형 (Reference Type)
function modifyObject(obj) {
    obj.name = "Bob";
}

let person = { name: "Alice" };
modifyObject(person);
console.log(person.name); // "Bob" → 원본 객체가 변경됨
```

```javascript
// 기본형 (Primitive Type)
function modifyNumber(n) {
    n += 1;
}

let x = 10;
modifyNumber(x);
console.log(x); // 10 → 원본 값이 변경되지 않음
```

<br>

### **5. 문자열(String)의 특이점**
- `string`은 **불변(immutable) 객체**이므로, 값을 변경하면 새로운 객체가 생성됨  
- 문자열 연산 (`+`, `concat()`)을 하면 새로운 문자열 객체가 만들어짐  

```javascript
let str = "hello";
console.log(str);  // "hello"
str += " world";
console.log(str);  // "hello world" (새로운 문자열 객체 생성)
```

- 문자열을 자주 변경해야 할 경우, `String` 대신 `Array`를 사용하면 성능이 향상될 수 있음  

```javascript
let strArr = ["hello"];
strArr.push(" world");
console.log(strArr.join("")); // "hello world"
```

<br>

### **6. 요약**

| 구분   | 기본형 (Primitive Type) | 참조형 (Reference Type) |
|--------|------------------------|------------------------|
| 저장 방식 | 값 자체 저장          | 참조값(주소) 저장 |
| 값 변경 | 불가능 (새 값 생성)  | 가능 (기존 객체 변경) |
| 연산 방식 | 연산 시 새 값 반환  | 연산 시 기존 객체 변경 |
| 함수 호출 | 값 복사 (원본 영향 없음) | 참조 복사 (원본 변경 가능) |
| 대표 예시 | `number`, `string`, `boolean` | `object`, `array`, `function` |

<br>

### **정리**
- **기본형 (Primitive Type)** → 값 자체를 저장하고 복사됨  
- **참조형 (Reference Type)** → 주소(참조값)를 저장하고 공유됨  
