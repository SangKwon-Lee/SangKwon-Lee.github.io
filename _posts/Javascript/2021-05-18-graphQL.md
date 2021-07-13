---
layout: post
title: 'GraphQL의 사용방법'
date: 2021-05-18 12:00:30  +0800
categories: [Javascript, GraphQL]
tags: [javascript, graphql]
---

GraphQL.

개념이 방대하서 어떻게 정리를 해야 하나 고민을 했다.  
아이에 안 쓸 수도 없고.

막막함을 없애기 위해  
일단 무작정 쓰고 본다.

그래야지 조금씩 정리가 될 것 같다.
해당 글은 front-end기준으로 작성하였다.

스키마 작성, API 제작은 이후에 알아보도록 하자.

---

## **GraphQL 소개**

GraphQL이 무엇인가?  
GraphQL 소개를 보면 쿼리 언어(query language)라고 한다.

쿼리 언어는 **"데이터베이스를 쉽게 이용할 수 있도록 만든 고수준 언어"**  
라는 뜻을 가지고 있다.

고수준이니까 그만큼 성능도 좋겠지?

GraphQL은 API 통신을 위한 언어이다.  
그러면 어떻게 하는지 지금부터 알아보자.

---

## **GraphQL 사용법**

GraphQL은 Apollo와 주로 사용이 되고, PlayGround라는 사이트를 통해  
API를 읽고 데이터를 확인할 수 있다.

중간에 Apollo가 잠깐 나온다.

우선 PlayGround부터 살펴보자.  
백엔드가 API를 만들었으면 PlayGround를 통해 확인할 수 있다.  
Axios-postMan과 같다.

![image](/assets/img/sample/graphql1.png)

백엔드가 알려준 주소를 통해 들어가면 된다.  
위에 사진이 playground 메인 화면이다.

오른쪽에 Docs를 눌러보면 만들어진 API를 확인할 수 있다.

![image](/assets/img/sample/graphql2.png)

이렇게 API를 볼 수 있다.  
여기서 Qurey에 해당하는 fetchBoard를 한 번 자세히 살펴보자.

![image](/assets/img/sample/graphql3.png)

이렇게 보면 어떻게 사용하는지 알 수 있다.  
직접 playground를 이용해서 docs와 코드를 비교해보자.

---

### **Query**

![image](/assets/img/sample/graphql5.png)

우선 위 사진에서 빨간색 부분을 먼저 써준다.  
Docs에서 Queries인지 Mutations인지 확인할 수 있다.
Query는 데이터를 받아온다는 것이다.
Mutation은 수정

우선 시작을 같이 맞춰주면 된다.

그리고 주황색이 API명령어이다.  
Axios였다면 www.aaaaa.com/fetchBoards 였을 것이다.

다시 중괄호를 열어  
그 안에서 front-end가 필요한 것만 쓰면 데이터가 가운데 부분처럼 넘어오게 된다.
(파란색 부분을 보자)

Docs에서 type을 보면 넘겨줄 수 있는 데이터가 참 많다.  
하지만 graphQL의 장점으로 우리는 필요한 데이터만 받을 수 있다.

---

### **Mutation**

Mutation은 조금 복잡할 수 있다.

![image](/assets/img/sample/graphql6.png)

자 빨간색 네모를 보자.  
우선 mutation을 써준다.

그리고나서 주황색 부분을 보자.  
주황색은 API의 이름이다. 여기서는 createBoard이다.

그 다음 초록색 부분을 보자.  
초록색은 API로 전달해야 하는 인자가 담겨있다.

```js
mutation{
   createBoard(createBoard:{

   })
}
```

이렇게 API를 함수처럼 열고, 안에 인자를 넣고 난 뒤  
객체 형태로 넘겨주게 된다.

다음은 파란색 부분이다.  
파란색 부분은 넘겨줘야하는 데이터의 키와 타입이 무엇인지 알 수 있다.

마지막으로 분홍색 부분은 서버에서 응답으로 우리에게 보내주는 부분이다.  
GraphQL답게 서버에서 보내주는 응답도 골라서 담을 수 있다.

필요한 것만 쏘옥쏙쏙 방울 빙글빙글

---

### **Vs Code Query**

playground에서 사용하는 방법을 잘 보았다.

이제 직접 vs code로 가보자.

![image](/assets/img/sample/graphql7.png)

이번에는 2개를 가져왔다.

첫 번째 FETCH_BOARD는 한 가지 게시글만 가져오는 것이다.  
우선 gql``(백틱) 안에 코드를 작성한다.

위에는 query 뒤에 fetchBoard라고 한 번 더 있는데 작업이름을 작성한 것이다.  
작업 이름은 해당 API와 똑같이 작성한다.

인자로 무엇이 들어가는지 적어야 한다.  
$를 통해 표시를하고, :뒤에는 타입을 적는다.  
ID!라고 했는데 이건 docs와 똑같이 맞춰주면 된다.

![image](/assets/img/sample/graphql8.png)

해당 docs를 보면 인자가 **boardId:ID!**  
라고 써있다. 이걸 그냥 그대로 쓰면 된다.

그리고 위 코드처럼 쓰면 된다.

![image](/assets/img/sample/graphql9.png)

그리고 UseQuery를 통해  
위에처럼 코드를 쓰면 data에 우리가 필요한 정보가 담겨오게 된다.  
router머시기는 내가 인자로 필요해서 쓴 거니까 신경쓰지 말자.

---

### **Vs Code Mutation**

![image](/assets/img/sample/graphql10.png)

![image](/assets/img/sample/graphql11.png)

Mutatin 코드이다.

gql 부분도 docs를 보고 맞춰주면 된다.  
주의할 점은 대문자도 잘 맞춰주자.

그리고 실제 Data를 보내게 될 때는
useMutation이라는 것을 이용하게 된다.  
사용 방식을 자세히 보고 어떻게 이름을 맞춰줬는지 보자.

그리고 데이터를 전송하는 것은 동기 방식으로 했다.  
**데이터를 보낼 때 달라지는 점은**  
**variables: {}라는 객체를 만들어서 안에 내용을 적어야 한다는 점.**

---

간단하게 사용방식을 알아보았다.
