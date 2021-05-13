---
layout: post
title: "React의 개념을 복습하자 [생명주기]"
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

## **React Lifecycle 생명주기**

리액트에는 **생명 주기**라는 것이 존재한다.  
왜 이름을 이렇게 지었는지는 모른다.  
리액트.. 살아있냐?

**생명 주기**란 간단하게 말해서 우리가 만든 컴포넌트에서 실행, 업데이트, 삭제 될 때마다  
리액트에서 특정한 이벤트가 발생하는 것이다.
이 생명주기는 나중에 **hooks**가 나오면서 조금 변했다.  
그래서 역사는 알아야 하니 옛날꺼도 배워보자.

#### **Mount**

리액트에서 처음 실행될 때 Mount라고 표현한다.  
우선 처음에는 state, context, defaultProps를 저장한다고 한다.(어디에 저장하는지는..)  
그 이후 **componentWillMount**라는 함수를 호출하게 된다.  
그리고 나서 render로 넘어가 render에 있는 내용을 DOM에 넘기게 된다.  
DOM에 다 넘기게 되면 **componentDidMount**를 호출하게 된다. (호출은 실행한다는 것)

여기서 WillMount는 render, DOM에 접근하기 전에 일어나는 상황이기에 여기서  
props나 state를 변경하면 안 된다.

그러나 DidMount는 이미 DOM이 생긴 뒤라 여기서는 state, props를 변경할 수 있다.  
그래서 보통 여기서 AJAX요청을 통해 데이터를 받아오게 되는 것이다.
**오호라!!**

여기까지가 처음 컴포넌트가 실행됐을 때 일어나는 일들이다.

#### **Props Update**

자 이제 기본적인 데이터는 받아왔다.  
그리고 데이터를 state에 저장했을 것이다.  
그리고 props로 데이터도 넘겨줬을 것이다.  
그 상황에서 prpos가 바뀔 때는 어떻게 될까??

업데이트가 직접적으로 되기 전에 **componentWillReceiveProps**가 호출된다.  
이름이 너무 길어서 짜증난다.  
그 후 **shouldComponentUpdata**, **componentWillUpdate**가 차례대로 호출된다.  
그리고 props를 통해 render가 업데이트 되면 **componentDidUpdate**가 호출된다.

여기서 render하기 전 상태는 sholdcomponentUpdate가 담당하고 있다.  
그래서 여기서 성능 최적화를 한다고 한다.  
필요 없는 건 지우는데 코드로는 본 적이 없다.

WillUpdate에서는 state를 바꿔서는 안 된다고 한다.  
아직 props가 업데이트 전이라 여기서 바꾸면 다시 should로 넘어가게 된다.  
DidUpdate에서는 render가 업데이트 된 이후이기 때문에 DOM에 접근할 수 있다.

여기까지 봤을 때 render가 완료되었는지 아닌지에 따라 기준이 나뉘는 것 같다.

#### **State Update**

우리는 setState를 통해 state를 업데이트 해준다.  
이 과정은 props 업데이트와 다 동일하지만 componentWillReceiveProps만 호출되지 않는다고 한다.

#### **Unmount**

컴포넌트가 제거되는 것을 unmount라고 한다.  
제거될 때는 **componentWillUnmount**라는 함수가 호출된다.  
여기에서는 이미 제거된 컴포넌트에서 만들어 놓은 함수들을 제거하는 활동을 한다고 한다.

---

## **React Hooks Lifecycle 생명주기**

위에 보면 너무 많은 mount들이 존재한다.  
그래서 hooks에 오면 많이 줄어들었다.

#### **useEffect**

바로 useEffect로 대부분을 해결한다.  
얘는 WillMount, DidMount, DidUpdate, Unmount를 모두 포함하고 있다.  
얼마나 좋아?  
그 말은 state, props가 변경될 떄마다 useEffect가 실핸 된다는 것이다.

useEffect에는 인자가 2개가 들어간다.  
첫 번째 인자에는 실행할 코드, 2번 째 인자에는 2번 째 인자가 바뀔 때마다 첫 번쨰 인자에 들어간 코드가 실행.

그래서 2번 째 인자에 아무것도 적지 않으면 무한 useEffect가 발생하니 조심할 것.

그런데 만약 DidUpdate만 하고 싶다면?  
useEffect는 DidMount와 DidUpdate를 모두 포함하기 때문에 힘들다.

그래서 사용하는 것이 useRef라는 것!!

#### **useRef**

state를 바꾸면 render가 다시 실행된다.  
그거랑 상관없이 render가 되지 않고 state만 저장하고 싶다면??

그게 바로 useRef다.
useState로 만들지 않고  
const aaa = useRef("");

이렇게 만들면 aaa의 값이 바뀌어도 render가 되지 않는다.
하지만 여기서 aaa값을 가져올 때는 aaa.current로 확인해야 한다.

---

그 외에도 useMemo, useCallback 등 많지만  
필요 없는 내용들.  
그래서 일단 여기까지만 쓰겠다.  
호호
