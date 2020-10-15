---
layout: post
title: Swift) Protocol
category: iOS
---
*Publishing Date:2020-10-03*

### 배경지식


### 프로토콜이란?
> 특정 기능을 하기 위한 메소드, 프로퍼티 및 다른 요구 조건들의 청사진
> 변수와 함수의 list
> Swift의 interface  

선언
```Swift
protocol SomeProtocol : InheritedProtocol, InheritedProtocol2 {
    var someProperty { get set }
    func someMethod(arg: String)-> SomeType
    // 상속받은 두개의 프로토콜 함수/변수 그대로 상속
}
```


### 프로토콜을 사용하는 이유
1. MVC 패턴과 같은 blind communication에서 효과적  
2. 권한을 주는데 유용함  
`Hashable`: [자세한 설명은 여기서](https://devejs.github.io/ios/2020/10/07/swift-hashable.html)
3. 다중 상속 가능  
4. Type 정의  
어떤 프로토콜을 채택하여 구현한 객체는 *해당 프로토콜 타입* 이다.

```Swift
struct someObject : aProtocol, bProtocol {
    func aMethod(){
    // aProtocol 메소드 구현
    }
    func bMethod(){
    // bProtocol 메소드 구현
    }
}
...
var x : aProtocol = someObject()
x.aMethod() // 가능
x.bMethod() // 불가능! 에러 발생
...
class someClass : aProtocol{
    ...
}
var y : aProtocol = someClass()

var arr : [aProtocol] = [x, y]

```

### 새로 안 사실
1. 클래스에만 적용될 프로토콜의 선언에 `class`키워드를 추가할 수 있음
```Swift
protocol ClassProtocol : class {
    // 함수에 mutating이 필요 없음
    // 클래스에만 상속될 것이기 때문에
    func changeIt()
}
```
굉장히 드문 케이스로 대부분은 어느 것에든 구현될 수 있게 선언함

2. 클래스 타입에서 이니셜라이저 구현시 `required`

지정 이니셜라이저든 편의 이니셜라이저든 관계 없이 클래스 타입에서 프로토콜의 이니셜라이저를 구현할 경우 `required` 식별자를 붙인 요구 이니셜라이저로 구현해야 한다.  
단, 클래스 자체가 `final`로 정의되어 있다면 상속이 애초에 불가능하므로 `required`를 붙여줄 필요가 없다.

* 지정 이니셜라이저  
모든 프로퍼티 초기화
모든 클래스는 하나 이상의 지정 이니셜라이저를 가져야 함

* 편의 이니셜라이저  
특정 목적에 필요한 이니셜라이저
전달 인자를 전달하기 어려울 경우
항상 같은 값으로 초기화 가능
지정 이니셜라이저를 자신 내부에서 호출  

다른 경우로 A 프로토콜을 채택한 클래스가 B 클래스를 상속할 경우, B 클래스에 이미 A 프로토콜의 요구 이니셜라이저가 있다면 `override`, `required`를 전부 표기한다. 순서는 관계x
```
// 프로토콜
protocol AProtocol {
  var arg : String

  init(_ arg: String){
    self.arg = arg
  }
}

// 클래스
class ParentClass {
  var arg : String

  init(_ arg: String){
    self.arg = arg
  }
}

// 자식 클래스
class ChildClass : ParentClass, AProtocol{
  override required init(_ arg: String){
    self.arg = arg
  }
  // required override라고 표기해도 관계 없음
}
```

3. 실패 가능한 이니셜라이저  
프로토콜에서 `init?()`을 정의하면 해당 프로토콜을 채택하는 타입은 구현시 실패 가능한 이니셜라이저로 구현해도 되고, 일반적인 이니셜라이저로 구현해도 된다.
가능한 케이스
* init!()
* init()
* required init()
* required init?()

4. 프로토콜 조합
매개변수 전달시 여러 프로토콜을 모두 준수하는 타입일 경우 `&` 연산자 사용해 여러 프로토콜 조합해서 사용
*프로토콜 타입 캐스팅 가능*  

5. 선택적 요구사항
`@objc`: Objective-C에서 사용할 수 있도록 만드는 속성

`objc` 속성을 가진 프로토콜은 Objective-C 클래스를 상속받은 클래스에서만 채택 가능
```
@objc protocol SomeProtocol {
  @objc optional func someMethod()
}
```



### Reference
[Swift Docs](https://docs.swift.org/swift-book/LanguageGuide/Protocols.html)
