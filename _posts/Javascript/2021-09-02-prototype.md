---
layout: post
title: 'prototype에 대해 알아보자'
date: 2021-09-02 12:00:30  +0800
categories: [Javascript, 개념정리]
tags: [javascript]
---

오늘은 잠깐 prototype에 대해 알아볼 것이다.  
조금씩 공부하는 중.  
작게, 기본적인거라도 일단 알아가면 언젠간 도움이 되지 않을까?  
어려운 것을 공부하기 보다  
일단 기본을 쌓아 다른 것들을 더 빨리 이해할 수 있는 밑거름으로 쓰자.  

prototype에 대해 한 번쯤은 누구나 들어보았을 것이다.  
하지만 실질적으로 prototype에 대한 코드를 작성하는 일은 없기에  
무슨 일을 하는지 잘 모를 수도 있다.  
마치 나처럼!  

이번에 조금이라도 알아보자.  


---

## **Prototype**  

prototype은 javascript에서 상속과 객체지향 프로그래밍을 만들기 위한 녀석이다.  
또한, prototype으로 코드의 재사용성을 높일 수 있다.  
예전 문법에는 모두 prototype 방식으로 코드를 작성했지만  
javascript 언어가 계속 진화하면서  
현재는 우리가 다르게 쓰고 있는 것이다.  

그럼 간단한 예제로 어떻게 prototype을 이용해서 상속을 받을 수 있는지 알아보자.  

여기 간단한 x,y의 빈 객체가 있다.  
얘네들을 console.log()로 한 번 확인해 보자.  
![image](/assets/img/sample/proto1.png)  

이렇게 prototype이라는 것이 들어있는 것을 확인할 수 있다.  
![image](/assets/img/sample/proto2.png)  

이 prototype은 한 번 더 object라는 것을 상속 받고 있다.  
그래서 toString()과 같은 메소드를 이용할 수 있게 되는 것이다.  
아래 사진을 보면 그 외의 많은 것들을 상속 받고 있다.  
![image](/assets/img/sample/proto3.png)  

그래서 아래와 같은 결과가 나온다.  
같은 Object를 상속받고 있기 떄문이다.  
```js
x.__proto__ === y.__proto__  // true
```
우리가 자주 사용하는 .map, .filter, .length 들도 모두  
Object를 상속 받고 있기에 가능한 일이다.  

그러면 이런 prototype과 같은 상속 개념으로 무엇을 더 해볼 수 있을까?  

---

#### **Instance member Level**
이번엔 함수를 하나 만들어 보자.  

CoffeeMachine이라는 함수를 하나 만들었고, 그 안에 또 다른 함수가 있다.  
그리고 new를 이용해 새로운 2개의 Instance를 만들어 주었다.  
machine1, 2는 CoffeeMachine을 상속 받고 있다.  

![image](/assets/img/sample/proto4.png)  

아래는 console.log()의 결과이다.  
![image](/assets/img/sample/proto5.png)  

이렇게 new를 통해 상속받는 것을 Instance Level 이라고 한다.  

---

#### **Prototype member Level**  

다음은 Prototype member Level 상속이다.  
위에서 만든 CoffeeMachine 안에 makeCoffee라는 함수의 위치를 바꿔보았다.  
![image](/assets/img/sample/proto6.png)  

그러면 기존의 makeCoffee는 prototype 안으로 들어가게 된다.  
![image](/assets/img/sample/proto7.png)  
위에서 보았듯이 proto는 Object를 상속 받고 있다.  
그렇게 되면 machine1은 CoffeeMachine을 상속 받고,  
그 CoffeeMachine은 Object를 다시 상속 받는 것이다.  

---