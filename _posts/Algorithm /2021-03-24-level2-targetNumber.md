---
layout: post
title: "알고리즘 > 프로그래머스 2단계 타겟넘버"
date: 2021-03-24 11:20:30  +0800
categories: [Algorithm, 프로그래머스 2단계]
tags: [Javascript, algorithm, 프로그래머스]
---

오늘은 DFS문제를 풀었다.  
요것도 당연히 내가 푼 것은 아니다.

몰라서 검색해서 풀었다.  
굉장히 쉬운 난이도의 DFS문제였던 것 같은데  
이제는 애초에 어떻게 접근해야 하는지를 모르겠다.

알고리즘 사고방식이 아니라 그냥  
개념 자체가 부족해서 떠오르지 않는다.

큰일..

---

## **타겟 넘버**

## **문제 설명**

n개의 음이 아닌 정수가 있습니다.  
이 수를 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다.  
예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

-1+1+1+1+1 = 3  
+1-1+1+1+1 = 3  
+1+1-1+1+1 = 3  
+1+1+1-1+1 = 3  
+1+1+1+1-1 = 3

## **제한 사항**

주어지는 숫자의 개수는 2개 이상 20개 이하입니다.  
각 숫자는 1 이상 50 이하인 자연수입니다.  
타겟 넘버는 1 이상 1000 이하인 자연수입니다.

## **입출력 예제**

![image](/assets/img/sample/targetNumber1.png)

---

## **코드**

![image](/assets/img/sample/targetNumber2.png)

---
