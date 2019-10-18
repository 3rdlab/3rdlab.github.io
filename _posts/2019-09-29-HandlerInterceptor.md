---
layout: post
title:  HandlerInterceptor와 HandlerInterceptorAdapter의 차이
categories: Spring
author: 3rdlab
publised: true
tag: spring, interceptor,handlerInterceptor, handlerInterceptorAdapter
---

# HandlerInterceptor와 HandlerInterceptorAdapter의 차이



 &nbsp;

Spring Interceptor는 `HandlerInterceptor` Interface를 구현해야 합니다.



&nbsp;

그렇다면 `Implements HandlerInterceptor`로 구현하는 것과 `extends HandlerInterceptorAdapter` 로 구현하는 것에는 어떠한 차이가 있을까요?

&nbsp;

---

&nbsp;





HandlerInterceptor**Adapter**는 `HandlerInterceptor` 인터페이스에서 필요한 기능만 가져와 쓰기 쉽게 해주기 위한 용도입니다. (더 정확하게는 `AsyncHandlerInterceptor`의)

&nbsp;





예를 들어 나는 "`preHandle`만 구현하고 싶다" 했을 때 `HandlerInterceptor`를 사용해서 메소드들을 다 override하는 것이 아니라 필요한 기능만 사용할 수 있습니다.

&nbsp;





스프링에서 보통 *Adapter 하는 클래스들은 Interface를 좀 더 간결하게 사용하게 해 주는 추상 클래스인 경우가 많습니다.

&nbsp;





그런데 Java8 이 등장한 이후  `HandlerInterceptor` 및 `AsyncHandlerInterceptor` 의 메소드들은 모두 default 선언이 되어있습니다.

구지 사용하지 않는 기능까지 override 할 필요가 없어졌다는 이야기이지요..

&nbsp;





이러한 이유에서 많은 **Adapter 클래스들이 deprecated 되지 않을까 싶습니다..

(`WebMvcConfigurerAdapter`는 이미 deprecated 되었습니다.)

&nbsp;

&nbsp;



>  제 결론은, java8 이상을 사용하고 있다면, 클래스의 다중상속이 지원되지 않는 자바의 특성 상, 특별한 경우가 아니면  `HandlerInterceptorAdapter` 보다는 `HandlerInterceptor`나 `AsyncHandlerInterceptor`를 구현하는 것이 더 좋은 방법이라 생각됩니다.





 