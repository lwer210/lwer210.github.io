---
title: Swift - 에러 핸들링에 대해서 알아보자.
date: 2024-12-06 00:05:00 + 09:00
categories: [iOS, Swift]
tags: [swift, error]   
---

오늘은 Swift에 에러 핸들링을 공부하였다. Java와 거의 비슷하지만 약간의 차이점들이 존재해서 조금 헷갈리기도 하였지만 어려운 부분 없이 잘 넘어간 것 같다.

어쨋든 바로 공부한 내용을 소개해보겠다.

## ❓ **에러 핸들링이란?**
쉽게 말하면 **메서드가 실행되는 동안에 발생하는 에러를 적절히 처리**하는 것을 말한다.

Java 또는 다른 언어를 학습하지 않았다면 살짝 어려울 수 있지만 조금만 익숙해지면 개념은 크게 어렵지 않다.

에러를 핸들링하는 것에는 두가지 단계를 거쳐야한다.

1. 메서드 내에서 원하는 결과가 아닌 다른 값이 나올 경우 에러를 발생시킨다.
2. 메서드가 던진 에러를 적절히 처리한다.

이 두가지 단계를 거쳐서 에러 핸들링을 진행할 수 있다.

우선 에러 타입을 어떤식으로 선언할 수 있는지부터 알아보자.

## 🚨 **에러 타입 선언**
일반적으로 에러 타입을 선언할떄는 열거형을 사용해서 선언한다.

예시
```swift
enum ErrorEnum: Error{
  case Error1
  case Error2
}
```
위 코드처럼 ``Error`` 프로토콜을 따르게 설정한후 열거형 인스턴스를 정의하면 된다.

다음으로 이렇게 정의한 에러를 어떻게 던질 수 있는지 알아보자.

## 💥 **에러 스로잉**
우선 메서드 내에서 에러가 발생할 수 있다는 것을 명시해줘야하는데 ``throws`` 키워드를 사용하여 명시가 가능하다.

예시
```swift
enum ErrorEnum: Error{
  case Error1
  case Error2
}

func error1Example() throws{
    throw ErrorEnum.Error1
}

func error2Example() throws{
  throw ErrorEnum.Error2
}
```

위 예시처럼 ``throws`` 키워드를 이용하여 메서드에서 에러가 발생할 수 있다는 것을 명시한 후 ``throw`` 를 사용하여 에러를 스로잉할 수 있다.

> 에러를 던진다는 것을 에러 스로잉이라고 한다.

만약 반환값이 있는 메서드에서 사용할 경우 반환 타입 앞에 ``throws``를 붙혀주면 된다.

예시
```swift
enum ErrorEnum: Error{
  case Error1
  case Error2
}

func error1Example(bool1: Bool) throws -> String{
    if bool1{
        return "Error1 Example"
    }else{
        throw ErrorEnum.Error1
    }
}

func error2Example(bool2: Bool) throws -> String{
    if bool2{
        return "Error2 Example"
    }else{
        throw ErrorEnum.Error2
    }
}
```
이런식으로 사용이 가능하다.

이렇게 에러 핸들링에 첫번째 단계인 에러를 던지는 것에 대해 알아봤으니 이제 메서드를 호출하여 에러가 발생할 경우 적절히 처리하는 법을 알아보자.

## 🧹 **에러 처리**
우선 ``throws`` 키워드가 붙은 메서드를 호출할때는 반드시 앞에 ``try`` 를 붙혀줘야한다.

예시
```swift
enum ErrorEnum: Error{
  case Error1
  case Error2
}

func error1Example(bool1: Bool) throws -> String{
    if bool1{
        return "Error1 Example"
    }else{
        throw ErrorEnum.Error1
    }
}

func error2Example(bool2: Bool) throws -> String{
    if bool2{
        return "Error2 Example"
    }else{
        throw ErrorEnum.Error2
    }
}

try error1Example(bool1: false)
try error2Example(bool2: false)
```
이런식으로 ``try`` 를 반드시 붙혀줘야한다.

하지만 이렇게만 사용하면 에러 핸들링이 아니라 그냥 에러를 발생시키는 것이다.

이때 ``do-catch`` 문을 사용해서 발생한 에러를 처리해야한다.

예시
```swift
enum ErrorEnum: Error{
  case Error1
  case Error2
}

func error1Example(bool1: Bool) throws -> String{
    if bool1{
        return "Error1 Example"
    }else{
        throw ErrorEnum.Error1
    }
}

func error2Example(bool2: Bool) throws -> String{
    if bool2{
        return "Error2 Example"
    }else{
        throw ErrorEnum.Error2
    }
}

do{
    try error1Example(bool1: false)
}catch ErrorEnum.Error1{
    print("Error1")
}catch let error{
    print("알 수 없는 에러: \(error)")
}

do{
    try error2Example(bool2: false)
}catch ErrorEnum.Error2{
    print("Error2")
}catch let error{
    print("알 수 없는 에러: \(error)")
}
```

실행 결과
```
Error1
Error2
```
이런식으로 ``do-catch`` 를 사용해서 발생한 에러를 처리할 수 있다.

```swift
do{
    try error1Example(bool1: false)
}catch ErrorEnum.Error1{
    print("Error1")
}catch let error{
    print("알 수 없는 에러: \(error)")
}
```
위 코드를 살펴보자.

``catch`` 옆에는 처리할 에러를 명시하여 그 에러가 발생했을 경우 실행한 코드를 작성하면 된다.

``catch``옆에 ``let error``로 명시되어있는 부분은 명시된 에러를 제외한 모든 에러를 처리하겠다는 뜻이다.

또한 ``let error`` 코드를 통해서 발생한 에러 객체를 넘겨받아서 에러를 처리할 수 있다.

개발을 하면서 에러에 종류와는 상관 없이 값을 반환하기전에 다른 작업을 수행한 후 값을 반환해야할 일이 생기기도 한다.

이때 어떻게 해결해야하는지도 알아보자.

## ⏳ **defer 구문 사용**
``defer`` 구문은 메서드가 값을 반환하기 전에 수행할 코드를 작성할 수 있다.

예시
```swift
enum ErrorEnum: Error{
  case Error1
  case Error2
}

func error1Example(bool1: Bool) throws -> String{
    
    defer{
        print("defer 구문")
    }
    
    if bool1{
        return "Error1 Example"
    }else{
        throw ErrorEnum.Error1
    }
}

do{
    try error1Example(bool1: false)
}catch ErrorEnum.Error1{
    print("Error1")
}catch let error{
    print("알 수 없는 에러: \(error)")
}
```

실행 결과
```
defer 구문
Error1
```

이런식으로 값을 반환하기 전에 수행해야할 코드를 작성할 수 있다.

## 🗂️ **정리**
에러 핸들링이란 메서드 내에서 원하는 값이 아닌 다른 값을 반환하게 될 경우 에러를 스로잉한 후 적절히 처리하는 것을 말한다.

``throws`` 키워드를 이용하여 메서드에서 에러가 발생할 수 있음을 명시할 수 있으며 ``throws`` 키워드로 명시된 메서드를 호출할때는 ``try`` 를 붙혀서 호출한다.

에러 처리는 ``do-catch``문을 사용하여 발생한 에러를 적절히 처리할 수 있다.

값을 반환하기전 수행해야할 코드가 있다면 ``defer`` 구문을 사용하여 처리할 수 있다.

## 💭 **느낀점**
Swift에서의 에러 핸들링은 기존에 Java에서 자주 사용하던 방식과 유사한 부분이 있긴하지만 형식 자체에서 차이를 많이 느끼고 조금은 헷갈리기도 하지만 이해하는데 큰 문제가 없어서 공부하기 수월했다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판