---
layout: post
title: iOS) NSOperationQueue vs GCD Queue
category: iOS
---
*Publishing Date:2020-11-10*

# NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.

### 배경지식
`동기`란, 코드가 **순차적**으로 실행되는 것이다. **동기** 라는 단어의 함정에 빠져 동시에 일어난다고 생각하기 쉬운데, 오히려 그 반대이다. 프로그램이 동기적으로 실행될 때 파일 입출력 등 시간이 오래 걸리는 작업이 진행된다면, 이 프로그램은 해당 코드에서 모든 작업이 끝날 때까지 기다렸다가 다음 코드를 실행한다.
`비동기`란, 코드가 순차적으로 실행되는 것을 보장하지 않는다. 즉, 비동기적으로 실행하는 코드가 있다면 우선 다음 코드를 실행하고, 비동기 코드가 끝나면 콜백을 받아 실행한다.

<!-- 해당 코드에 break point 걸어두면 확인하고 지나치는지 그냥 지나쳤다가 실행 완료 후에 지나치는지 실행시켜보기 -->

#### 비동기를 사용하는 이유
스레드는 로우 레벨의 툴이기 때문에 스레드를 직접 작성하는 것은 까다롭다. 특히 하드웨어나 시스템에 의존해 동적으로 스레드 개수를 조절하는 것은 거의 불가능하다. 따라서 iOS에서는 스레드를 직접 만드는 대신에 애플리케이션에서는 특정한 태스크만 정의하고 시스템이 실행하도록 위임한다. 즉, 시스템이 스레드를 관리하게 하면 애플리케이션은 스레드를 신경쓰지 않아도 되기 때문에 확장성이 높아지고, 단순하고 효율적으로 프로그래밍을 할 수 있다.  
스레드를 신경쓰지 않는다는 것은 비동기 프로그래밍에서 스레드를 여러 개 사용하지 않는다는 것이 아니다. 단지 스레드를 직접 제어하지 않고 시스템에 위임함으로써 태스크만 관리하는 것이다.


### NSOperationQueue

nil



### GCD Queue
GCD(Grand Central Dispatch) Queue는 곧 `DispatchQueue` 라고도 한다. 디스패치 큐는
* 블록 형태의 태스크가 들어온다.
* Serial 큐(한번에 태스크 하나 처리)와 Concurrent 큐(한번에 여러 태스크 처리)가 존재한다.
* 시스템에 의해 관리되는 스레드 풀에서 태스크가 실행되나, 메인 큐를 제외하고 어떤 태스크가 어느 스레드에서 실행되는지는 보장되지 않는다.
* 동기적/비동기적으로 태스크를 처리할 수 있다.

> **중요!**
> Async/sync와 Serial/Concurrent는 다른 개념이다!
> Async와 sync는 비동기-동기 개념으로 하나의 작업이 끝날때까지 기다리느냐 마느냐의 문제이고,
> Serial/Concurrent는 한번에 실행하는 작업의 수에 관한 문제이다.

> 동기적으로 실행되는 코드를 메인 큐에서 실행시키면 데드락이 발생할 수 있다.

### Differences


OperationQueue | GCD(DispatchQueue)
---|---
high-level Objective-C 클래스| low-level C-based API
GCD Wrapper| 사용하기 가벼움
operation의 라이프사이클 컨트롤 가능(Pause, Cancel, Resume)| -
Operation간의 의존성| -
KVO로 프로퍼티 관찰 가능| -

  
**결론**  
Operation Queue : 비동기적 실행작업을 객체 지향적인 방법으로 사용하는데 적합
Dispatch Queue : 복잡하지않은 간단한 작업이나 특정유형 시스템이벤트 비동기처리시 적합

### Reference
[Apple Docs- Concurrency Programming Guide](https://developer.apple.com/library/archive/documentation/General/Conceptual/ConcurrencyProgrammingGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40008091)  
[Apple Docs- NSOperationQueue](https://developer.apple.com/documentation/foundation/nsoperationqueue)  
[Apple Docs- DispatchQueue](https://developer.apple.com/documentation/dispatch/dispatchqueue)  
[Swift Thread- Dispatch Queue, Operation Queue](https://nsios.tistory.com/31)
[Multi Threading in iOS](https://abhimuralidharan.medium.com/understanding-threads-in-ios-5b8d7ab16f09)
