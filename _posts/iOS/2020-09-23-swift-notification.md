---
layout: post
title: Swift) Notification
category: iOS
---
*Publishing Date:2020-09-24*

### 배경지식


### Notification Center
> A notification dispatch mechanism that enables the broadcast of information to registered observers.
>
> 등록된 observer들에 정보를 브로드캐스트할 수 있게 하는 알림 발송 메커니즘


* `class NotificationCenter : NSObject`  
* default Noti-Center  
하나의 애플리케이션 안에 기본적으로 설정된 `NotificationCenter`가 존재하며 특정 `context`끼리의 커뮤니케이션을 위해 새 `NotificationCenter`을 설정할 수 있다.
* Single Program  
기본적으로 하나의 프로세스 안에서만 작동하며, 서로 다른 애플리케이션(프로세스)에서 작동하기 위해서는 `DistributedNotificationCenter` 클래스를 사용한다.

### Notification
> A container for information broadcast through a notification center to all registered observers.
>
> notification center을 통해 등록된 모든 observer에게 브로드캐스트되는 정보 객체

* `struct Notification`


### How to use


### Reference
[Notification in swift](https://medium.com/@dmytro.anokhin/notification-in-swift-d47f641282fa)
