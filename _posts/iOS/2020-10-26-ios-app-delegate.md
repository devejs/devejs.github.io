---
layout: post
title: iOS) App Delegate Methods
category: iOS
---
*Publishing Date:2020-10-27*

# 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오

### 배경지식
xcode에서 app 프로젝트를 생성하면 생기는 기본적인 파일 중에는 `AppDelegate.swift` 파일이 있다.

```Swift
import UIKit

@main
class AppDelegate: UIResponder, UIApplicationDelegate {

    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        return true
    }

    // MARK: UISceneSession Lifecycle

    func application(_ application: UIApplication, configurationForConnecting connectingSceneSession: UISceneSession, options: UIScene.ConnectionOptions) -> UISceneConfiguration {
        // Called when a new scene session is being created.
        // Use this method to select a configuration to create the new scene with.
        return UISceneConfiguration(name: "Default Configuration", sessionRole: connectingSceneSession.role)
    }

    func application(_ application: UIApplication, didDiscardSceneSessions sceneSessions: Set<UISceneSession>) {
        // Called when the user discards a scene session.
        // If any sessions were discarded while the application was not running, this will be called shortly after application:didFinishLaunchingWithOptions.
        // Use this method to release any resources that were specific to the discarded scenes, as they will not return.
    }
}
```
`AppDelegate` 클래스는 `UIResponder` 클래스를 상속하고, `UIApplicationDelegate` 프로토콜을 채택한다.

#### UIResponder
이 클래스는 이벤트를 핸들링하고 응답하는 인터페이스로, 이 클래스를 상속하면 UIKit의 이벤트 응답 객체를 생성할 수 있다. `UIApplication` 객체뿐만 아니라 `UIViewController` 객체, 그리고 모든 `UIView` 객체들이 응답 객체에 속한다.  
응답 객체들은 특정 이벤트에 대해 핸들링하기 위해 해당 이벤트에 관한 메소드를 오버라이드해 사용한다.


#### UIApplicationDelegate
애플리케이션의 공통 행동을 제어하기 위한 프로토콜로 `UIApplication` 객체와 연계하여 시스템과의 상호작용을 관리한다. UIKit은 이 프로토콜을 채택한 앱 델리게이트 객체를 애플리케이션이 실행되는 초기에 생성하여 항상 존재할 수 있게 하는데, 이 객체가 앱 실행 초기부터 앱이 존재하기 위한 시스템적인 일들을 하기 때문이다. 예를 들면 다음과 같다.
* 앱의 중심 데이터 구조를 초기화
* 앱의 scene들을 구성
* 푸시 알림과 같은 필요한 서비스에 앱 등록

이 외에도 배터리 부족과 같은 앱 외적인 요소나 앱 자체를 타겟으로 한 이벤트와 알림에도 반응한다.


### Methods

먼저 앱이 처음 초기화될 때의 대표적인 메소드는 다음과 같다.
* `application(_:willFinishLaunchingWithOptions:)`  

* `application(_:didFinishLaunchingWithOptions:)`  
앱 시작 프로세스가 끝날무렵 앱이 시작될 준비가 거의 됐다는 것을 알림

애플리케이션 scene 관련 메소드
* `application(_:configurationForConnecting:options:)`  
새로운 scene이 생성될 때 UIKit이 사용할 구성 데이터 반환
* `application(_:didDiscardSceneSessions:)`  

### Scene-Based Life-Cycle
![](https://docs-assets.developer.apple.com/published/61283402a3/024b99c5-4ab6-4ee0-bb41-6e6426ec6a64.png)  
출처: Apple Documentation  

`scene`이란 실행중인 애플리케이션의 UI를 나타내는 하나의 객체이다. 하나의 화면뿐만 아니라 탭 바, 내비게이션 컨트롤러도 하나의 scene이다.  
scene을 지원하는 app의 경우 scene마다 각각의 생명주기를 가진다. 따라서 각각의 scene마다 실행 상태가 다르기 때문에 다른 상태 메서드가 실행된다.



### App-Based Life-Cycle
![](https://docs-assets.developer.apple.com/published/c63cd35863/4d403429-fa30-4706-863f-5e3617ee21d0.png)
출처: Apple Documentation  


### iOS13 ~
iOS13부터 scene을 지원하는 application에서는 Lifecycle 이벤트에 ` UISceneDelegate`를 사용한다. scene을 지원하지 않거나 iOS12 이하의 app에서 `UIApplicationDelegate`를 사용한다.


### Reference
[Apple Docs- UIResponder](https://developer.apple.com/documentation/uikit/uiresponder)  
[Apple Docs- UIApplicationDelegate](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)  
[Apple Docs- Managing Your App's Life Cycle](https://developer.apple.com/documentation/uikit/app_and_environment/managing_your_app_s_life_cycle)  
