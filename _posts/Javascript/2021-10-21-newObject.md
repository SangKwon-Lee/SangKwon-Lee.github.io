---
layout: post
title: '생성자 함수에 대해 알아보자'
date: 2021-10-21 12:00:30  +0800
categories: [Javascript, 개념정리]
tags: [javascript]
---

오늘은 생성자 함수에 대해 알아보자.

---

## **생성자 함수**  

생성자 함수는 new연산자로 호출하는 것을 말한다.  
우리가 가장 많이 쓰는 new 연상자와 쓰이는 생성자 함수는  
아마도 new Date() 라고 생각한다.  
이렇게 new로 만드는 것에 대한 장단점은 무엇일까?  

---  

new로 만들 수 있는 것은 생각보다 많다.  
```js
new Object();
new String("A");
new Number(1);
new Boolean(true);
new Function('x', 'return x*x');
new Array(1,2,3);
new RegExp(/ab+c/i);
new Date(); 
```  

위의 것들이 모두 가능하다.  
객체 말고도 함수, 배열, 정규표현식 등을 만들 수 있다.  
여기서 만들어진 객체들을 **인스턴스**라고 부른다.  

하지만 우리는 보통 이렇게 만들지 않고 객체 리터럴 방식으로 만든다.  
객체 리터럴 방식은  
```js
let obj ={
  name: "A"
}
```  
이렇게 만드는 것을 말한다.  
이 방식이 직관적이고 간편하다. 하지만 단 하나의 객체만 만들 수 있다.  
동일한 내용의 객체를 여러 개 만들 때는 불편하다.  

생성자 함수로 여러 개의 객체를 간편하게 만드는 예제를 한 번 보자.  
아래 예제는 radius빼고는 모두 동일하다.  
하지만 radius값만 계속 변경되고 여러 개를 만들어야 할 때는 생성자 함수가 유리하다.  

```js
const circle1 = {
  radius:5,
  getDiameter(){
    return 2* this.radius;
  }
}
const circle2= {
  radius:10,
  getDiameter(){
    return 2* this.radius;
  }
```  


생성자 예시다.  
이렇게 로직만 잘 만든다면  
간편하게 동일한 내용의 객체를 여러 번 만들 수 있다.  

```js
function Circle(radius){
  this.radius = radius;
  thie.getDiameter = function (){
    return 2* this.radius;
  }
}

const circle1 = new Circle(5)
const circle2 = new Circle(10)
```

생성자 함수는 new를 앞에 붙이면 자동으로 생성자 함수로 동작하게 된다.  
위에서 new를 붙이지 않으면 undefined가 나온다.  

---  

## **생성자 함수의 인스턴스 생성 과정**  

생성자 함수는 쉽게 생각하면 하나의 **템플릿**을 만들어 두는 것이다.  
생성자 함수는 생성될 때 암묵적으로 인스턴스를 생성하고, 초기화 한 후 인스턴스를 반환한다.  

1. 인스턴스 생성과 this 바인딩 

생성자 함수 내부에 있는 this는 생성자 함수 내부에 자동으로 바인딩이 된다.  
그래서 this는 생성될 인스턴스를 가리킨다.  
여기서 바인딩이란 식별자와 값을 연결하는 과정을 의미한다.  

2. 인스턴스 초기화  
코드를 실행하면서 this에 바인딩되어 있는 인스턴츠를 초기화 한다.  
그리고 인수로 전달받은 값을 할당한다.  

3. 인스턴스 반환  

내부 과정이 모드 끝나면 인스턴스 생성이 끝난다.  

---  

## **내부 메서드 Call, Contruct**  

여기서부터는 조금 어려웠다.  

우리가 만드는 함수 선언문, 함수 표현식은 일반적인 함수로서 호출이 가능하며  
또한 생성자 함수로서 호출할 수 있다.  
생성자 함수로 호출하는 것은 함수를 호출 할 때 앞에 new를 붙이는 것을 말한다.  

우리가 만드는 함수는 함수 객체이다.  
함수 객체는 일반 객체처럼 내부 슬롯, 메서드를 갖고 있으며 Environment, FormalParameters, Call, Construct  같은
내부 메서드를 추가로 갖고 있다.  

함수가 일반 함수초 호출되면 내부 메서드 Call이 호출되고  
생성자 함수로 호출하면 내부 메서드 Construct가 호출된다.  

```js
function foo(){}  

foo() // 일반 호출 Call
new foo() // 생성자 함수 호출 Construct
```  
Call을 갖는 함수 객체를 **callalbe**이라고 하며  
Construct를 갖는 함수 객체를 **constructor**라고 한다.  
갖고 있지 않으면 **non-constructor**라고 한다.  

함수는 호출을 해야 하므로 반드시 callable이지만  
모든 함수가 Construct를 갖는 것은 아니다.  

그 말은 모든 함수는 호출할 수 있지만  
모든 함수를 생성자 함수로 호출할 수 있는 것은 아니다.  

---  

## **constructor & non-constructor**  

자바스크립트 엔진은 함수를 정의하는 방식에 따라 constructor와 non-constructor을 나눈다.  

constructor : 함수 선언문, 함수 표현식, 클래스  
non-constructor : 메서드, 화살표 함수  

---  


