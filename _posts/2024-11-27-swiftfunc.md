---
title: Swift - 함수에 대해서 알아보자.
date: 2024-11-27 00:09:00 + 09:00
categories: [iOS, Swift]
tags: [swift, function]
---

평화롭던 어느날 Swift를 공부하던 도중 함수에 대해서 공부하게 되었다. Java를 공부했었기 때문에 쉽게 배울줄 알았지만...생각보다 어려웠다.

오늘은 함수에 대해서 공부한 내용을 설명하겠다.

## ❓ **함수란?**
**특정 작업을 위해 호출할 수 있게 이름을 붙혀놓은 것**을 말한다.

설명부터가 쉽지 않아보이지만 천천히 알아보자.<Br>
함수에 구조부터 알아보자.

### **함수의 구조**
```swift
func 함수명(매개변수1: 데이터 타입, 매개변수2: 데이터 타입) -> 반환 타입{
  // 함수 코드
}
```
위와 같은 형태를 가지고 있다.<br>
이때 함수는 **매개변수나 반환 값이 없을 수도 있다.**

> 매개변수와 인자<br>
> 
> 매개변수는 함수를 선언하는 선언문에서 작성하며 함수 내부에서 참조되는 변수를 말한다.<br>
> 
> 인자는 매개변수를 가진 함수를 호출할때 함수에 값을 넘겨줘야하는데 이때 넘어가는 값을 인자라고 한다.

바로 사용 예시를 확인해보자.
### **함수 사용**
예시
```swift
func add(num1: Int, num2: Int) -> Int{
  return num1 + num2
}

var result = add(num1: 10, num2: 20)
print(result)
```

실행 결과
```
30
```

이런식으로 사용이 가능한데 이때

```swift
func add(num1: Int, num2: Int) -> Int{
  return num1 + num2
}
```
num1, num2가 매개변수이고
```swift
var result = add(num1: 10, num2: 20)
```
10, 20이 인자이다.

그 밖에도 매개변수나 반환 값이 없는 예시도 확인해보자.

예시
```swift
func hello(){
  print("hello")
}

hello()
```

실행 결과
```
hello
```
이런식으로 반환 값과 매개변수가 없는 함수를 만들 수 있다.

예시
```swift
var count = 0

func increment() -> Int{
  return count + 1
}

print(increment())
print(count)
```

실행 결과
```
1
0
```
이런식으로 매개변수가 없이 반환값만 존재하는 함수도 사용이 가능하다.<br>

이때 print(count)를 했을때 count는 그대로인데 이 이유는 좀 더 아래에서 더 설명하겠다.

함수 내부에 코드가 **단일 표현식을 가지고 있다면 return을 생략해서 사용도 가능**하다.

예시
```swift
func add(num1: Int, num2: Int) -> Int{
  num1 + num2
}

print(add(num1: 10, num2: 20))
```

실행 결과
```
30
```
위 예시처럼 함수 내부 코드가 단일 표현식이라면 return 없이 사용이 가능하다.

만약 반환값을 사용하지 않는 경우가 생긴다면

```swift
func add(num1: Int, num2: Int) -> Int{
  return num1 + num2
}

_ = add(num1: 10, num2: 20)
```
위 코드처럼 **밑줄(_)을 사용해서 반환값 버릴 수도 있다.**

만약 다른 프로그래밍 언어를 공부한 사람이라면 아까부터 거슬렸던 부분이 있을 것이다.<br>
```swift
var result = add(num1: 10, num2: 20)
```
위 코드처럼 함수에 인자를 전달하는 과정중에서 매개변수 이름을 적는 것이 상당히 거슬릴 것이다. (처음 배웠을때 굉장히 낯설고 거슬렸다...)

이 부분을 해결 할 수 있는 방법을 알아보자.

### **지역 매개변수명과 외부 매개변수명**

**함수 내부에서 사용하는 매개변수명**을 **지역 매개변수명**라고 하며,<br>
**함수를 호출할때 지정하는 매개변수 이름**을 **외부 매개변수명** 이라고 한다.

이것을 이용하여 함수를 호출할때 매개변수명을 쓰는 것을 해결할 수 있다.
바로 예시를 확인해보자.

예시
```swift
func add(_ num1: Int, _ num2: Int) -> Int{
  return num1 + num2
}

var result = add(10, 20)
print("result : \(result)")
```

실행 결과
```
result : 30
```
위 코드처럼 외부 매개변수명을 지역 매개변수명을 짓는 앞쪽에 짓을 수 있으며 **밑줄(_)을 사용시 함수를 호출할때 매개변수명을 생략**할 수 있다.

외부 매개변수명을 지역 매개변수명과 다르게 지정도 가능하다.

예시
```swift
func add(num1 number1: Int, num2 number2: Int) -> Int{
  return number1 + number2
}

var result = add(num1: 10, num2: 20)
print("result : \(result)")
```

실행 결과
```
result : 30
```
위 코드처럼 외부 매개변수명을 지정할 수 있다.

그렇다면 만약 함수를 호출할때 매개변수에 값을 안넣으면 어떻게 될까??<br>
바로 확인해보자.

예시
```swift
func add(num1: Int, num2: Int) -> Int{
  return num1 + num2
}

var result = add(num2: 20)
print("result : \(result)")
```

실행 결과
```
MyPlayground.playground:1:6: note: 'add(num1:num2:)' declared here
func add(num1: Int, num2: Int) -> Int{
     ^
```
위 실행 결과처럼 오류가 발생한다.

이런 경우를 대비하려면 어떻게 해야할까??<br>
바로 매개변수에 기본값을 지정해주는 것이다.

### **매개변수 기본값 지정**
함수 호출시 **매개변수 값을 넘겨주지 않을 경우 지정된 기본값이 할당**되도록 하는 것이다.

바로 예시를 확인해보자.

예시
```swift
func add(num1: Int = 10, num2: Int) -> Int{
  return num1 + num2
}

print("result : \(add(num2: 20))")
```

실행 결과
```
result : 30
```
위 코드처럼 기본값을 지정할 수 있다.

함수를 사용할때 반환값은 하나만 반환시킬수 있을까?? 아니다.<br>
이럴때 사용하는 것이 튜플이다. 

아래에서 자세하게 알아보자.

### **튜플을 이용한 반환값 여러 개 사용**
**튜플을 사용하면 반환값을 여러 개 반환**할 수 있다.

바로 예시를 확인해보자.

예시
```swift
func tupleReturn(_ num1: Int, _ num2: Int) -> (sum: Int, avg: Int){
    var sum = num1 + num2
    var avg = sum / 2
  return (sum, avg)
}

var result = tupleReturn(10, 20)

print(result.sum)
print(result.avg)
```

실행 결과
```
30
15
```
위 코드처럼 반환값이 여러 개 일때는 튜플을 사용해서 반환할 수 있다.

지금까지 확인해본 예시들은 모두 매개변수가 몇개인지 정해져 있었다. 그럼 만약 매개변수가 몇개가 올지 모르는 상태라면 어떻게 해야할까??

가변 매개변수를 사용해서 처리할 수 있다.

아래에서 자세히 확인해보자.

### **가변 매개변수**
가변 매개변수는 **매개변수를 0개부터 그 이상을 받는다는 것을 의미**한다.

점 세 개(...)를 이용해서 사용이 가능하다.<Br>
바로 예시를 확인해보자.

예시
```swift
func varInt(_ nums: Int...){
  for item in nums{
    print(item)
  }
}

varInt(1, 2, 3, 4, 5)
```

실행 결과
```
1
2
3
4
5
```

이런식으로 사용이 가능하며 가변 매개변수는 **배열 형식으로 넘어오기 떄문에** 반복문을 이용하여 처리하였다.

아주 많이 미뤄지긴 했지만 위 예시들중 

예시
```swift
var count = 0

func increment() -> Int{
  return count + 1
}

print(increment())
print(count)
```

실행 결과
```
1
0
```

이 예시를 기억하고 있나? 보다시피 count에 값이 변하지 않았다.

이제 그 이유와 해결 방법에 대해서 알아보자.

### **입출력 매개변수 이용**
위 예시에 해결 방법에 대해 얘기 하기전에 확실히 알고 넘어가야할 부분이 있다.

함수에 사용되는 **매개변수는 기본적으로 상수로 인식**된다. 이 말은 즉 매개변수에 값을 직접 바꿀 수 없닫는 것을 의미한다.

그렇기 때문에 **매개변수의 값을 사용하려면 복사본을 만들어서 사용**해야한다.<br>
아래 예시를 확인해보자.

예시
```swift
var example = 10

func numNum(_ num: Int) -> Int{
  var number = num
  number *= num
  return number
}

print(numNum(example))
print(example)
```

실행 결과
```
100
10
```
위 코드처럼 복사본을 이용하면 실제 변수의 값이 변하지 않는다.<Br>
앞서 확인해봤던 예시가 이런 상황에 놓인 것이다.

그렇다면 어떻게 해결해야할까??

입출력 매개변수를 이용해야한다.

바로 예시를 확인해보자.

예시
```swift
var example = 10

func numNum(_ num: inout Int) -> Int{
  num *= num
  return num
}

print(numNum(&example))
print(example)
```

실행 결과
```
100
100
```
위 코드처럼 함수 선언시 **매개변수에 데이터 타입 앞에 inout을 붙혀주고** 함수를 **호출할때 인수 앞에 & 를 붙혀주면** 입출력 매개변수가 사용되면서 문제가 해결된다.

또한 함수를 상수나 변수에 넣을 수도 있다.

### **함수 변수 또는 상수에 할당**
바로 예시를 확인해보자.

예시
```swift
func add(_ num1: Int, _ num2: Int) -> Int{
  return num1 + num2
}

var functionAdd = add
print("add : \(functionAdd(10, 20))")
```

실행 결고
```
add : 30
```
위 코드처럼 **변수나 상수에 함수를 할당하는 것이 가능**하다. 

그렇다면 변수에 데이터 타입은 뭘로 지정되는 것일까??

이럴땐 확인해보는 것이 가장 빠르다.

예시
```swift
func add(_ num1: Int, _ num2: Int) -> Int{
  return num1 + num2
}

var functionAdd = add
print(type(of: functionAdd))
```

실행 결과
```
(Int, Int) -> Int
```
위 실행 결과처럼 (Int, Int) -> Int 라는 데이터 타입을 가진다.<br>
이처럼 **함수의 데이터 타입은 매개변수와 반환 타입에 따라 달라진다.**

몇 가지 예시를 더 확인해보자.

예시
```swift
func testDataType(_ strings: String, _ ints: Int) -> Double{
    return 3.14
}

let test = testDataType
print(type(of: test))
```
실행 결과
```
(String, Int) -> Double
```
이처럼 매개변수와 반환값에 따라 함수의 데이터 타입이 정해진다는 것을 이해할 수 있다.

이것을 이용해서 함수를 다른 함수의 매개변수로 사용이 가능하다.<br>
아래에서 더 자세히 알아보자.

### **다른 함수의 매개변수로 함수를 사용**
위에서 알아본 **함수의 데이터 타입을 이용해서 함수를 매개변수로 받는 것이 가능한데** 바로 예시를 통해 알아보자.

예시
```swift
func add(_ num1: Int, _ num2: Int) -> Int{
  return num1 + num2
}

var functionAdd = add

func testAdd(_ add: (Int, Int) -> Int){
  print(add(10, 10))
}

testAdd(functionAdd)
```

실행 결과
```
20
```
위 코드 처럼 함수의 데이터 타입을 이용해서 매개변수로 받는 것이 가능하다. 

그렇다면 반환 하는 것도 가능하지 않을까?? 당연히 가능하다.<br>
아래에서 확인해보자.

### **함수 반환**
**함수의 데이터 타입을 반환 타입으로 지정하여 함수를 반환할 수도 있는데** 바로 예시를 확인해보자.

예시
```swift
func add(_ num1: Int, _ num2: Int) -> Int{
  return num1 + num2
}

func minus(_ num1: Int, _ num2: Int) -> Int{
  return num1 - num2
}

let varAdd = add
let varMinus = minus

func isVar(_ bol: Bool) -> (Int, Int) -> Int{
  if bol{
    return varAdd
  }else{
    return varMinus
  }
}

var varResult = isVar(true)
print(varResult(10, 20))
```

실행 결과
```
30
```
위 코드처럼 함수의 데이터 타입을 이용해서 함수를 반환하는 것도 가능하다.

## 🗂️ 정리 
함수는 특정 작업을 할 수 있게 이름을 붙혀놓은 것으로 제대로 이해하면 활용도가 끝없이 높아지기 때문에 개념을 잡고 가는게 아주 중요하다.

## 💭 느낀점
기존에 Java를 배웠기 때문에 함수도 무리없이 잘 배울 것이라고 생각했는데 생각했던 것과는 달리 이해하는데 상당히 어려움이 많았고 익숙해질때까지 많이 사용해봐야 할 것 같다.

## 📚 **참고자료**
- [핵심만 골라 배우는 SwiftUI 기반의 iOS 프로그래밍], 닐 스미스 저, 황반석 옮김, 제이펍 출판
