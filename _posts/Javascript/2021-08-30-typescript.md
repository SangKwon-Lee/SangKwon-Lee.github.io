---
layout: post
title: '타입스크립트 공부를 다시 시작하자 1편'
date: 2021-08-30 12:00:30  +0800
categories: [Javascript, typescript]
tags: [javascript, typescript]
---

오늘은 typescript에 대해 기초부터 다시 공부해보려고 한다.  

예전에 엘리 강의를 들었는데 아직 기초가 부족한 듯 하다.  
지금도 조금은 쓰고 있지만 아직 뭔가 부족한 느낌적인 느낌.  
typescript는 진짜 잘 써야지 간지인데 아직 간지가 안 난다 이말이야  

typescript를 85% 라도 활용하기 위해 다시 공부합시다.  
일단 오늘은 1편이다.  
1편은 언제나 가장 기초적인 내용만 들어가 있다.  
그러니 큰 기대는 하지 말아라.  

---

## **Typescript**

TypeScript는 어느덧 Javascript 개발자에겐 필수 요소가 됐다.  
typescript 없이 개발하는 건 취급하지 않을 정도다.  
매우 귀찮은 녀석이지만 모든 곳에서 요구한다.  
어떤 녀석이길래 이렇게까지 중요한 요소가 됐을까?  
오늘부터 하나씩 알아가보면 왜 그런지 알 수도 있..  

우선 typescipt의 주요 기능은  
javascript의 모든 요소에게 "Type"이란 것을 지정해주는 역할을 해준다.  
"Type"을 지정해주면, 해당 데이터는 해당 지정된 Type만 할당할 수 있다.  

예를 들어, 주요 Type은 string, number, boolean과 같은 녀석들이 있다.  
우선 한 가지 예시를 보자.  
아래 str 변수에 string이라는 type을 지정해주었다.  
그러면 str은 string만 들어갈 수 있게 된다.  
```js
let str: string = "hello"
str = "good"
// str = 5 => 오류!!
```

언뜻 보면 매번 type을 지정해주어야 하기 때문에 매우 귀찮을 수 있다.  
하지만, 나중에 보면 더 좋은 기능들도 많으니 기다리라.  

--- 

## **Typescript 기본 type 지정**

위에서 간단하게 string 타입을 지정해 주는 것을 보았다.  
그 외에 어떤 타입들이 있을까?  


#### **기본 타입**  
아래처럼, number, boolean 타입도 있다.    
```js
let num: number = 5;
const boal : boolean = false;
```

#### **2가지 이상의 타입 A 혹은 B**  
혹은 2가지 타입을 동시에 지정할 수도 있다.  
마크다운 코드는 안 예쁘니 스샷을 찍자.  
![image](/assets/img/sample/type1.png)  

#### **함수의 type**  
혹은 함수가 어떤 type을 return 하는지도 지정할 수 있다.  
![image](/assets/img/sample/type2.png)  

그런데 우리가 함수를 쓰다보면 return이 없을 때도 있다.  
그런 건 void라고 한다.  
react를 쓰다보면 void 함수가 참 많긴 하다.  
![image](/assets/img/sample/type3.png)  

#### **any & unknown**  
이렇게 모든 곳에 type을 지정할수록 코드는 좋아진다.  
하지만, 나 같은 초보자들이 코드를 작성하다 보면,  
어떤 것이 어떤 type인지 쉽게 알지 못하는 경우도 많다.  
그럴 때는 임시로 써주는 any 타입이라는 것이 있다.  

any는 모든 종류의 type이 다 들어와도 상관이 없다는 뜻이다.  
하지만, 그만큼 typescript를 쓰는 의미가 없어지니 정말 머리 터질 때만 쓰자.  
![image](/assets/img/sample/type4.png)  

사진에는 '절대'라고 썼지만,  
인생 살다보면 '절대'라는 것이 어디있나?  

any랑 비슷한 것이 있는데 unknown도 있다.  
![image](/assets/img/sample/type5.png)  
역시나 any와 같기 때문에 되도록 쓰지말자.  
unknown과 any는 비슷한 역할이기 때문에  
주로 any를 쓴다.  

#### **never**  

never 타입은 에러를 return 할 때 쓰는 타입이라고 한다.  
하지만 지금까지 써본 적은 없다.  
그래도 알아두면 핵간지?  
딱 한 번이라도 쓸 때 그 때를 위해 알아두는 것.  
그것이 간지.  

![image](/assets/img/sample/type6.png)  

#### **object**  

object 타입 또한 잘 쓰지 않는다고 한다.  
any와 같은 느낌으로,  
원시타입이 아닌 모든 것이 다 들어가기 때문이다.  

뒤에서 더 나오겠지만,  
모든 객체의 키 값에도 type을 다 지정해주기 때문에  
한 번에 object 타입을 지정해주는 일은 없다.  

![image](/assets/img/sample/type7.png)  

#### **Array**

배열은 타입을 지정하고 나서,  
배열 안의 요소들이 어떤 타입으로 들어가는지도 지정해줘야 한다.  

![image](/assets/img/sample/type10.png)  
하는 방법은 2가지 이지만,  
주로 string[] 모양을 쓴다.  

Array<number>은 나중에 readonly를 쓰지 못하기 때문이다.  

---

## **Typescript 함수**  

위에서는 간단한 변수들에 타입을 지정하는 것을 주로 알아봤다.  
그럼 함수에는 어떻게 활용할까?  

기본적으로 함수에는 인자와 어떤 것을 return 하는지에 대한 타입을 지정한다.  
![image](/assets/img/sample/type8.png)  

그리고 우리가 주로 쓰는 동기함수인 Promise, async도 타입이 따로 있다.  
![image](/assets/img/sample/type9.png)  
async, Promise 모두 Promise타입으로 지정한다.  

---

## **Type Aliases**  

Type Aliases는 가장 많이 쓰는 경우이다.  
우리가 string, number 이렇게 간단한 건 바로 쓸 수 있지만,  
보통 객체 안에 어떤 요소들이 들어간다면 type Aliases를 쓰게 된다.  

![image](/assets/img/sample/type11.png)  

이렇게 Text라는 이름을 만들고 string으로 지정해준다.  
그리고 다른 변수에 Text라는 type을 지정해주면 된다.  

가장 많이 쓰는 방식이 아래와 같다.  
![image](/assets/img/sample/type12.png)  

---

## **Type Union**  

Union type은 발생할 수 있는 많은 케이스 중에 하나를 선택하는 것이다.  
예를 들어 A라는 변수는 B 혹은 C 타입이다.  
라고 지정하는 것.  

이렇게 하면 direction에는 Direction Type에 있는 4가지 string만 할당할 수 있다.  
![image](/assets/img/sample/type13.png)  

그러면 이런 Union은 언제 주로 쓰게 될까?  
아래 예시를 한 번 보자.  

![image](/assets/img/sample/type14.png)  

login이라는 함수는 LoginState라는 type을 return하게 된다.  
그리고 LoginState는 SuccessState 혹은 FailState 둘 중의 하나의 값으로 밖에  
지정할 수 없다.  

이렇게 해서 return 값을 정확하게 지정해줘서  
오류를 줄이는 것.  
하지만 이렇게 하면 그렇게 좋은 예시는 아니다.  
밑에서 더 좋게 만들어 보자.  

---

## **Type Discriminated**  

위에서 Login 함수로 Union Type을 만들어주었다.  
하지만 함수에서 return 하는 값을 Union으로 줄 때는  
return값의 공통점을 두는 것이 함수를 작성할 때 더 편하다.  

지금 SuccessState와 FailState의 안에는 공통점이 없다.  
한 번 만들어 주자.  

![image](/assets/img/sample/type15.png)  
위에처럼 만들면 두 개의 State는 result라는 공통 키를 갖고 있다.  

그러면 아래 함수처럼 공통된 값을 갖고 if를 작성할 수 있다.  
훨씬 직관적으로 함수를 바꿀 수 있는 것이다.  
![image](/assets/img/sample/type16.png)  

정리하면, Union Type을 객쳋로 만들 때는  
각각의 공통점을 만들어서 코드를 더 직관적이고 구별하기 쉽게 만들어 주자.  

---

그 외에 Enum, inference, assertion도 있지만  
실무에서 사용하는 일은 보지 못했다.  
그래서 요거는 패스!  

다음 2편에서 다시 만나자.  

