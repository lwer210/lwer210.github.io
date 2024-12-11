---
title: Swift - 클래스 상속에 대해 알아보자.
date: 2024-12-01 00:10:00 
categories: [iOS, Swift]
tags: [swift, class]
---

오늘은 클래스에 상속에 대해서 공부하였다. 

생각보다 어렵진 않았지만 이번에도 새로운 개념이 나와서 확실히 이해하고 넘어가고자하여 공부하는데 시간이 조금 걸렸다.

어쨌든 클래스의 상속에 대해서 알아보자.

## ❓ **클래스란의 상속이란?**
간단히 설명해서 부모 클래스가 가진 기능을 자식 클래스가 그대로 받는 것을 말한다. 

객체지향 프로그래밍 언어를 공부해본적이 없다면 설명만 들었을 경우 헷갈릴 수도 있다.

우선 상속을 어떤식으로 받는지 그 방법부터 알아보자.

## 🌳 **상속의 구조**
```swift
class 자식 클래스: 부모 클래스{

}
```
이런식의 형태로 받을 수 있다.<br>
구조를 살펴봤으니 이제 어떤식으로 사용하는지에 대해서 알아보자.

## 🔗 **상속 사용**
아래의 코드를 살펴보자.
```swift
class ExampleParent{
  var exNum: Int
  var exFlo: Float

  init(num: Int, flo: Float){
    self.exNum = num
    self.exFlo = flo
  }

  func exPrint(){
    print("exNum: \(exNum), exFlo: \(exFlo)")
  }
}
```
위와 같은 클래스가 있다고 가정해보자.<br>
위 클래스를 상속받는 코드는 아래와 같다.
```swift
class ExampleChild: ExampleParent{
  
}
```
이런식으로 상속을 받을 수 있다.

이런식으로 상속을 받았을때 ``ExampleParent``가 부모 클래스, ``ExampleChild``가 자식 클래스가 된다.

코드를 보면서 생각해보면 그다지 이해하기 어렵지 않다.

``ExampleParent`` 를 상속받은 ``ExampleChild`` 클래스는 ``ExampleParent`` 의 기능을 그대로 사용할 수 있으며 기능을 더 추가할 수도 있다.

예시
```swift
class ExampleChild: ExampleParent{
    var exampleDou: Double = 0.0

    func exReturnDouble() -> Double{
    return exampleDou
  }
}
```
위 코드처럼 하위 클래스를 더 확장할 수 있다.

이렇게 선언된 상속 클래스를 사용하는 것은 아래 코드와 같다.

예시
```swift
class ExampleParent{
  var exNum: Int
  var exFlo: Float

  init(num: Int, flo: Float){
    self.exNum = num
    self.exFlo = flo
  }

  func exPrint(){
    print("exNum: \(exNum), exFlo: \(exFlo)")
  }
}

class ExampleChild: ExampleParent{
    var exampleDou: Double = 0.0

    func exReturnDouble() -> Double{
    return exampleDou
  }
}

var example: ExampleChild = ExampleChild(num: 10, flo: 10.0)
example.exPrint()
print(example.exReturnDouble())
```
실행 결과
```
exNum: 10, exFlo: 10.0
0.0
```

위와 같이 사용이 가능하다. 

여기서 문득 의문이든다. 
```swift
var example: ExampleChild = ExampleChild(num: 10, flo: 10.0)
```
초기화를 부모 클래스가 가진 프로퍼티만 진행하고 있다. 그럼 하위 클래스가 가진 프로퍼티도 초기화하려면 어떻게 해야할까?

아래에서 자세히 알아보자.

## ⚙️ **하위 클래스 초기화**
하위 클래스에 ``init`` 메서드를 사용하여 하위 클래스에 프로퍼티를 초기화 한 후 상위 클래스에 ``super`` 를 사용해서 상위 클래스로 값을 보내는 것이다.

이것 또한 설명보단 코드로 보는것이 이해하기가 빠르다.

예시
```swift
class ExampleParent{
  var exNum: Int
  var exFlo: Float

  init(num: Int, flo: Float){
    self.exNum = num
    self.exFlo = flo
  }

  func exPrint(){
    print("exNum: \(exNum), exFlo: \(exFlo)")
  }
}

class ExampleChild: ExampleParent{
    var exampleDou: Double = 0.0
    
    init(exampleDou: Double, num: Int, flo: Float) {
        self.exampleDou = exampleDou
        super.init(num: num, flo: flo)
    }

    func exReturnDouble() -> Double{
    return exampleDou
  }
}

var example: ExampleChild = ExampleChild(exampleDou: 10.0, num: 10, flo: 10.0)
example.exPrint()
print(example.exReturnDouble())
```

실행 결과
```
exNum: 10, exFlo: 10.0
10.0
```

이렇게 ``init`` 메서드를 사용해서 하위 클래스에 프로퍼티를 초기화 시킨 후 상위 클래스로 프로퍼티 값을 보내주면 해결이 가능하다.

이제 상위 클래스에 기능을 확장하는 방법에 대해서 알아보자.

## 🚀 **클래스 기능 확장**
우선 가장 간단한 방법은 오버라이딩을 하는 방법이 있다.<br>
아래에서 자세하게 알아보자.

### **오버라이딩**
오버라이딩은 상위 클래스에서 정의된 메서드를 하위 클래스에서 재정의를 하여 기능을 확장하는 것을 말하는데 이때 지켜야만 하는 규칙들이 있다.

**오버라이딩 규칙**
1. 부모 클래스에서 선언되있는 메서드의 매개변수 개수와 타입이 일치해야만 한다.
2. 부모 클래스에서 선언되어있는 메서드의 반환타입과 같아야만 한다.

오버라이딩은 ``override`` 키워드를 사용해서 할 수 있는데 바로 예시를 확인해보자.

```swift
class ExampleChild: ExampleParent{
    var exampleDou: Double = 0.0
    
    init(exampleDou: Double, num: Int, flo: Float) {
        self.exampleDou = exampleDou
        super.init(num: num, flo: flo)
    }

    func exReturnDouble() -> Double{
        return exampleDou
    }
    
    override func exPrint() {
        print("exNum: \(exNum), exFlo: \(exFlo), exampleDou: \(exampleDou)")
    }
}
```
이런식으로 ``override`` 키워드를 사용하여 오버라이딩을 할 수 있다.

이제 전체 코드와 실행 결과를 확인해보자.

예시
```swift
class ExampleParent{
  var exNum: Int
  var exFlo: Float

  init(num: Int, flo: Float){
    self.exNum = num
    self.exFlo = flo
  }

  func exPrint(){
    print("exNum: \(exNum), exFlo: \(exFlo)")
  }
}

class ExampleChild: ExampleParent{
    var exampleDou: Double = 0.0
    
    init(exampleDou: Double, num: Int, flo: Float) {
        self.exampleDou = exampleDou
        super.init(num: num, flo: flo)
    }

    func exReturnDouble() -> Double{
        return exampleDou
    }
    
    override func exPrint() {
        print("exNum: \(exNum), exFlo: \(exFlo), exampleDou: \(exampleDou)")
    }
}

var example: ExampleChild = ExampleChild(exampleDou: 10.0, num: 10, flo: 10.0)
example.exPrint()
print(example.exReturnDouble())
```

실행 결과
```
exNum: 10, exFlo: 10.0, exampleDou: 10.0
10.0
```

오버라이딩 말고 한가지 방법이 더 존재하는데 바로 익스텐션을 사용하는 방법이다.

아래에서 더 자세하게 알아보자.

### **익스텐션**
익스 텐션은 하위 클래스를 생성하거나 참조할 필요가 없으며 메서드, 연산 프로퍼티 등을 추가하기 위해 사용된다.

스위프트 언어에 내장된 클래스에도 기능을 새로 추가할 수 있다.

구조에 대해서 먼저 알아보자.

**구조**
```swift
extension 클래스명{
  // 추가할 기능 
}
```
생각보다 단순하다. 구조를 알아봤으니 바로 사용 예시에 대해서 알아보자.

예시
```swift
extension Int{
  var add: Int {
      return self + self
  }
}
```

이런식으로 스위프트 내부에 클래스에도 연산 프로퍼티를 추가가 가능하다.

사용 예시
```swift
extension Int{
    var add: Int{
        return self + self
    }
}

var example: Int = 10
print(example.add)
```

실행 결과
```
20
```

이런식으로 사용이 가능하다.

## 🗂️ **정리**
클래스의 상속은 상위 클래스에 있는 메서드와 프로퍼티들을 그대로 받을 수 있게 한다. 

또한 상속을 받은 하위 클래스에서 추가적으로 기능 확장이 가능하며 기능을 확장하는 방법은 오버라이딩과 익스텐션이 있다.

## 💭 **느낀점**
클래스의 상속은 사실 어려운 부분이 없어서 금방 이해하였지만 익스텐션이라는 새로운 것을 배우면서 확실히 이해하고자 시간을 좀 더 많이 투자하였다. 확실히 객체지향 언어는 너무 편리하고 좋은 것 같다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판
