---
layout: post
title: Swift) Optional
category: iOS
---
*Publishing Date:2020-09-08*

### Optional이란?
말 그대로 `옵션`, 즉 값이 있을 수도, 없을 수도 있다는 것을 의미한다.

#### NullPointException
* nil
nil은 `값이 없음`을 나타내는 키워드이다. Swift에서는 `NULL`을 nil로 표기한다. 어떤 변수가 nil일 때 해당 변수에 접근하면 `NullPointException`이 발생한다.
* NullPointException

#### 옵셔널을 사용하는 이유
1. 안정성
컴파일할 때 안정성을 높여줄 수 있다. Swift에서 옵셔널과 옵셔널이 아닌 값은 철저하게 구분되므로 런타임 에러가 줄어든다.  
2. 가독성
`?` 하나로 많은 코드를 생략하게 해 준다.  
`var opVar: dataType?`은 해당 변수가 옵셔널이라는 것을 의미한다. 예를 들어 단순히 매개변수에 옵셔널 변수를 명시해준다면 해당 매개변수로 NULL이 전달될 수 있는지 등 NULL과 관련된 모든 의미가 표현된다.


#### 옵셔널 문법
* 옵셔널 열거형의 정의
```Swift
public enum Optional<Wrapped> : ExpressibleByNulLiteral {
  case none
  case some(Wrapped)

  public init(_ some: Wrapped)
  ...
}
```
위 정의에 따르면, 옵셔널은 값을 갖는 케이스와 값을 갖지 않는 케이스로 나눌 수 있다. 값이 있는 경우(some), 연관값으로 Wrapped을 가진다. 즉, 값이 <b>옵셔널이라는 열거형에 래핑되어있다</b>는 것이다.

* 옵셔널을 초기화하지 않으면 기본값은 nil
* `??` : 값이 nil이면 `??` 뒤의 default값 사용

#### 강제 추출
`opVar!`
옵셔널의 값이 있는지 없는지 관계 없이 강제로 그 값을 빼낸다. 로직상 해당 값에 nil이 없다는 것이 확실시될 때 암시적으로 추출하는 방법을 사용할 수 있으나, 확실하지 않다면 런타임 오류를 발생시킬 수 있는 위험한 방법이다.

#### 옵셔널 바인딩
```Swift
if let value = opVar(, secondValue = opVar2, additional condition) {
  //값이 있을 때만 실행
  //여러 옵셔널을 바인딩할 수 있지만,
  //바인딩된 모든 옵셔널의 값이 있을 때만 실행됨
  //','로 조건이 딸려 있다면 조건까지 같이 검사한다
}
```
<b>옵셔널의 값이 존재하는지를 검사한 후 그 값을 추출</b>해주는 것을 의미한다.

#### 옵셔널 체이닝
옵셔널을 중첩해 사용할 때 효과적; 즉, 어떤 옵셔널의 값에 따라 그 이후의 값이 정상적으로 호출되거나 nil이 호출된다.
> 자전거의 체인을 생각해보자. 체인이 한칸이라도 없다면 그 체인은 사용할 수 없다.
> 마찬가지로 중첩된 옵셔널 중 하나라도 값이 없다면 nil을 리턴한다.

옵셔널의 속성에 접근할 때 옵셔널 바인딩 과정을 ? 키워드로 바꿀 수 있다. 매번 nil 체크를 해줄 필요가 없다는 점에서 유용하다.
```
opValue?.secondValue?.opFunc()
// nil일 때
  return nil
// nil이 아닐 때
  return opValue!.secondValue?.opFunc()
...
(repeated)
```

#### ImplicitlyUnwrappedOptional
옵셔널을 정의할 때 `?`가 아니라 `!`로 정의해줄 수 있다. 이렇게 정의된 옵셔널은 nil을 포함할 수 있지만, 접근할 때 옵셔널 바인딩이나 옵셔널 추출 과정 없이도 바로 값에 접근할 수 있다.  
그러나 일반적인 옵셔널 사용이 더 권장됨.

### 궁금했던 점
1. 옵셔널 자체를 하나의 데이터 타입으로 볼 수 있나?
  - 옵셔널 내부에 nil과 Wrapped가 들어있잖아
2. ...
