---
title: Swift - 튜플에 대해서 알아보자.
date: 2024-11-18 01:12:00 + 09:00
categories: [iOS, Swift]
tags: [swift, tuple]
---

Swift에서는 여러 타입의 데이터를 간단하게 하나로 묶을 수 있는 방법으로 **튜플(Tuple)**을 제공한다.
이번에는 튜플에 대해서 자세하게 알아보자.

# 튜플이란?
**여러 값을 하나의 항목으로 임시적으로 그루핑하는 매우 간단한 방법**이다.
데이터의 타입이 서로 다르더라도 튜플에 저장될 수 있다.

어떤식으로 사용할까?

## 튜플 사용법

아래와 같이 사용할 수 있다.
```swift
var example = ("Hello", 10)
```
위 코드처럼 한 변수 안에 다른 타입의 값을 넣을 수 있다.
위 방법 말고도
```swift
var example: (Int, String) = (10, "Hello")
```
이런식으로도 사용이 가능하다.

또한 생성하는 시점에서 각각의 값을 변수에 할당할 수도 있다.
```swift
var example = (exampleNum: 10, exampleStr: "Hello", exampleDou: 2.3232)
```
이런식으로 튜플을 생성하는 시점에서 변수에 할당이 가능하다.

이렇게 저장한 값을 어떤식으로 가져올 수 있을까??

## 튜플 값 추출
튜플의 저장된 값을 어떤식으로 가져올 수 있을지 알아보자.

### 튜플 인덱스
튜플로 저장된 데이터에는 인덱스가 부여되는데 첫번째 데이터에 인덱스 0번이 부여되면서 뒤로 갈수록 1, 2, 3 이런식으로 인덱스 번호가 부여된다.

사용 예시를 보자.
```swift
var example = (10, 3.141592, "Hello World")

var exampleData1 = example.0
var exampleData2 = example.1
var exampleData3 = example.2

print(exampleData1)
print(exampleData2)
print(exampleData3)
```

**실행 결과**
```swift
10
3.141592
Hello World
```

이런식으로 튜플에 부여되는 인덱스를 사용해서 값을 추출할 수 있다.

### 모든 값 추출
튜플에 저장된 모든 데이터를 한번에 가져오는 방법도 있다.
바로 예시를 들어보겠다.

```swift
var example = (10, "test", "sample", 3.14)

var (example1, example2, example3, example4) = example

print(example1)
print(example2)
print(example3)
print(example4)
```

**실행 결과**
```
10
test
sample
3.14
```

이처럼 한번에 튜플에 저장된 데이터를 가져올 수 있다.
이 방법을 사용하여 튜플에 데이터를 선택적으로 가져올 수도 있다.

### 튜플 선택적 데이터 추출
위에서 설명했던 튜플의 모든 값을 가져오는 방법을 사용하지만 밑줄(_) 을 가져오지 않을 데이터 자리에 사용하면 그 데이터는 무시된다.

코드 예시를 들어보겠다.
```swift
var example = (10, "test tuple", 3.141592)
var (example1, _, example2) = example

print(example1)
print(example2)
```

**실행 결과**
```
10
3.141592
```
이런식으로 원하는 튜플의 데이터만 가져올 수도 있다. <br>

### 튜플 생성 시점 변수 지정
튜플 사용법에서 설명했던 튜플의 생성 시점에서 변수 바로 변수에 할당했을 경우 어떻게 데이터를 사용할 수 있는지에 대해서도 설명하겠다.

```swift
var example = (exampleNum: 10, exampleStr: "Hello", exampleDou: 2.3232)

print(example.exampleNum)
print(example.exampleStr)
print(example.exampleDou)
```

**실행 결과**
```
10
Hello
2.3232
```
이런식으로 튜플의 생성 시점에서 변수에 데이터를 할당했을때 사용할 수 있다.

이처럼 튜플은 타입에 관계 없이 여러 타입을 하나의 항목으로 묶을 수 있다는 장점이 존재하지만 단점 또한 존재한다. 튜플의 장단점에 대해서 알아보자.

## 튜플의 장/단점
튜플을 사용했을때의 장점과 단점에 대해서 알아보자.

### 튜플의 장점
- 다양한 타입의 값을 하나로 묶어서 사용할 수 있다.
- 함수에서 여러 값을 반환할때 간단하게 사용할 수 있다.

### 튜플의 단점
- 튜플의 크기가 고정되어 있기 때문에 유연성이 부족하다.
- 코드의 가독성을 해칠 수 있기 때문에 복잡한 데이터 구조에는 구조체나 클래스를 권장한다.

# 정리
튜플은 데이터 타입에 관계 없이 여러 값들을 하나의 항목으로 그루핑을 하는데 사용되며 튜플의 저장된 값을 꺼낼때는 인덱스를 활용하거나 선택적 추출, 모든 값 추출을 사용해서 꺼낼 수 있다.