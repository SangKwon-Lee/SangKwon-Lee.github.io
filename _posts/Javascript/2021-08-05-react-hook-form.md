---
layout: post
title: 'React-hook-form과 yup에 대해 알아보자'
date: 2021-08-05 12:00:30  +0800
categories: [Javascript, React]
tags: [javascript, react]
---

React-hook-form 이라는 라이브러리를 써보았다.  
기능도 간편하고 State나 함수를 많이 만들 필요도 없었다.  
회사마다 쓰는 form이 다르다고 하는데 React-hook-form은 알아두면 나쁘지 않을 것 같다.

오늘은 React-hook-form의 간단한 사용방법을 전체적으로 둘러볼 예정이다.  
내가 나중에 써도 까먹지 않기 위하여..

---

## **React-hook-form**

React-hook-form은 그래도 공식 문서가 친절한 편이다.  
물론 그래도 처음 보는 사람이 바로 적용하기에는 쉽지 않을 것 같다.  
간단하게 사용방법만 알려주면 그래도 그 이후에 적용하는 것은 어렵지 않을 것 같다.

물론 내가 간단하게만 적용해서 그런 것 같기도.

개념 설명보다는 그냥 사용 방법에 대해 정리할 것이다.  
우선 라이브러리이기 때문에 설치를 해야 사용이 가능하다.

```js
npm install react-hook-form
yarn add react-hook-form
```

둘 중에 하나로 설치하자.

---

## **React-hook-form 간단한 사용 방법**

우선 설치를 했다면 상위에 불러와야지 사용이 가능하다.

```js
import { useForm } from 'react-hook-form';
```

요렇게 하면 useForm을 통해 사용할 수 있다.

![image](/assets/img/sample/useForm1.png)

그렇게 하면 useForm 안에 있는 기능들을 이용할 수 있다.  
그리고 그 안에 mode가 있는데 이는 언제 유효성 검사를 할지 정하는 것이다.  
크게 onChage나 onSumit으로 하는 것 같다.

그 외에 내가 오늘 쓸 기능들은 크게 3가지이다.

register, handleSubmit, formState.

---

### **register**

register는 useForm의 필수 기능이다.  
우리가 기존에 name을 이용해서 event.target.name으로 각각의 input을 불러왔다.  
그 역할을 register가 해준다.

![image](/assets/img/sample/useForm2.png)

register의 사용법은 위와 같다.

```js
<input type="text" {...register("email")}>
```

이렇게 하면 name과 동일한 역할을 하게 된다.  
register를 통해 form에 필요한 모든 input에 register를 달아주면 끝이다.  
register하나로 모든 input을 관리하게 된다.

이렇게 하면 event.tartget.name / event.target.value를 안 써도 되고  
이걸 안 쓰니 스프레드 연산자, 그에 따른 함수들도 만들어 주지 않아도 된다.

짱 편함!!

그 외에 register 안에는 다양한 규칙들도 넣을 수 있다.

```js
<input
	type="text"
	{...register('email', {
		required: true,
		maxLength: 20,
		pattern: /^[A-Za-z]+$/i,
	})}
/>
```

공식 문서에도 몇 가지가 나와있다.  
required: true를 하면 필수 요소이고  
그 외에 최소, 최대 길이와 정규식표현도 사용할 수 있다.

위의 사항들을 어기게 되면  
error로 가게 되는데 그건 밑에서 따로 적을 예정.

---

### **handleSubmit**

제출은 handleSubmit을 이용하면 된다.  
우선 코드를 보자.

![image](/assets/img/sample/useForm3.png)

보면 추가된 부분이 있다.

```js
<form onSubmit={handleSubmit(onSubmit)} >

<button type="submit">로그인하기</button>
```

이렇게 두 부분이다.  
form 태그에 onSumbit안에 handleSubmit함수를 호출한다.  
handleSubmit함수 안에 인자로는 우리가 실제로 실행시킬 함수를 적게 되는 것이다.  
그러면 자동으로 우리가 만든 onSubmit이라는 함수에 인자로 register를 해놓은 input들의 value가 들어오게 된다.

그리고 onSubmit은 type="submit"인 태그를 누르면 작동된다.

나는 지금 onSubmit이라는 함수를 만들고 그 함수를 로그인하기 버튼을 눌렀을 떄 실행되도록 만들었다.

```js
const onSubmit = (data) => {
	console.log(data);
};
```

한 번 register들이 어떤 식으로 들어오는지 보자.

![image](/assets/img/sample/useForm4.png)

위의 처럼 데이터가 한 번에 잘 들어오게 된다.  
이러니 ...newInput 이런 식으로 안 만들어줘서 좋다.

---

### **formState**

formState는 안에 여러 기능들이 있지만 그 중에서도 errors, isVali만 볼 것이다.
위에서 나는 추가로 register에 몇 가지 옵션을 넣어주었다.

![image](/assets/img/sample/useForm5.png)

required, maxLength, pattern 3가지를 넣었는데  
각각의 조항들을 어기면 errors가 자동으로 생기게 된다.

그럼 에러가 났을 때 메시지는 어떻게 보내느냐?

![image](/assets/img/sample/useForm6.png)

위에 처럼 사용할 수 있다.

```js
{
	errors.email?.type === 'required' && <span>반드시 입력</span>;
}
```

각각의 조항들을 어기면 errors에 자동으로 데이터와 어떤 type의 조항을 어겼는지 생기게 된다.  
그에 따른 에러메시지도 각각 입력해주면 된다.

isValid는 위에서 에러가 모두 없으면 true, 있으면 false의 값이 나오는 녀석이다.

![image](/assets/img/sample/useForm7.png)

이런 식으로 사용하게 되면 errors가 없을 때만 submit을 할 수 있도록 만들 수도 있다.

---

이렇게 하면 간단하게 form을 사용하는 것은 끝났다.  
앞으로 자주 이용해서 코드를 더욱 간결하게 만들어 보자.

그런데 잠깐!

여기서 추가로 정규식표현과 같은 검사를 해주는 yup이라는 라이브러리가 또 존재한다.  
실제 공식 문서에소 yup과 함께 쓰는 부분도 존재한다.

---

## **yup**

yup은 form에서 정규식 표현, 문자의 길이 등 검사를 도와주는 라이브러리이다.  
이 역시 설치가 필요하다.

hookeform과 같이 사용하려면 2개를 설치해야 한다.

```js
yarn add yup
hookform/resolvers
```

---

## **yup 간단한 사용 방법**

yup같은 경우 2가지를 해줘야 한다.

1. schema 작성
2. resolver 이용

#### **schema**

![image](/assets/img/sample/useForm8.png)

스키마는 위에처럼 작성한다.  
우리가 register로 만들어 준 애들을 키로 작성하고  
값으로는 어떤 것들을 검사할지 적는다.

똑같이 required, max, min 등이 있고 가장 좋은 것은  
email() 하나로 이메일 정규식 표현을 사용할 수 있다는 것이다.

그 외에 () 안에 텍스트를 넣으면 그게 에러 메시지로 뜨게 된다.

#### **resolver**

이건 useForm 안에 작성하면 끝이다.

![image](/assets/img/sample/useForm9.png)

이렇게하면 react-hook-form && yup의 환상의 콜라보가 완성된다.

---

## **결론**

form 같은 경우는 react-hook-form 말고도 다양하게 있다고 한다.  
그런데 사용 방법이 비슷해서 하나만 익혀두면 러닝 커브는 짧은 듯.

회사마다 사용하는 form이 다른데 새로운 곳에서는 hook-form을 이용했으면 좋겠다.  
그리고 yup을 통한 관리도 마음에 든다.  
아직 익숙하지 않아서 귀찮은 부분도 분명 존재하지만 관리는 진짜 편한 것 같다.  
간단한 수정으로 유지보수가 되니 form 관련 라이브러리는 꼭 사용하도록 하자.

코드도 간단해지고  
만드는 함수도 적어지고  
유지보수도 쉬우니  
짱짱맨 !!

![image](/assets/img/sample/useForm10.png)
