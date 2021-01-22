---
layout: post
title: "Scope / Closure/currying 개념 파악"
date: 2020-12-05 11:20:30  +0800
categories: [자바스크립트, 개념 정리]
tags: [자바스크립트]
---

오늘은 스코프와 클로저에 대해 아.라.보.자.

# **Scope**

#### **Scope : 변수 접근 규칙에 따른 유효 범위**

사전적 의미는 저렇다. 하지만 저것만 보면 누가 이해 하냐?  
일단 당신이 Scope를 배운다는 것은, 이미 선언과 할당에 대해 배웠다는 뜻.  
**Scope는 당신이 선언하고 할당한 let, var, const, function이 가지고 있는 범위이다.**

---

# **Local Scope / Global Scope (지역변수 / 전역변수)**

```js
let greeting = "Hello";
function greetSomeone() {
  let firstName = "Josh";
  return greeting + " " + firstName;
}

greetSomeone(); // => 'Hello Josh'
firstName; // => Error
```

위의 코드를 살펴보면 local과 global에 대해 조금 이해가 가능하다.  
function greetSomeone() 안이 local 이고, 함수 밖에 선언한 greeting이 global이다.

위에 결과가  
greetSomeone(); // => 'Hello Josh'  
firstName; // => Error 로 나오는 이유  
**안쪽 scope에서 바깥 변수/함수를 접근하는 것은 가능**  
**바깥쪽 scope에서 안쪽 변수/함수를 접근하는 것은 불가능**

![image](/assets/img/sample/scope1.png)

요렇게.  
local이 안쪽이고, global이 바깥쪽이다.  
local은 global에서 선언된 let greeting을 사용 가능이지만,  
local에서 선언된 firstName은 local밖에서는 사용 불가능.

**Global scope는 최상단의 scope로, 전역 변수는 어디서든 접근이 가능**  
**지역 변수는 함수 내에서 전역 변수보다 더 높은 우선 순위를 가진다.**
**오키?**

```js

let name = "Richard";

function showName() {
  name = "Jack"; // 지역 변수
  // showName 함수 안에서만 접근 가능
  console.log(name); // Jack
}

console.log(name); // Richard //
지역 변수 안에서 바꾼 값은 지역 변수 밖에서는 값을 불러올 수없다.
showName(); // 하지만 함수를 실행하면 지역 변수를 사용해서 name 값이 바뀜.
console.log(name); // Jack

```

---

# **Block Scope / Function Scope (let / var / const 비교)**

#### **Block : 중괄호의 시작과 끝나는 단위**

## **var과 let**

**Block Scope는 Block안에서만 사용 가능한 스코프다.**  
**let은 Block Scope이다. 그래서 {}안을 벗어나면 값을 불러오지 못함.**

```js
for(let i=0; i<5; i++) {
  console.log(i); // 다섯번 iteration
}
console.log('final i:', i); //  -> 에러
{}안에서 i의 값을 선언 했기에, {} 밖에서는 i의 값을 불러올 수 없다.
```

**하지만 var은 function scope라서 block을 벗어나도 사용 가능.**

```js
for (var i = 0; i < 5; i++) {
  console.log(i); // 다섯번 iteration
}
console.log("final i:", i); // -> 5
```

i를 나중에 또 쓸 수 있기 때문에 var 보다는 사용했던 범위 안에서만 가능한 let을 사용하는 것이 안전.

---

## **const**

값이 변하지 않는 변수, 즉 상수를 정의할 때 사용.  
let과 동일하게 block을 따름. 하지만 값을 재할당은 하지 못 함.

```js
Let pi  = 3.14
Pi = 3.141592 // 가능 / let은 재할당은 가능
Const pi  = 3.14
Pi = 3.141592 // 불가능 / const는 재할당 노노


let pi = 3.14
let pi = 3.141592 // 불가능 / let은 재할당은 되지만 재선언은 노노
var pi = 3.14
var pu = 3.141592 // 가능
```

![image](/assets/img/sample/scope2.png)

---

# **Closure**

#### **closure정의 : 외부 함수의 변수에 접근할 수 있는 내부 함수.**

```js
function outer() {
  let outer = "outer";
  console.log(outer);

  function inner() {
    let inner = "inner";
    console.log(inner);
  }
}
```

여기서 보면 함수 outer 안에 inner이라는 함수가 또 있다. 함수 안에 함수가 있는 모양.  
**inner가 내부함수, outer가 외부 함수.**

inner와 outer 둘 다 지역 변수인 Let outer / let inner이 있다.  
**inner함수는 외부 함수인 outer에서 선언된 변수인 let outer에 접근하여 값을 바꿀 수 있다.**  
**이렇게 내부 함수에서 외부 함수의 변수의 값을 바꾸거나 불러올 수 있는 것을 Closure라고 한다. Closure함수라고도 함.**

하지만 외부 함수인 outer에서는 내부 함수 안에 선언된 let inner의 값을 바꿀 수 없음.

# **Currying**

#### **커링은 함수 하나가 n개의 인자를 받는 과정을 n개의 함수로 각각의 인자를 받도록 하는 것이다.**

#### **ex) f(a, b, c)처럼 단일 호출로 처리하는 함수를 f(a)(b)(c)와 같이 각각의 인수가 호출 가능한 프로세스로 호출된 후 병합되도록 변환하는 것**

```js
function sum(a, b, c) {
  return a + b + c;
}

let curriedSum = curry(sum);

curriedSum(1, 2, 3); // 6, 보통때 처럼 단일 callable 형식으로 호출하기
curriedSum(1)(2, 3); // 6, 첫 번째 인수를 커링하기
curriedSum(1)(2)(3); // 6, 모두 커링하기
```
