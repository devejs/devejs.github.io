---
layout: post
title: iOS) Foreground & Background
category: iOS
---
*Publishing Date:2020-10-23*

### 배경지식
**앱 생명주기**
![life cycle](https://docs-assets.developer.apple.com/published/61283402a3/024b99c5-4ab6-4ee0-bb41-6e6426ec6a64.png)  
*이미지 출처: Apple Docs*  


### Foreground
**App이 실행되어 사람들에게 보여지고 있는 상태**  
* Active
* Inactive

#### 제약사항


### Background
**Foreground에서 Homescreen으로 이동한 상태**  

#### 제약사항
* 사용자 이벤트 받기 어려움
* 공유 시스템 리소스 해제, 이미지 객체 참조 해제 등 메모리 제한
* 특정 유형의 앱만 백그라운드에서 실행 가능함



### Reference
[Apple Docs- App's Life Cycle](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle)  
[iOS Background Mode](https://medium.com/cashwalk/ios-background-mode-9bf921f1c55b)
