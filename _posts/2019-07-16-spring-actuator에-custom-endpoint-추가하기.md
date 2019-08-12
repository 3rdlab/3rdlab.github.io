---
layout: post
title:  "Spring Actuacotr에 Custom Endpoint 추가하기"
categories: Spring Actuator
date:   2019-07-16 18:15:04 +0900
author: 3rdlab
---

**Spring Actuator**는 어플리케이션을 관리 및 모니터링 하는데에 유용한 다양한 기능들을 제공합니다.

기본적으로 제공되는 endpoint 들은 [여기](https://docs.spring.io/spring-boot/docs/current/reference/html/production-ready-endpoints.html)  에서 확인 가능하며, 기본 path는 `/actuator` 이며, HTTP뿐만 아니라 JMX로도 노출이 가능합니다.

endpoint는 사용자가 추가할 수도 있고, default endpoint의 기능을 수정할 수도 있습니다.    

​          

---

​    

# Custom Endpoint 만들어보기

​     



서버의 uptime을 출력하는 간단한 Custom EndPoint를 추가해 보겠습니다.



먼저 Spring Boot Web프로젝트에 spring-boot-actuator 의존성을 추가합니다.

gradle을 사용하는 경우 `build.gradle`에 아래를 추가합니다.

```groovy
implementation 'org.springframework.boot:spring-boot-starter-actuator'
```

​      

기본적으로 custom endpoint는 Spring에 등록된 `@Bean`에 `@Endpoint` 어노테이션과 `@ReadOperation`, `@WriteOperation` 또는  `@DeleteOperation` 어노테이션을 함께 사용하면 자동적으로 JMX 또는 HTTP 상에 노출되게 됩니다.

| Operation          | HTTP method |
| ------------------ | ----------- |
| `@ReadOperation`   | `GET`       |
| `@WriteOperation`  | `POST`      |
| `@DeleteOperation` | `DELETE`    |

(  `@ServletEndpoint`,  `@ControllerEndpoint`, `@RestControllerEndpoint`  등도 있습니다만, Reference에 의하면 새로운 endpoint를 추가하는 경우에는 `@Endpoint` 나 `@WebEndpoint`를 우선적으로 고려해야 합니다.)

​      

먼저 uptime을 출력하는 uptimer라는 객체를 만들어주고,

```java
public class UpTimer {
    
	public String getUptime() {
		
		RuntimeMXBean runtimeMxBean = ManagementFactory.getRuntimeMXBean();
		long uptime = runtimeMxBean.getUptime();
		
		return String.format("%02d:%02d:%02d", 
					TimeUnit.MILLISECONDS.toHours(uptime),
					TimeUnit.MILLISECONDS.toMinutes(uptime) % TimeUnit.HOURS.toMinutes(1),
					TimeUnit.MILLISECONDS.toSeconds(uptime) % TimeUnit.MINUTES.toSeconds(1));	
	}

}

```

​      

Uptimer를 출력하는 endpoint를 생성합니다.

```java
@Endpoint(id = "uptime")
public class UptimeEndpoint {

    @ReadOperation
    public UpTimer getUptime(){
        return new UpTimer();
    }

}
```

​      

마지막으로 해당 endpoint를 등록해줍니다.

```java
@Configuration
public class EndpointConfiguration {

	@Bean
	@Description("Display Application's Uptime")
	public UptimeEndpoint uptimeEndpoint() {
		return new UptimeEndpoint();
	}
}

```



이제 `@Endpoint`의 id로 설정되어 있는 `/uptime` 경로로 접속하면 다음과 같은 결과를 볼 수 있습니다.

(actuator의 기본경로를 바꾸지 않았다면 `/actuator/uptime` 입니다.)

```json
{"uptime":"00:00:10"}
```

​      

사실 HTTP상에서만 사용할 경우에는 그냥 Controller에서 처리할지, Actuator에서 처리할지에 관해서는 고민해볼 문제입니다.

제공하는 정보의 성격이나 역할에 따라 달라지겠지요..

​      

전체 소스는 <https://github.com/3rdlab/spring-actuator-custom-endpoint-example.git> 에서 확인 가능합니다.



