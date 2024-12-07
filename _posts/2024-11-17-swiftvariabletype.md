---
title: Swift - 변수의 타입에 대해서 알아보자.
date: 2024-11-17 07:15:00 +09:00
categories: [iOS, Swift]
tags: [swift, variable, type]
---

Swift에서 변수를 사용하는데 있어서 변수의 타입은 굉장히 중요한 요소이다.
변수의 타입에 대해서 자세하게 알아보자.

## 🧩 **변수의 타입이란?**
이해하기 쉽게 예를 들어서 설명하겠다.

분리수거를 한번 생각해보자.
![Example Image](https://github.com/PetOfLSE/PetOfLSE.github.io/blob/main/assets/img/frontimage/2024-11-15-typeexample.png?raw=true)

종이, 플라스틱, 캔, 유리 등 종류에 맞게 분류가 되어있고 종이에는 종이 쓰레기가 플라스틱에는 플라스틱 쓰레기가 들어가도록 용도가 정해져 있다.

이처럼 Swift의 변수에도 각각에 용도(타입)가 있다.
이제부터 그 종류에 대해서 알아보도록 하자.

## 📊 **타입의 종류**
swift의 **모든 데이터 타입의 첫 글자는 대문자로 시작**한다.

### **String - 문자열 타입**
흔히 사용하는 **문자열을 할당 할 수 있다.**

**String 변수 예시**
```swift
var fruit: String = "Banana"
```

### **Int(Integer) - 정수형**
8, 16, 23, 64 비트 형태의 **부호가 있는 정수와 없는 정수 지원**한다.
이러니 저러니 해도 그냥 **Int 사용을 권장한다.**

**Int 변수 예시**
```swift
var number: Int = 10
```

**부호가 없는 정수형 변수 예시**
```swift
var age: UInt = 32
```

**부호가 없는 정수형 변수에 음수값을 할당하면 어떻게 될까?**

**부호가 없는 정수형 변수에 음수를 할당할 경우**
```swift
var testNumber: UInt = -10 // Negative integer '-10' overflows when stored into unsigned type 'UInt'
```
이처럼 Negative integer '-10' overflows when stored into unsigned type 'UInt' 라는 오류가 발생하게 된다.

>Int에 특정 크기를 지정하고 싶다면 Int8, Int16, Int32, Int64 처럼 사용할 수 있다.
Uint도 마찬가지로 크기를 지정하고 싶다면 UInt8, UInt16, UInt32, UInt64로 사용할 수 있다.

### **Float - 실수형**

**부동 소수점 방식을 사용**한다.
Int 보다 더 크거나 작은 값을 저장할 수 있다.
**32 비트 부동 소수점 표기, 6자리의 소수 정확도를 가진다.**

**Float 변수 예시**
```swift
var height: Float = 183.8
```

### **Double - 실수형**

**부동 소수점 방식을 사용**한다.
Int 보다 더 크거나 작은 값을 저장할 수 있다.
**64 비트 부동 소수점 표기, 15자리의 소수 정확도**를 가지기 때문에 **Float보다 더 정확도가 높다.**

**Double 변수 예시**
```swift
var pi: Double = 3.1415926535
```

### **Bool - 참거짓**

true or false 와 같은 **참 거짓을 나타내는 타입**이다.
if와 같은 **조건문을 동작시킬때 유용**하다.

**Bool형 변수 예시**
```swift
var isAdmin: Bool = true
```

이렇게 기본적인 타입에 대해서 알아보았다. 이 밖에도 튜플, 컬렉션, 옵셔널 등 여러가지 타입이 존재하지만 나머지 타입은 다른 포스팅에서 다룰 예정이다.

그렇다면 궁금증이 한가지 생긴다.
만약 타입을 지정하지 않고 데이터만 넣는 경우는 어떻게 될까?

## ❓ **타입을 지정하지 않고 데이터만 넣는 경우**
다음과 같이 변수를 정의하고 데이터를 할당하였다.
오류가 날까?

```swift
var str = "Hello World!"
```

아무 문제도 생기지 않는다.
그 이유는 변수 & 상수 선언시 타입을 적지 않으면 Swift에서 타입을 추론하여 처리하기 때문이다. 이것을 **타입 추론** 이라고 한다.

예시를 몇가지 더 들어보겠다.

```swift
var num = 10 // 정수형이 들어갔으니 Int 형으로 추론된다.
```
**정수형을 할당할 경우** Swift가 **Int로 타입을 추론**한다.
그렇다면 실수형은 어떨까?

```swift
let pi = 3.141592 // 실수형이 들어왔기 때문에 Double로 추론된다.
```
Float도 있는데 왜 Double로 추론이 될까?
Swift에서는 **타입 추론을 할때 항상 Float 보다 Double을 선택하기 때문이다.**

그럼 변수를 선언한 후 값을 넣는건 어떨까?
```swift
var example // Type annotation missing in pattern
example = 20
```
이처럼 Type annotation missing in pattern이란 오류가 난다.
**데이터를 바로 할당할 것이 아니라면 데이터 타입을 꼭 명시**해줘야만 한다.

이렇듯 변수의 타입을 공부하다 보면 드는 의문이 있다.

변수의 타입을 굳이 이렇게까지 공부해야할까? 그렇게 중요한가?
Swift에서 타입은 아주 중요하다 아래에서 자세하게 설명하겠다.

## 💡 **타입이 중요한 이유**
Swfit에서 타입이 중요한 이유는 Swift는 **타입 안전성을 굉장히 중요하게 여기기 때문이다.**

예시를 들어보겠다.

```swift
var age: Int = 20
```

위처럼 age라는 변수를 Int 형 변수로 선언하고 20을 할당하였다.
여기서 age에 문자열을 넣으면 어떻게 될까?

```swift
age = "20" //error: siwft-basics-1.playground:46:7: error: cannot assign value of type 'String' to type 'Int'
```

이처럼 타입 불일치 오류가 발생한다.

## 🗂️ **정리**
Swift는 타입 안전성을 굉장히 중요하게 여기기 때문에 데이터 타입은 굉장히 중요한 부분이다. Int, String, Bool, Double 등 데이터 타입에 대해서는 꼭 알고 넘어가는게 좋다.