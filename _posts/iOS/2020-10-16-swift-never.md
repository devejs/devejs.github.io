---
layout: post
title: Swift) Never
category: iOS
---
*Publishing Date:2020-10-20*

### Never
> The return type of functions that do not return normally, that is, a type with no values.
> 일반적으로 리턴하지 않는 함수의 리턴 타입으로 값이 없는 타입이라고 할 수 있다.

이전에 `defer` 키워드 관련해서 공부할 때 `Never`에 대해서 다음과 같이 정리한 바 있다.
> 간단히 말해서 `Never`은 일종의 타입으로, 비반환 함수에서 반환 값 타입으로 사용된다. 즉, 리턴값이 `Never`인 경우 해당 함수는 비반환 함수가 되고, 비반환 함수 안에서는 오류를 던지거나 중대한 시스템 오류를 보고하는 등의 일을 하고 프로세스를 종료하기 때문에 `defer`가 실행되지 않는다.



애플 문서에서는 이를 다음과 같이 설명한다.
> Use Never as the return type when declaring a closure, function, or method that unconditionally throws an error, traps, or otherwise does not terminate.
> 무조건 오류나 트랩, 어찌됐든 종료되지 않는 무언가를 발생시키는 메소드, 함수, 클로저를 정의할 때 반환 값으로 Never을 사용한다.

트랩에 관한 내용은 [여기](https://donghoson.tistory.com/1) 보고 더 공부하기.  

해당 글을 쓸 때에는 `Never` 자체가 함수의 일종인 줄 알았지만, `Never`은 Enumeration으로 그냥 하나의 타입이다. 비반환 함수에 사용되어 반환 값이 없이 프로세스가 종료되는 것을 의미해주는 것이다.
```
@frozen enum Never
```

`@frozen` 키워드에 관한 내용은 [여기](https://medium.com/@jllnmercier/swift-unknown-and-frozen-attributes-8d4eea52d5ac) 보고 더 공부하기.  

스위프트 표준 라이브러리에서 사용되는 대표 예시에는 `fatalError`함수가 있다. 이 함수는 message의 내용을 출력하고 무조건 프로그램을 중단시킨다.
```Swift
public func fatalError(_ message: @autoclosure () -> String = String(), file: StaticString = #file, line: UInt = #line) -> Never
```
  
Zedd님 블로그에 의하면 `generic class`에서 작업할 때 유용하다고 하는데, 아직 이해하지 못한 부분이지만 나중을 위해 기록해둔다.

### Reference
[Apple Docs- Never](https://developer.apple.com/documentation/swift/never)  
[야곰- Swift 프로그래밍 3판]()  
[Zedd님 블로그](https://zeddios.tistory.com/680)
