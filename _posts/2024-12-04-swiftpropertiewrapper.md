---
title: Swift - 프로퍼티 래퍼에 대해서 알아보자.
date: 2024-12-04 00:56:00 
categories: [iOS, Swift]
tags: [swift, wrapper]   
---

오늘은 프로퍼티 래퍼에 대해서 공부하였다.<br>처음 보는 개념이라 이해하는데 고생 좀 했다..후..

아무튼 오늘은 프로퍼티 래퍼에 대해 공부한 내용을 소개하겠다.

## ❓ **프로퍼티 래퍼란?**
구조체에 선언한 연산 프로퍼티에 기능을 다른 구조체에서 사용해야할때 일일이 복붙을 하기엔 좀 번거롭다.

그때 프로퍼티 래퍼를 사용해서 기능을 뺄 수 있다.

설명보단 사용 예시를 보면서 이해하는게 훨씬 빠르다.<br>
바로 사용 예시로 넘어가자.

## 🚀 **프로퍼티 래퍼 사용**
프로퍼티 래퍼를 사용하는 예시들을 소개해보겠다.

### **프로퍼티 래퍼 사용 예시**
예시
```swift
@propertyWrapper
struct ExampleWrapper {
    var value: Int
    var addValue: Int
    
    init(wrappedValue: Int, addValue: Int) {
        self.value = wrappedValue
        self.addValue = addValue
    }
    
    var wrappedValue: Int {
        get { value }
        set { value = addValue + newValue }
    }
}

struct ExampleStruct {
    @ExampleWrapper(addValue: 10) var number: Int = 5
}

var ex = ExampleStruct()
print(ex.number)

ex.number = 20
print(ex.number)
```

실행 결과
```
5
30
```

위 코드를 확인해보자. 아주 머리아프게 생겼다. 실제로도 이해하는데 1시간 넘게 걸렸다. 

가장 먼저 확인해야할 것은 ``@propertyWrapper`` 를 사용해서 프로퍼티 래퍼를 선언할 수 있다는 것이다.

이때 프로퍼티 래퍼에는 ``wrappedValue`` 라는 속성이 반드시 존재해야만 한다. 

``wrappedValue``를 반드시 포함해야하는 이유로는 ``wrappedValue``는 프로퍼티 래퍼가 감싸고 있는 실제 값을 의미하기 때문이다.

``wrappedValue``를 통해 값을 제어하거나 변환이 가능하다.

코드 동작을 하나씩 살펴보자.

```swift
@propertyWrapper
struct ExampleWrapper {
    var value: Int
    var addValue: Int
    
    init(wrappedValue: Int, addValue: Int) {
        self.value = wrappedValue
        self.addValue = addValue
    }
    
    var wrappedValue: Int {
        get { value }
        set { value = addValue + newValue }
    }
}
```
위 코드가 프로퍼티 래퍼를 정의한 부분인데 오늘 살펴보는 내용에 가장 핵심인 부분이다.

``@propertyWrapper``를 사용해서 선언하고 있으며 ``init``메서드를 사용해서 값을 초기화하고 있다.

``wrappedValue``를 사용해서 ``value``에 값을 조회 및 설정하고 있다.

```swift
struct ExampleStruct {
    @ExampleWrapper(addValue: 10) var number: Int = 5
}
```
위 코드는 프로퍼티 래퍼를 설정하는데 ``@ExampleWrapper``를 사용해서 프로퍼티 래퍼를 설정하고 있으며 바로 옆에 ``addValue`` 값을 넘기고 있다. 

또한 ``number`` 변수의 기본값을 5로 설정하고 있으며 이때 ``number`` 는 프로퍼티 래퍼에 ``wrappedValue`` 가 된다.

```swift
var ex = ExampleStruct()
print(ex.number) // 5

ex.number = 20
print(ex.number) // 30
```
위 코드처럼 처음 ``ExampleStruct`` 를 초기화 했을땐 ``setter``가 작동하지 않기 때문에 기본값인 5가 출력된다.

``number``를 설정했을때는 ``wrappedValue``에 ``setter``가 동작하면서 값을 더한다.

이렇게 하나씩 뜯어가면서 살펴보니 어렵지 않다. 

또한 여러 타입을 이용하고 싶을때는 프로토콜을 사용할 수 있다.

### **프로퍼티 래퍼 프로토콜 사용 예시**
예시
```swift
@propertyWrapper
struct ExampleWrapper<T: AdditiveArithmetic> {
    private var value: T
    private var addValue: T
    
    init(wrappedValue: T, addValue: T) {
        self.value = wrappedValue
        self.addValue = addValue
    }
    
    var wrappedValue: T {
        get { value }
        set { value = addValue + newValue }
    }
}

struct ExampleStruct {
    @ExampleWrapper(addValue: 10) var number: Int = 5
}

var ex = ExampleStruct()
ex.number = 20
print(ex.number)
```
실행 결과
```
30
```

위 코드와 같이 프로토콜을 이용해서 프토로콜을 따르는 타입을 사용하는 것도 가능하다.

> AdditiveArithmetic 프로토콜이란?<br>+ 연산자와 - 연산자를 지원하는 타입들에 적용할 수 있는 프로토콜이다.

## 🗂️ **정리**
프로퍼티 래퍼란 구조체들이 공통적으로 사용하는 연산 프로퍼티를 빼내서 효율적으로 사용할 수 있게 해준다.

프로퍼티 래퍼는 ``@propertyWrapper``를 사용해서 선언이 가능하며 이때 반드시 ``wrappedValue``를 포함해야한다.

## 💭 **느낀점**
처음 배우는 프로퍼티 래퍼라는 개념을 배우면서 이해가 너무 안되어서 시간을 많이 투자하였고 겨우 이해하는데 성공하였다. 활용하는데 있어서 자주 연습하고 사용해봐야할 것 같다..

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판