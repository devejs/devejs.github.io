---
layout: post
title: Swift) Access Control
category: iOS
---
*Publishing Date:2020-10-14*
# 접근제어자

### 배경지식
파일 간 또는 모듈 간에 접근을 제한할 수 있는 기능
-> 코드의 상세 구현은 숨기고 허용된 기능만 사용하는 인터페이스 제공  

캡슐화   
은닉화   



### Access Control in Swift
* Open  
공개(Public)과 흡사하나 클래스에서만 사용 가능  

* Public  
어디에서든 사용 가능  
주로 프레임워크에서 외부와 연결될 인터페이스를 구현하는데 많이 사용됨  

* Internal  
default: 기본적으로 모든 요소에 지정되는 기본 접근 수준  
소스 파일이 속한 모듈에서는 전부 사용 가능하나 외부에서 접근 불가  
* File-private  
구현된 소스파일 내부에서만 사용 가능   

* Private  
그 기능을 정의한 범위 내에서만 사용 가능  


<!-- Open access and public access enable entities to be used within any source file from their defining module, and also in a source file from another module that imports the defining module. You typically use open or public access when specifying the public interface to a framework. The difference between open and public access is described below.
Internal access enables entities to be used within any source file from their defining module, but not in any source file outside of that module. You typically use internal access when defining an app’s or a framework’s internal structure.
File-private access restricts the use of an entity to its own defining source file. Use file-private access to hide the implementation details of a specific piece of functionality when those details are used within an entire file.
Private access restricts the use of an entity to the enclosing declaration, and to extensions of that declaration that are in the same file. Use private access to hide the implementation details of a specific piece of functionality when those details are used only within a single declaration. -->  

**구현시 주의사항**  
1. 상위 요소가 하위 요소보다 더 높은 접근 수준을 가질 수 없다
2. 함수의 매개변수로 전달된 타입보다 함수의 접근 수준이 높을 수 없다


**읽기 전용 구현**  
저장 프로퍼티를 구현할 때 허용된 접근 수준에서 값을 변경할 수 없도록 읽기 전용으로 구현  
```
// 공개 접근 수준
// setter만 비공개 접근 수준
public private(set) var propertyName
```



### 왜 사용하는가?
외부에서 보거나 접근하면 안 되는 코드의 필요한 부분만을 제공

### Reference
[야곰- Swift 프로그래밍 3판]()
