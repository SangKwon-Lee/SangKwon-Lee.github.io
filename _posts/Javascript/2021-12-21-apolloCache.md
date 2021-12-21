---
layout: post
title: 'Apollo InmemoryCache에 대해 짧은 공부'
date: 2021-12-21 12:00:30  +0800
categories: [Javascript, gql]
tags: [javascript]
---

오랜만에 정리 글을 쓴다.  
내용은 매우 짧지만  
그동안 아무 생각 없이 썼던 것이라  
반성하는 의미에서 정리..  

---

## **InMemoryCache**  

GraphQL & Apollo를 쓰다보면 설정에서 InmemoryCache()를 해준다.  
그동안 그냥 초기 설정이라고 생각하고  
무조건적으로 쓰고 넘어갔다.  

오늘에 와서야 이걸 왜 하는지 약간 알게 됐다.  

---  

Apollo는 모든 네트워크 통신을 InMemoryCache에 저장한다.  
그래서 통신을 하기 전에 InMemoryCache를 먼저 확인한다.  

InMemoryCache에 이미 등록된 네트워크 통신이라면 GraphQL Server를 거치지 않고  
InMemoryCache에서 데이터를 꺼내와 쓰게 된다.  

이렇게 되면 서버와 통신을 하지 않고도  
기존 데이터를 불러오기 때문에  
동일한 요청에 대해서는 더 빠른 속도로 불러올 수 있다.  

---   

그러면 InMemoryCache는 어떤 방식으로  
동일한 요청을 구별할까?  

먼저 데이터를 정규화 시킨다.  

1. 객체 식별  

각각의 요청을 구벼랗기 위해 쿼리 응답에 포함된 모든 개체를 식별한다.   

2. 캐시 ID 생성  

각 식별된 개체에 대한 캐시 ID를 생성해준다.  

캐시 ID는 __typename과 ID로 구별이 된다.  

예를 들어 

![image](/assets/img/sample/memory1.png)  

이렇게 요청을 했을 때  

각 객체에는 __typename과 id가 존재한다.  
그럼 __typenmae을 key, id를 value로 저장한다.  
Board:61c14548c444860029e62fbb  
이런식이다.  

3. 개체 필드를 참조로 교체  

받아 온 데이터를 참조 형태로 바꾼다.  
위 사진에는 write: "안녕"이렇게 나와 있지만,  
이 "안녕"이라는 값을 참조 형태로 바꾼다.  
"__ref": "Board:61c14548c444860029e62fbb"  
이렇게 말이다.  

4. 정규화된 객체 저장  

다시 쿼리를 부를 때 기존캐시의 개체와 동일할 경우 병합된다.  
이 때 값을 덮어쓰며  
변경될 때는 업데이트를 하게 된다.  

---  

이것을 시각화 하려면 Apollo Client Devtools를 설치해보라!  

---  

끝!  

그래도 조금 InMemoryCache에 대해 알게 됐따 ^__^





