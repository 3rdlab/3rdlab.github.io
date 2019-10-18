---
layout: post
title:  "@RequestMapping에 private을 사용하면?"
categories: Spring
author: 3rdlab
published: true
tag: spring, aop, controller

---



sonarQube의 java rule들 둘러보다가 흥미로운 내용을 발견했다.

&nbsp;



> "@RequestMapping" methods shoud be "public"



&nbsp;

거의 본능적으로 `public` 으로 선언하지, `private`으로 선언하면 어떠한 일이 일어날지 생각해 본 적이 없었다.



`private`으로 선언 가능한 메소드라면 구지 `public`을 사용할 이유가 없다.



`private`으로 바꾸어 보아도 url은 정상적으로 매핑된다(물론 `@GetMapping`, `@PostMapping`등도 마찬가지).





그러면 왜 작동을 하는데 문제가 없어보이지만 `private`으로 선언하지 말라는 것일까?



&nbsp;

먼저 해당 메소드들은 Spring에서 reflection을 사용해 불러오기 때문에 가시성과는 무관하다.

> ...because Spring invokes such method via reflection

private, public, protected 뭐든 기능자체는 수행된다.

&nbsp;

문제는 다른데에 있다.

> ... private, @RequestMapping method by making it @Secured... it will still be called, whether or not the user is authorized to access it. That's because AOP proxied are not applied to non-public methods.



AOP 프록시 자체가 public이 아닌 메소드에는 작동하지 않는다.

@Secured나 @PreAuthorize 같은 기능들이 수행되지 않는다.

겉으로 문제없어 보이고, Runtime 시에 error도 나지 않지만 치명적인 문제가 될 수 있다.

&nbsp;

조금 더 들여다 보자.

&nbsp;&nbsp;

 [Spring AOP - Supported Pointcut Designators](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/aop.html#aop-pointcuts-designators) 



>Due to the proxy-based nature of Spring's AOP framework, protected methods are by definition *not* intercepted, neither for JDK proxies (where this isn't applicable) nor for CGLIB proxies (where this is technically possible but not recommendable for AOP purposes). As a consequence, any given pointcut will be matched against *public methods only*!
>
>If your interception needs include protected/private methods or even constructors, consider the use of Spring-driven [native AspectJ weaving](https://docs.spring.io/spring/docs/3.0.0.RC3/spring-framework-reference/html/ch07s08.html#aop-aj-ltw) instead of Spring's proxy-based AOP framework. This constitutes a different mode of AOP usage with different characteristics, so be sure to make yourself familiar with weaving first before making a decision.

&nbsp;

**proxy-based AOP는 public이 아니면 작동하지 않는다.** 

public이 아닌곳에 관점지향적 접근이 필요하다면 AspectJ를 고려해보자.
 