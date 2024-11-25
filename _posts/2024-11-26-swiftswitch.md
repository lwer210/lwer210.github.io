---
title: Swift - switch에 대해서 알아보자.
date: 2024-11-26 01:00:00 + 09:00
categories: [iOS, Swift]
tags: [swift, switch]
---

전에 쓴 글에서 if, guard 에 대해서 알아보았다. 원래는 if와 switch를 같이 다루려고 했는데 guard 라는 새로운 개념을 배우면서 if문과 같이 다루면 좋을 것 같다고 생각되어 if와 guard를 같이 다루고 switch를 따로 빼두었다.

C나 Java에서 사용되는 switch와 Swift에서 사용되는 switch는 조금 다르게 동작된다. 

지금부터 switch 문에 대해서 알아보자.

## 🔀 **switch 문**
조건식이 많지 않을때는 switch보단 if, else if를 사용하여 처리하는게 훨씬 효율적이며 코드가 복잡해지지 않는다.

이떄 조건식이 많아질수록 if, else if 문은 더 복잡해지고 읽기가 어려워진다. 이런 경우에 switch 사용은 가뭄에 단비같은 역할을 하게된다.

switch 문에 구조에 대해서 먼저 알아보자.

### **switch 구조**

```swift
switch 표현식{
  case 값1:
    // 표현식의 값이 값1과 일치할 경우 실행되는 코드
  case 값2:
    // 표현식의 값이 값2와 일치할 경우 실행되는 코드
  default:
    // case와 일치하는 값이 없을 경우 실행되는 코드
}
```
switch에 구조는 위와 같이 생겼다. 언뜻봐서는 다른 언어에서 사용되는 switch와 다를 점이 없어보인다.

다른 언어와에 차별점은 switch에 사용에서 드러나게 된다.

이제부터 switch를 사용하는 예시를 확인해보자.

가장 기본적인 사용 예시부터 확인해보자.

예시
```swift
var example: Int = 3

switch (example){
  case 1:
    print("1")
  case 2:
    print("2")
  case 3:
    print("3")
  default:
    print("해당 사항 없음")
}
```

실행 결과
```
3
```

다른 언어를 공부해본 사람은 이미 이상한 점을 느꼈을 것이다. 바로 **break를 사용하지 않았다는 것**이다.

왜 break를 사용하지 않을까?? 

Swift는 case 에 지정된 값이 표현식과 일치하여 case 문 안에 코드가 실행 될 경우 **자동으로 switch문을 빠져나가게 구성되어 있기 때문**이다.

그렇다고 아예 break를 안사용하는 것은 아니다.

default가 처리할 작업이 아무것도 없을 경우에 break를 사용하기도 한다.

예시
```swift
var example: Int = 1

switch (example){
  case 1:
    print("1")
  default:
    break
}
```

이런식으로 break가 사용되기도 한다.

또한 case문에 범위 연산자를 사용해서 범위를 지정할 수도 있다.<br>
범위 연산자를 이용한 switch 사용에 대해서 알아보자.

### **case 범위 지정**
예시
```swift
var score: Int = 78

switch (score){
  case 0...29:
    print("최하")
  case 30...49:
    print("하")
  case 50...59:
    print("중")
  case 60...79:
    print("상")
  case 80...100:
    print("최상")
  default:
    print("해당 사항 없음")
}
```
실행 결과
```
상
```

위 예시 처럼 case에 범위 연산자를 사용하여 값의 범위를 지정할 수 있다.

또한 case 문에 조건을 걸 수도 있다.<Br>
case에 조건을 거는 방법에 대해서도 알아보자.

### **case에 조건식 지정**
where를 이용해서 case에 조건을 지정할 수 있다.

바로 사용 예시를 살펴 보자.

예시
```swift
var number: Int = 12

switch (number){
  case 0...29 where number % 2 == 0:
    print("0과 29 사이에 짝수")
  case 30...49 where number % 2 == 0:
    print("30과 49 사이에 짝수")
  default:
    print("해당 사항 없음")
}
```
실행 결과
```
0과 29 사이에 짝수
```

이처럼 범위 연산자와 섞어서 사용하면 활용도가 아주 높아진다.

## 🗂️ **정리**
조건식의 양이 많아져 if, else if로 처리하기엔 무리가 있을 경우 switch 문 사용이 효율이 좋다.

Swift에 switch문은 case 값과 표현식에 값이 일치할 경우 자동으로 switch문을 빠져나와주기 때문에 break를 사용하지 않아도 된다.

case에 범위 연산자 지정이 가능하며, where를 통한 조건 지정이 가능하다.

## 💭 **느낀점**
Java, C 를 먼저 공부해봤기 때문에 switch 문도 별거 아니란 생각으로 공부에 임했다가 작동 방식에 차이를 느끼게 되었고 switch 문에 활용성이 상당히 높다는 것을 다시 한번 깨닫게 되는 좋은 계기가 되었다.