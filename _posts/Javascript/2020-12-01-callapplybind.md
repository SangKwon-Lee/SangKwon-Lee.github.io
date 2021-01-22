---
layout: post
title: "call, apply, bind"
date: 2020-12-02 11:20:30  +0800
categories: [자바스크립트, 개념 정리]
tags: [자바스크립트, call, apply, bind]
---

내가 보기 위해 적는 비공개 함수 메소드 이해방식.

처음에 콦듮슶텞잆츲의 설명을 읽었을 때는 진짜 이해가 1개도 안 감. 왜 쓰는지도.  
바인딩이라는 말을 처음 보는데 this는 ~~을 바인딩 한다. 이렇게 설명하면 누가 알아들음? 개짜증나네 진짜;

1. this

우선 this는 기본적으로 가지고 있는 의미는 window객체가 있지만 사용자가 어떻게 쓰냐에 따라 this가 가리키는 것은 다양해진다.  
this의 값을 window객체가 아닌 다른 것으로 바꿔주기 위해 필요한 함수가 바로 call, apply, bind이다.  
내가 이해한 this를 바인딩 한다는 것은 this의 값을 우리가 설정한 것으로 바꾼다는 의미.

2. call 과 apply

- 둘은 똑같은 역할을 한다. 단지 차이점은 call(this, 인자1, 인자2 ...인자3)  
  이렇게 들어가지만 apply(this, [인자1, 인자2, ...인자3] 이런 식으로 apply는 배열을 사용해서 쓴다는 점.
- call, apply / bind의 차이점은 call, apply는 함수를 바로 실행시켜 return 값으로 나오지만, bind는 다른 곳에 return 값을 담아두어 내가 원할 때 값을 받을 수 있다. bind는 마치 에네르기 까지 모아두는 것.
- 그럼 왜 쓰냐? call 없어도 인자를 넣을 수 있는데 ? -> this의 값을 추가로 넣을 수 있으니까 !

```js
const obj = { name: "kogong" };

const say = function (city) {
  console.log(`Hello, my name is ${this.name}, I love ${city}`);
};

say("seoul"); // Hello, my name is , I love seoul
say.call(obj, "seoul"); // Hello, my name is kogong, I love seoul
say.apply(obj, ["seoul"]); // Hello, my name is kogong, I love seoul
```

이렇게 call 과 apply는 첫 번째 인자에는 this의 값을 설정을 해주고, 2번 째 인자부터는 say의 함수에 들어갈 인자를 사용하면 된다.

3. bind

- 위에도 썼지만 call, apply는 함수를 바로 실행, 위에 코드처럼 Hello, my name is kogong, I love seoul가 바로 나오게 된다.
- 하지만 bind는 다른 곳에 Hello, my name is kogong, I love seoul를 담아두는 것이다.

```js
const obj = { name: "kogong" };

const say = function (city) {
  console.log(`Hello, my name is ${this.name}, I love ${city}`);
};

const boundSay = say.bind(obj);
boundSay("seoul"); // Hello, my name is kogong, I love seoul
```

요런 식으로 This를 넣은 값을 boundSay에 넣어 두었다가 내가 필요할 때 쓸 수 있다. This가 담긴 함수를 간결하게 여러 번 사용할 수 있어서 좋을 듯.
