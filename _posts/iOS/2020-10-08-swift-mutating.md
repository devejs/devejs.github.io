---
layout: post
title: Swift) Mutating
category: iOS
---
*Publishing Date:2020-10-07*

### 배경 지식
`mutating` 관련 내용은 이전에 instance/class method에 관한 내용을 다루면서 잠깐 언급한 적이 있다. [링크](https://devejs.github.io/ios/2020/09/14/static-self.html)

### mutating
`mutating`은 `객체를 바꾸는 함수`임을 알리는 키워드이다.  
구조체 내부 함수에서 변수를 바꾸려고 할 때 `mutating` 키워드가 없으면 `'self' ~~` 에러가 발생한다.  
  
구조체는 `값 타입`이다. 인스턴스 자체가 힙 메모리에 저장되어 참조할 수 있는 클래스와 다르게, 구조체는 자체가 값을 가지고 있으므로 **스택 메모리에 저장이 된다.** 따라서 구조체는 전달될 때마다 참조가 아니라 매번 복사되어 전달되기 때문에 굉장히 비효율적이라고 할 수 있다.   
그래서 Swift는 효율적으로 동작하기 위해 **'값이 변경되었을 때에만'** 복사하도록 만들어졌다.  
동일하게 스택 메모리에 저장되는 변수들을 보자. 일반 변수들은 이미 선언될 때 `var`, `let`으로 선언되기 때문에 스위프트에서 해당 변수가 바뀌는 것에 대해 알고 있다. `Computed variable` 역시 `get`, `set`으로 스위프트에게 바뀐다고 알려주게 된다.  
그리고 구조체의 값을 변경하는 함수의 경우 스위프트에게 알려주는 키워드가 바로 `mutating`이다.

### Copy in Swift  
깊은 복사/얕은 복사   
내용 추가 공부할 것

### Reference
[Stanford iOS 강의](https://www.edwith.org/swiftapp/)  
[Copy-on-Write](https://oaksong.github.io/2018/01/06/copy-on-write/)
