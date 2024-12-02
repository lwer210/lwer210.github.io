---
title: Swift - 구조체에 대해서 알아보자.
date: 2024-12-02 09:10:00 + 09:00
categories: [iOS, Swift]
tags: [swift, struct]   
---

오늘은 구조체에 대해서 공부하였다. 공부해보니 클래스와 유사한점이 아주 많았다. 지금부터 구조체에 대해서 알아보자.

## ❓ **구조체란?**
**데이터와 메서드를 재사용할 수 있는 객체로 캡슐화도 가능**하다.<br>
설명만 어렵지 그냥 클래스와 비슷하다.

어떤 구조를 가지는지 부터 알아보자.

## 🧱 **구조체의 구조**
```swift
struct Example{
  // 구조체 코드
}
```

위 코드와 같은 구조를 가졌다. 이제 구조체를 사용해보자.

## 🚀 **구조체 사용**
예시
```swift
struct Example{
    var ex1: Int
    
    init(ex1: Int) {
        self.ex1 = ex1
    }
    
    func printEx1(){
        print("Hello \(ex1)")
    }
}
```
위 코드와 같이 구조체를 선언할 수 있다. 

클래스와 생김새가 ``struct`` 키워드를 사용해서 선언한다는 것을 제외하곤 아주 유사하다.

계속해서 예시를 확인해보자.
```swift
struct Example{
    var ex1: Int
    
    init(ex1: Int) {
        self.ex1 = ex1
    }
    
    func printEx1(){
        print("Hello \(ex1)")
    }
}

var ex: Example = Example(ex1: 10)
ex.printEx1()
```

실행 결과
```
Hello 10
```
이런식으로 사용이 가능하다. 

사용 방법조차도 클래스와 너무 유사하다.<br>하지만 구조체와 클래스는 아주 명확한 차이를 가지고 있다. 

지금부터 클래스와 구조체에 차이점을 알아보자.

## 🎨 **클래스와 구조체의 차이점**
클래스와 구조체의 차이점은 **클래스는 참조 타입, 구조체는 값 타입**이라는 것에서 나타난다.

이것이 무엇인지 아래에서 자세히 알아보자.

### **값 타입**
예시를 보면서 설명하겠다.

예시
```swift
struct Example{
    var ex1: Int
    
    init(ex1: Int) {
        self.ex1 = ex1
    }
    
    func printEx(){
        print("Hello \(ex1)")
    }
}

var ex: Example = Example(ex1: 10)
var ex2: Example = ex
ex2.ex1 = 20

ex.printEx()
ex2.printEx()
```

실행 결과
```
Hello 10
Hello 20
```
위 코드처럼 ``ex``를 ``ex2`` 에 복사하였다. 그리고 값을 설정하고 출력한다.

위 코드에서 알 수 있듯이 구조체는 **복사본에 데이터를 수정하더라도 원본에 영향을 전혀 주지 않는다.**

이런 특성을 **값 타입** 이라고 한다.

이제 참조 타입에 대해서 알아보자.

### **참조 타입**
위와 마찬가지로 예시를 보면서 설명하겠다.

예시
```swift
class Example{
    var ex1: Int
    
    init(ex1: Int) {
        self.ex1 = ex1
    }
    
    func printEx(){
        print("Hello \(ex1)")
    }
}

var ex: Example = Example(ex1: 10)
var ex2: Example = ex
ex2.ex1 = 20

ex.printEx()
ex2.printEx()
```

실행 결과
```
Hello 20
Hello 20
```

위 코드를 확인했을때 구조체를 사용했을때와는 다르게 복사본에 값 변경이 원본에도 영향을 미쳤다.

**클래스 인스턴스는 메모리의 주소를 참조**하기 때문에 값을 복사를 하더라도 같은 객체를 가르킨다.

이런 특성을 **참조 타입** 이라고 한다.

이렇게 보면 클래스를 왜 쓰나 싶지만 구조체의 단점 또한 존재한다. 이제 구조체에 단점에 대해서 알아보자.

## 🔒 **구조체 단점**
위 설명만 들었을때 구조체가 있는데 클래스를 왜 쓰나 싶겠지만 이제 구조체에 단점을 차례대로 알아보자.

### **상속 불가능**
구조체는 클래스처럼 상속이 불가능하다.(포토토콜은 사용 가능)

예시
```swift
struct Example{
    var ex1: Int
    
    init(ex1: Int) {
        self.ex1 = ex1
    }
    
    func printEx(){
        print("Hello \(ex1)")
    }
}

struct Example2: Example{
    
}
```
위 코드처럼 다른 구조체를 상속 받는게 불가능하다.

### **deinit 사용 불가**
클래스 인스턴스의 생명 주기가 끝날때 다시말하면 메모리에서 인스턴스가 제거 될때 호출되는 것이 소멸자인데 구조체는 이것을 사용하는 것이 불가능하다.

## 🗂️ **정리**
구조체는 클래스와 비슷한 기능을 가졌지만 구조체는 값 타입, 클래스는 참조 타입에 특성을 지녔으며 구조체는 상속, ``deinit`` 메서드 사용이 불가능하다. 

## 💭 **느낀점**
구조체와 클래스에 차이점을 처음엔 뭔지 몰랐지만 값 타입과 참조 타입의 개념을 이해하면서 자연스럽게 알게되었다.

