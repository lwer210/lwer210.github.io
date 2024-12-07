---
title: Swift - 클래스 대해 알아보자.
date: 2024-11-29 00:26:00 + 09:00
categories: [iOS, Swift]
tags: [swift, class]
---

함수와 클로저를 지나 오늘은 클래스에 대해서 공부를했다.<br>
객체지향 프로그래밍 언어에서 굉장히 중요한 클래스라는 개념에 대해서 알아보자.

## ❓ **클래스란?**
애플리케이션을 구성하는 **기본적인 단위**로 생각하면 이해하기 쉬우며 각각에 **독립적인 기능 모듈**을 뜻한다.

클래스는 **프로퍼티(속성)과 메서드**로 구성된다. 이때 프로퍼티와 메서드를 포괄적으로 **클래스 맴버**라고 한다.

이제 클래스에 구조에 대해서 한번 알아보자.

## 📦 **클래스의 구조**
구조
```swift
class 클래스 이름{
  // 프로퍼티
  // 인스턴스 메서드 또는 타입 메서드
}
```
위 코드와 같은 구조를 가지고 있다.

프로퍼티에는 변수나 상수가 선언되며 인스턴스메서드 또는 타입 메서드에는 클래스에서 호출되는 메서드들이 정의된다.

인스턴스 메서드, 타입 메서드 무슨 말일까??<br>
이 얘기는 조금 더 뒤에서 자세하게 알아보자.

우선 클래스에 네이밍 규칙에 대해서 부터 알아보자.

사실 이 부분은 별거 없다.<br>
클래스를 만들때 단어의 첫 글자를 대문자로 만들어주기만 하면 된다.

예시
```swift
class ExampleClass{

}
```

이런식으로 이름을 짓어주면 된다.

이제 타입 메서드와 인스턴스 메서드에 대해서 알아보자.

## ⚙️ **인스턴스 메서드와 타입 메서드**
우선 타입 메서드부터 알아보자.

### **타입 메서드**
타입 메서드란 **클래스 레벨에서 동작하는 메서드**를 말한다.<br>

Java를 공부한 사람이라면 사실 이름만 다를뿐 그냥 static 정적 메서드를 생각하면 쉽다.

타입 메서드는 표준 함수 선언문과 구문은 같지만 ``func`` 키워드 앞에 ``class`` 만 붙히면 된다.

예시를 확인해보자.

예시
```swift
class ExampleClass{

  class func exampleFunc() -> Int{
    return 100
  }
}

print(ExampleClass.exampleFunc())
```
실행 결과
```
100
```
이런식으로 클래스 레벨에서 바로 사용이 가능한 메서드를 타입 메서드라고 한다.

이제 인스턴스 메서드에 대해서 알아보자.

### **인스턴스 메서드**
인스턴스 메서드란 **클래스의 인스턴스에 대한 작업만을 진행**한다.

쉽게 생각해서 클래스 내부에 평소에 사용하던 함수를 사용한다고 생각하면 쉽다.<br>
바로 예시를 확인해보자.

예시
```swift
class Example{
  var num1 = 10
  var num2 = 20

  func add() -> Int{
    return self.num1 + self.num2
  }
}

var exampleInstance: Example = Example()
print(exampleInstance.add())
```
실행 결과
```
30
```
이렇게 사용되는게 인스턴스 메서드이다.

사실 객체지향 프로그래밍 언어를 공부해본적 있다면 이름만 조금 다를뿐이지 이해하기 어렵지 않다.

이제 클래스 인스턴스를 초기화 하는 방법에 대해서 알아보자.

## 🚀 **클래스 인스턴스 초기화**
인스턴스를 생성하는 시점에 초기화 작업을 해야할 경우 사용한다.

``init`` 메서드를 통해서 초기화를 할 수 있다.<br>
바로 예시를 보자.

예시
```swift
class Example{
  var num1: Int
  var num2: Int

  init(num1: Int, num2: Int){
    self.num1 = num1
    self.num2 = num2
  }
}

var exampleInstance: Example = Example(num1: 30, num2: 10)
print(exampleInstance.num1)
print(exampleInstance.num2)
```
실행 결과
```
30
10
```
이런식으로 클래스 인스턴스를 생성하는 시점에서 값을 초기화할 수 있다.<br>

이제 이전 예시에서도 사용한 ``self`` 에 대해서 알아보자.

## 🪞 **self 키워드**
``self`` 키워드는 **클래스에 속한 메서드나 프로퍼티를 가르킬때 사용**한다.<br>
자바에 ``this`` 와 굉장히 유사하다.

사실 Swift 내부에서 알아서 처리해주기 때문에 ``self`` 를 사용할 일이 거의 없다.

``self`` 를 사용하는 경우는 함수의 매개변수 이름이 클래스 프로퍼티의 이름과 같을때 사용하는데 이전에 사용했던 예시를 다시 확인해보자.

예시
```swift
class Example{
  var num1: Int
  var num2: Int

  init(num1: Int, num2: Int){
    self.num1 = num1
    self.num2 = num2
  }
}

var exampleInstance: Example = Example(num1: 30, num2: 10)
print(exampleInstance.num1)
print(exampleInstance.num2)
```
위 코드처럼 함수의 매개변수 이름과 프로퍼티 이름이 같을 경우에 사용한다. 

클래스 인스턴스의 프로퍼티나 메서드에 접근하는 것을 여태까지 예시에서 이미 많이 사용하였지만 사용법을 확실히 하기 위해서 설명하겠다.

## 🔍 **클래스 인스턴스 값 접근**
아주아주아주 간단하다. 클래스 인스턴스에 **마침표(.)**만 찍어주면 된다.<br>
예시를 통해서 확인해보자.

예시
```swift
class ExampleClass{
  var example1: Int
  var example2: Int
    
    init(example1: Int, example2: Int) {
        self.example1 = example1
        self.example2 = example2
    }

  func add(num1: Int, num2: Int) -> Int{
    return num1 + num2
  }
}

var exampleInstance: ExampleClass = ExampleClass(example1: 20,example2: 30)
print(exampleInstance.example1)
print(exampleInstance.add(num1: 10, num2: 30))
```
실행 결과
```
20
40
```
이런식으로 사용하면 된다.

이제 프로퍼티에 대해 좀 더 깊게 알아보도록 하자.

## 💾 **저장 프로퍼티와 연산 프로퍼티**
클래스의 프로퍼티는 **저장 프로퍼티와 연산 프로퍼티**로 나뉜다.

우선 저장 프로퍼티부터 알아보자.
### **저장 프로퍼티**
저장 프로퍼티는 단순히 여태까지 우리가 클래스에서 사용하던 변수나 상수이다.<br>
바로 예시를 확인해보자.

예시
```swift
class Example{
  var example1: Int
  var example2: Int

  init(_ num1: Int, _ num2: Int){
    example1 = num1
    example2 = num2
  }
}

var instance: Example = Example(20, 50)
print(instance.example1)
print(instance.example2)
```
실행 결과
```
20
50
```
위 코드처럼 평소에 사용하던 프로퍼티가 저장 프로퍼티이다.<br>
이제 연산 프로퍼티에 대해서 알아보자.

### **연산 프로퍼티**
연산 프로퍼티는 **값을 설정하거나 가져오는 시점에서 어떤 연산이나 로직에 따라 처리되는 것**을 말한다.

연산 프로퍼티는 게터(getter)를 생성하며 선택적으로 세터(setter)를 생성한다.

설명만 봐선 좀 어렵게 느껴진다.<br>
바로 예시를 확인해보자.

예시
```swift
class Example{
  var example1: Int
  var example2: Int
  
  var examplePlus: Int {
    get {
      return example1 + example2
    }
  }

  init(_ num1: Int, _ num2: Int){
    example1 = num1
    example2 = num2
  }
}

var exampleIns = Example(2, 5)
print(exampleIns.examplePlus)
```
실행 결과
```
7
```
이런식으로 사용하는 것을 연산 프로퍼티라고 한다.

이제 프로퍼티를 초기화 하는 방법을 좀 더 자세히 알아보자.

## 🌟 **프로퍼티 초기화**
프로퍼티 초기화에는 다양한 방법이 있지만 가장 기본적인 것은 값을 직접 할당하는 것이다.

예시
```swift
class Example{
  var num1 = 0
  var num2 = 0
}
```

그 다음 방법으로는 ``init`` 을 사용해서 초기화하여 사용하는 것인다.

```swift
class Example{
  var num1: Int
  var num2: Int

  init(_ num1: Int, _ num2: Int){
    self.num1 = num1
    self.num2 = num2
  }
}
```
그리고 프로퍼티에 최초로 접근했을때 초기화 되도록할 수도 있다.

예시
```swift
class Example{
  var example = 10
  lazy var lazyExample: Int = {
    return example * 10
  }()
}

var exampleIns = Example()
print(exampleIns.lazyExample)
```
실행 결과
```
100
```
위 코드는 ``lazy`` 키워드를 이용해서 프로퍼티에 접근하기 전까진 초기화하지 않고 있다가 접근했을때 초기화를 진행하도록 할 수도 있다.

## 🗂️ **정리**
클래스란 애플리케이션을 구성하는 가장 기본적인 단위라고 생각하면 이해하기 편하며 각각 독립적인 모듈이다.

클래스는 프로퍼티와 메서드로 구성되며 프로퍼티에는 저장 프로퍼티, 연산 프로퍼티가 있으며 메서드에는 인스턴스 메서드, 타입 메서드가 있다.

## 💭 **느낀점**
클래스에 대한 개념을 공부하는건 어렵지 않았지만 익숙하지 않은 문법들이 많아 나타났기 때문에 복습을 처저하게 해야할 것 같다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판