---
layout: post
title:  "아마도 당신이 몰랐을 Interceptor"
categories: Spring
date:   2019-09-22 18:15:04 +0900
author: 3rdlab
published: false
tag: spring, interceptor
---



Spring Interceptor와 관련하여 아마도 여러분이 쉽게 정답을 떠올리기 힘들

( ~~저는 몰랐던~~) 질문을 몇개 드려보겠습니다.



 `**HandlerInterceptor** ` interface를 이용하여 구현하고, 해당 interface는 3개의 method로 구성되어 있죠.

- preHandle
- postHandle
- afterCompletion



1. handler

Interceptor는 filter를 거친 후에 실행됩니다. 

조금 더 정확히 표현하자면 Dispatcher Servlet에 등록된 Handler에 대한 Interceptor라고 할 수 있을 것입니다. 

그렇다면 preHandle의 parmaeter로 넘어오는 **Object Handler**에는 무엇이 넘어올까요?













1. controller 내부에서 exception 발생 시 afterCompletion 으로 propagation 되는가?
2. 



( HandlerInterceptor와 HanderlInterceptorAdapter와의 차이.)



아마 이제는 별 차이가 없다. 뭐든 편한거 하면 되지만 이왕이면 interface 구현이 낫겟지.



