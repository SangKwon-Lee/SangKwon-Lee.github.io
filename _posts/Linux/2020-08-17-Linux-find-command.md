---
layout: post
title: "[Linux] find 명령어"
categories: [Linux]
tags: [command]

---

## find
#### 지정된 문자열 패턴의 파일 검색
-name 옵션을 통해 파일을 이름으로 검색할 수 있다.
> $find \[directory] **-name** "\[file name]"

#### 예제
현재 디렉토리(.)에서 "install_drivers" 라는 이름을 가진 파일을 찾아라.
(이때 검색되는 경로는 하위 디렉토리를 포함한다.)
> $find . **-name** "install_drivers" 

