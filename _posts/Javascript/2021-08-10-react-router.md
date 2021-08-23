---
layout: post
title: 'React-Router-Dom에 대해 알아보자'
date: 2021-08-10 12:00:30  +0800
categories: [Javascript, React]
tags: [javascript, react]
---

이직하는 곳에서 Next가 아니라 React를 쓴다.  
그래서 라우트하는 방법이 달라졌다.

예전에 react 라우트하는 방법을 알았지만  
안 쓴지 너무 오래돼서  
오랜만에 다시 공부하려고 한다.

미리미리 공부해가자.

---

## **React-Router-Dom**

React를 사용한다면 필수로 설치해야 하는 route다.  
기능이 간편하고 좋다.

물론 Next에서 기본으로 제공해주는 것보다는 불편하긴 하다.  
설치도 해야하고 page이동도 다 설정을 해줘야 하니..

그래도 react사용하니까 배워두자.

일단 기본적으로 설치를 하자.

```js
yarn add react-router-dom
```

---

## **기본 설정**

우선 app.js에서 설정을 해야 할 것이 있다.

![image](/assets/img/sample/route1.png)

요게 가장 기본적인 준비이다.  
이렇게 BrowerRouter에 감싸여진 컴포넌트들은 새로고침을 하지 않고도 주소 변경이 가능하다.

그리고 라우트할 페이지를 2개 만들어 주었다.

![image](/assets/img/sample/route2.png)

![image](/assets/img/sample/route3.png)

---

## **Route Path**

Route path는 우리가 어떤 주소로 들어갈 때 어떤 컴포넌트를 보여줄지 도와주는 기능이다.

우선 위에서 사용할 기능들을 불러온다.  
미리 여러 개 불러왔다.  
![image](/assets/img/sample/route4.png)

아래와 같이 작성을 하고, 해당 주소로 들어가면 해당 컴포넌트가 보이게 된다.  
exact를 설정을 해두지 않으면 다른 컴포넌트와 함께 뜨는 경우도 있다.

그러니까 해주자.

path를 한 번에 여러개 넣는 방법은 []안에 배열로 넣어주면 가능하다.  
![image](/assets/img/sample/route5.png)

---

## **Route Link**

Link는 우리가 무엇가를 클릭했을 때 해당 주소로 이동하게 도와주는 녀석이다.

![image](/assets/img/sample/route6.png)

우선 설정은 위와 같다.  
그러면 페이지에는 아래 처럼 나온다.

![image](/assets/img/sample/route7.png)

개 못생겼다.  
Link태그 꾸미는 건 나중에 하련다.  
우선 기능이 잘 돌아가니 다행.

---

## **Route URL**

중요한 부분이다.  
우리가 게시글을 클릭하면 해당 게시글로 가서 맞는 데이터를 보여줘야 한다.  
그러면 게시글 마다 페이지를 만드는 것이 아니라  
한 페이지를 만들고 게시글 마다 다른 데이터를 보여줘야 한다.  
어쨌든 주소는 각각 다를텐데 한 컴포넌트에서 해결해야 하는 것.

아래처럼 해보자.

![image](/assets/img/sample/route8.png)

우리는 보통 Query를 통해 데이터를 받아오게 된다.  
그리고 그 data를 return에 뿌려주는 형식이다.

지금은 데이터가 따로 없으니 억지로 만들어 주었다.  
그리고 여러 코드들이 있다.

![image](/assets/img/sample/route9.png)

그리고 Route 부분은 위와 같다.  
:username 이런 식으로 하면 :username은 하나의 변수처럼 작동하게 된다.  
그래서 Profile컴포넌트에 match라는 props가 자동으로 전달이 된다.  
그러면 match에 어떤 내용들이 있는지 한 번 보자

위 사진에서 길동프로필을 클릭해서 해당 주소로 들어가서  
console.log(match)를 한 결과이다.

![image](/assets/img/sample/route10.png)

보면 path, url 등이 들어있다.  
안에 보면 :username도 있고, killdong도 있다.

이걸 보면 유추할 수 있는 것은  
next.js에서 다이나믹 라우트를 했던 것처럼  
데이터를 받아오고 나서 해당 게시글에 Link to 태그를 통해 Name같은 거를 주면  
해당 게시글 페이지로 따로 들어와서 해당 게시글에 대한 정보를 보여줄 수 있다는 것이다.

---

## **withRouter**

HOC 개념이다.  
HOC는 A컴포넌트가 실행될 때  
B 컴포넌트의 코드도 같이 적용되어 실행되어야 할 때 사용된다.

그래서 B컴포넌트 같은 경우는 공통 컴포넌트로 빠지게 된다.  
많은 컴포넌트에서 동일한 코드가 필요할 때 사용하기 때문이다.

withRouter는 router가 없는 컴포넌트에서도  
route 기능들을 모두 사용할 수 있도록 따로 공통 컴포넌트로 뺀 녀석이다.

![image](/assets/img/sample/route11.png)

위에처럼 코드를 쓰고 우리가 원하는 컴포넌트에 함께 사용하면  
해당 컴포넌트 cosnole.log()에는 route에 관련된 모든 정보가 뜨게 된다.

그러면 다른 컴포넌트에서는 어떻게 쓰느냐

![image](/assets/img/sample/route12.png)

2번 째와 28번 쨰 코드를 보라.

```js
import WithRouterPage from './withRouter';
<WithRouterPage />;
```

이렇게 공통 컴포넌트를 불러오고 return 부분에서 사용해주면 된다.

![image](/assets/img/sample/route13.png)

---

## **Switch**


![image](/assets/img/sample/route14.png)

그래서 보통 이렇게 다 감싸준다.

---

## **마무리**

그 외에도 route에는 부가적은 다양한 기능들이 있었다.  
하지만 아직 다 정리하기에는 시간도, 내 실력도 부족하기에  
기본적인 기능들만 정리했다.

해당 내용들은
"리액트를 다루는 기술" 이라는 책의 내용들을 다시 적은 것이다.

이제 다시 react를 쓰고 route를 쓰라하면  
그래도 금방 적응할 수 있을 것 같다.
