---
layout: post
title: "Async & Await"
date: 2020-12-28 11:20:30  +0800
categories: [Javascript, 개념 정리]
tags: [Javascript, Async & Await]
---

![image](/assets/img/sample/async1.png)

# **Async & Await**

Async & Await 는 무엇일까?  
앞서 배운 비동기함수를 조절해주는 Promise를 더욱 간단하게 쓸 수 있는 새로운 문법이다.

### **Async**

Async은 함수 앞에다가 붙이면 return 값을 자동으로 promise처럼 바꿔준다. 쒸엣

![image](/assets/img/sample/async2.png)

그럼을 보면 func1은 Function 앞에 async을 붙여주었고 func2 는 앞에서 배운 promise로 리턴을 하였다.  
두 함수의 결과는 같다.

### **Await**

**Await는 Async를 붙인 함수 안에서만 활용이 가능한 녀석이다.**  
Await를 쓰면 promise 함수의 결과값을 가져올 수 있다.

![image](/assets/img/sample/async3.png)

지난 번에 작성한 Promise 함수이다. 한 번 then으로 한 것과 async & await를 비교해보자.

#### **async & await를 쓸 때**

![image](/assets/img/sample/async4.png)

#### **then을 쓸 때**

![image](/assets/img/sample/async5.png)

두 녀석의 결과는 같다.

## **하지만 누가 더 편리해 보이는가?**
