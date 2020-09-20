---
layout: post
title: Swift) Delegation Pattern
category: iOS
---
*Publishing Date:2020-09-16*

<!-- ### Delegation
위키피디아에 Delegation 항목이 엄청 많다. 대체 왜 이렇게 많은거지..?
1. [Delegation Pattern](https://en.wikipedia.org/wiki/Delegation_pattern)
2. [Delegation(object oriented programming)](https://en.wikipedia.org/wiki/Delegation_(object-oriented_programming))
3. [Delegation(Computing)](https://en.wikipedia.org/wiki/Delegation_(computing))
4. [Delegation(Computer security)](https://en.wikipedia.org/wiki/Delegation_(computer_security))
5. [Delegate(CLI)](https://en.wikipedia.org/wiki/Delegate_(CLI))

들어가서 읽어보니, 5번은 CLI(Commom Language Infrastructure)에서 사용되는 문법의 형태라 보지 않기로 했다. CLI라는게 있다는 것만 알고 가자.
4번 역시 보안 관련해서 사용자가 다른 사용자에게 권한을 위임하는 내용인 것 같아 생략.
어째 아래부터 올라가고 있는데, 3번에서는 컴퓨터에서 말하는 Delegation의 전체적인 내용으로 링크된다. 컴퓨터에서 일반적으로 사용되는 Delegation은 어떠한 엔티티에서 다른 엔티티로 무언가를 넘겨주는 것이다. 좁은 의미에서 특별한 형태의 다양한 관계를 말한다고 한다. 우리가 찾고 있는 것은 1번, 2번으로 연결된다.
(목록에 `Forwarding`이 있는데, 어디서 들어본 적은 있으나 자세히는 알지 못한다. 나중에 더 공부하도록 하자.)
2번에서는 객체지향 프로그래밍에서 사용하는 Delegation에 대해 읽을 수 있었다. 객체지향에서 Delegation은 수신자 객체의 프로퍼티나 메소드를 송신자 객체의 컨텍스트에서 평가하는 것이라고 한다. 이게 무슨 말이람? -->

### Delegation
Delegation 패턴은 객체지향 디자인 패턴중의 하나로 객체 구조가 상속처럼 코드 재사용을 할 수 있게 한다. 즉, 객체는 `Delegate`라는 헬퍼 객체를 만들어 권한을 위임함으로써 요청을 처리하는데, 이 때 delegate는 원래 객체의 context를 사용한다.
<!-- Delegation인지 알지 못하고 사용하고 있었던 Delegation 중 하나는 `self`이다.
this is done implicitly by having self in the delegate refer to the original (sending) object, not the delegate (receiving object) -->

그렇다면 Delegation은 왜 사용할까?
처음에는 단순히 Delegation을 사용했던 상황(특정 뷰가 뷰 컨트롤러에게 처리를 맡긴 경우)만을 생각하고 뷰가 처리하기 어려운 상황에 처리할 수 있는 대리자를 만드는것인가 추측했다.
그러나 Delegation의 정의에서 위와 같은 단순한 1차원적인 이유가 아니라 코드 재사용이라는 넓은 이유로 사용한다는 것을 알 수 있었다. 보통 객체 지향에서는 코드를 재사용하기 위해 상속을 하는데,

즉, 상속을 하기 어려운 상황에 Delegation을 대신 사용할 수 있다는 것이다.
그럼 언제 상속을 하고 언제 Delegation을 사용하나요?

이 질문에 대해서는 [내가 참고한 글](https://magi82.github.io/ios-delegate/)에 워낙 설명이 잘 되어 있어서 읽어보길 권한다.





### Examples
Delegate 패턴을 활용하는 경우를 예를 들어 설명
* Observer
* Event Listener


### Reference
[Delegation Pattern](http://best-practice-software-engineering.ifs.tuwien.ac.at/patterns/delegation.html)
[Delegate 이해에 도움이 된 글](https://magi82.github.io/ios-delegate/)
[Observers](https://benoitpasquier.com/observer-design-pattern-swift/)
