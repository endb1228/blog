---
title: 컴포넌트 간의 바인딩
author: Jonghyeok Lee
date: 2023-03-04
category: [Javascript]
tags: [Javascript]
layout: post
---



**Documentation [ [English][1] / [Korean][2] ]**

양방향 바인딩은 자식 컴포넌트가 부모 컴포넌트를 변경시킬 때, 변경점이 명확하지 않다는 문제가 있음.
이러한 이유로 자식->부모 방향 바인딩은 emitting event를 사용함.
```javascript
<child v-bind:title="doc.title"
               v-on:update:title="doc.title = $event"
></child>
```
위 코드와 같이 부모->자식 방향 바인딩은 child 컴포넌트의 title 프로퍼티를 이용하며,
자식->부모 방향 바인딩은 child 컴포넌트에서 'update:title'를 emit하는 방식을 이용함.

따라서 부모 컴포넌트에서 바인딩된 객체가 변경될 때에는 자식 컴포넌트의 객체가 변경되지만,
반대의 경우 emitting event 함수를 명시적으로 호출해야 함.

위 코드는 아래와 같이 줄일 수 있음.
```javascript
<child :title.sync="doc.title"></child>
```

<br>

***이 글은 2021/11/19에 작성된 글입니다.***

[1]: https://vuejs.org/v2/guide/components-custom-events.html?#sync-Modifier
[2]: https://kr.vuejs.org/v2/guide/components.html#sync-%EC%88%98%EC%8B%9D%EC%96%B4


