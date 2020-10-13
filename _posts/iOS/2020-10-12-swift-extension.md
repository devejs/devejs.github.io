---
layout: post
title: Swift) Extension
category: iOS
---
*Publishing Date:2020-10-12*

### 배경지식
#### 상속(Inheritance)
객체지향 언어에서 `상속`이란 base가 되는 클래스나 객체를 기반으로 새로운 클래스나 객체를 생성하는 메커니즘이다. 새로 생성된 객체와 기반 객체 사이에 계층적 관계가 형성되며, 주로 `부모 클래스(객체)`, `자식 클래스(객체)`로 표현한다.  
![계층적 관계](https://upload.wikimedia.org/wikipedia/en/0/0e/Multilevel_Inheritance.jpg)  
출처: Wikipedia  
상속은 개발자들이 기반 클래스를 바탕으로 같은 기능을 유지하면서 새로운 기능을 구현할 수 있도록 도와주기 때문에 코드의 재사용성을 높여준다.

### Extension
> Extensions add new functionality to an existing class, structure, enumeration, or protocol type.
> 클래스, 구조체, 열거형, 프로토콜 타입에 추가 기능을 더하는 문법

`Extension`은 Swift에서 처음 본 문법이었는데, `Objective-C`의 `category`와 비슷하다고 한다.  
> Category란 특정 클래스에서도 분류되는 기능들을 나누어 카테고리화하고, 별도의 파일로 저장하는 것을 말한다.  
> 이 때 기존 클래스에 대해 새로운 기능을 추가하여 확장하는 것도 가능한데, 기존 클래스를 참조할 경우 카테고리에서 추가한 기능도 사용이 가능하다.  
> 기존에 있던 메소드를 오버라이드해서 사용할 경우 기존 메소드가 아닌 카테고리에서 재정의된 메소드를 사용하기 때문에 주의해야 한다.  

`Extension`이 `Category`와 다른 점은 **Extension에서는 기존 기능을 재정의할 수 없다** 는 것과 카테고리에서처럼 별도로 이름을 붙여줄 필요가 없다는 것이다.  
Object C의 자세한 문법까지는 공부하지 않았지만, 확장 자체의 개념은 흡사하나 사용법이나 기능에는 약간 차이가 있다. 내가 이해한 바에 의하면, 카테고리는 기존의 클래스를 좀 더 모듈화해서 사용할 수 있게 해주고, 확장은 말 그대로 기능을 추가해주는 느낌인 것 같다(전적으로 내가 느낀 바로, 정확하지 않음).   
그러나 새로운 기능을 추가해준다는 개념은 흡사하다고 할 수 있으므로, 확장을 사용하여 **다양한 연산 프로퍼티, 메소드(이니셜라이저 포함), 서브스크립트 등을 정의** 해줄 수 있으며, **특정 프로토콜을 채택** 하게 해줄 수도 있다.

Extension 문법은 다음과 같다.

```Swift
extension SomeType {
    // new functionality to add to SomeType goes here
}
```

***주의할 점***
* Extension에 연산 프로퍼티는 추가가 가능하지만, 저장 프로퍼티는 추가할 수 없다.
* 기존에 존재하던 프로퍼티에 [프로퍼티 감시자]()를 추가할 수 없다.
* Extension에서 **클래스 타입** (값 타입은 관계 없음)에 [이니셜라이저]()를 추가할 때, 편의 이니셜라이저만 추가할 수 있다. (지정 이니셜라이저는 반드시 클래스 구현부에 존재해야 함)

* 여러 기능 추가시 기능별로 각각 익스텐션 블록에 구현하는 것을 권장한다.

** 프로퍼티 감시자, 이니셜라이저 내용 추가 공부해서 포스팅하기!
**


#### 왜 사용하는가?
일반적으로 기능 확장을 위해서는 `상속`을 사용할 수도 있다. 그러나 상속을 위해서는 기존에 존재하는 코드가 구현한 모든 메소드와 프로퍼티들에 대하여 알아야 한다. 부모 클래스의 모든 것을 받아와야 하기 때문이다. 즉, 상속은 수직적 확장이다.   
그러나 `확장`은 **기존 코드를 모르더라도 내가 원하는 기능을 추가할 수 있다** 는 장점이 있다. 수직적이 아니라 수평적 확장이기 때문이다. 바로 아래 활용 예시에서 볼 수 있듯이, 다른 언어를 사용할 때는 기존에 존재했던 자료형들에 없는 메소드는 사용할 생각도 해보지 못했는데 Swift에서는 내 커스텀 메소드를 만들어 사용할 수 있다는 것이 굉장히 매력적으로 다가왔다.    

또한, 상속은 클래스에서만 사용이 가능하다. 하지만 확장은 클래스뿐 아니라 구조체, 열거형, 프로토콜, 제네릭 등 모든 타입에서 전부 사용이 가능하다.  

\+ 피어세션 중 다른 분이 설명해주신 익스텐션의 추가 사용법   
Extension은 기능 확장뿐 아니라 코드를 깔끔하게 정리하는 용도로도 자주 사용한다고 한다. 클래스 안에 모든 메소드와 프로퍼티들을 정의하는 대신 Extension을 사용하여 기능에 따라 코드를 분리함으로써 코드 가독성을 높일 수 있는 것이다.   
그 대표적인 예로 특정 프로토콜을 채택하는 타입을 구현할 때 *프로토콜의 요구 사항을 미리 구현해놓는 용도* 로도 사용할 수 있다.


#### 활용 예시
```Swift
extension Int {
    func repetitions(task: () -> Void) {
        for _ in 0..<self {
            task()
        }
    }
}

3.repetitions
```
위 코드는 `Int` 자료형을 확장하여 `task()` 메소드를 반복할 수 있는 `repetitions` 메소드를 추가한 것이다.   
개인적으로는 Swift에서 `String` 다루는 것이 까다로워서 미리 메소드를 추가해놓고 사용한 적이 많았다. [이 gist](https://gist.github.com/albertbori/0faf7de867d96eb83591)에서 다양한 String 확장 메소드들을 참고할 수 있다.  
또 다른 예시는 중첩 데이터 타입이다.  
```Swift
extension Int {
    enum Kind {
        case negative, zero, positive
    }
    var kind: Kind {
        switch self {
        case 0:
            return .zero
        case let x where x > 0:
            return .positive
        default:
            return .negative
        }
    }
}
```

### 피어세션 내용 추가
피어세션 진행 중 피어 한 분이 좋은 질문을 해 주셨다. `Extension`으로 확장한 클래스를 상속받는다면 확장한 메소드나 연산 프로퍼티를 사용할 수 있을까?
<script src="https://gist.github.com/devejs/d9bb383c8ff0fd447a748259f1d111bb.js"></script>  
결과적으로 말하자면 확장한 클래스를 상속받는다면 확장한 메소드를 사용할 수 있다.  
해당 코드의 실행 결과는 다음과 같다.
```
> GrandParent
first function
> Parent
override first function
> Parent 2
override first function
Working Hard...
> Child
override first function
Working Hard...
Do additional Job
```

### Reference
[위키피디아- 상속](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))
[Objective C- category](https://soooprmx.com/archives/2436)
[Swift Docs- Extension](https://docs.swift.org/swift-book/LanguageGuide/Extensions.html)
