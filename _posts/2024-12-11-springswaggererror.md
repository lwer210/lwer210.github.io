---
title: "Error - java.lang.NoSuchMethodError: 'void org.springframework.web.method.ControllerAdviceBean.<init>(java.lang.Object)' 오류 해결"
date: 2024-12-11 02:30:00 
categories: [Error, Spring]
tags: [error, solved, spring]   
---

평화롭게 Spring으로 백엔드 API를 개발하고 RestControllerAdvice로 Exception 핸들링을 설정한 후 swagger에 접속하려고 보니

![error](/assets/img/swagger_error.png)

이런 오류가 나면서

![errorui](/assets/img/swagger-ui-error.png)
이런 화면이 나왔다.

아무리 구글링을 해봐도 마땅한 해결 방법이 나오지 않았다.

```
java.lang.nosuchmethoderror: 'void org.springframework.web.method.controlleradvicebean.<init>(java.lang.object)'
```
이 에러의 원인은 해당 메서드를 찾지 못했을때 발생하는데 흔히 의존성에 버전 차이로 인해 발생하는 경우가 많다고 한다.

도저히 답이 안나오자 swagger를 가장 최신 버전으로 바꿔볼까 하는 마음으로 maven repository에 있는 swagger에 가장 최신 버전을 가져와서<br>
버전 업데이트를 해줬다.

```
implementation group: 'org.springdoc', name: 'springdoc-openapi-starter-webmvc-ui', version: '2.7.0'
```

그러자...

![solved](/assets/img/swagger-error-solved.png)

swagger에 접속이 되었다!!

아무래도 swagger와 Spring boot에 버전 차이 때문이였던 것 같다
