---
layout: post
title: Swift) Singleton
category: iOS
---
*Publishing Date:2020-09-*

### Singleton
> 특정 클래스의 인스턴스가 `오직 하나`임을 보장하는 객체

* 단 한번 메모리에 할당된 후 해당 객체 참조
* 애플리케이션 내의 특정 클래스의 인스턴스가 하나만 존재

### 왜 사용하는가?
* 데이터 공유(하나의 객체 지속적 참조)
* 메모리 절약

### 활용 예시
* 싱글톤 생성

```
class MySingletonClass {
    static let sharedInstance = MySingletonClass()
}
```
```
class MySingletonClass {
    static let sharedInstance: MySingletonClass = {
        let instance = MySingletonClass()
        // additional setup code
        return instance
    }()
}
```

* URLsession
