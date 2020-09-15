---
layout: post
title: Instance / Class Method
category: iOS
---
*Publishing Date:2020-09-14*

# 인스턴스 메소드와 클래스 메소드

### 배경지식
* 프로퍼티(Attribute)  
클래스, 구조체 또는 열거형 등에 관련된 값(변수/상수)
  - 저장 프로퍼티: 인스턴스의 변수 혹은 상수 (클래스, 구조체에 사용)
    - var, let
  - 연산 프로퍼티: 특정 연산을 실행한 결괏값 (클래스, 구조체, 열거형에 사용)
    - getter, setter
    - getter 메서드만 구현하거나 getter/setter을 모두 구현할 수 있지만 setter만 구현할 수는 없음
    - 인스턴스 외부에서 메서드를 통해 인스턴스 내부 값에 접근하기 위해 메서드를 구현할 경우 두 메서드가 분산 구현되어 코드의 가독성이 나빠짐
    - 프로퍼티 감시자(willSet, didSet)
  - 타입 프로퍼티: 특정 타입에 사용되는 프로퍼티  
  즉, 각각의 인스턴스가 아니라 타입 자체게 종속되는 프로퍼티  
  인스턴스의 생성 여부와 관계 없이 타입 프로퍼티의 값은 유일함
    - 저장 타입 프로퍼티: 변수 또는 상수로 선언; 반드시 초깃값 설정; 지연 연산(lazy) 가능
    - 연산 타입 프로퍼티: 변수로만 선언
* 인스턴스 프로퍼티: 타입을 정의하고 해당 타입의 인스턴스가 생성되었을 때 사용할 수 있는 `인스턴스`의 프로퍼티; 즉, 저장/연산 프로퍼티가 해당됨
* 메소드: 특정 타입에 관련된 함수

### 인스턴스 메소드
클래스, 구조체, 열거형 등에서 각각의 인스턴스가 특정 작업을 실행하는 기능을 캡슐화하기 위해 인스턴스 메소드를 사용  
함수와 문법이 동일하나 특정 타입 내부에 구현하므로 반드시 인스턴스가 생성되어야만 메소드 사용 가능

> 클래스와 다르게, 구조체와 열거형은 값 타입(value)이므로
> 인스턴스 메소드가 인스턴스 프로퍼티를 변경하게 되면
> `mutating` 키워드를 붙여줘야 한다.

* `self` 프로퍼티
모든 인스턴스는 암시적으로 인스턴스 자신을 가리키는 `self` 프로퍼티를 갖는다. 자바의 `this` 와 비슷하다.
  - 언제 사용하는가?  
  클래스 내부에서 `self` 키워드를 사용한 적이 있고 사용한 적이 없어서 언제 사용하는지 항상 헷갈렸는데, 인스턴스를 좀 더 명확히 지칭하고 싶을 때, 즉, 인스턴스 프로퍼티와 인스턴스 메소드 내부 변수명이 동일할 때 확실하게 명시해주기 위해 사용  
  Swift에서 동일 변수명을 가진 변수를 사용하는 순서  
  > 1. 메서드 내부 지역변수
  > 2. 메서드 매개변수
  > 3. 인스턴스의 프로퍼티

  - 다른 방식의 사용  
  스탠포드 강의 들을 때 이 방법에 대해서 한 번 배운 적이 있는데, `self` 프로퍼티는 값 타입 인스턴스 자체의 값을 치환할 수 있다. 즉, 구조체나 열거형 등의 값 타입 인스턴스는 그 자체의 값을 내부에서 사용할 수 있다.  


* `self`와 `Self`  
부스트캠프 챌린지 할 때 `Self` 키워드를 처음 봤는데, 간단하게 말하면 `현재`의 타입을 참조해주는 키워드라는 것 같다.
> *Swift Docs*
> The Self type isn’t a specific type, but rather lets you conveniently refer to the current type without repeating or knowing that type’s name.
> In a protocol declaration or a protocol member declaration, the Self type refers to the eventual type that conforms to the protocol.

그런데 이 내용만으로는 대체 `self`와 `Self`가 무슨 차이가 있는지 잘 감이 안 왔다. 더 찾아보다보니 스위프트 문서의 두번째 문장에 더 집중하면 되는 것 같다.
다음 예시를 보자.
```
class Superclass {
    func f() -> Self { return self }
}
let x = Superclass()
print(type(of: x.f()))
// Prints "Superclass"

class Subclass: Superclass { }
let y = Subclass()
print(type(of: y.f()))
// Prints "Subclass"

let z: Superclass = Subclass()
print(type(of: z.f()))
// Prints "Subclass"
```
이 예시는 링크한 스위프트 문서에서 가져왔다.
`Superclass`의 `f` 메소드를 보면, `Self` 타입의 `self`를 리턴한다.
상수 x는 Superclass의 인스턴스이므로 `x.f()`는 Superclass를 리턴한다.
상수 y는 Subclass의 인스턴스이다. `y.f()`는 Subclass를 리턴한다.
마지막으로 상수 z를 보자. 상수 z는 Superclass 타입이지만, Subclass의 인스턴스이다. `z.f()`가 반환하는 타입은 Superclass가 아니라 Subclass이다.
즉, `프로토콜을 따르는 최종적인 타입`의 의미가 여기서 나온다. `Self`는 z의 컴파일시 타입인 Superclass가 아니라 런타임시 타입인 Subclass, 최종적인 타입을 참조한다는 것이다.
와, 어렵다. 몇 번 더 써봐야 좀 들어올 것 같다.

이 내용을 참고한 스택 오버플로우에서 해당 내용에 관해 발표한 애플 WWDC 2015의 영상 링크를 알려줘서 적어놓는다.
[나는 아직 못봤다. 16:05에 해당 내용이!](https://developer.apple.com/videos/play/wwdc2015/408/)


### 클래스 메소드
Swift의 타입 메소드와 유사한 개념  
인스턴스를 생성하지 않고 클래스 범위에서 바로 메소드 사용 가능
> 메소드 앞에 `static` 키워드 사용하여 타입메소드 표기
> 클래스의 타입 메소드는
> `static`으로 정의하면 상속 후 메소드 오버라이딩이 불가능하고
> `class`로 정의하면 상속 후 메소드 오버라이딩이 가능함


* `self` 프로퍼티  
인스턴스의 `self`와 다르게 타입 그 자체를 가리킨다. 다시 한 번 말하지만, 타입의 프로퍼티는 유일하며 `self`가 가리키는 타입 자체도 유일하다.

### 피어세션 후 내용 추가
- class 키워드  
일반적으로 다른 언어에서 `static` 키워드는 자주 사용하지만, `class` 키워드는 클래스 선언할 때 외에는 사용한 적이 없어서 이게 뭔가 했는데 말 그대로 `class` 키워드를 사용해 함수를 선언할 수 있다.
```
class exClass{
  var exVar: Int = 0

  static func changeVar(){
    exVar += 1
    // 셋 다 동일한 표현
    // self.exVar += 1
    // exClass.exVar += 1
  }
  class func classMethod(){
    print("original class method")
  }
}
```
이 경우 exClass 클래스를 상속할 때, `changeVar` 함수는 오버라이드할 수 없지만 `classMethod` 함수는 오버라이드할 수 있다.  

- Static 메모리  
`Static 메소드 안에서는 Static 변수에만 접근 가능하다.`
라고만 알고 있고 왜 그런지 생각해 본 적이 없었는데, 띄엄띄엄 배웠던 기초 지식을 종합해보면 답이 나왔다.
기본적인 메모리의 구조는 다음과 같다.
![메모리구조](http://tcpschool.com/lectures/img_c_memory_structure.png)
(출처: TCPSchool)
static 메소드와 변수는 프로그램이 컴파일될 때 데이터 메모리에 올라가고, 일반적으로 프로그램에서 사용하는 인스턴스 메소드/변수들은 힙 메모리에 생성된다. 메모리의 영역이 다르기 때문에 정적 메소드(데이터 메모리)에서 인스턴스 변수(힙 메모리)에 접근할 수 없는 것이다.

- static, mutating  
피어세션 중 피어님께서 좋은 질문을 해주셨다.
구조체 내부에서 변수의 값을 변경하는 메소드를 선언할 경우, `mutating` 키워드를 반드시 붙여줘야 한다.
[자세한 내용은 구조체 참고!^^!]()
그런데 `static` 키워드가 붙은 구조체 메소드에도 `mutating` 키워드를 사용할까?
실제 struct 내부에서 변수의 값을 변경하는 static 메소드에 `mutating` 키워드를 추가했을 때, xcode가 에러를 뿜어냈다.
```
Static functions must not be declared mutating
Replace 'mutating ' with ''
```
즉, `static`과 `mutating`은 함께 사용할 수 없다.
이 이유는 아마 struct에서 `mutating`을 사용하는 이유가 구조체가 값 타입으로 `복사`되기 때문인데, static 변수/메소드들은 그 타입 자체의 값이기 때문에 새로 인스턴스가 생성될 필요가 없어서인 것 같다.

### Reference
[Swift Docs- Self Type](https://docs.swift.org/swift-book/ReferenceManual/Types.html#ID610)
[Self- stack overflow](https://stackoverflow.com/questions/27863810/distinction-in-swift-between-uppercase-self-and-lowercase-self)
