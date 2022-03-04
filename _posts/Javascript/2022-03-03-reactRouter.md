---
layout: post
title: 'React-router 복습하기'
date: 2022-03-03 12:00:30  +0800
categories: [Javascript, React]
tags: [javascript, react]
---

리액트는 SPA 방식을 사용한다.  
한 번에 모든 페이지를 다운로드 받고  
url에 맞춰 해당 페이지만 보여주는 방식이다.  


#### SPA 라우팅 과정  

1. 브라우저는 최초에 '/'경로로 요청을 하면,  
2. React Web App 을 내려준다.  
3. 내려받은 React App에서 '/' 경로에 맞는 컴포넌트를 보여준다.  
4. React App 에서 다른 페이지로 이동하는 동작을 수행하면,  
5. 새로운 경로에 맞는 컴포넌트를 보여준다.  


위와 같은 역할은 React의 기본 기능이 아니다.  
React-Router-Dom이라는 라이브러리가 해주는 역할이다.  
react-router-dom은 공식 패키지가 아니기 때문에 다른 router 라이브러리가 많지만,  
대표적인 라이브러리라서 요즘에는 React 설치시 같이 설치가 된다.  

---  

#### 실습 전 만약 이런 오류가 뜬다면?  

실습을 하려고 하자마자 이런 오류가 떴다.  

![image](/assets/img/sample/reactRouter1.png)  

분명 BrowerRouter도 잘 쓰고 코드에 이상이 없다면,  
react-router-dom의 버전 문제일 것이다.  

```js
  npm install react-router-dom@5.3.0
```

위의 명렁어로 react-router-dom을 다시 한 번 설치해보자.  
나는 이렇게 해결했다.  
미래의 나, 꼭 기억해!!  

---  

### 기본 설정  

기본적으로 index.js에서 아래와 같이 **BrowerRouter**로 감싸주자.  

![image](/assets/img/sample/reactRouter2.png)  

그리고 간단하게  
아래처럼 **Route**를 이용한다면 기본적인 route를 이용할 수 있다.  

![image](/assets/img/sample/reactRouter3.png)  

하지만, 단순하게 저렇게 하면 문제가 하나 생긴다.  
/profile로 한 번 이동해보자.  

![image](/assets/img/sample/reactRouter4.png)  

그러면 의도하지 않게 home과 profile에 관한 내용들이 모두 나오게 된다.  
그 이유는,  
'/profile'이라는 경로는 '/'라는 기본 경로를 포함하고 있기 때문에  
'/' 컴포넌트와 '/profile'이라는 컴포넌트가 동시에 보이게 된다.  

이럴 경우 포함되는 경로를 모두 보여주는 것이 아니라,  
경로가 **완전히 일치** 하는 컴포넌트만 보여주라는 설정을 해야한다.  
**exact**라는 설정을 route 안에 넣어보자.  

![image](/assets/img/sample/reactRouter5.png)  

이렇게 하면 우리가 원하는 컴포넌트만 잘 보일 것이다.  

---  

### Dynamic 라우팅 설정  

동적 라우팅은 우리가 경로 주소에 바뀌는 값을 넣고,  
해당 값을 컴포넌트에서 받아 각각 다른 정보를 불러오는 것이다.  

동적 라우팅 설정은 아래와 같다.  
:를 이용하여 만든다.  

![image](/assets/img/sample/reactRouter6.png)  

이렇게 하고 profile 컴포넌트에서 아래 처럼 확인해보자.  

![image](/assets/img/sample/reactRouter7.png)  
![image](/assets/img/sample/reactRouter8.png)  

꼭 동적 라우팅에서만 위의 정보들이 나오는 것은 아니다.  
Route 설정이 됐다면 볼 수 있다.  

이후 '/profile/1' 페이지로 이동하고 아래처럼 console.log을 찍으면 1을 확인할 수 있다.  

![image](/assets/img/sample/reactRouter9.png)  

---  

### Dynamic 라우팅 설정 2  

쿼리 스트링 설정을 한 번 해보자.  

현재 About 쪽에는 위에서 했던 것처럼 다른 동적 라우팅을 해주지 않았다.  

![image](/assets/img/sample/reactRouter10.png)  

주소를 한 번 아래처럼 들어가보자.  

![image](/assets/img/sample/reactRouter11.png)  

![image](/assets/img/sample/reactRouter12.png)  

그러면 그냥 props로 안에 search에 우리가 주소창에 적은 쿼리 스트링이 있다.  

여기 들어있는 것을 조금 더 간단하게 사용해보자.  

![image](/assets/img/sample/reactRouter13.png)  

이런 식으로 **URLSearchParams** 라는 브라우저 내장 기능을 이용하면 간단하게 mark만 꺼낼 수 있다.  
하지만 이 방식의 단점은 2가지가 있다.  

1. obj.get()을 써야 한다는 귀찮음  
2. 지원하지 않는 브라우저도 존재  

이 문제를 해결하기 위한 라이브러리가 존재한다  

```js
 npm i query-string
```  

설치해보자.  

설치가 끝났다면 아래처럼 사용하면 된다.  


![image](/assets/img/sample/reactRouter14.png)  

![image](/assets/img/sample/reactRouter15.png)  

이러면 편하게 사용할 수 있다.  

---  

### Switch & NotFound  

Switch는 여러 Route 중 하나만 보여준다.  
exact를 뺄 수 있고, path를 잘못 들어갔을 때 NotFound 페이지를 보여줄 수도 있다.  

Switch 같은 경우는 if, else if 처럼 작동하게 된다.  
그래서 제일 상단에 있는 Route부터 시작해서 아래로 내려가며 같은 경로를 찾게 된다.  


![image](/assets/img/sample/reactRouter16.png)  

![image](/assets/img/sample/reactRouter17.png)  

위의 2개 이미지는 비슷해보이지만 다르다.  

위의 사진 같은 경우에는 /profile이 들어간 것이 보이고,  
아래의 사진 같은 경우에는 /:id가 들어간 것이 보이게 된다.  

그래서 가장 많이 포함된 경로를 제일 아래로 내리는 것이 좋다.  
아니면 그냥 exact 속성을 이용해도 괜찮다.  

또한, 제일 아래에 NotFound 페이지를 넣었을 경우,  
Switch를 통해 동일한 경로가 없을 경우 제일 아래에 있는 NotFound페이지를 보여주게 된다.  

![image](/assets/img/sample/reactRouter18.png)  

---  

### JSX 링크로 라우팅  

Link 태그로 라우팅을 한 번 해보자.  

![image](/assets/img/sample/reactRouter19.png)  

![image](/assets/img/sample/reactRouter20.png)  

![image](/assets/img/sample/reactRouter21.png)  

Link로 했을 경우 a태그로 작동을 하고 있다.  
서버에서 페이지를 가져오는 것이 아니라  
클라이언트에서 URL을 변경해서 그냥 가져오는 것이기 때문에 속도가 빠르다.  

NavLink라는 기능도 있는데,  
여기에는 actvie 기능을 이용해 스타일 지정이 추가로 가능하다.  
또한 exact 속성도 사용 가능하기에 매우 유용하다.  

---  

![image](/assets/img/sample/reactRouter22.png)  

이번엔 NavLink와 activeStyle, exact를 모두 적용시켜보았다.  

![image](/assets/img/sample/reactRouter23.png)  

그럴 경우 현재 경로와 똑같을 경우 Style 변경이 가능하다.  

---  

query string이 들어간 경우 actvieStyle 사용법이 조금 다르다.  

아래 코드를 보면 NavLink에는 isActive라는 콜백함수를 이용할 수 있다.  
isActive가 true일 경우에만 activeStyle이 발동되도록 할 수 있는데,  
isActive에는 인자가 2개가 들어온다.  

match, location.  
이 두 가지를 이용하면 특정 조건의 query string이나 경로일 때만  
activeStyle을 이용할 수 있다.  


![image](/assets/img/sample/reactRouter24.png)  

---  

### Ridirect  

우리가 원하는 컴포넌트로 바로 이동할 수 있도록 도와주는 역할이다.  

![image](/assets/img/sample/reactRouter25.png)  

Redirect를 이용한다면,  
특정 조건에 맞춰 바로 페이지를 이동시킬 수 있다.  

---  

끝!