---
layout: post
title: "TIL 31일차 - modal 만들기"
date: 2020-11-25 11:20:30  +0800
categories: [TIL, 2020년 11월]
tags: [TIL]
---

![image](/assets/img/sample/modal1.png)

#### **201125**

평화로운 수요일  
나와 지상이는 solo week 계획대로 첫 날에는 **modal**을 만들어 보았다.

---

#### **⚈. modal 이란?**

모달은 **터럭 모(毛) + 달달하다**와 합쳐진 말로 **풍성한 털이 있어서 달달하다.** 라는 말이다. 친구로는 팝업이 있다.

**팝업**은 기존 브라우저 페이지에서 새로운 브라우저 페이지를 여는 것이다. 새 탭을 여는 것과 같다.  
반면 **모달**은 기존 브라우저 페이지 위에 포토샵처럼 새로운 레이어 페이지를 띄우는 것이다.

팝업은 제거 하지 않으면 계속 남아있지만, 모달은 다른 곳으로 이동하면 없어지거며 모달창은 제거를 하지 않고도 페이지를 이동하면 자연히 사라진다.

요즘은 팝업보다는 모달이 더 많이 사용되고 있으며, 주로 필수적인 내용을 보여줘야 할 때 사용된다고 한다.

**여기까지 understand 했습니다. 예시를 보면 더 쉬워요**

**모달창 예시**  
![image](/assets/img/sample/modal2.png)

---

#### **⚈. modal을 직접 만들어 보자**

우선 기존에 만들었던 트위틀러에 모달 버튼을 추가했다.  
![image](/assets/img/sample/modal3.png)  
내가 만들었던 트위틀러이다. 자세히 보면 Twittiler제목 밑에 **"모달달 버튼"**이 있다.  
버튼을 누르기 전에 기존 트윗을 한 번 읽어보고 가자. **GOD지상, 보경꾸, 효주호주, 택택, 코공이**의 글이 보인다. 각자 평소의 생각을 트윗으로 올려주었다.

---

#### **⚈. modal 창 클릭**

![image](/assets/img/sample/modal4.png)  
**"모달창 버튼"** 을 누르면 위 사진 처럼 내가 만든 모달 창이 기존 브라우저 페이지 위에 뜨게 된다. 포토샵, 일러스트, 파워포인트를 생각하면 쉽다. **도형 위에 도형을 얹은 것! ** 브라우저 페이지를 보는 것이 방해 되지 않도록 뒤를 약간 투명하게 만들어 주었다.  
![image](/assets/img/sample/modal5.png)  
**모달에 들어가는 내용이 필수라면 이렇게 크게 만들어 주면 된다.**  
![image](/assets/img/sample/modal6.png)  
나의 모달의 특징은 브라우저에 fixed를 해서 페이지를 내려도 모달창은 항상 똑같은 위치에 있다.  
**그러니까 빨리 모달의 내용일 읽어달라 이말이야**  
**뒤에 트윗을 보면 우리 친구들이 열심히 글을 올린 것을 볼 수 있다. 깨알재미.**

---

#### **⚈. 나의 modal code**

나는 아직 **배운지 31일** 밖에 안 된 초보이기 때문에 코드는 예쁘지 않을 것이다. 코드 설명은 사진 파일 안에 보면 잘 적혀있다.

#### **HTML CODE**

```js
<!-- modal 부분 -->
<button id ="modal_btn">모달달 버튼 +_+</button>
<div id="myModal">
    <div id="modal-content">
        <span class="close"> &times; </span>
      <p>모달 is 달달. 달달한 모달달. 모달이를 읽어줘</p>
    </div>
</div>
```

#### **CSS CODE**

![image](/assets/img/sample/modal7.png)

![image](/assets/img/sample/modal8.png)

#### **Javascript CODE**

```js
// 모달과 버튼 지정 //
let modal = document.getElementById("myModal");
let btn2 = document.getElementById("modal_btn");

// 열기 버튼 //
btn2.onclick = function () {
  modal.style.display = "block";
};

// 닫기 버튼 //
let span = document.getElementsByClassName("close")[0];
span.onclick = function () {
  modal.style.display = "none";
};
```

---

이렇게 첫 날 계획은 잘 마무리했다. 앞으로 modal을 어떻게 활용하는지에 따라 다양하게 적용시킬 수 있을 것 같다.  
우리 모두 모달을 통해 달달해지자.
