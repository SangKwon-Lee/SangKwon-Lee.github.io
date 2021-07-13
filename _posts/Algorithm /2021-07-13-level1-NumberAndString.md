---
layout: post
title: '알고리즘 > 프로그래머스 1단계 2021 카카오 채용연계형 인턴쉽 숫자 문자열과 영단어'
date: 2021-07-13 11:20:30  +0800
categories: [Algorithm, 프로그래머스 1단계]
tags: [Javascript, algorithm, 프로그래머스]
---

오랜만에 알고리즘 문제를 포스팅한다.  
그동안 알고리즘을 너무 손 놓고 있었다.  
왜냐하면 자신이 없었기 때문..

푸는 것이 두려워 아이에 처다보지도 않았다.  
하지만 이제 조금씩이라도 해보려고 한다.

---

## **숫자 문자열과 영단어**

## **문제 설명**

네오와 프로도가 숫자놀이를 하고 있습니다. 네오가 프로도에게 숫자를 건넬 때 일부 자릿수를 영단어로 바꾼 카드를 건네주면 프로도는 원래 숫자를 찾는 게임입니다.

다음은 숫자의 일부 자릿수를 영단어로 바꾸는 예시입니다.

1478 → "one4seveneight"  
234567 → "23four5six7"  
10203 → "1zerotwozero3"  
이렇게 숫자의 일부 자릿수가 영단어로 바뀌어졌거나, 혹은 바뀌지 않고 그대로인 문자열 s가 매개변수로 주어집니다. s가 의미하는 원래 숫자를 return 하도록 solution 함수를 완성해주세요.

## **제한 사항**

1 ≤ s의 길이 ≤ 50  
s가 "zero" 또는 "0"으로 시작하는 경우는 주어지지 않습니다.  
return 값이 1 이상 2,000,000,000 이하의 정수가 되는 올바른 입력만 s로 주어집니다.

## **입출력 예제**

![image](/assets/img/sample/stringAndNumber1.png)

---

## **코드**

![image](/assets/img/sample/stringAndNumber2.png)

처음에는 반복문이랑 if로 해서 풀었는데 딱 봐도 비효율적이라는 것이 많이 느껴졌다.  
그래서 조금 수정을 해보았다.  
다른 사람들의 풀이를 보니까 객체 혹은 배열로 미리 만들어서 한 사람들도 있는데  
어쨌든 공통적으로 들어가는 것은 replace였다.  
그 중에 위의 방법이 내 수준에서는 제일 나은 것 같았다.

더 좋은 방법이 있었지만 그것은 내 아이디어가 아니었기에..

---