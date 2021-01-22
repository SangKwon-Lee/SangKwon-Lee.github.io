---
layout: post
title: "데이터 자료구조. Stack / Queue"
date: 2020-12-03 11:20:30  +0800
categories: [자바스크립트, Data Structure]
tags: [자바스크립트]
---

## **1. 자료 구조 (Data Structure)**

- 데이터 타입 : 하나의 데이터를 어떻게 해석할지 정의한 것.
- 자료 구조 : 여러 데이터들의 묶음을 어떻게 저장하고 사용할지 정의한 것

## **2. Stack**

![image](/assets/img/sample/stack.png)

먼저, **스택은 한 쪽 끝에서만 자료를 넣거나 뺄 수 있따.** 위 사진 처럼.  
이런 구조를 **LIFO: last in, first out** 라고 한다.  
**가장 최근에 넣은 자료부터 추출**할 수 있다는 것.  
** 1,2,3,4,5 를 순서대로 넣으면 꺼낼 때는 5,4,3,2,1 로 꺼내야 한다.**

![image](/assets/img/sample/stack1.png)
**요 그림이나, 프링글스를 생각하면 쉽다.**  
넣은 순서대로 꺼낼 수 있는 것이 아니라, 가장 마지막에 넣은 것부터 꺼낼 수 있는 구조. 오키?

**Stack에는 기본 내장 메소드가 6개가 있다.**

- push(): 값을 추가
- pop(): 값을 제거
- peek(): 제일 위에 있는 값을 추출
- isEmpty(): 스택이 비어 있으면 true, 아니면 false
- clear(): 스택의 모든 내용을 제거.
- size(): 스택의 길이.

---

```js
class Stack {
  constructor() {
    this.storage = {}; // 내가 저장할 빈 객체. 혹은 빈 배열도 가능 // this.storage ={} 말고 storage = {} 해도 괜찮음.
    this.top = -1; // -1이면 객체의 시작을 0으로 한다는 것. 0이면 1로 시작.
  }
  size() {
    return this.top + 1; // 객체에 길이. 값을 몇 번이나 추가 했는지 알려주는 것.
  }

  push(element) {
    this.top++; // 값을 넣기 전에 우선 top의 값을 올려준다.
    this.storage[this.top] = element; // 그리고 그 객체에 키를 this.top으로 주고, 값을 element.
  }

  pop() {
    if (this.top < 0) {
      // 빈 객체여도 pop의 명령어가 오류를 뱉지 않도록 만들어주는 조건문.
      return;
    }
    let pop = this.storage[this.top]; // 우선 추출할 값을 할당을 해줘야 한다.
    delete this.storage[this.top]; // 값을 할당 후 추출할 값을 객체에서 삭제.
    this.top--; // 그리고 나서 키 값을 1개를 줄여줘서 이후 push를 할 때 this.top의 값이 정상적으로 나오기 위함.
    return pop; // 그리고 나서 할당해 줬던 값을 추출.
  }
}
```

코드이다.  
this 때문에 보기가 불편하지만 어쩔 수 없다. 나만 불편해?

```js
push 부분 자세히 보기
stack.push('a')  // this.storage = {0: 'a'}
stack.push('b') // this.storage = {0: 'a', 1: 'b'}
stack.push('c') // this.storage = {0: 'a', 1: 'b', 2: 'c'}
이렇게 나온다. this.top이 this.storage의 키가 되고,
element는 this.storage[this.top]의 value가 된다.

this.top의 첫 값이 -1이고 이후 pop할 때마다 ++가 되기 때문에 객체 시작은 0.

pop 부분 자세히 보기
stack.pop() // this.storage = {0: 'a', 1: 'b'}
return = 'c'
stack.pop() // this.storage = {0: 'a'}
return = 'b'
이렇게 나온다.

1. let pop = this.storage[this.top]을 통해
let pop = 'c'가 되게 만들어 준다. this.storage[this.top]의 value를 우선 담아주자.

2. delete this.storage[this.top]을 통해
{0: 'a', 1: 'b', 2: 'c'} --> {0: 'a', 1: 'b'}

3. This.top -- ==> 3에서 2로 값을 낮춤. 그래야지 push를 할 때 다시 3으로 됨.
(만약 하지 않는다면 다음 push를 할 때 {0: 'a', 1: 'b' 3: 'c'}의 형태가 된다.

4. Return pop => 'c'
요 순서를 지켜야 추출과 동시에 객체에서 삭제할 수 있다.

```

## **3. Queue**

큐는 스택과 조금 다르다.  
먼저 집어 넣은 데이터가 먼저 나오는 FIFO (First In First Out)구조.  
가장 먼저 넣은 애가 값으로 나온 다는 것.  
1,2,3,4,5 로 넣었으면 나올 때도 1,2,3,4,5가 된다.

놀이동산 줄 기다리는 거, 게임 큐 잡힌다고 하는 것 등 예시가 많다.

```js
class Queue {
  constructor() {
    this.storage = {}; // 빈 객체를 지정. 여기다가 데이터를 넣을 것이다.
    this.front = 0; // 객체의 시작 부분 // 우리가 추출할 부분
    this.rear = 0; // 객체의 끝 부분 // 데이터가 들어가는 곳.
    // 스택은 출입구가 똑같아 1개지만 큐는 입구와 출구가 달라 front/rear로 나뉘는 것.
  }

  size() {
    return this.rear - this.front; // 객체의 전체 길이
  }
  enqueue(element) {
    this.storage[this.rear] = element; // 이번에는 초기 값이 0이니 먼저 데이터를 넣고 그 이후에 ++
    this.rear++;
  }
  dequeue() {
    if (this.rear - this.front < 1) {
      return; // 객체가 비어도 계속 사용할 수 있게.
    }
    let removed = this.storage[this.front]; // 추출할 값을 먼저 할당
    delete this.storage[this.front]; // 그리고 추출할 값을 객체에서 삭제
    this.front++; // 삭제하고 나서 ++를 해줘야지 그 다음 객체를 삭제할 수 있다.
    return removed; // 삭제한 값 추출
  }
}
```

```js
enqueue('a') // this.storage === {0: 'a'}
enqueue('b') // this.storage === {0: 'a', 1: 'b'}
enqueue('c') // this.storage === {0: 'a', 1: 'b', 2: 'c'}
데이터가 이렇게 들어간다.
스택과는 달리 ++를 뒤에 넣은 점은, 시작이 0이기 때문에.

dequeue로 자료 빼기.
this.storage === {0: 'a', 1: 'b', 2: 'c'}
dequeue() // this.storage === {1: 'b', 2: 'c'}
return 'a'
dequeue() // this.storage === {2: 'c'}
return 'b'

1. let removed === this.storage[this.front] 로 담자.
그러면 let removed === 'a'가 된다. 추출할 값을 먼저 담아야 함.
(위의 스택과 같다)

2. delete this.storage[this.front] ==
여기서 현재 this.top의 값은 맨 위에 0으로 설정되어 있기에 객체에서 0인 부분,
즉 가장 먼저 enqueue로 넣은 값 삭제하는 것.

3. 그 이후 this.front의 값을 ++ 해준다. 그래야지 dequeue를 한 번 더 썼을 때
this.storage[this.front] === this.storage[1]이라서 다음 값을 추출할 수 있다.
(처음에는 front가 0이라서 this.storage[this.front] === this.storage[0]
dequeue를 하고 나면 남은 객체는 {1: 'b', 2: 'c'}이다. ++를 통해
this.storage[this.front] === this.storage[1]을 만들어 주자.)

4. 1번에서 담아준 'a'를 리턴.

```
