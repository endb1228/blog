---
title: Javascript 팁 정리
author: Jonghyeok Lee
date: 2023-03-06
category: [Javascript]
tags: [Javascript]
layout: post
---

1. image src 쓸 때 local path 넣을 떈 require() 쓰면 됨

2. 동적으로 component를 추가해야할 땐 v-bind:is='[컴포넌트 이름]' 입력

3. javascript에서 object를 호출할 때 pass by value되므로 for문이나 function 등 내부에서 변경 시에는 주의해야 함.  
   object 내부의 property를 변경 시에는 pass by reference되어 변경되므로, pass by value를 막기 위한 트릭으로도 사용할 수 있을 듯


<br>

***이 글은 2022/03/25에 작성된 글입니다.***
