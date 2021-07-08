---
layout: post
title: 'intersectionObserver 대해 알아보자'
date: 2021-07-08 12:00:30  +0800
categories: [Javascript, CSS]
tags: [javascript, intersectionObserver]
---

오늘은 Notion 정리를 하다가 우연히  
IntersectionObserver API를 발견하였고,  
그 내용을 Notion에 정리하면서  
똑같이 내 블로그에 정리하려고 한다.

---

## **IntersectionObserver란?**

IntersectionObserver는 우리가 UI를 만들고 난 뒤  
스크롤을 내려서 특정 위치에 도달하면 특정 애니메이션을 실행시키는 것이다.

기존에는 Scroll Event를 이용하여 함수를 실행했었다.  
하지만 이 방식에는 아주 크나큰 문제가 있다.  
바로 우리가 스크롤을 움직일 때마다 함수가 미친듯이 실행된다는 것이다.

물론 이 문제를 디바운싱과 쓰로틀링을 통해 개선할 수는 있지만,  
너무 번거롭지 않은가?

최신 방식인 IntersectionObserver API는 디바운싱, 쓰로틀링 없이도  
함수가 미친듯이 실행되는 것을 막아준다.

그러면 일단 기존 방식인 Scroll Event의 문제점 부터 알아보도록 하자.

---

## **Scroll Event 방식의 문제점**

![image](/assets/img/sample/inter1.png)

한 번 간단한 예제를 만들어 보았다.  
다른 것은 없고 그냥 onScroll을 통하여 스크롤을 이동할 때마다 console.log()를 찍었다.

그 결과는??

![image](/assets/img/sample/inter2.png)

오우 미친듯이 찍히고 있다.  
이러면 브라우저에 과부하가 걸린다.  
또한, 우리의 DOM은 특정 요소, 혹은 페이지 전체를 랜더링하고 있을 것이다.
이렇게 랜더링이 계속 되는 것을 **리플로우** 라고 한다.

위에서 말했다 싶이  
이런 문제를 디바운싱과 쓰로틀링을 통해 해결할 수 있다.  
그런데 우리 그러지 말고  
새로운 방식 좀 써보자..!

## **IntersectionObserver API 방식**

자 새로운 방식을 써보자.  
한 가지 주의할 점은 SSR환경에서는 오류가 뜬다.  
그래서 각자의 방식대로 이 문제를 해결 해야 하는데  
나는 일단 useEffect와 setTimeout을 조합하여 바로 IntersectionObsever를 불러오지 않고  
브라우저가 다 그려진 이후 1초 뒤에 불러오기로 했다.

![image](/assets/img/sample/inter3.png)

하나씩 코드를 까보자.  
우선 intersectionObserver를 불러와야 한다.  
그 방식은 이 코드다.

```js
const io = new IntersectionObserver(callback, options);
```

IntersectionObserver를 불러오면, 그 인자로 callback 함수와 options가 들어가 된다.

```js
const io = new IntersectionObserver((entries) => {
	entries.forEach((entry) => {
		if (entry.intersectionRatio > 0) {
			setIsTrue(true);
			console.log('실행');
		} else {
			setIsTrue(false);
			console.log('실행');
		}
	});
});
```

내가 실행한 callback 함수의 내용이다.  
우선 대부분의 코드는 공식문서에서 사용한 방식을 그대로 가져왔다.  
그게 마음이 편하거든..

일단 entries라는 것이 인자로 들어간다.  
얘는 누구일까?

![image](/assets/img/sample/inter4.png)

이런 내용들이 담겨있다.
참 많은 요소가 있네요..

많은 예제들을 보았지만  
일단 가장 주로 쓰이는 것이 intersectionRatio이다.  
얘는 우리가 원하는 관찰 대상이 화면에 들어왔을 경우 그 위치를 0~1사이의 값으로 알려준다.  
이 값을 계산하는 방식이 **intersectionRect 영역에서 boundingClientRect 영역까지 비율** 이라고 한다.  
너무 어렵지만 중요한 건 이거다.

**화면에 보이면 0보다 크고 안 보이면 0**  
이것만 기억하고 이 조건으로 우리가 원하는 함수를 실행하면 된다.

그래서 나의 코드를 보면 entry.intersectionRatio > 0을 이용하여 함수를 실행한다.  
눈에 보이면 true, 안보이면 false인것.  
간단하죠?

혹은 isIntersecting은 화면에 보이면 true, false값을 반환하여 얘를 써도 된다.

```js
const boxElList = document.getElementById('1');
io.observe(boxElList);
```

요 부분은 우리가 누구를 관찰하고 싶은지 그 요소를 설정하는 것이다.  
태그를 여러 개 해도 상관 없다.

---

## **IntersectionObserver API options**

options에는 3가지 설정이 들어갑니다.

- root
  기본값 : null, 브라우저의 viewport  
  관찰 대상으로 등록할 태그(요소)는 반드시 root의 하위 요소여야 합니다.

- rootMargin
  기본값: "0px, 0px, 0px, 0px"  
  위에 root 엘리먼트의 마진값입니다.

- threshold  
  기본값 : 0  
  0.0~1.0 사이의 숫자가 들어갑니다. 0.0의 경우 관찰 대상이 보이자마자 실행을 하고, 1.0으로 갈수록 관찰 대상이 전부 보여야지 함수를 실행합니다.

---

## **IntersectionObserver API Method**

- IntersectionObserver.observe(targetElement)  
  타겟 엘리먼트에 대한 IntersectionObserver를 등록할 때(관찰을 시작할 때) 사용합니다.

- IntersectionObserver.unobserve(targetElement)  
  타겟 엘리먼트에 대한 관찰을 멈추고 싶을 때 사용하면 됩니다.  
  예를 들어 Lazy-loading(지연 로딩)을 할 때는 한 번 처리를 한 후에는 관찰을 멈춰도 됩니다.  
  이 경우에는 처리를 한 후 해당 엘리먼트에 대해 unobserve(targetElement)을 실행하면 이 엘리먼트에 대한 관찰만 멈출 수 있습니다.

- IntersectionObserver.disconnect()  
  다수의 엘리먼트를 관찰하고 있을 때, 이에 대한 모든 관찰을 멈추고 싶을 때 사용하면 됩니다.

- IntersectionObserver.takerecords()  
  IntersectionObserverEntry 객체의 배열을 리턴합니다.

---

## **IntersectionObserver API Property**

- IntersectionObserverEntry.intersectionRatio:  
  IntersectionObserver 생성자의 options의 threshold와 비슷합니다.  
  교차 영역에 타겟 엘리먼트가 얼마나 교차되어 있는지(비율)에 대한 정보를 반환합니다.  
  threshold와 같이 0.0부터 1.0 사이의 값을 반환합니다.

- IntersectionObserverEntry.isIntersecting:  
  타겟 엘리먼트가 교차 영역에 있는 동안 true를 반환하고, 그 외의 경우 false를 반환합니다.

- IntersectionObserverEntry.target:  
  타겟 엘리먼트를 반환합니다.

- IntersectionObserverEntry.time:  
  교차가 기록된 시간을 반환합니다.

---

http://blog.hyeyoonjung.com/2019/01/09/intersectionobserver-tutorial/  
이 블로그가 상당히 많은 도움이 됐다.  
여기에는 이미지 로드할 시 어떻게 하면 더 효율적인지 예제가 나온다.  
그것도 차차 공부하자.

이미지 로드 예제이다.

```js
// IntersectionObserver의 options를 설정합니다.
const options = {
	root: null,
	// 타겟 이미지 접근 전 이미지를 불러오기 위해 rootMargin을 설정했습니다.
	rootMargin: '0px 0px 30px 0px',
	threshold: 0,
};

// IntersectionObserver 를 등록한다.
const io = new IntersectionObserver((entries, observer) => {
	entries.forEach((entry) => {
		// 관찰 대상이 viewport 안에 들어온 경우 image 로드
		if (entry.isIntersecting) {
			// data-src 정보를 타켓의 src 속성에 설정
			entry.target.src = entry.target.dataset.src;
			// 이미지를 불러왔다면 타켓 엘리먼트에 대한 관찰을 멈춘다.
			observer.unobserve(entry.target);
		}
	});
}, options);

// 관찰할 대상을 선언하고, 해당 속성을 관찰시킨다.
const images = document.querySelectorAll('.image');
images.forEach((el) => {
	io.observe(el);
});

<div class="example">
  <img src="https://picsum.photos/600/400/?random?0" alt="random image" class="image-default">
  <img data-src="https://picsum.photos/600/400/?random?1" alt="random image" class="image">
  <img data-src="https://picsum.photos/600/400/?random?2" alt="random image" class="image">
  <img data-src="https://picsum.photos/600/400/?random?3" alt="random image" class="image">
  <img data-src="https://picsum.photos/600/400/?random?4" alt="random image" class="image">
  <img data-src="https://picsum.photos/600/400/?random?5" alt="random image" class="image">
  <img data-src="https://picsum.photos/600/400/?random?6" alt="random image" class="image">
  <img data-src="https://picsum.photos/600/400/?random?7" alt="random image" class="image">
</div>
```
