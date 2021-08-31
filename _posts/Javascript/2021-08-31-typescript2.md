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

--- 


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

---  



#### **Type Alias & Interface**  


Utility Type에 들어가기 앞서 일단 이거부터 배우고 가자.  
언뜻 보면 Type Alias와 Interface는 큰 차이점이 없어 보인다.  
실제로 두 개를 같이 써도 실무에서는 큰 문제가 없는 듯 하다.  
정확하게 구별하면서까지 써야 할 일이 생기지 않아서 그런가?  

일단 간단하게 비교해 보자.  

![image](/assets/img/sample/type17.png)  
우선 만드는 방식은 똑같다.  
그리고 적용시키는 방법도 똑같다.  

아래처럼 type, interface 모두 class, Extends, object형태 모두 같다.  
사실 React를 하다보면 object형태를 가장 많이 쓰게 된다.  
나머지는 이용한 적이 없다.  
![image](/assets/img/sample/type18.png)  

다음은 차이점이다.  
우선 Type Alias는 Union Type으로 만드는 것이 가능하다.  
Union Type은 종종 쓰는 일이 있으니 그럴 땐 Type Alias를 이용하자.  
![image](/assets/img/sample/type19.png)  

보통 data를 담는 목적이면 type을 쓰고  
function, class 같이 규격이 필요할 때는 interface를 쓰는 것이 국룰이라고 한다.  

여기서 규격이라고 함은,  
잘 모르겠지만 느낌상 함수 같은 것들??  
단순히 변수, 객체의 타입을 간단하게 정할 때는 type 아니면 interface.  

---  

#### **Index Type**  

Index Type은 우리가 객체의 키 값에 타입을 지정해 두었다면,  
다른 곳에서 해당 키 값으로 Type을 지정할 수 있는 것이다.  
예제를 한 번 보자.  

현재 Animal에는 name, age, gender 키가 있고, 해당 키에는 각각의 type이 지정되어 있다.  
![image](/assets/img/sample/type20.png)  

위에 지정한 Animal Type으로 아래와 같은 것들이 활용 가능하다.  
type Name은 Animal["name"]에 지정했던 type이랑 같게 된다.  

혹은 Person에 있는 gender도 Animal에 있는 'gender'의 Type과 같게 된다.  
그래서 "male" | "female"만 할당이 가능하다.  
![image](/assets/img/sample/type21.png)  
![image](/assets/img/sample/type22.png)  

Index Type의 활용도는 아직 잘 모르겠다.  
반복되는 코드가 있을 때 Type 지정을 줄일 수 있을 정도??  

한 번 기회가 되면 쓰고 싶다.  


---  

#### **Mapped Type**  

배열에서 map은 뺴놓을 수 없는 기능이다.  
배열 속 요소들에게 반복적인 일을 할 때 for 대신 아주 유용하게 쓸 수 있는 녀석이었다.  
이런 map이 Typescript에도 있다는 사실!  

여기 간단한 Type 하나가 있다.  
아직은 아무런 옵션이 붙어있지 않다.  
![image](/assets/img/sample/type23.png)  

하지만 경우에 따라  
해당 타입의 키들을 모두 optional로 바꾸고 싶거나 readonly로 바꾸고 싶을 때가 있을 것이다.  
그럴 때 모든 키에 하나 하나 readonly나 ?를 붙이는 귀찮은 작업을 하지 않아도 된다.  

아래에 보면  
"in keyof"를 이용했다.  
이것은 for in과 같은 역할을 한다.  
type 안에 있는 모든 key들을 돌면서 원하는 작업을 해준다.  

첫 번째는 ?를 붙였고  
아래에는 readonly를 앞에 붙였다.  
뒤메 있는 T[P]에서 T는 우리가 넣을 배열이나 타입이고, [P]는 키을 이야기한다.  
즉, T[P]는 기존 T배열에 있던 키의 type을 그대로 적용시킨다는 점.  
그 앞에 readonly나 ?를 추가하는 것 뿐이다.  
![image](/assets/img/sample/type24.png)  

아래가 적용된 모습이다.  
Video type은 title, author가 있었고,  
각 키에 ?를 다 붙여주었다.  
![image](/assets/img/sample/type25.png)  

언젠가 한 번은 쓸지도?  
지금은 아직 ?나 readonly를 적극적으로 활용하지는 않는다.  
쓰는 일이 있어도 미리 적어둘 듯.  

---  

#### **Conditional Type**  

Conditional Type은 타입에 조건을 걸어  
입력되는 값에 따라 type을 바꾸는 것을 이야기 한다.  

아래처럼 type에 조건을 달 수 있다.  
![image](/assets/img/sample/type26.png)  

Check type에서 <T>자리에 string이 들어오면 Check는 Boolean 타입이 된다.  

이런거 어디다가 써먹냐?  

그냥 있다는 것만 알아두자~  

---  

#### **Readonly Type**  

Readonly는 보기에 자주 사용할 것 같다.  
아직은 쓸 일이 없긴 하지만  
중요한 경우에는 일부로라도 쓸 것 같다.  
간지 나니까!!  

사용법은 아래와 같다.  
기존에 만든 Type이 있다면  
이렇게 Readonly를 써주자.  

![image](/assets/img/sample/type27.png)  


---  

#### **Partial Type**  

얘도 굳이 필요한가 싶다.  
기존 값을 변경하고 싶을 떄 쓰는 type이라고 하는데  
흠..  

활용도를 잘 몰라 그냥 한 번에 사진 롤리고 끝낸다.  

![image](/assets/img/sample/type28.png)  

---  

#### **Pick Type**  

Pick은 기존에 선언했던 type에서 필요한 값만 몇 개 뽑아서 쓰는 것을 말한다.  
보통 객체 안에 여러가지 키가 들어가는데  
해당 키를 한 번 더 다르게 사용하는 경우에 쓰면 좋을 것 같다.  

만약 Video라는 타입 안에 id, title만 뽑아서 다시 쓰고 싶다면  
아래처럼 Pick을 이용해서 type을 만들어주면 된다.  
![image](/assets/img/sample/type29.png)  

Pick 의 반대 개념으로는 omit이 있지만  
이거 쓸 바엔 그냥 Pick을 쓰는 것이 좋기에  
omit은 따로 적지 않겠다.  

---  

여기까지가 2편의 끝이다.  
마지막으로 Record라는 것도 있었지만  
얘는 더 쓸모가 없어보였기에 안 썼다.  

Utility Type은 실무에서 안 쓰는 것이 더 많을 것 같다.  
아직 내가 Typescript를 깊게 공부하고 고민하지 않아서 그럴 수도 있다.  

모두가 쓸모 없는 것은 아니니  
실무에 적용할 수 있은 부분은 적극적으로 적용하며 실력을 기르자.  

3편이 있다면 또 돌아오겠다.  

