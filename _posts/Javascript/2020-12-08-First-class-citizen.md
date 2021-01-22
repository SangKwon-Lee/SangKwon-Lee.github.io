---
layout: post
title: 'First-class citizen 일급 객체'
date: 2020-12-08 11:20:30  +0800
categories: [Javascript, 개념 정리]
tags: [javascript, 일급 객체]
---

# **First-class citizen 일급 객체**

### **일급 객체의 3가지 조건**

#### **1. 변수에 할당(assignment)할 수 있다.**

#### **2. 다른 함수의 인자(argument)로 전달될 수 있다.**

#### **3. 다른 함수의 결과로서 리턴될 수 있다.**

이 3가지 조건을 충족하는 것을 First-class citizen 일급 객체라고 한다.

---

### **이 일급 객체에는 함수도 포함된다**

이는 함수를 데이터(string, number, boolean, array, object)를 다루듯이 다룰 수 있다는 걸 의미한다.
변수에 저장할 수 있기 때문에 배열의 요소나 객체의 속성값으로 저장하는 것도 가능하다.

---

**함수를 변수에 저장하는 방법을 배웠습니다. 바로 함수 표현식(function expression) 입니다**

#### **1. 변수에 함수를 할당하는 경우**

```js
let square = function (num) {
	return num * num;
};
```

**아래의 함수 표현식은 함수 선언식(function declaration)과 다르게 호이스팅(hoisting)이 적용되지 않습니다.**  
--> 요 말에 대해서는 더 공부해야 한다.

#### **2. 함수를 전달하는 경우**

```js
function sayHello() {
	return 'Hello, ';
}
function greeting(helloMessage, name) {
	console.log(helloMessage() + name);
}
// `sayHello`를 `greeting` 함수에 인자로 전달
greeting(sayHello, 'JavaScript!');
```

MDN 예제이다.

#### **3. 다른 함수의 리턴값이 될 수 있다.**

```js
function sayHello() {
	return function () {
		console.log('Hello!');
	};
}
```
