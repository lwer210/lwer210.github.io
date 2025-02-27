---
title: Swift - 문자열에 대해서 알아보자.
date: 2024-11-17 10:15:00 
categories: [iOS, Swift]
tags: [swift, type, string]
---

Swift에서 문자열이 어떤식으로 이루어져 있고 어떤식으로 사용할 수 있는지에 대해서 자세하게 알아보자. <br>

전 포스팅에서 아주아주 기초적인 부분만 다뤘었다.. <br>
[Swift - 변수의 타입에 대해 알아보자.](https://petoflse.github.io/posts/swiftvariabletype/)

## 📝 **문자열이란?**
문자열이란 문자들의 집합으로 **그래핌 클러스터의 형태**로 저장된다.
여기서 그래핌 클러스터가 무엇일까?

>그래핌 클러스터는 눈에 보이는 하나의 문자를 표현하기 위해 둘 이상의 유니코드 스칼라가 결합되어 구성되는 것을 말한다.

여기서 유니코드 스칼라는 유니코드에서 각 문자를 고유하게 식별하기 위해 부여한 숫자라고 생각하면 이해하기 쉽다.

Swift에서 다음과 같이 유니코드 스칼라를 사용할 수 있다.
```swift
var testChar = "\u{0041}"
print(testChar) // A
```
이제 그래핌 클러스터에 대한 예를 알아보자.
그래핌 클러스터에 대한 예는 다음과 같다.
```swift
var testChar2 = "\u{65}\u{301}"  
print(testChar2)  // é
```
이처럼 그래핌 클러스터는 두 개 이상의 유니코드 스칼라가 결합되어 구성된다.

그렇다면 문자열을 동적으로 변경해야할때는 어떻게 해야할까?
이럴때 사용하는게 **문자열 보간** 이다.

## ⚙️ **문자열 보간**
문자열 보간이란 **문자열 안에 변수, 상수, 표현식, 함수 호출을 삽입하여 동적으로 문자열을 생성**하는 것을 말한다.

### **문자열 보간 사용법**
문자열 보간을 어떤식으로 사용해야할까??
다음과 같이 사용할 수 있다.

**변수 사용**
```swift
var name: String = "홍길동"
print("\(name)님 환영합니다.")
```
이처럼 변수에 값을 할당한 후 문자열 보간을 사용해서 문자열을 동적으로 사용할 수 있다. 다음으로는 표현식을 사용한 방법을 알아보자.

**표현식 사용**
```swift
var a: Int = 10
var b: Int = 20
print("\(a)와 \(b)의 합은 \(a + b)") // 10와 20의 합은 30
```
이처럼 표현식을 사용해서도 문자열 보간을 사용할 수 있다.
함수 호출로는 어떤식으로 사용할 수 있을까?

**함수 호출**
```swift
func add(a: Int, b: Int) -> Int{
	return a + b
}

print("\(add(a: 10, b: 20))") // 30
```
이처럼 함수 호출을 문자열 보간에 사용할 수 있다.

그렇다면 ", \ 이런 문자들은 어떻게 사용할 수 있을까?
아래에서 알아보자.

## 🔒 **특수 문자/이스케이프 시퀀스**
우선 이스케이프 시퀀스에 대해서 알아보자.
>이스케이프 시퀀스란? 개행, 탭 또는 문자열 내에 특정 유니코드 값을 지정하는 것을 말한다.

이러한 특수 문자들은 **역슬래시(\\)를 앞에 써서 구별하게 되는데 이것을 이스케이핑** 이라고 한다.

예시를 한번 보자.
아래는 개행 문자를 할당한 것이다.
```swift
var testNextLine = "\n"
```

기본적으로 역슬래시(\\)가 붙은 문자는 특수 문자로 간주된다.
그렇다면 일반적인 역슬래시(\\) 또는 쌍따옴표(")는 어떻게 사용해야 할까??
아래에서 같이 확인해보자.

```swift
var testSlash = "\\" // \
```

이렇게 역슬래시(\\)를 두개 붙혀서 사용하면 하나에 역슬래시(\\)로 인식된다.

### **Swift에서 자주 사용되는 특수 문자는 뭐가 있을까?**

**\n - 개행 문자**<br>
문자열을 개행 처리한다.
위에서 한번 설명했지만 또 한번 예를 들어보겠다.
```swift
var exampleText = "Hello\nWorld"
print(exampleText)
```

**실행 결과**
```
Hello
World
```
이렇게 다음 문자열로 개행 처리된다.

**\t - 탭**<br>
Tab 키를 누르면 띄어쓰기 4칸이 적용되는데 이것을 \t를 이용해서 문자열을 깔끔하게 사용할 수 있다.
```swift
var exampleText = "Hello\tWorld"
print(exampleText)
```

**실행 결과**
```
Hello	World
```
위처럼 Tab 키를 눌렀을때 기능이 사용되었다.

**\" - 쌍따옴표**<br>
문자열 안에서 쌍따옴표가 필요할때 아래처럼 사용하면 된다.
```swift
var exampleText = "Hi, my name is \"lee\""
print(exampleText)
```

**실행 결과**
```
Hi, my name is "lee"
```
이렇게 문자열 안에 \" 를 사용해서 쌍따옴표를 사용할 수 있다.

**\' - 홀따옴표**<br>
문자열 안에서 홀따옴표가 필요할때 아래처럼 사용하면 된다.
```swift
var exampleText = "I\'m hungry"
print(exampleText)
```

**실행 결과**
```
I'm hungry
```
이렇게 문자열 안에 \' 를 사용해서 홀따옴표를 사용할 수 있다.

## 🗂️ **정리**
Swift에서 문자열은 **그래핌 클러스터 형태**로 저장되며 **그래핌 클러스터는 두 개 이상의 유니코드 스칼라가 결합된 형태**로 구성된다.

**동적으로 문자열을 사용할때는 문자열 보간**을 사용해서 동적으로 문자열을 구성할 수 있다.


개행 , 탭 과 같은 **이스케이프 시퀀스, 특수 문자를 사용할때는 역슬래시(\\)를 사용해서 이스케이프 처리**를 해야한다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판
