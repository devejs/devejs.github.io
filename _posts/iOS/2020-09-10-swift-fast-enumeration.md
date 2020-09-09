---
layout: post
title: Swift) Fast-Enumeration
category: iOS
---
*Publishing Date:2020-09-10*

### Fast Enumeration이란?
Apple Developer

> Fast enumeration is a language feature that allows you to efficiently and safely enumerate over the contents of a collection using a concise syntax.

> 컬렉션의 내용을 간결한 문법을 사용해서 효율적이고 안전하게 셀 수 있게 해주는 문법적 특성

Fast Enumeration은 Objective-C에서 사용하던 문법이다. 즉, Objective-C의 반복문이라고 요약할 수 있다. Swift는 Objective-C에서 사용되던 해당 문법(반복문)을 지원하도록 만들어졌다. Swift가 기본적으로 지원하는 다음 Collections들은   
  * `Array<Element>`
  * `Dictionary<Key:Hashable,Value>`
  * `Set<Element:Hashable>`  

`for..in` 구문에 적용이 가능하다.

갑자기 `for..in`이 왜 나오냐면, Objective-C에서 fast enumeration의 예제를 보면 알 수 있다.

```ObjectiveC
NSArray *array = [NSArray arrayWithObjects:
        @"one", @"two", @"three", @"four", nil];

for (NSString *element in array) {
    NSLog(@"element: %@", element);
}

NSDictionary *dictionary = [NSDictionary dictionaryWithObjectsAndKeys:
    @"quattuor", @"four", @"quinque", @"five", @"sex", @"six", nil];

NSString *key;
for (key in dictionary) {
    NSLog(@"English: %@, Latin: %@", key, [dictionary objectForKey:key]);
}
```
낯익은 문법이 보인다.
`for ~ in array/dictionary`


### Fast Enumeration을 사용하는 이유
1. 효율성
2. 간결성
3. 안전성

### Sequence? Collection?
Xcode에서 for..in 반복문을 사용할 때 in 이후에 아무 정수나 넣으면, 다음과 같은 에러를 만나볼 수 있다.
![for_in_error](/assets/스크린샷%202020-09-10%20오전%206.18.43.png)  

> For-in loop requires 'Int' to conform to 'Sequence'

시퀀스를 따르기 위해 Int가 필요하댄다. 그럼 시퀀스가 뭘까?  
> *Protocol*
> A type that provides sequential, iterated access to its elements.

> 요소에 연속적이고 반복적인 접근을 제공하는 프로토콜

Swift에서 프로토콜은 지켜야하는 껍데기, 즉 인터페이스같은 것이다. 그렇다면 For-in 반복문은 `Sequence 프로토콜`을 준수하는 정수형이 필요하다고 한다. 아 그렇다면 우리가 흔히 쓰는
> * 0..<number
> * [array]
> * [Dictionary]

이런 친구들은 Sequence 프로토콜을 따른다는 말이 된다.  
그렇다면 Collection은 무엇인가?

> *Protocol*
> A sequence whose elements can be traversed multiple times, nondestructively, and accessed by an indexed subscript.

> 파괴되지 않고 여러 번 순회할 수 있는 요소들을 가진 시퀀스인데 인덱스 달린 서브스크립트에 의해 접근 가능함ㅇㅇ

`traversed` 라는 단어가 무슨 느낌일지 좀 생각을 해봤는데 그냥 어렵게 생각하지 않고 간단히 생각하기로 했다. 배열을 가로지르는 게 배열을 순회하는 것 말고 더 있나?  
결론적으로, 컬렉션도 시퀀스 프로토콜을 따르기 때문에 for..in에서 사용할 수 있다는 것이다.   
위에서 봤다시피, Swift에서 지원하는 Collections는 세 가지다.
`Array, Dictionary, Set`

해당 컬렉션들은 CS 자료구조 공부하면서 따로 다루는 게 나을 것 같아서 굳이 여기서 미주알 고주알 늘어놓지 않기로 한다.  
(공부하면 링크 추가해 주세용!)  
서브스크립트도 공부해야되는데, 곧..

### 궁금했던 점
1. for in 반복문 사용할 때 [String]뿐만 아니라 그냥 시퀀스 타입이면 전부 사용 가능할텐데 에러 메세지에 나오는 Int의 의미는 뭘까? 인덱스?

2. 시퀀스는 프로토콜인데 문서에 보면 Type이라고 한다. Swift에서 Type의 의미가 뭘까?
-> 옵셔널이 데이터 타입인지 아닌지 공부하면서 같이 공부했다.  
[여기로](https://devejs.github.io/ios/2020/09/07/swift-optional.html)

### References
* [Apple Developer Document](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/ObjectiveC/Chapters/ocFastEnumeration.html)
* [Apple Developer- Sequence](https://developer.apple.com/documentation/swift/sequence)
* [Swift Docs- Colleciton Types](https://docs.swift.org/swift-book/LanguageGuide/CollectionTypes.html)
