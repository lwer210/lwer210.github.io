---
title: Swift - 반복문에 대해 알아보자.
date: 2024-11-24 04:49:00 + 09:00
categories: [iOS, Swift]
tags: [swift, for, while]
---

Swift 뿐만 아니라 어떤 언어에서든 반복문은 자주 사용되며 중요한 개념이다. 

C언어로 처음 프로그래밍을 배울땐 반복문이 엄청 어렵게 느껴졌지만 지금은 또 그렇지 않다. 나이가 먹어서 그런지..어쨌든 Swift에서 사용되는 반복문을 알아보자.

## 🌀 **for-in 반복문**
컬렉션이나 숫자 범위에 포함된 항목들을 반복하는데 사용되며 사용법이 아주 간단하다. 

프로그램에서 반복해야할 횟수를 알고 있을때 굉장히 유용하게 사용된다.

사용법부터 알아보자.

### **for-in 사용법**
```swift
for 변수명 in 컬렉션 or 범위{
  // 반복될 코드
}
```
여기서 컬랙션 또는 범위에 값을 변수명으로 선언된 변수에 하나씩 짚어넣으면서 반복을 진행한다.

말로 하면 복잡해보이지만 코드로 확인해보면 아주 쉽다.
예시로 확인해보자.

예시
```swift
for exIndex in 1...5{
  print("enIndex 값 : \(exIndex)")
}
```
실행 결과
```
enIndex 값 : 1
enIndex 값 : 2
enIndex 값 : 3
enIndex 값 : 4
enIndex 값 : 5
```

이런식으로 범위 연산자로 범위를 지정하였고 값이 하나씩 exIndex에 들어가서 반복 코드에 사용된 것을 알 수 있다.

exIndex 처럼 꼭 변수명을 지정해서 사용할 필요는 없다.

예시
```swift
var count: Int = 0

for _ in 1...5{
  count += 1
  print("count : \(count)")
}
```

실행 결과
```
count : 1
count : 2
count : 3
count : 4
count : 5
```

위처럼 변수명을 지정하지 않고도 사용할 수 있다.

## 🌀 **while 반복문**
지정된 조건식이 true일때만 반복한다.

사용법에 대해서 알아보자.
### **while 사용법**
```swift
while 조건식{
  // 반복될 코드
}
```
조건식이 true일때만 반복되며 false가 되면 바로 종료된다.
바로 사용 예시를 보자.

예시
```swift
var exampleNum: Int = 0

while exampleNum < 10{
  exampleNum += 1
  print("exampleNum : \(exampleNum)")
}
```

실행 결과
```
exampleNum : 1
exampleNum : 2
exampleNum : 3
exampleNum : 4
exampleNum : 5
exampleNum : 6
exampleNum : 7
exampleNum : 8
exampleNum : 9
exampleNum : 10
```

위 코드처럼 조건식이 false가 되면 실행이 종료된다.

## 🌀 **repeat while 반복문**
다른 프로그래밍 언어를 미리 학습 해본사람은 잘 아는 do while문을 대체한 것이다.

반복문의 코드가 무조건 한번은 실행되는 반복문이다.<br>
설명이 조금 어려운 것 같기도 하다. (내가 설명을 못한걸 수도...)

바로 사용법을 알아보겠다.

### **repeat while 사용법**
```swift
repeat{
  // 반복될 코드
}while 조건식
```
반복될 코드가 실행된 후 조건식으로 검증한다.<br>
true일 경우에만 반복되며 false가 될 경우 종료된다.

사용 예시를 확인해보자.

예시
```swift
var exampleNum: Int = 0

repeat{
  print("exampleNum : \(exampleNum)")
  exampleNum += 1
}while (exampleNum < 10)
```

실행 결과
```
exampleNum : 0
exampleNum : 1
exampleNum : 2
exampleNum : 3
exampleNum : 4
exampleNum : 5
exampleNum : 6
exampleNum : 7
exampleNum : 8
exampleNum : 9
```

위처럼 먼저 코드를 실행 후 조건을 검증한다.

반복문에 대해서 알아보았으니 반복 코드를 건너뛰는 법과 반복문을 탈출하는 방법에 대해서 알아보자.

## ⛔ **반복문 탈출**
실행 중인 반복문을 탈출 하는 방법은 아주 간단하다.

break 를 사용해서 실행중인 반복문을 탈출할 수 있다.<br>
바로 사용법을 알아보자.

예시
```swift
var exampleNum: Int = 1

for _ in 1...10{
  if exampleNum % 2 == 0{
    print("짝수 : \(exampleNum)")
    break;
  }

  print("exmapleNum : \(exampleNum)")
  exampleNum += 1
}
```

실행 결과
```
exmapleNum : 1
짝수 : 2
```

위 코드는 exampleNum이 짝수라면 break를 이용해서 탈출하게 된다.

이런식으로 break를 사용해서 반복문을 탈출할 수 있다.
그럼 반복문을 탈출하지 않고 반복되는 코드를 건너뛰는 방법도 알아보자.

## ⤴️ **반복문 건너뛰기**
실행중인 반복문을 탈출하지 않고 반복중이 코드를 건너뛰고 다시 반복되게 하는 방법 또한 아주 간단하다.

continue 를 사용해서 실행중인 반복문 코드를 건너뛰게 할 수 있다.<br>
바로 사용 예시를 확인해보자.

```swift
var exampleNum: Int = 0

while exampleNum < 10{
    exampleNum += 1
    
    if exampleNum % 2 == 0{
        continue
    }
    
    print(exampleNum)
}
```

실행 결과
```
1
3
5
7
9
```

위 코드는 짝수인 경우 출력하지 않고 다시 반복문 시작부분으로 넘어가서 동작한다.

## 🗂️ **정리**
Swift에서 사용되는 반복문은 for-in, while, repeat-while 문이 존재한다.

for-in: 프로그램에서 반복될 횟수를 알고 있을 경우 유용
while: 조건을 지정해서 true일 동안만 반복
repeat-while: 무조건 한번은 반복될 코드 실행

반복문 탈출은 break를 사용하고, 실행되는 코드 건너뛰기는 continue를 사용한다.

## 💭 **느낀점**
다른 언어에서 사용하는 반복문과 매우 유사하여 이해하는데 크게 어려움 없이 배울 수 있어서 다행이였다.
