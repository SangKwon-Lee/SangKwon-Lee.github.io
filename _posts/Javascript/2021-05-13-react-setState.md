---
layout: post
title: "React의 개념을 복습하자 [불변성]"
date: 2021-05-13 12:00:30  +0800
categories: [Javascript, react]
tags: [javascript, react]
---

React.  
이미 React로 개발도 하고 Next로도 해봤다.  
이제와서 React를 기초 개념을 다시 정리하는 이유는?  
더 정확하게, 더 자세하게 알기 위함.  
오키오키?

---

## **React의 불변성**

리액트에서는 state의 불변성을 지켜야 한다고 한다.  
그 이유는 무엇일까?  
그 이유를 찾기 위한 코공의 모험이 시작된다.

그 뿌리를 알려니 React의 render과정을 먼저 알아야 했다..  
이 선택 좋은 것인가??

---

### **기존 DOM의 render 과정**

DOM은 HTML문서를 객체 기반으로 표현한 방식이다.  
그래서 우리는 javascript에서 document.querySelector를 이용해서 HTML에 접근할 수 있는 것이다.

1. html문서를 읽고 안에 있는 html태그들을 이용해 DOM으로 바꾼다.
2. 그러면 자연스럽게 document객체가 생김!
3. 그 이후에 css파일을 가져온다.
4. 그리고나서 화면에 그려주게 된다.

---

### **Virtual DOM의 render 과정**

말 그대로 가상 DOM이다.  
가짜라는 것.

왜 가상 DOM이 필요했을까?  
요즘 아무리 VR이 많이 발전했다고 하지만  
DOM 너도 VR하고싶냐?

만든 이유는 DOM을 더 빠르고 간결화하기 위해서이다.  
어떻게 하느냐?

1. 기존 DOM은 처음부터 끝가지 모든 부분을 랜더링하게 된다.
2. 그러면 조금의 데이터만 바뀌어도 처음부터 다 다시 랜더링 해야 한다는 점..

3. 그래서 Virtual DOM을 만들었다.
4. 이 녀석의 역할은 DOM에 뿌리기 전에 Virtual DOM에 미리 만들어 보고
5. 거기서 기존 DOM과 비교해 바뀐 부분만 DOM에 render할 수 있도록 해준다.  
   오우!

React가 이 Virtual DOM을 이용해 render를 한다 이말이야.

---

## **React Render**

```js
ReactDOM.render(<App />, document.getElementById("root"));
```

요런 비슷한 코드를 React에서 봤을 것이다.  
이게 바로 Virtual DOM을 만드는 함수이다.

그리고 컴포넌트를 실행한다.

React화면에서 바뀌는 부분은 State로 만들어준 녀석들 밖에 없다.  
그래서 State 기준으로 render가 발생하는 것이다.

그런데 그 변하는 것을 어떻게 아느냐?  
바로 setState()를 통해 알 수있다.  
setState()는 State의 불변성을 지켜주면서 값을 바꾸게 된다.

그 말은 무엇이냐?  
불변성을 지킨다는 것은 기존 값을 기억하고 있다는 것과 같다.  
기존 State값을 알고 있는 상태로 새로운 State값을 넣어주면서  
기존 State와 바뀐 State의 변화을 알아차리는 것이다.

그러면 State의 변경을 확인했으니  
React는 Render에 들어가게 된다.

---

## **이제 나오는 React 불변성**

우리는 지금까지 React의 Render 과정과  
setState가 불변성을 유지시켜준다는 것도 배웠다.

그러면 setState()가 객체, 배열이며  
객체의 일부분만 바꾼다면..?

그럴 때를 위해 우리는 ...연산자를 써야한다.

```js
let a = { b: "123" };
let c = a;

c.b = "1234";
```

이렇게 하면 a와 c의 값이 모두 바뀌게 된다.  
그러면 기존 값이 무엇인지 알 수가 없기 때문에  
State에서 무엇이 변경된지 인지하지 못하고,  
이는 Virtual DOM 에서도 문제를 일으키게 된다.

```js
let a = { b: "123" };
let c = a;

c.b = { ...c, c: "1234" };
```

이렇게 ... 연산자를 이용하면 기존 a의 값이 변경되지 않는다.  
그러면 a, c가 서로의 값을 비교할 수 있고,  
State의 값이 바뀐 것을 인지할 수 있다.

그래서 State의 불변성을 꼭 지켜줘야 한다는 것이다.

---

유익한 시간이다.  
하하하
