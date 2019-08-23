---
layout: post
title:  "Pivotal101 세미나 후기"
categories: Spring, Pivotal, PKS, PAS
date:   2019-08-21 23:15:04 +0900
author: 3rdlab
---





삼성동 Google Campus에서 진행된 Pivotal101 세미나에 참가하였습니다.

Pivotal은 Spring Framework, Cloud Foundry, RabbitMQ등을 개발, 관리하고 있기에 친숙한 사람들에겐 친숙한 기업일 껍니다.

(*Wiki에 따르면 Dell 이 Pivotal 지분의 70%를 가지고 있습니다.*)



세미나는 두 세션으로 진행됐습니다.











## 첫번째 세션 - PKS, PAS와 Platform

-----------------------------

* **PKS**(Pivotal Container Service)
* **PAS**(Pivotal Application Service)

 첫번째 세션에서는 요즘 개발환경에 새롭게 등장하게 된 Platform Team과 그 역할을 중심으로  Platform 솔루션인  PKS(CaaS, Kubernates), PAS(PaaS) 에 대한 설명이 있었습니다.

해당 기술들은 이제 업계 표준이 되었다고 할 수 있는 Docker와 Kubernates를 기반으로 개발자들이 platform 을 보다 효율적으로 관리할 수 있는 추상화된 서비스를 제공합니다.

간략한 제품군은 추상화 정도에 따라 아래같이 될 것 같습니다.



* Faas(KNative(google), **PFS**) - Serverless, 곧 정식 버전 출시
  * Pass(Cloud Foundry, **PAS**)
    * Caas(Kubernates, **PKS**)
      * Iaas(AWS, Azure, GCP등)
        * Hardware









## 두번째 세션 - Agile Coaching

---------------------------

* Pivotal Labs
* Dojo
* App Tx

두번째 세션은 Agile 전도사(?)로써 Pivotal의 역할과 해당 솔루션들(Dojo, Pivotal Labs, App Tx)에 대한 소개 및 Platform product의 데모가 이루어졌습니다.

2-Pizza Team, DDD, TDD, MSA등 agile 개발문화와 관련된 여러가지 이야기가 나왔습니다.

간단히 설명하면

- Pivotal Labs : pivotal 사무실에 방문하여 한 팀으로 진행되는 agile coaching

* Dojo : 우리 사무실에 방문하여 한 팀으로 진행되는 agile coaching

* App Tx : agile 컨설팅







## 후기

Pivotal의 product들을 중심으로 세미나가 이루어졌지만 ,해당 제품개발의 바탕이 되는 철학 및 지향하는 바들을 통해 인프라 및 플랫폼 관련 환경이 어떻게 발전해 나가는지에 대해 간략하게나마 접할 수 있었습니다.









## 한마디 요약

__**Pivotal loves Kubernetes**__









## 둘러볼만한 링크

[Cloud Foundty](https://www.cloudfoundry.org/)

[Knative](https://knative.dev/-)

[BuildPack](https://buildpacks.io/)

[Bosh](https://bosh.io/)

[PFS](https://pivotal.io/platform/pivotal-function-service)

[PKS](https://pivotal.io/platform/pivotal-container-service)

[PAS](https://pivotal.io/platform/pivotal-application-service)

