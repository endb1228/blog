---
title: 쿠키와 세션
author: Jonghyeok Lee
date: 2023-03-04
category: [HTTP]
tags: [HTTP, cookie, session, authentication]
layout: post
---

HTTP는 기본적으로 connectionless, stateless한 특성을 가짐.

> ### Connectionless
>
> 하나의 요청에 대해 하나의 응답을 보낸 후 연결을 끊음.
> 응답 이후 바로 연결을 끊어버리기 때문에 여러 클라이언트로부터 한 번에 많은 요청이 와도 비교적 적은 부담으로 처리할 수 있음.
> 따라서 지속적으로 응답을 받기 위해서는 지속적으로 요청을 보내야 함.
> 또한 매 요청에 대해서 3-way handshaking을 수행해야 함.

> ### Stateless
>
> 이전에 주고받은 상태를 저장하지 않음.
> 이 역시 리소스 부담이 적고 이전과 다른 서버에 요청이 들어오더라도 동일한 응답을 내릴 수 있음.
> 따라서 여러 개의 요청에 중복된 데이터가 포함되어 있더라도 매번 같은 데이터를 포함하여 요청을 보내야 함.

위 특징 중 Stateless로 인해 생기는 문제점이 있음.
로컬환경에서만 저장되는 정보가 요청에 필요하다고 하면, 매번 해당 정보를 담아서 요청을 보내야 함.
예를 들어 유저 인증이 필요한 웹사이트를 이용하고자 할 때, 클라이언트에서 요청을 보낼 때마다 유저 인증과 관련된 정보를 매번 함께 보내야 함.

이 문제점을 해결하기 위해 세션과 쿠키라는 개념이 생겨났음.
세션과 쿠키 모두 클라이언트의 상태를 유지하기 위해 사용됨. (ex. 유저 인증)

### Cookie

쿠키는 클라이언트의 상태를 브라우저에 저장하고, 요청에 쿠키를 담아서 보내는 방식임.

쿠키는 지속 쿠키(persistent cookie)와 세션 쿠키(session cookie)로 나뉨.
지속 쿠키는 유효기간을 설정하여 해당 기간이 지나면 만료되도록 하며, 브라우저가 종료되도 삭제되지 않음.
세션 쿠키는 세션을 이용한 연결에서 사용되며, 브라우저가 종료되면 삭제됨.

지속 쿠키의 라이프사이클은 다음과 같음.
> 1. 클라이언트에서 쿠키가 발급되는 요청을 보냄.
> 2. 서버는 쿠키를 포함하여 응답을 보냄.
> 3. 클라이언트는 응답에 포함된 쿠키를 브라우저에 저장함.
> 4. 쿠키가 필요한 요청을 할 때마다 해당 쿠키를 포함하여 요청함. (HTTP header에 저장)
> 5. 쿠키의 유효기간이 지나면 쿠키가 만료됨.

쿠키는 클라이언트에 저장되기 때문에 탈취 및 변조에 취약함.

### Session

세션은 클라이언트의 상태를 서버에서 관리함.
클라이언트도 세션이 연결되었다는 것을 알 수 있도록 세션 id를 발급해줌. (주로 세션 쿠키의 형태)
세션의 라이프사이클은 다음과 같음.
> 1. 클라이언트가 세션이 생성되는 요청을 보냄.
> 2. 서버는 클라이언트의 상태를 저장하고, 세션 id를 발급해줌.
> 3. 클라이언트는 세션 id를 브라우저에 저장함.
> 4. 클라이언트가 세션이 필요한 요청을 할 때마다 세션 id를 포함하여 요청을 보냄.
> 5. 브라우저가 종료되면 쿠키가 삭제되고, 서버에서도 세션 연결을 종료함.

세션은 클라이언트 상태가 서버에 저장되기 때문에 쿠키에 비해 비교적 안전함.
연결된 세션이 많을 경우 서버에 부담이 큼.


<br>

***이 글은 2021/12/04에 작성된 글입니다.***
