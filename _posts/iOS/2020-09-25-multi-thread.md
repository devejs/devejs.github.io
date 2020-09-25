---
layout: post
title: iOS) Multi Threading
category: iOS
---
*Publishing Date:2020-09-25*

### 멀티 스레딩을 사용하는 이유
1. 시간이 오래 걸리는 작업 진행시 애플리케이션의 실행을 방해하면 안 됨
2. 멀티 코어에서 큰 작업을 여러 개로 분할하여 진행
3. 메모리 공간과 시스템 자원 절약


### GCD(Grand Central Dispatch)
> Execute code concurrently on multicore hardware by submitting work to dispatch queues managed by the system.
>
> 멀티코어 하드웨어에서 시스템이 관리하는 큐에 작업을 넣어서 코드를 병렬적으로 실행시키는 것

GCD는 시스템 레벨에서 여러 개의 앱들이 균형 있게 시스템 자원을 사용할 수 있도록 해준다. 이 때 `Dispatch Queue`를 사용하여 스레드 풀에서 작업을 실행한다.


### DispatchQueue
*Dispatch Framework > DispatchQueue*
애플리케이션에서 작업을 블록 객체 형태로 Dispatch Queue(FIFO)에 넣는다. 디스패치 큐에 들어간 작업들은 시스템에서 관리하는 스레드 풀에서 실행되는데, 메인 스레드에서 생성된 디스패치 큐를 제외하면 시스템은 디스패치 큐 안에 들어가는 작업이 어떤 스레드에서 실행되는지 모른다.

```
//
let serialQueue = DispatchQueue(label: "com.uraimo.Serial1")  //attributes: .serial
let concurrentQueue = DispatchQueue(label: "com.uraimo.Concurrent1", attributes: .concurrent)
```
라벨은 큐를 식별하는 데 사용되며, `All about Concurrency in Swift - Part 1: The Present` 문서에서는 도메인을 뒤집어 사용하라고 권장한다.

```
// default queues
// 1. 메인 스레드에서 처리되는 main queue
let mainQueue = DispatchQueue.main
// 2. 전체 시스템에 공유되는 concurrent queue
let globalDefault = DispatchQueue.global()
```

* QoS(Quality of Service)  
`global queue`를 사용할 때 작업의 우선순위를 미리 지정된 QoS를 사용하여 지정한다.  
1. userInteractive
2. userInitiated
3. utility
4. background


큐에서 클로저 형태의 작업들은 두 가지 방식으로 큐에 담긴다.  
1. sync: 작업이 끝나는 것을 기다렸다 실행
2. async: 기다리지 않고 바로 실행  
`asyncAfter` 메소드로 일정 시간 후에 코드를 실행시킬 수도 있다.


### Operating Queue
*Foundation > Task Management > Operations*
Operation 객체를 Queue에 넣어서 비동기적으로 실행할 수 있다.

### 추가 질문
Q> GCD를 왜 Dispatch로 한정하는가

### Reference
[네이버 블로그](http://blog.naver.com/PostView.nhn?blogId=jdub7138&logNo=220949191761&parentCategoryNo=&categoryNo=112&viewDate=&isShowPopularPosts=true&from=search)
[]()
