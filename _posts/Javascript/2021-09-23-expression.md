---
layout: post
title: '표현식과 문에 대해 알아보자'
date: 2021-09-23 12:00:30  +0800
categories: [Javascript, 개념정리]
tags: [javascript]
---

추석 잘 쉬고 다시 공부하려고 한다.  
추석 때 너무 늦게 자버릇 하니 엄청 피곤하지만  
근성으로 버텨낸다.  

---

## **연산자**  

오늘은 연산자에 대해 알아보자.  
누구나 아는 연산자이지만 그래도 그 속에 숨겨진 의미가 있다는 것을..  

연산자는 다양한 것들이 존재한다.  
가장 기본적인 것부터 시작해서 연산자의 비밀을 파해쳐 보자.  

---  

## **산술 연산자**  

가장 기본적인 연산자다.  
+,-,/,*,%가 있다.  

이거는 설명 안 해도 될 것 같다.  
그리고 **단항 산술 연산자**라고 있다.  

++ 이렇게 쓰면 증가,  
-- 이렇게 쓰면 감소이다.  
여기에는 약간의 비밀이 있다.  

우선 얘네 둘은 값을 변경시킨 후 **할당**까지 하게 된다.  

```js
let x = 1;

x++
console.log(x) // 2
```  

이렇게 말이다.  
따로 담아주지 않아도 암묵적 할당이 이루어진다.  
그리고 ++, --를 숫자 앞, 뒤에 쓰는 것에도 약간의 차이가 있다.  

```js
let x =1;

console.log(x, x++)
// 1, 1

let y =1
console.log(y, ++y)
// 1, 2
```  

위의 식을 보면 어떤 차이가 있는지 알겠지?  
x++ 처럼 뒤에 쓰면 할당 후 연산을 하며  
++y 처럼 앞에 쓰면 연산을 하고 난 뒤에 할당을 하게 된다.  
요건 모르는 사람이 많을 듯!  

+, -는 다른 잔재주도 존재한다.  

```js
let x = "1";

// 문자열을 숫자열로 변환
console.log(+x) //1

let y = true;
//boolean을 숫자로 변환
console.log(+y) // 1

y = false;
console.log(+y) // 0

```  

그 외에 산술 연산자 +는 연결하는 의미도 존재한다.  

```js
"1" + 1 // "11"

// true는 1
1 + true; //2

// false는 0
1 + false; // 1

// null은 0
1+ null // 1
```  

이렇게 + 연산자는 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환 된다.  
이런 것을 "암묵적 타입 변화", "타입 강제 변환" 이라고 한다.  

이제 왜 +의 결과가 저렇게 나오는지 알겠지?  

---  

## **할당 연산자**  

할당 연산자는 연산을 하고 다시 할당하는 것이다.  

```js
let x = 10;

x+=5 // 15
```
이렇게. += 말고도 -+, *=, /=, %= 모두 된다.  

---  

## **비교 연산자**  

비교 연산자도 많이 알 것이다.  
==, ===, !=, !== 이렇게 4가지가 있다.  
하지만 우리는 ===, !==만 쓴다.  

왜 ==, !=가 안 좋아서 안 쓰지만,  
왜 안 좋은지는 모를 것이다.  

==, !=는 좌항, 우항을 비교할 때 **암묵적 타입 변환**을 하고 나서 비교를 한다.  
위에서 배운 것이다.  

그래서 아래와 같은 결과가 나오는 것이다.  

```js
5 =='5' // true
```  

---  

## **typeof 연산자**  
 
typeof도 우리가 자주 쓰는 것이다.  
하지만 이게 완벽하지는 않다.  
null, [], {}, new Data()를 모두 "object"로만 결과를 나타내기 때문에  
정확히 어떤 것인지 알 수가 없다.  

여기서 null 또한 "object"로 나오는데  
이거는 **자바스크립트의 첫 번째 버전의 버그** 라고 한다.  

신기해서 적어본다.  
기존 코드에 영향을 줄 수 있기에 아직도 수정이 안 됐다고 한다..  

--- 

## **지수 연산자**  

지수 연산자는 ES7에서 도입된 것이다.  
나는 ES6까지만 잘 배웠는데  
언제 ES7이 나왔냐..  
아주 최신 문법이라는 것이다.  

```js
2 ** 2 // 4
```  

거듭제곱 해주는 연산자이다.  
이게 없을 때는 우리에게 익숙한 Math.pow()를 사용했다.  

---

오늘도 새로운 사실을 몇 가지 알아갔다.  
책에는 그 외의 내용들이 더 있었지만  
해당 내용들은 훨씬 간단하고  
기존에 알고 있었던 것이라 굳이 적지는 않았다.  





