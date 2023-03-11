---
title: 스프링 이미지
author: Jonghyeok Lee
date: 2023-03-04
category: [Spring]
tags: [Java, Spring, image transfer]
layout: post
---

[Link][1]

Spring MVC를 이용하여 이미지/미디어 전송.

1.  HttpServletResponse  
	가장 기본적인 구현 방식으로서 response 객체 및 servlet 구현을 이용.
	```java
	@RequestMapping(value = "/image-manual-response", method = RequestMethod.GET)
	public void getImageAsByteArray(HttpServletResponse response)throws IOException{
		InputStream in=servletContext.getResourceAsStream("/WEB-INF/images/image-example.jpg");
		response.setContentType(MediaType.IMAGE_JPEG_VALUE);
		IOUtils.copy(in,response.getOutputStream());
	}
	``` 
	다음과 같은 URL로 요청을 보낼 수 있음.
	```
	http://localhost:8080/spring-mvc-xml/image-manual-response.jpg
	```

2.  HttpMessageConverter    
	1의 방식은 [Message Conversion][2] 및 [Content Negotiation][3]의 면에서 문제점이 있음.

	> **Message Conversion**    
	Java에서는 http를 통해 데이터를 주고받는 과정에서 java object와 JSON 형식을 변환하는 것을 말함.

	> **Content Negotiation**   
	같은 URI로부터 어떤 형태로 데이터를 받을지를 결정하는 것을 말함.
	대표적으로 같은 URI에 접속하더라도 접속하는 국가에 따라서 언어가 달라지는 경우가 해당함.

	Controller 메소드에 @ResponseBody annotation을 적용하고, 메소드의 리턴 타입에 따라 적절한 message converter를 선택.

	```java
	@RequestMapping(value = "/image-byte-array", method = RequestMethod.GET)
		public @ResponseBody byte[] getImageAsByteArray() throws IOException {
		InputStream in = servletContext.getResourceAsStream("/WEB-INF/images/image-example.jpg");
		return IOUtils.toByteArray(in);
	}
	```
	다음과 같은 URL로 요청을 보낼 수 있음.
	```
	http://localhost:8080/spring-mvc-xml/image-manual-response.jpg
	```

	Method 안에서 response 객체에 대해 처리할 필요가 없음.
	Data source에서 image를 탐색하는 로직을 구현해야 하며, header나 status code를 추가할 수 없음.


3.  ResponseEntity  
	ResponseEntity<Byte[]>타입으로 데이터 전송.
	ResponseEntity는 body 및 header, status code를 control할 수 있도록 구현이 되어 있음.
	```java
	@RequestMapping(value = "/image-response-entity", method = RequestMethod.GET)
		public ResponseEntity<byte[]> getImageAsResponseEntity() {
		HttpHeaders headers = new HttpHeaders();
		InputStream in = servletContext.getResourceAsStream("/WEB-INF/images/image-example.jpg");
		byte[] media = IOUtils.toByteArray(in);
		headers.setCacheControl(CacheControl.noCache().getHeaderValue());
		
		ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(media, headers, HttpStatus.OK);
		return responseEntity;
	}
	```
	적절한 예외 처리와 그에 대한 적절한 response만 구현해주면 됨.


4.  ResponseEntity + Resource  
	Resource는 low-level resource에 대한 인터페이스로, 다양한 타입의 resource(local files, remote files, classpath resources)에 대해 쉽게 접근할 수 있도록 해줌.
	```java
	@RequestMapping(value = "/image-resource", method = RequestMethod.GET)
	@ResponseBody
	public ResponseEntity<Resource> getImageAsResource() {
		HttpHeaders headers = new HttpHeaders();
		Resource resource =
		new ServletContextResource(servletContext, "/WEB-INF/images/image-example.jpg");
		return new ResponseEntity<>(resource, headers, HttpStatus.OK);
	}
	```

<br>

***이 글은 2021/11/20에 작성된 글입니다.***




[1]: https://www.baeldung.com/spring-mvc-image-media-data
[2]: https://www.baeldung.com/spring-httpmessageconverter-rest
[3]: https://www.baeldung.com/spring-mvc-content-negotiation-json-xml
