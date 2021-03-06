---
layout: post
title: '알고리즘 > 프로그래머스 2단계 프린터'
date: 2021-07-20 11:20:30  +0800
categories: [Algorithm, 프로그래머스 2단계]
tags: [Javascript, algorithm, 프로그래머스]
---

이번에는 문제를 제대로 이해하지 못해서 오래 걸렸다.  
그래서 결국 또 블로그를 찾아 보았다.  
블로그 코드들은 다 이해가 가는데  
왜 나는 직접 못 쓸까?

이번에 가장 문제였던 것은  
프린트에서 출력이 됐으면 목록에서 빼줘야 하는데 그렇게 하지 않았던 것.  
그래서 비교하기 어려웠고 찾기 어려웠다.

그러다보니 머리도 꼬이고

이번에도 새롭게 알게 된 것이 있다.  
단순하게 data와 배열의 값들을 비교할 때 data보다 큰 값이 있는지는

```js
if (priorities.filter(data => now < data).length > 0)
```

이렇게 비교할 수 있었다.

그리고 배열에서 가장 큰 값을 찾는 것은 반복문이 아닌

```js
let max = Math.max.apply(null, priorities);
```

이런 방식도 있었다.  
알고리즘을 내가 풀지는 못해도  
푸는 방법을 찾아보면서  
다양한 풀이를 보고 거기서 새로운 풀이법을 볼 수 있다.

배열끼리 같은 값이 몇 개나 있는지

```js
const sameData = lottos.filter((n) => win_nums.includes(n)).length;
```

혹은

```js
new Map();
```

등 배우는 것이 많아서 좋다.  
언젠가는 나도 하나씩 풀 수 있겠지?

---

## **프린터**

## **문제 설명**

일반적인 프린터는 인쇄 요청이 들어온 순서대로 인쇄합니다.  
그렇기 때문에 중요한 문서가 나중에 인쇄될 수 있습니다.  
이런 문제를 보완하기 위해 중요도가 높은 문서를 먼저 인쇄하는 프린터를 개발했습니다.  
이 새롭게 개발한 프린터는 아래와 같은 방식으로 인쇄 작업을 수행합니다.

1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면 J를 대기목록의 가장 마지막에 넣습니다.
3. 그렇지 않으면 J를 인쇄합니다.  
   예를 들어, 4개의 문서(A, B, C, D)가 순서대로 인쇄 대기목록에 있고 중요도가 2 1 3 2 라면 C D A B 순으로 인쇄하게 됩니다.

내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 알고 싶습니다. 위의 예에서 C는 1번째로, A는 3번째로 인쇄됩니다.

현재 대기목록에 있는 문서의 중요도가 순서대로 담긴 배열 priorities와  
내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지를 알려주는  
location이 매개변수로 주어질 때,  
내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지 return 하도록 solution 함수를 작성해주세요.

## **입출력 예제**

![image](/assets/img/sample/print2.png)

---

## **코드**

![image](/assets/img/sample/print1.png)

---
