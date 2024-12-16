---
title: Swift - 배열과 딕셔너리에 대해서 알아보자.
date: 2024-12-05 00:05:00 + 09:00
categories: [iOS, Swift]
tags: [swift, array, dictionary]   
---

오늘은 배열과 딕셔너리에 대해서 공부하였다. 어디선가 많이 본 개념들이라 이해하는데 크게 어렵지 않았다.

어쨌든 오늘은 배열과 딕셔너리에 대해 공부한 내용을 소개하겠다.

## ❓ **배열이란?**
배열은 같은 데이터 타입을 가진 여러개의 데이터들을 넣을 수 있는 순서(인덱스)가 존재하는 데이터 타입이다.

워낙 많이 사용되고 있기때문에 사실 별로 소개할 것이 없다. 그럼에도 뭘하던지간에 기본기가 중요하다는 것을 몸으로 배웠기 때문에 제대로 알고 넘어가보자.

우선 Swift에서 사용되는 배열의 구조를 알아보자.

## 🧱 **배열의 구조**
구조
```swift
var or let 변수명: [데이터 타입] = [값1, 값2, 값3, 값4]
```
위와 같은 아주 단순한 구조를 가지고 있다.<br>
바로 사용 예시로 넘어가보자.

## 🚀 **배열의 사용**
아래 코드를 확인해보자.
```swift
var example: [String] = ["book1", "book2", "book3", "book4"]
```
위 코드처럼 아주 쉽게 배열을 구성할 수 있다.

배열을 사용할때 반드시 알아야하는 것은 인덱스이다.

인덱스는 배열 요소의 순서를 나타내는데 인덱스는 0번 부터 시작한다.

### **인덱스 사용**

예시
```swift
var example: [String] = ["book1", "book2", "book3", "book4"]

// book1: 0
// book2: 1
// book3: 2
// book4: 3

print(example[2])
```

실행 결과
```
book3
```
이런식으로 배열의 첫번째 요소부터 0, 1, 2 이런식으로 인덱스가 지정된다.

그럼 배열에 요소를 전부 출력할때는 일일이 이렇게 인덱스를 매핑해줘야하나? 그건 아니다.

반복문을 사용하면 아주 쉽게 해결할 수 있다.

### **반복문 사용**

예시
```swift
var example: [String] = ["book1", "book2", "book3", "book4"]

for item in example{
    print(item)
}
```

실행 결과
```
book1
book2
book3
book4
```

이런식으로 ``for-in`` 반복문을 이용해서 쉽게 해결이 가능하다.
``example`` 배열에 값이 하나씩 ``item`` 으로 들어가서 처리된다고 생각하면 된다.

그렇다면 배열을 사용할때 꼭 값을 초기화 해줘야만 할까?<br>
당연히 아니다. 빈 배열을 선언할 수 있다.

### **빈 배열 사용**

예시
```swift
var example = [String]()
```

위 코드처럼 선언하면 빈 배열로 선언이 된다.<br>
또한 빈 배열에 기본값을 할당할수도 있다.

### **빈 배열에 기본값 지정**
예시
```swift
var example = [String](repeating: "Hello", count: 5)
for item in example{
    print(item)
}
```

실행 결과
```
Hello
Hello
Hello
Hello
Hello
```

위 코드처럼 빈 배열에 기본값과 요소 수를 설정할 수 있다.

### **배열 요소 수**
배열 요소 수를 구하는 것은 아주 간단하다.<br>``count`` 프로퍼티를 이용해서 할 수 있다.

예시
```swift
var example = ["book1", "book2", "book3", "book4"]
print(example.count)
```

실행 결과
```
4
```

이런식으로 배열 요소의 수를 알 수 있다.

추가로 배열에 값을 추가하거나 삭제하는 방법에 대해서 알아보자.

## 📥 **배열 요소 추가**
배열에 요소를 추가하는 방법은 두가지가 있다.

### **배열 요소 연산기호 할당**

예시
```swift
var example = ["book1", "book2", "book3", "book4"]
var element = ["book5"]

example += element

for item in example{
    print(item)
}
```

실행 결과
```
book1
book2
book3
book4
book5
```

이렇게 ``+`` 연산 기호를 사용해서 값을 더 추가할 수 있다.

### **append 메서드 사용**
예시
```swift
var example = ["book1", "book2", "book3", "book4"]
example.append("book5")

for item in example{
    print(item)
}
```

실행 결과
```
book1
book2
book3
book4
book5
```

이런식으로 사용이 가능하다.

## ❌ **배열 요소 삭제**
요소를 삭제하는 ``remove`` 메서드를 사용해서 처리가 가능하다.

예시
```swift
var example = ["book1", "book2", "book3", "book4"]
example.remove(at: 2)

for item in example{
    print(item)
}
```

실행 결과
```
book1
book2
book4
```
위 코드처럼 ``remove`` 메서드를 사용해서 처리가 가능하며 ``at:`` 에는 삭제할 요소에 인덱스 값을 넣어주면 된다.

이제 딕셔너리로 넘어가보자.


## ❓ **딕셔너리란?**
쉽게 생각하면 키-값(key-value) 형태로 이루어진 컬렉션 타입이다.<br>
딕셔너리라고 해서 처음엔 의아했지만 자바에 ``Map`` 과 비슷하다.

딕셔너리에 구조에 대해서 알아보자.

## 🧱 **딕셔너리 구조**
구조
```swift
var or let 변수명: [키 값 데이터 타입:값 데이터 타입] = [키 값1: 값1, 키 값2, 값2]
```
위 코드와 같은 구조를 띄고 있다.

바로 사용 예시로 넘어가보자.

## 🚀 **딕셔너리 사용**
잘 이해가 되지 않는다면 이 부분에 예시 코드들을 잘 살펴보는게 좋다.

### **딕셔너리 선언**
예시
```swift
var example1: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"] 
var example2 = [String:String]() // 빈 딕셔너리
```

위 예시 코드처럼 딕셔너리를 선언할 수 있다,

사용 또한 매우 간단하다.

예시
```swift
var example1: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"]
var example2 = [String:String]()

print(example1["11-11"]!)
```

실행 결과
```
hungry
```

위 코드처럼 키 값을 통해서 데이터를 조회할 수 있다.

주의점은 데이터를 조회했을때 옵셔널타입으로 조회되기 때문에 강제 언래핑 또는 옵셔널 파인딩을 해야한다.

### **딕셔너리 요소 수**

딕셔너리에 요소 수를 구하는 법도 배열과 똑같이 ``count`` 프로퍼티에 접근하여 알 수 있다.

예시
```swift
var example: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"]
print(example.count)
```

실행 결과
```
3
```
이런식으로 딕셔너리 요소의 수를 알 수 있다.

딕셔너리도 배열처럼 반복문을 통해서 한번에 요소를 출력할 수 있다.

### **반복문 사용**
예시
```swift
var example: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"]

for (key, value) in example{
    print("key: \(key) value: \(value)")
}
```

실행 결과
```
key: 22-22 value: angry
key: 11-11 value: hungry
key: 33-33 value: sad
```
이런식으로 사용이 가능하다.

## 🔑 **딕셔너리 요소 추가**
아주 단순하다.

예시
```swift
var example: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"]
example["44-44"] = "enjoy"

for (key, value) in example{
    print("key: \(key) value: \(value)")
}
```
실행 결과
```
key: 11-11 value: hungry
key: 33-33 value: sad
key: 22-22 value: angry
key: 44-44 value: enjoy
```
이런식으로 키-값을 새롭게 추가할 수 있다.

## ❌ **딕셔너리 요소 삭제**
삭제에는 두가지 방법이 존재한다.

### **nil 할당**
삭제할 값에 ``nil`` 을 할당해주는 것이다.

예시
```swift
var example: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"]
example["11-11"] = nil

for (key, value) in example{
    print("key: \(key) value: \(value)")
}
```
실행 결과
```
key: 33-33 value: sad
key: 22-22 value: angry
```
이런식으로 ``nil`` 을 할당해서 요소를 제거할 수 있다.

### **removeValue 메서드 사용**
또 다른 방법으로는 ``removeValue`` 메서드를 사용하는 것이 있다.

예시
```swift
var example: [String:String] = ["11-11":"hungry", "22-22":"angry", "33-33":"sad"]
example.removeValue(forKey: "22-22")

for (key, value) in example{
    print("key: \(key) value: \(value)")
}
```

실행 결과
```
key: 33-33 value: sad
key: 11-11 value: hungry
```
이런식으로 ``removeValue`` 를 사용해서 값을 제거할 수 있다.<br>
``forkey``에는 삭제할 값에 키값을 넣으면 된다.

## 🗂️ **정리**
배열은 같은 타입에 여러 데이터를 순서(인덱스)를 가지게 하면서 저장하는 방식이고 딕셔너리는 키-값(key-value) 형식으로 저장하는 방식이다.

## 💭 **느낀점**
배열이나 딕셔너리는 Java를 사용하면서 배열과 ``Map``을 자주 다뤄봤기때문에 이해하는데 어려움없이 금방 배울 수 있었다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판