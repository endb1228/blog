---
title: CSS 페이지 레이아웃
author: Jonghyeok Lee
date: 2023-03-04
category: [Javascript, CSS]
tags: [Javascript, CSS]
layout: post
---

## Page Layout

[Blog][page layout, blog]

### 1. Normal flow

기본적으로 대부분의 요소들은 normal flow를 따라 부모 요소 안에서 순서대로 배치됨  
만약 특정 요소에 normal flow를 벗어나는 스타일이 적용되면 해당 요소는 normal flow가 적용된 요소들과 독립적으로 배치됨

### 2. Containing Block

[MDN][containing black, MDN]

컨테이닝 블록은 어떤 요소의 크기 및 위치를 결정하는 기준이 되는 영역을 뜻함
일반적으로는 부모 요소의 content 영역이지만, 이는 position 프로퍼티에 따라 달라짐

### 3. Position

[MDN][position, MDN]

Position 속성은 어떤 요소를 컨테이닝 블록으로 식별할 것인지를 결정함  
Position 속성에는 다음 5가지 종류가 있음

* static  
  기본값으로, 요소가 normal flow를 벗어나지 않으며 top, left같은 프로퍼티에도 영향을 받지 않음


* relative  
  요소가 normal flow를 벗어나지 않으며 자기 자신의 위치(아마 static일 때의 위치)를 기준으로 top, left같은 프로퍼티의 영향을 받음


* sticky
  요소가 기본적으로 normal flow를 벗어나지 않고 static과 유사하게 작동  
  top, left같은 프로퍼티로 지정한 임계값을 벗어나면 normal flow를 벗어나고 fixed와 유사하게 작동  
  컨테이닝 블록의 content 영역에 다다르면 다시 fixed가 해제됨


* absolute  
  요소가 normal flow를 벗어나며 상위 요소를 기준으로 top, left같은 프로퍼티의 영향을 받음


* fixed  
  요소가 normal flow를 벗어나며 뷰포트나 페이지 영역을 기준으로 top, left같은 프로퍼티의 영향을 받음


보다 자세한 내용은 MDN 참조

### 4. Display

display는 normal flow 상에서 요소가 어떻게 배치될 것인지를 결정  
display 프로퍼티는 display-outside와 display-inside 2가지를 설정할 수 있음

1. display-outside

- inline  
  요소의 앞뒤를 줄바꿈하지 않는 inline 요소가 됨  
  뷰포트를 넘어설 때까지 같은 줄 안에서 배치되며, 뷰포트를 넘어서면 다음 줄로 넘어감


- block  
  요소의 앞뒤를 줄바꿈하는 block 요소가 됨


- inline-block  
  요소의 앞뒤를 줄바꿈하지 않는 block 요소가 됨


- none  
  요소 및 하위 요소가 접근성 트리에서 제거되어 표시되지 않음


2. display-inside

- flow  
  하위 요소가 normal flow를 따름


- flow-root  
  새로운 block formatting context(블록 박스가 생성되고 float가 다른 요소와 상호작용하는 공간)을 생성한다고 함  
  어떤 요소에 float가 적용됐을 경우 부모 요소가 box의 크기를 결정할 때 해당 요소를 인식하지 못 하는 문제를 해결할 수 있음


- flex  
  flex layout은 웹앱이나 복잡한 웹페이지에서 쉽게 공간을 분배하고 배열하기 위해 생겨났음  
  flex layout은 따로 문서를 하나 작성할 예정 <!-- TODO -->


- grid  
  grid layout은 세로 열과 가로 행을 기준으로 요소를 정렬하기 위해 생겨났음
  table과 유사하지만, table보다 유연하고 쉽게 레이아웃을 구현할 수 있음
  grid layout 역시 따로 문서를 하나 작성할 예정 <!-- TODO -->


### 5. Float / Clear


1. float

float는 요소가 normal flow를 벗어나고 display-outside가 block으로 변경됨  
float 값에 따라 컨테이너의 왼쪽 혹은 오른쪽으로 정렬됨  
float가 적용된 요소가 여러 개일 경우 해당 요소들끼리 자동으로 정렬됨
float가 설정된 요소는 상위 요소가 해당 요소를 인식하지 못 하기 때문에 따로 처리가 필요함

2. clear

텍스트 및 inline 요소들은 float가 적용된 요소들과 같은 줄에도 배열되지만,
clear가 젹용된 요소는 float가 적용된 요소들과 같은 줄에 배열되지 않고 위아래로만 배열됨  
clear가 left / right 일 경우 같은 값의 float가 적용된 요소에만 적용되며, clear가 both일 경우 left, right 모두 해당됨


<br>

***이 글은 2022/03/18에 작성된 글입니다.***

[page layout, blog]: https://blog.tommyzip.co.kr/code/css-basic-layouts-display/#display-outside-inside
[containing black, MDN]: https://developer.mozilla.org/ko/docs/Web/CSS/Containing_block
[position, MDN]: https://developer.mozilla.org/en-US/docs/Web/CSS/Containing_block
