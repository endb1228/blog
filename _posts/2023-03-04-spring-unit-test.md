---
title: 스프링 유닛 테스트
author: Jonghyeok Lee
date: 2023-03-04
category: [Spring, unit test]
tags: [Java, Spring, unit test]
layout: post
---

[Getting Started][1]    
[Documentation][2]

Spring intializr를 통해 프로젝트를 생성하면 기본적으로 JUnit을 이용한 unit test 모듈도 아래와 같이 자동으로 생성됨.

```java

@SpringBootTest
class GymApplicationTests {

    @Test
    void contextLoads() {
    }
}
```

@SpringBootTest annotation을 적용한 class에서는 아래와 같이 @AutoWired를 사용하여 주입할 수 있음.

```java

@SpringBootTest
class GymApplicationTests {

    @Autowired
    private GymController controller;

    @Test
    void contextLoads() {
        assertThat(controller).isNotNull(); // assertNotNull 보다 assertThat을 사용하자.
    }
}
```

주요 서버 동작을 테스트 하기 위해 Service에 대한 테스트를 아래와 같이 작성함.

```java
@SpringBootTest
@AutoConfigureMockMvc
class GymServiceTest {

    @Autowired
    MockMvc mockMvc;

    @Test
    void insertGym() throws Exception {
        Gym gymTest = new Gym("testName1", "testAddress", new java.sql.Date(new Date().getTime()));

        MockMultipartFile info = new MockMultipartFile("info", null, "application/json", gymTest.getInfoString().getBytes());

        MockMultipartHttpServletRequestBuilder builder = multipart("/gyms")
                .file(info);
        mockMvc.perform(builder)
                .andExpect(status().isOk());
    }
}
```

class에 @AutoConfigureMockMvc annotation을 붙여주고 class 안에서 @Autowired annotation이 붙은 MockMvc 인스터스를 만들어줌.
MockServletRequestBuilder 타입의 builder를 통해 method와 content를 정의하고, mockMvc.perform으로 작업 수행.

<br>

***이 글은 2021/11/19에 작성된 글입니다.***

[//]: # (
TODO: MockMvc, Mockito, BDDMockito
)
[//]: # (
TODO: hibernate h2
)


[1]: https://spring.io/guides/gs/testing-web/

[2]: https://docs.spring.io/spring-framework/docs/current/reference/html/testing.html

[//]: # (
TODO: https://mangkyu.tistory.com/145 참고해서 다시 작성
)
