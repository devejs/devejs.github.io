---
layout: post
title: Swift) Escaping Closure
category: iOS
---
*Publishing Date:2020-10-10*
# 탈출 클로저

### 배경 지식
클로저: 일정 기능을 하는 코드를 하나의 블록으로 모아놓은 것

### 탈출 클로저
> A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns.
> 클로저가 함수의 매개변수로 전달되어 함수 종료 후에 호출되면 탈출 클로저라고 한다.

클로저를 매개변수로 갖는 함수를 선언할 때 `argumentName : @escaping` 키워드를 사용하여 탈출 클로저임을 명시한다.

```
var completionHandlers = [() -> Void]()
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
    completionHandlers.append(completionHandler)
}
```

탈출 클로저임을 명시한 경우, 클로저 내부에서 해당 타입의 프로퍼티나 메소드, 서브스크립트 등에 접근하기 위해서는 반드시 `self` 키워드를 사용해야 한다.  
비탈출의 경우 반드시 명시해줄 필요는 없다(선택적).



### 어디에 사용하는가
주로 비동기 작업을 할 때, 함수가 종료되고 나서도 특정 클로저를 호출해야 할 때 사용  
위의 예시처럼, 비동기 작업을 하는 함수들은 `completionHandler` 전달인자를 클로저 형태로 받는 경우가 많다. 

### Reference
[Swift Docs - Closure](https://docs.swift.org/swift-book/LanguageGuide/Closures.html)
