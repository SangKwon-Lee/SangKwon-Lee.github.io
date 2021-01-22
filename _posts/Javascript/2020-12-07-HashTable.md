---
layout: post
title: "데이터 자료구조. Hash Table"
date: 2020-12-07 11:20:30  +0800
categories: [Javascript, Data Structure]
tags: [Javascript, Data Structure, Hash Table]
---

hash table 이해하기 너무 어렵잖아.  
공부는 계속 해야지 안 밀리잖아.  
읽어도 100%는 이해하지 못해도 블로깅은 해야 연습이 되잖아.  
그래서 한다 이말이야.

# **Hash Table 개념**

**hash table도 자료 구조 중의 하나이다.**

우리가 입력한 정보들(key와 value)에서 key를 index로 바꿔서 배열[index]에다가 우리가 입력한 정보들(key와 value)을 넣는 것이다.

![image](/assets/img/sample/hash1.png)

사실 그림만 보면 어렵다. 나도 이해하기 힘들다구~ 하지만 이해하고 나니 이런 그림이 좋긴 하다.

또한  
**해시 테이블 안의 데이터가 25% ~ 75% 정도 차 있을 때 가장 최상의 효율을 내기 때문에, 25% ~ 75%의 공간을 맞추기 위하여 resizing을 할 수 있다.**  
**주의 : hash table의 크기를 수정하였다면, 기존 데이터를 수정한 크기에 다시 처음부터 넣어주어야 한다.**

# **Hash table은 어떻게 정리할까?**

**hash table은 어떻게 자료를 정리할까?**

1. 키와 값을 데이터로 넣는다.
   ex) 티모 : 탑 --> key = 티모 // 탑 = value<br>
2. 그러면 hash 함수라는 것을 통해 key를 index로 바꿔준다
   ex) hashfunction(티모) ==> 3 // 여기서 key를 index로 바꿔주는 해쉬 함수는 각자 사람들이 만들기 나름이다. **이걸 잘 만들어야지 나중에 "충돌"이라는 것이 없다.**<br>

```js
function hashfn(key) {
  let pw;
  pw = Math.floor(key.length / 2);
  return pw;
}
//간단하게 이런식으로 만들 수 있다. 이건 너무 간단하고
//아스키 코드를 이용하거나 여러 방법이 있다고 한다. 호호
```

삼. 그러면 저장공간인 storage(배열)의 3번째 // storage[3]에 {티모 : 탑}을 넣어준다.

사. 이후 우리가 만든 코드를 통해 key인 '티모'를 넣으면 value인 "탑"이 나오는 것!

# **Hash 충돌 (collision)이란?**

해쉬함수의 **key의 양은 셀 수 없지만** **index는 정수**라서 한계가 있다.

그래서 다른 key라도 같은 Index를 만들어 내어 같은 곳에 저장하기도 한다.  
이런 경우를 **collision 혹은 해쉬 충돌이 일어났다 라고 표현**한다.

ex)

1. 위에 티모를 넣었을 때 storage[3]에다가 저장을 했다.
2. 그런데, {경보 : 갓킹}을 넣으려고 하는데 key인 '경보'를 index로 바꾸니 3이 나온다면?
3. 이미 storage[3]에는 {티모 : 탑}이 저장되어 있어서 충돌이 일어난다.

# **Hash 충돌 해결**

open addressing: 다른 여분의 인덱스에 설정하기  
1-1. 선형 탐사: 만약 1번 칸이 비어 있다면 2번 칸이 비어 있는지 검사 후, 비어 있다면 2번 칸에 넣음.  
1-2. 이중 해시: 해시 함수를 2개로 두고, 평소에는 1만 쓰다가 충돌시 2를 써서 새로운 인덱스로 조정  
Close addressing: 충돌이 일어나도 해당 위치에 저장한다. 하지만 여러 개를 둘 수 있는 다른 방법을 사용함.  
2-1. 버켓: 배열의 한 요소가 다시 배열임. 2차원 배열처럼. 그래서 해시 충돌이 일어나게 되면 요소 안의 배열로 쌓인다.  
2-2. 체이닝: 충돌된 값들을 연결 리스트로 연결.

https://velog.io/@riceintheramen/hash-Table#%ED%95%B4%EC%8B%9C-%EC%B6%A9%EB%8F%8C%EC%9D%84-%EB%8F%8C%ED%8C%8C%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95

[출처 - 코드스테이츠 이유정 강사님의 블로그]

**여러 방법이 있지만, linked list를 이용해서 같은 index에 여러 정보를 저장 가능!**

# **Hash table method**

insert: 키와 값을 해시 테이블에 넣어 줍니다.  
retireve: 키를 넣었을 때, 값이 나옵니다.  
remove: 해당 데이터를 삭제합니다.  
\_resize: 25%~75%의 효율을 지킬 수 있도록 배열의 사이즈를 줄이거나 키웁니다.

# **Hash table 코드**

**해시 테이블 안의 데이터가 25% ~ 75% 정도 차 있을 때 가장 최상의 효율을 내기 때문에, 25% ~ 75%의 공간을 맞추기 위하여 resizing을 할 수 있다.**  
잊지말자! 이것도 코드로 만들어야 한다.  
**주의 : hash table의 크기를 수정하였다면, 기존 데이터를 수정한 크기에 다시 처음부터 넣어주어야 한다.**

#### **1. hash function // key를 index로 바꿔 주는 함수. 친절하게 부트캠프에서 만들어 줌.**

```js
const hashFunction = function (str, max) {
  let hash = 0;
  for (let i = 0; i < str.length; i++) {
    hash = (hash << 5) + hash + str.charCodeAt(i);
    hash &= hash; // Convert to 32bit integer
    hash = Math.abs(hash);
  }
  return hash % max;
};

module.exports = hashFunction;
```

#### **2. limited_array 라고 storage저장공간을 순회하고, index를 받아오고, 값을 넣을 수 있도록 도와주는 함수. 친절하게 부트캠프에서 만들어 줌.**

```js
const LimitedArray = function (limit) {
  const storage = [];

  const limitedArray = {};
  limitedArray.get = function (index) {
    checkLimit(index);
    return storage[index];
  };
  limitedArray.set = function (index, value) {
    checkLimit(index);
    storage[index] = value;
  };
  limitedArray.each = function (callback) {
    for (let i = 0; i < storage.length; i++) {
      callback(storage[i], i, storage);
    }
  };

  var checkLimit = function (index) {
    if (typeof index !== "number") {
      throw new Error("setter requires a numeric index for its first argument");
    }
    if (limit <= index) {
      throw new Error("Error trying to access an over-the-limit index");
    }
  };

  return limitedArray;
};

module.exports = LimitedArray;
```

#### **3. hash table 뼈대**

```js
class HashTable {
  constructor() {
    this._size = 0;                                 // 크기를 알아야지 언제 resize하는지 알 수 있다!
    this._bucketNum = 8;                            // hash table의 크기는 처음부터 정해놓고 시작해야 하기 떄문에 가볍게 8로 시작.
    this._storage = LimitedArray(this._bucketNum);  // storage라는 저장 공간을 만들자!
  }
```

**hash table에 들어간 데이터의 길이, hash table의 첫 크기, 저장공간 storage를 만드는 기본 뼈대 함수이다.**  
위에 1, 2번 째 줄은 위 사진 (1, 2)와 연결해 주는 함수.

#### **4. insert 함수 (데이터 넣기)**

```js
  insert(key, value) {
    const index = hashFunction(key, this._bucketNum);  // 이거를 통해 우리가 넣은 키와 값에서 키를 index(숫자)로 바꿀 수 있다.
    let bucket = {};                                   // 데이터는 객체로 저장되기 떄문에 빈 객체를 우선 만든다.
    if (this._storage.get(index) === undefined) {      // 만약, storage[index], 즉 (배열의[index])가 없다면 여기에 데이터를 넣을 것!
      bucket[key] = value;                             // 위에 만든 빈 객체에다가 우리가 넣을 Key와 value를 넣어주자.
      this._storage.set(index, bucket);                // set은 storage[index]에 우리가 넣을 buckt[key] =value를 넣는 함수이다.

    } else {                                           // 그런데 만약 storage[index]에 이미 데이터가 있다면?
      bucket = this._storage.get(index);               // {}객체를 storage[index]로 바꾼다.
      bucket[key] = value;                             // 위에 만든 빈 객체에다가 우리가 넣을 Key와 value를 넣어주자.
      this._storage.set(index, bucket);                // 그리고 기존에 있던 storage[index] value에 새로운 value를 덮어쓴다.
    }
    this._size++;                                      // 넣을 때 마다 사이즈는 ++!

    if ((this._size / this._bucketNum) * 100 > 75) {  // 만약 사이즈가 75%가 넘어가면, storage(배열)의 크기를 2배로 늘리자.
      this._resize(this._bucketNum * 2);
    }
    return this._storage
  }
```

**원래는 데이터가 충돌하면 linked list를 만들어야 하지만, 아직은 초보라서 기존 데이터 덮어쓰기 할 꺼야~~**

차근차근 살펴보자.

```
1. 우선 insert에는 key, value가 들어간다. '티모, 탑' 을 넣어보자
 const index = hashFunction(key, this._bucketNum); 를 통해
 우리가 넣은 '티모'가 특정 index로 바뀐다. 그냥 1이라고 생각하자.
 티모 = 1
 // 14번 줄
2. 빈 객체 bucket {}을 만든다. // 15번 줄

3. this._storage.get(index)의 값은 storage[1]이다. 만약 여기에 아무 데이터도 없다면 // 16번 줄
빈 객체였던 bucket{}을 {티모 : 탑}으로 만들어 주자.  // 17번 줄

4. 그리고 this._storage.set(index, bucket) 을 통해
storage[1]에다가 {티모 : 탑}을 넣어주자.  // 18번 줄

그럼 storage[1] === {티모: 탑}이 된다.
storage는 배열이기 때문에 [[],  {티모: 탑}, [],[],[],[],[],[],[]]
이 된다. 나머지 배열에는 값을 안 넣었기 때문에 아마 빈 배열일 것이다.

5. 데이터를 또 넣자. {티모 : 미드}를 넣고 싶다.

6. 그러면 storage[1]은 이미 {티모 : 탑}이 존재한다. //20번 줄

7. 그러면 빈 객체 bucket을 {티모 : 미드}로 하고 // 21번 줄

8. this._storage.set(index, bucket)을 통해 storage[1]에 그냥 넣어주자. // 23번 줄
이러면 storage[1] === {티모: 탑}에서
storage[1] === {티모: 미드}가 된다.

9. 그리고 사이즈를 늘리자

10. 사이즈가 만약 75%가 찼다면, resize함수를 실행시켜
storage배열 저장 공간을 2배로 늘리자.
기존은 8이지만, 늘리면 16칸!
```

#### **5. retrieve함수를 이용해 key를 넣어 value 찾기**

```js
  retrieve(key) {                                       // 이건 우리가 저장한 데이터에서 Key를 통해 value를 넣는 것.
    const index = hashFunction(key, this._bucketNum);   // 이거를 통해 우리가 넣은 키와 값에서 키를 index(숫자)로 바꿀 수 있다.
    if (this._storage.get(index) === undefined) {       // 만약 storage[index]에 데이터가 없다면
      return undefined;                                 // undefined
    }
    return this._storage.get(index)[key];               // 있으면 storage[1][key]를 통해 value를 빼자.

  }
```

**우리는 기존 storage[1] === {티모 : 탑}을 넣었다.**  
**여기서 retrieve(티모)를 넣어서 '탑'을 리턴할 수 있다.**

차근차근

```
1. const index = hashFunction(key, this._bucketNum)을 통해
'티모'의 index인 1을 만들자.

2. 만약 데이터가 기존에 없으면 그냥 undefined!

3.  return this._storage.get(index)[key]
보기엔 복잡하지만
storage === [[], {티모 : 탑}, [],[],[],[],[],[] ]
storage[1] === {티모 : 탑}
storage[1][key] === '탑'

차근차근 보면 이런 모습이다. 그래서 key를 통해 value를 찾을 수 있다.

```

#### **6. remove함수를 이용해 데이터 삭제**

```js
  remove(key) {
    const index = hashFunction(key, this._bucketNum);   // 이거를 통해 우리가 넣은 키와 값에서 키를 index(숫자)로 바꿀 수 있다.

    this._storage.each(function (bucket, i) {           // each함수는 storage를 처음부터 끝까지 반복해주는 함수이다. LimitedArray에 만듦
      if (index === i) {                                // 존재한다면?
        delete bucket[key]                              // 배열을 삭제하는 것이 아니라, 객체를 삭제!
      }
    })

     this._size--;                                      // 데이터 삭제 했으니 --

    if ((this._size / this._bucketNum) * 100 < 25) {    // 데이터가 25%미만이면 storage의 크기 줄이자
      this._resize(this._bucketNum / 2);
    }
  }
```

차근차근
위에서 넣은 {티모:탑}을 삭제해보자.

```

1. const index = hashFunction(key, this._bucketNum)을 통해
'티모'의 index인 1을 만들자.

2.  this._storage.each(function (bucket, i)을 통해
storage 배열을 처음부터 끝까지 살펴보자.
 (each는 LimitedArray에 부트캠프가 만들어 줌. 착하네?)

3. 찾으면 {티모:탑}을 삭제하자
(불쌍한 티모.. 다음에는 {티모: 서폿}.넣어줄게

4. 데이터가 삭제 됐으니 크기 --

5. storage에 데이터의 크기가 전체의 25%도 안 된다면,
storage 배열 크기를 절반으로 줄이자.
```

#### **7. resize를 통해 storage크기 바꾸기**

**주의 : hash table의 크기를 수정하였다면, 기존 데이터를 수정한 크기에 다시 처음부터 넣어주어야 한다.**

```js
  _resize(newBucketNum) {                               // 여기에는 우리가 크기를 늘릴 숫자가 들어간다.
    let oldStorage = this._storage;                     // 우선 기존 storage에 있는 데이터를 모두 저장해주자.
    this._size = 0;                                     // 사이즈 초기화
    this._bucketNum = newBucketNum;                     // 배열의 크기를 기존 크기에서 새로 들어갈 크기로 바꿔준다.
    this._storage = LimitedArray(this._bucketNum);      // 새로운 크기의 storage를 만든다.

    oldStorage.each(bucket => {                         // each를 통해 데이터를 순회하고
      for (let key in bucket) {
        this.insert(key, bucket[key]);                  // 데이터를 다시 새로운 storage에 insert 해주자.
      }
    });

    return this._stroage;

  }
```

차근차근

```
주의에 써둔 것을 통해 만들었다.

1. let oldStorage = this._storage를 통해
기존 데이터를 저장하자.

2. size 초기화

3.  this._bucketNum = newBucketNum을 통해 사이즈 재설정.
(만약 줄인다면 원래 크기 8에서 4로, 늘린다면 8에서 16으로)

4.  this._storage = LimitedArray(this._bucketNum)
이것은 storage(배열)을 다시 만들어 주는 기능이다.
LimitedArray에 부트캠프가 만들어 놓았다. 착하네?
###
5. oldStorage.each(bucket => 을 통해 기존에 저장해 두었던
데이터를 처음부터 끝까지 순회해주자.

6.  this.insert(key, bucket[key])
바뀐 storage에다가 다시 추가해주자.

만약 처음 만든
storage === [[], {티모 : 탑}, [],[],[],[],[],[] ]
이것을 기준으로 resize한다면
데이터가 전체의 25%를 차지하지 못하여  storage 크기를 줄여야 한다.
기존 8에서 4로 줄이자.
그러면?

storage === [[], {티모 : 탑}, [],[] ]
이 된다. 티모의 집이 작아졌다.

```

# **끝**
