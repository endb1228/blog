---
title: MIME type과 multipart
author: Jonghyeok Lee
date: 2023-03-04
category: [HTTP, MIME]
tags: [HTTP, MIME]
layout: post
---


### MIME

[MIME][1] (Multipurpose Internet Mail Extensions) 타입은 원래 이메일에서 전송 시 데이터의 타입을 정의해주기 위해 사용되었고,
그러다가 웹의 발달과 함께 HTTP 통신에도 사용하게 됨.

HTTP에서는 body에 들어가는 데이터 타입을 헤더에서 content-type으로 명시를 해주는데,
content-type을 MIME타입으로 명시해줌으로써 데이터가 어떤 형식인지 알 수 있음.

MIME타입은 [TYPE]/[SUBTYPE]형식을 가짐.

MIME타입의 [TYPE]에는 text, image, audio, video, application 등이 있음.


### Multipart

MIME타입 중 multipart는 여러 타입의 데이터를 하나의 request에 담기 위해 사용됨.

원래 html form의 enctype(인코딩 타입)은 default로 application/x-www-form-urlencoded를 사용함  
이 형식은 [KEY1]=[VALUE1]&[KEY2]=[VALUE2]&...의 key-value tuple로 인코딩됨.    
영어가 아닌 문자의 경우 percent encoded되기 때문에 바이너리 데이에 사용하기에는 적절하지 않음.

따라서 html form에 바이너리 데이터가 포함되어 있다면 multipart/form-data를 사용하는 것이 적절함.


<br>

***이 글은 2021/11/19에 작성된 글입니다.***

[1]: https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types
