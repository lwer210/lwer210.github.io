---
title: Swift - 열거형에 대해서 알아보자.
date: 2024-12-03 00:05:00 + 09:00
categories: [iOS, Swift]
tags: [swift, enum]   
---

오늘은 열거형에 대해 공부하였다. 열거형은 Java를 사용할때도 굉장히 많이 사용하였는데 Swift에서는 사용 방식이 조금 다른 것 같다.

지금부터 열거형에 대해 살펴보자.

## ❓ **열거형이란?**
간단하게 설명해서 **사용자가 직접 값을 정의하는 것**이다.<br>

바로 열거형에 구조로 넘어가보자.

## 🧱 **열거형 구조**
```swift
enum 열거형명{
  case 열거형 상수1
  case 열거형 상수2
}
```
위와 같이 ``enum`` 키워드와 ``case`` 키워드를 사용해서 열거형을 선언할 수 있다.<br>
이제 사용 예시로 넘어가보자.

## 🚀 **열거형 사용**
아래 코드를 확인해보자.<br>

예시
```swift
enum Example{
  case num
  case dou
  case str
}
```

위 코드와 같이 열거형을 정의할 수 있다.

이렇게 정의된 열거형을 사용하는 방법은 더 간단하다.

예시
```swift
enum Example{
  case num
  case dou
  case str
}

var ex: Example = Example.num

switch ex{
case Example.num:
    print("num")
case Example.dou:
    print("dou")
case Example.str:
    print("str")
}
```
실행 결과
```
num
```

이렇게 간단하게 열거형을 사용할 수 있다.<br>
스위프트에 타입 추론 덕분에 ``Example`` 을 빼고도 사용할 수가 있다.

예시
```swift
enum Example{
  case num
  case dou
  case str
}

var ex: Example = .num

switch ex{
case .num:
    print("num")
case .dou:
    print("dou")
case .str:
    print("str")
}
```
실행 결과
```
num
```

이런식으로 타입을 명시했기 떄문에 ``.`` 만 찍어서 사용이 가능하다.

열거형 상수에 변수를 추가할 수도 있다.

예시
```swift
enum Example {
    case num(numb: Int)
    case dou(doub: Double)
    case str(stri: String)
}

var ex1: Example = Example.dou(doub: 3.14)
var ex2: Example = Example.num(numb: 10)
var ex3: Example = Example.str(stri: "Hello")

func ExampleSwitch(example: Example){
    switch example{
    case .num(let numb):
        print("numb: \(numb)")
    case .dou(let doub):
        print("doub: \(doub)")
    case .str(let stri):
        print("stri: \(stri)")
    }
}

ExampleSwitch(example: ex1)
ExampleSwitch(example: ex2)
ExampleSwitch(example: ex3)
```

실행 결과
```
doub: 3.14
numb: 10
stri: Hello
```
이런식으로 열거형 상수에 변수를 넣어서 사용할 수도 있다.

## 🗂️ **정리**
열거형은 사용자가 값을 직접 정의하여 사용하는 것으로 열거형 상수에 변수를 넣어서 사용도 가능하다.

## 💭 **느낀점**
Java에서 사용하는 열거형과 살짝 다른점이 있긴 하지만 틀은 비슷하여 공부하는데 아무 이상 없이 잘 이해하고 넘어간 것 같다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판