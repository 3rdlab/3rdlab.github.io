---
layout: post
title:  "아마도 당신이 몰랐을 Interceptor #1"
categories: Spring
date:   2019-09-22 18:15:04 +0900
author: 3rdlab
published: false
tag: spring, interceptor
---



Spring Interceptor와 관련하여 *아마도* 쉽게 정답을 떠올리기 힘들

( ~~저는 몰랐던~~) 질문을 몇개 드려보겠습니다. 오늘은 그 첫번째.





Interceptor는 filter를 거친 후에 실행됩니다. 

조금 더 정확히 표현하자면 Dispatcher Servlet에 등록된 Handler에 대한 Interceptor라고 할 수 있을 것입니다. 



스프링의 Interceptor는  `**HandlerInterceptor** ` interface를 이용하여 구현하고, 해당 interface는 3개의 method로 구성되어 있죠.

- `preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)`
-  `postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, @Nullable ModelAndView modelAndView)`
- `afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, @Nullable Exception ex)`



보통 실무에서는 `preHandle`이나 `postHandle`을 이용할 때 request나 response에 비해서는 세번째 파라미터인 `Object handler` 를 사용할 일은 많지 않을 것입니다.



그렇다면 `preHandle`이나 `postHandle의` parmaeter로 넘어오는 **Object Handler**에는 무엇이 넘어올까요? 

&nbsp;&nbsp;

&nbsp;

------

&nbsp;

&nbsp;



확인해 보면 대부분 `org.springframework.web.method.HandlerMethod` 로 확인이 될 것입니다.



해당 클래스는 Handler에서 해당 Request를 처리하기 위해 사용된 method를 나타냅니다.



예를들면 

```java
@GetMapping("/hello")
public String helloWorld() {
	return "world";
}
```



그러면 왜 변수명이 `handlerMethod`가 아니고 `handler` 라고 되어있는 것일까요?









여기서 `helloWorld()` 메소드의 정보가 `HandlerMethod`   에 담겨 넘어오게 됩니다.











1. controller 내부에서 exception 발생 시 afterCompletion 으로 propagation 되는가?
2. 



( HandlerInterceptor와 HanderlInterceptorAdapter와의 차이.)



아마 이제는 별 차이가 없다. 뭐든 편한거 하면 되지만 이왕이면 interface 구현이 낫겟지.



