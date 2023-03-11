---
title: 스프링 시큐리티 인증
author: Jonghyeok Lee
date: 2023-03-04
category: [Spring, Spring Security]
tags: [Java, Spring, Spring Security, authentication, authorization]
layout: post
---

Login 인증에 대한 Spring security의 flow

1. 사용자가 인증 요청
2. 사용자의 id, password, role 등을 기반으로 authentication token 발행 및 사용자에게 전달
3. 이후 사용자로부터 인가가 필요한 요청이 들어왔을 때 요청에 포함되어 있는 token을 authenticationManager에 전달
4. authenticationManager의 구현체인 providerManager에서 다시

https://kobumddaring.tistory.com/60?category=976215



[1]: https://gregor77.github.io/2021/04/21/spring-security-02/
[2]: https://velog.io/@sa833591/Spring-Security-2
