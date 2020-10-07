---
layout: post
title: Swift) Hashable, Equatable
category: iOS
---
*Publishing Date:2020-10-07*
# Hashable이 무엇이고, Equatable을 왜 상속해야 하는가?

### 배경지식
`Hash`

### Hashable
> A type that can be hashed into a Hasher to produce an integer hash value.

애플 개발자 문서에 따르면, `Hashable`은 프로토콜 중 하나로, `Hasher`에 의해 해시 값을 `hash`할 수 있는 타입이다. 즉, 이 프로토콜을 채택한 타입은 유일한 값(해시값)으로 구분될 수 있다는 것이다.  

> 딕셔너리의 키는 중복이 되지 않는다.  
> Set 역시 중복된 값을 담을 수 없다.  

대표적으로 Swift에서 Standard Library에 속하는 주요 자료형들(`String`, `Int`, `Float`, `Bool`)은 대부분 `Hashable` 프로토콜을 채택한다. 해당 자료형들은 Hashable하기 때문에 딕셔너리에서 키로 사용되거나 Set 내 원소가 될 수 있다.  


**그렇다면 우리는 언제 `Hashable`한 값을 신경써야 할까?**  

> Hashable한 구조체의 내부 프로퍼티는 Hashable해야 한다.
> Hashable한 열거형의 연관값은 Hashable해야 한다.

코드를 짜다 보면 커스텀 자료형을 구현하게 된다. 우리가 `struct`와 `enum`을 선언할 때 이 자료형들을 딕셔너리의 키나 set의 원소로 사용하기 위해서는 `struct`의 모든 프로퍼티와 `enum`의 연관값들은 모두 `Hashable`해야 한다. 만약 열거형에 연관값을 따로 지정해주지 않더라도 자동적으로 Hashable을 채택하게 된다.  
즉, 표준 자료형 프로퍼티를 가지는 구조체나 표준 자료형 연관값을 가지는 열거형이 `Hashable`을 채택한다면 컴파일러가 자동적으로 `hash(into:)` 함수를 호출해주어 지금까지는 신경쓸 필요가 없었지만, 그렇지 않다면 사용자가 직접 `hash(into:)` 함수를 통해 구현해주어야 한다는 것이다.  
다음은 애플 공식 문서에 나와 있는 예제이다.
```
struct GridPoint {
    var x: Int
    var y: Int
}

extension GridPoint: Hashable {
    static func == (lhs: GridPoint, rhs: GridPoint) -> Bool {
        return lhs.x == rhs.x && lhs.y == rhs.y
    }

    func hash(into hasher: inout Hasher) {
        hasher.combine(x)
        hasher.combine(y)
    }
}
```

`GridPoint` 구조체는 `Hashable`한 프로퍼티들을 가지고 있지만 `Hashalbe` 프로토콜을 채택하지 않았기 때문에 해당 구조체를 Set의 원소로 쓰려고 하려면 다음 에러를 볼 수 있다.  
> Type 'GridPoint' does not conform to protocol 'Hashable'

이 때 `Hashable` 프로토콜을 채택해주면 컴파일러가 자동으로 hash(into:) 함수를 구현해준다. 혹은 위 예제처럼 직접 함수를 구현해줄 수 있다.  
Swift 4.1 이전까지는 자동으로 구현되지 않아 반드시 사용자가 hash(into:) 함수와 == 연산자를 구현해주어야 했다고 한다.(글 작성 기준 현재는 Swift 5.3)

### Equatable
> A type that can be compared for value equality.

`Equatable`은 값의 비교가 가능함을 보장해주는 프로토콜이다. 이 프로토콜을 채택한 타입들은 `==` 연산자나 `!=` 연산자를 사용해 값을 비교할 수 있다. `Array`에서 `contains(_:)` 메소드를 사용할 수 있는 것도 `Array`가 `Equatable` 프로토콜을 채택하고 있기 때문이다.

### Equatable을 상속하는 이유

### Learn More...
[이 블로그](https://baked-corn.tistory.com/123)에서 가져왔는데 내가 정확한 출처(애플 리소스 등)를 찾지 못한 사항들. 확인되면 수정할 것.  

1. `a==b` 이면 `a.hashvalue == b.hashvalue` 는 참이고 역은 성립하지 않는다.   
2. 클래스는 컴파일러가 자동으로 `hash(into:)` 함수를 구현해주지 않는다.

### Reference
[Apple Docs- Hashable](https://developer.apple.com/documentation/swift/hashable)
[Apple Docs- Equatable](https://developer.apple.com/documentation/swift/equatable)
[Apple Docs- Hasher](https://developer.apple.com/documentation/swift/hasher)
