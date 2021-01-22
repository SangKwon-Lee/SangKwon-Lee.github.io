---
layout: post
title: 'JavaScript에서 Prototype을 알아보자'
date: 2020-12-09 11:20:30  +0800
categories: [자바스크립트, 개념 정리]
tags: [javascript, prototype]
---

### 주의

**여기에 적는 정리글은 나도 제대로 이해하지 못한 것들이 많다.**  
**그래서 틀린 정보가 많을 수도 있다.**

**class의 개념을 알고 있다면 이해가 쉬울 것입니다.**

---

# **Prototype**

자바스크립트가 ES6로 와서 Class를 사용할 수 있지만, 그 전에는 class가 없어서 prototype을 사용했다.

그러면 Class가 없던 시절 Class대신 prototype은 어떻게 사용했을까??

예시

```js
function Character() {}

Character.prototype.age = 20;

let kim = new Character();

console.log(kim.age); // 20
```

**모든 함수에는 Prototype라는 속성이 있다.**

Function Character() {}라는 함수를 만들면  
**Character.prototype이라는 빈 Object{} 만들어진다.**  
Character 함수로부터 생성된 **객체(kim)는 자신의 부모인 Object(Character)에게 상속을 받아 안에 있는 Character.prototype의 값을 사용할 수 있다.**

function Charcter와  
let kim = new Character()의 관계를 더 알아보자.

---

# **constructor (생성자)**

함수를 만들게 되면 constructor라는 것이 생기게 된다. **이건 자신의 부모를 가리킨다.**  
![image](/assets/img/sample/prototype1.png)

위에 만든 Character는 함수니까 constructor가 있다.  
**이것이 있으면 new 키워드를 사용할 수 있게 된다. 자식을 만들 수 있게 되는 것!!!**

![image](/assets/img/sample/prototype2.png)
Character.prototype으로도 확인할 수 있다.  
여기에 보면 **proto**라는 것이 있다. 이것도 밑에서 배워보자.

---

# **proto / Prototype Chain**

**proto는 링크의 역할을 한다. 즉, 자신의 부모로부터 상속을 받을 수 있게 만들어 준다.**  
**proto** 속성을 prototype 링크라고도 한다.  
모든 객체가 proto를 갖고 있다.

```js
function Character() {}

Character.prototype.age = 20;

let kim = new Character();

console.log(kim.age); // 20
```

여기서 **Kim은 new키워드로 만들었기에 Character의 속성들을 상속 받는다.** (상속 개념은 다른 글에 적어놓았다.)

![image](/assets/img/sample/prototype3.png)

그래서 사진을 보면 Character의 proto는 'native code'..( 이 개념은 머리가 터져서 찾지는 않았다. .)

우리가 주목할 것은 kim이다.**kim은 Character를 통해 만들어져서 proto를 열어보면 constructor가 Character로 되어 있다.**  
**부모가 Character라는 것.**

밑에있는 proto:Object는 최상위 부모(조상)를 가리킨다.  
![image](/assets/img/sample/prototype4.png)

당연 Character도 보면 조상이 Object다.  
그래서 Object의 기능인 toString()을  
Character와 kim에 넣어주지 않아도 상속을 받아 사용할 수 있다.  
![image](/assets/img/sample/prototype5.png)

그래서 kim.age에 넣지 않고  
Character.prototype.age에 넣어도  
**kim은 Character의 속성을 상속 받아서 kim.age에도 같은 값이 나오게 된다.**

**이렇게 특정 속성을 받아오는 관계를 프로토타입 체이닝이라 한다.**

---

# **Object.create()**

지정된 프로토타입 객체 및 속성(property)을 갖는 새 객체를 만듭니다.  
라는 뜻이지만  
간단하게 생각하면 prototype를 만들어 주는 것이다.  
![image](/assets/img/sample/prototype6.png)

원래 위에서 만든 kim에는 prototype이 없다.  
Object.create기능을 쓰면 인자로 Character를 넣어서  
똑같은 기능을 하는 prototype을 만들어 줄 수 있다.

**그런데 이 기능에는 약간의 함정이 있다.**

**함정 새로 보기 **  
![image](/assets/img/sample/prototype7.png)

그림을 보면

```js
// 2개의 함수를 만들었다.
function Person(name) {
this.name = name }
function Say() {}


//Person.prototype.sleep에 함수를 넣었다.

Person.prototype.sleep = function () {
console.log("bye")
}

//Say함수의 prototype을 Object.create를 통해
Person.prototype을 복제 했다.

Say.prototype = Object.create(Person.prototype)

Say.prototype.sleep()
// bye가 잘 출력된다.
```

**여기서 Say를 참조하여 만든 kim을 만들어 보자**
![image](/assets/img/sample/prototype8.png)

**여기서 Kim은 Say를 참조하여 만들었따.  
그럼 kim의 부모는 누구인가? 원래는 Say가 되어야 한다.**

**그런데???!!!**

![image](/assets/img/sample/prototype9.png)

**kim의 부모 상속을 보았더니 Say가 아니라 Person이다.**  
(Constructor는 부모를 가리킨다.)  
누가 kim의 부모를 바꿔치기 했다.  
두두두둥!!!

이게 함정이다.

그래서 constructor를 재조정해야 한다.  
![image](/assets/img/sample/prototype10.png)

문제는 Say가 Person의 prototype을 가져올 때 생긴 것.  
**그래서 위 사진처럼 Say의 constructor를 재설정 해주면 kim은 Say를 상속받기 때문에 잘 바뀐다.**

그래서 ES6 Class 에서는

```js
class Character {
    constructor(age) { .....

```

이런식으로 안에 constructor를 쓰는 것이다.  
그냥 우리 Class만 쓰자.

---
