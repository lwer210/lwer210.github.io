---
title: Swift - 프로토콜 대해 알아보자.
date: 2024-11-30 00:05:00 
categories: [iOS, Swift]
tags: [swift, protocol]
---

오늘은 처음보는 개념인 프로토콜에 대해서 공부하였다.<br>
내용은 그렇게 어렵지 않았지만 뭔가...설명하기 어려운 느낌...? 

어쨌든 오늘은 프로토콜에 대해서 알아보자.

## ❓ **프로토콜이란?**
**클래스가 충족해야만 하는 요구 조건들을 정의하는 것**을 프로토콜이라고 한다.

프로토콜은 ``protocol`` 키워드를 사용해서 선언할 수 있으며 내부에는 **클래스가 반드시 포함해야하는 메서드와 프로퍼티를 정의**한다.<br>

내용 자체는 그다지 어렵지 않다.<br>

바로 사용 방법에 대해서 알아보자.

## 🧩 **프로토콜 사용**

프로토콜 사용 예시 
```swift
protocol ExampleProtocol{
  var example: String { get }
  func exampleFunc () -> Int
}
```

이런식으로 클래스가 반드시 포함해야할 프로퍼티와 메서드를 정의할 수 있다.

이때 프로퍼티에 ``{ get }`` 또는 ``{ get, set }`` 을 꼭 명시해줘야 한다.

``get``은 읽기 전용, ``get, set`` 은 읽기, 쓰기 전용이란 뜻이다.

클래스 예시
```swift
class ExampleClass: ExampleProtocol{
    var example: String
    
    init(example: String) {
        self.example = example
    }
    
    func exampleFunc () -> Int{
        return 10
    }
}

var examplePro: ExampleClass = ExampleClass(example: "Hello")

print(examplePro.example)
print(examplePro.exampleFunc())
```
실행 결과
```
Hello
10
```

이런식으로 클래스에서 프로토콜을 구현해서 사용할 수 있다.

프로토콜에 또 다른 기능으로는 함수의 반환 타입으로 지정할 수 있다는 것인데 이것에 대해서 알아보자.

## 📦 **함수 반환 타입 프로토콜**
보통 함수를 선언할때 반환값이 있을 경우 반환 타입을 명시하도록 되어있다.

예시
```swift
func add(_ num1: Int, _ num2: Int) -> Int{
  return num1 + num2
}
```

위 코드처럼 반환하는 값에 타입을 명시해줘야한다.

이때 반환 타입을 프로토콜로 지정할 경우 **프로토콜을 따르는 모든 타입이 반환**될 수 있게 한다.

예시를 살펴보자.

예시
```swift
protocol ExampleProtocol{
    var example1: String { get }
    var example2: Int { get }
    var example3: Double { get }
}

class ExampleClass1: ExampleProtocol{
    var example1: String = "Class1"
    var example2: Int = 1
    var example3: Double = 1.0
}

class ExampleClass2: ExampleProtocol{
    var example1: String = "Class2"
    var example2: Int = 2
    var example3: Double = 2.0
}

func exampleFunc1() -> some ExampleProtocol{
    var example: ExampleClass1 = ExampleClass1()
    return example
}

func exampleFunc2() -> some ExampleProtocol{
    var example: ExampleClass2 = ExampleClass2()
    return example
}

var example1 = exampleFunc1()
var example2 = exampleFunc2()

print(example1.example1)
print(example2.example1)
```

실행 결과
```
Class1
Class2
```

위 코드처럼 ``some`` 키워드를 사용해서 프로토콜을 반환 타입으로 설정할 수 있으며 프로토콜을 따르는 타입들을 반환할 수 있다.

## 🗂️ **정리**
프로토콜은 클래스가 반드시 포함해야할 프로퍼티나 메서드들을 정의해둔 것을 말한다.

프로토콜을 따르는 클래스들은 반드시 프로토콜에 정의되어 있는 프로퍼티, 메서드들을 구현해야한다.

## 💭 **느낀점**
프로토콜이라는 새로운 개념을 배우면서 낯설기도 하지만 새로운 것을 배웠다는 성취감이 들었고 앞으로 클래스와 함께 자주 사용될 것 같다는 생각이 든다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판
