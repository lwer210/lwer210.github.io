---
title: Swift - 변수에 대해서 알아보자.
date: 2024-11-17 05:03:00 +09:00
categories: [iOS, Swift]
image: /assets/img/frontimage/Swift_변수에_대해_알아보자.png
---

# Swift - 변수에 대해서 알아보자.

>Swift에서 사용하는 변수에 대해서 알아보자.

### 변수란 무엇일까??
변수란 말 그대로 **변하는 수**를 뜻하며 **데이터가 저장되는 공간**을 의미한다.

그렇다면 변수를 언제 그리고 어떻게 사용하는 것일까??
우선 선언하는 방법부터 알아보자.

### 변수 선언
```swift
var example: String
```
- var 는 변수임을 나타내는 키워드이다. var 이외에도 let 키워드가 존재한다.
- example은 변수의 이름을 나타낸다.
- 콜론(:)뒤에 타입을 붙히면 타입이 지정된다.

### var와 let의 차이가 뭘까??
var는 변수를 선언 후 값을 변경할 수 있다.
```swift
var fruit: String = "Apple"
fruit = "Banana" // 변경 가능
```
반면 let은 상수로 정의가 되기 때문에 값을 변경할 수 없다.
```swift
let fruit: String = "Apple"
fruit = "Banana" // 오류
```

> 여기서 **상수란 값을 한 번 할당하면 변경할 수 없는 변수**를 뜻한다.

### 변수의 선언 방법을 알아봤으니 왜 사용해야하는지를 알아보자.

변수를 왜 써야할까? 쓰지 않는다고 프로그램을 작성하지 못하나?

다음과 같이 예를 들어보겠다.

**변수를 사용하지 않은 코드**
```swift
import SwiftUI

struct ContentView: View {
    
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text("Banana")
            Text("Banana")
            Text("Banana")
            Text("Banana")
        }
        .padding()
    }
}

#Preview {
    ContentView()
}
```
이처럼 **변수를 사용하지 않고도 프로그램을 작성할 수는 있다.**

여기서 예를 한가지 들어보겠다.

만약 Text의 수가 20개이고 데이터를 "Banana"에서 "Apple"로 변경해야할 일이 생긴다면 모든 Text에 데이터를 일일이 변경해줘야한다.

이처럼 코드가 길어질수록 번거로워질뿐만 아니라 아주 비효율적이다.

### 이제 변수를 사용한 예를 살펴보자.

**변수를 사용한 코드**
```swift
import SwiftUI

struct ContentView: View {
    
    var fruit: String = "Banana" // fruit 변수에 "Banana" 할당
    
    var body: some View {
        VStack {
            Image(systemName: "globe")
                .imageScale(.large)
                .foregroundStyle(.tint)
            Text(fruit)
            Text(fruit)
            Text(fruit)
            Text(fruit)
        }
        .padding()
    }
}

#Preview {
    ContentView()
}
```
이처럼 변수를 사용할 경우 **데이터를 한곳에서 수정하면 되므로 코드가 길어질수록 효율적**이다.

### 정리
변수를 사용하지 않는다고 해서 프로그램을 작성하지 못하는 것은 아니다.
하지만 **변수를 사용하면 프로그램을 훨씬 효율적으로 작성할 수 있다.**
