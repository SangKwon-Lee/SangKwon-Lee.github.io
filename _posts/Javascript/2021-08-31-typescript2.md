---
layout: post
title: '타입스크립트 공부를 다시 시작하자 2편'
date: 2021-08-31 12:00:30  +0800
categories: [Javascript, typescript]
tags: [javascript, typescript]
---

2편이 시작됐다.  
지난 번에는 가장 기초적인 타입들을 공부했다.  
예전에 배웠던 것들이라 잊고 있던 부분이 많았다.  

늘 쓰던 타입만 쓰니까 그런듯.  
확실히 더 배워야지 활용도가 높은 타입스크립트를 쓸 수 있을 것 같다.  
오늘 배웠던 내용도  
너무 새로운 내용들..  
안 쓰니까 다 까먹지.  

---

## **Typescript**

블로깅을 하지 않지만  
객체지향 프로그래밍, 제네릭, 에러 처리 등을 배웠다.  

그중 오늘의 주 내용은 Utility Type이다.  
강의는 들었지만 실무에서 얼마나 활용할 수 있을지는 모르겠다.  
이렇게까지 쓰는 사람을 본 적이 없기에..  
그래도 알아두면 쓸 수 있지 않을까?  

## **Utility Type**

Utility Type이란 무엇인가?  
Javascript에 보면 미리 만들어 둔 method들이 많다.  
length, map, reduce, filter 등등..  

Typescript도 마찬가지이다.  
자주 쓸 것 같은 기능들을  
미리 만들어두어 개발자들이 편하게 사용하라고 둔 것이다.  

하지만 나는 실제로 쓴 적이 없는 걸..  
그래도 알아가자.  
어떤 Utility type이 있는지 보자.  

#### **Type Alias & Interface**

Utility Type에 들어가기 앞서 일단 이거부터 배우고 가자.  
언뜻 보면 Type Alias와 Interface는 큰 차이점이 없어 보인다.  
실제로 두 개를 같이 써도 실무에서는 큰 문제가 없는 듯 하다.  
정확하게 구별하면서까지 써야 할 일이 생기지 않아서 그런가?  

일단 간단하게 비교해 보자.  

