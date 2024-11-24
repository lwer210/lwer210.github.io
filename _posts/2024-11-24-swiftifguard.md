---
title: Swift - if, guard 에 대해서 알아보자.
date: 2024-11-24 06:29:00 + 09:00
categories: [iOS, Swift]
tags: [swift, if, guard]
---

조건 제어 흐름을 공부하면서 원래는 if와 switch를 같이 다루려고 했지만 guard 라는 처음 보는 구문을 배우게 되었다..

공부하다 보니 if 문과 비슷하면서도 다른 부분이 보였고 if와 guard를 같이 다루면 좋을 것 같다고 생각해서 다루게 되었다.

if문과 guard문에 대해서 알아보자.

## ❓ **if문**
if문은 조건식을 기준으로 **조건식이 true라면 if문 안에 있는 코드를 실행하고 false라면 실행하지 않는다**.

다른 프로그래밍 언어와 거의 똑같기 때문에 다른 프로그래밍 언어를 학습해본 경험이 있다면 if, else, if else, 는 딱히 배울게 없을 것이다.

어쨋든 if문에 구조부터 알아보자.

### **if문의 구조**
```swift
if 조건식{
  // 조건식이 true 일때 실행할 코드
}
```
한가지 다른 언어와 다른점은 if의 조건식이 true 일때 실행할 코드가 한줄이라면 괄호를 안사용해도 됬었지만 

**swift는 실행할 코드가 한줄이라도 괄호를 꼭 사용해야한다.**

이제 사용 예시를 확인해보자.

### **if의 사용 예시**

예시
```swift
var example: Int = 5

if example > 1{
  print("example은 1보다 크다.")
}
```

실행 결과
```
example은 1보다 크다.
```

이런식으로 조건식이 true라면 if문 안에 코드가 실행된다.

이제 else문에 대해서 알아보자.

## 🚦 **else 문**
if문에서 **조건식이 false일때 실행된다**.

바로 구조에 대해 알아보자.
### **else 구조**
```swift
if 조건식{
  // 조건식이 true일때 실행할 코드
}else{
  // 조건식이 false일때 실행할 코드
}
```
이런식의 구조를 가지고 있다.

너무 쉬워서 설명할 것이 없다.. <br>
바로 사용 예시를 확인해보자.

### **else 사용 예시**
예시
```swift
var example: Int = 9

if example > 10{
  print("example은 10보다 크다.")
}else{
  print("example은 10보다 작다.")
}
```
실행 결과
```
example은 10보다 작다.
```

이런식으로 if문이 false 일때 else문이 실행된다.

다음으로는 else if에 대해 알아보자.

## 🪜 **else if 문**
else if문은 **다양한 조건식을 이용해야할때 사용할 수 있다.**

구조에 대해서 살펴보자.
### **else if 구조**
```swift
if 조건식1{
  // 조건식1이 true일때 실행할 코드
}else if 조건식 2{
  // 조건식2이 true일때 실행할 코드
}else if 조건식 3{
  // 조건식3이 true일때 실행할 코드
}else{
  // 조건식이 모두 false일때 실행할 코드
}
```
이런식의 구조를 가지고 있다.

바로 사용 예시를 확인해보자.

### **else if 사용 예시**
예시
```swift
var score: Int = 80

if score >= 100{
    print("A")
}else if score >= 90{
    print("B")
}else if score >= 80{
    print("C")
}else{
    print("D")
}
```
실행 결과
```
C
```

이런식으로 여러 조건을 이용해야할때 else if를 사용할 수 있다.

**조건식이 많지 않을땐 효율적이지만 조건식이 많아질 경우 번거로워진다.**<br>
그럴때 switch문을 사용해야한다.(switch문은 다음 글에서...)

이제 if문에 대해서 알아봤으니 오늘의 글에서 제일 중요한 guard문에 대해서 알아보자.

## 🛡️ **guard 문**
guard문은 if문과 다르게 **ture일땐 guard문 다음에 위치한 코드가 실행되며, false일때는 else문이 수행**된다.

또한 guard문에 **else는 반드시 포함**되어야 한다.

이때 else문에는 **현재 코드 흐름을 빠져나가는 코드가 있어야하며**, 또 다른 방법으로는 else 문에서 **자기 자신을 반환하지 않는 다른 함수나 메서드를 호출** 해야한다.

이제 guard문에 구조에 대해서 알아보자.

### **guard 구조**
```swift
guard 조건식 else{
  // 조건식이 false 일때 실행할 코드
}

// 조건식이 true일때 실행되는 코드
```
이런식의 구조를 가지고 있다.

바로 사용 예시를 확인해보자.

### **guard 사용 예시**
예시
```swift
func addExample(num1: Int?, num2: Int?) -> Int{
    guard let num1, let num2, num1 + num2 > 0 else{
        print("음수")
        return 0
    }
    
    var result = num1 + num2
    return result
}

var result1: Int = addExample(num1: 10, num2: 20)
var result2: Int = addExample(num1: -10, num2: -20)

print("result1 : \(result1)")
print("result2 : \(result2)")
```

실행 결과
```
음수
result1 : 30
result2 : 0
```

위 예시를 보면서 눈 여겨봐야할 점이 있다.

addExample은 옵셔널 Int 변수 두개를 받고 guard문으로 옵셔널 바인딩을 하였다. 여기서 if문과 차이가 나타난다.

if문의 옵셔널 바인딩은 if문 안에서만 사용할 수 있지만 **guard문에 옵셔널 바인딩은 guard문 밖에서도 사용이 가능**하다.

## 🗂️ **정리**
조건문에는 if, guard, switch(다음 글에서 다룰 예정)문이 존재한다.<br>

if문: 조건식이 true면 if문 안에 코드 실행한다.<br>

else문: if문의 조건식이 false일때 else문 안에 코드 실행한다.<br>

else if문: 다양한 조건식을 사용해야할때 사용한다.

guard문: 조건식이 true일때 guard문에 다음에 위치한 코드가 실행된다. false일땐 guard문에 else문이 실행된다.

guard문에 else문은 필수적으로 포함되어야 하며 else문에는 현재 코드 흐름을 빠져나가는 코드가 있어야한다.

## 💭 **느낀점**
if, else, else if는 이미 많이 사용해봐서 배우는데 어려움이 없었지만 

guard라는 처음 보는 문법을 배우면서 헷갈리고 어려웠지만 이해하고 나니까 사용 활용도가 아주 높다는 생각이 들었다.