---
layout: post
title: iOS) Scene Delegate
category: iOS
---
*Publishing Date:2020-11-04*

# scene delegate에 대해 설명하시오

### 배경지식
AppDelegate에 이어서, xcode 프로젝트를 생성하면 `SceneDelegate.swift` 파일이 자동으로 생성된다.  
```Swift
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

    var window: UIWindow?

    func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
        // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
        // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
        guard let _ = (scene as? UIWindowScene) else { return }
    }

    func sceneDidDisconnect(_ scene: UIScene) {
        // Called as the scene is being released by the system.
        // This occurs shortly after the scene enters the background, or when its session is discarded.
        // Release any resources associated with this scene that can be re-created the next time the scene connects.
        // The scene may re-connect later, as its session was not necessarily discarded (see `application:didDiscardSceneSessions` instead).
    }

    func sceneDidBecomeActive(_ scene: UIScene) {
        // Called when the scene has moved from an inactive state to an active state.
        // Use this method to restart any tasks that were paused (or not yet started) when the scene was inactive.
    }

    func sceneWillResignActive(_ scene: UIScene) {
        // Called when the scene will move from an active state to an inactive state.
        // This may occur due to temporary interruptions (ex. an incoming phone call).
    }

    func sceneWillEnterForeground(_ scene: UIScene) {
        // Called as the scene transitions from the background to the foreground.
        // Use this method to undo the changes made on entering the background.
    }

    func sceneDidEnterBackground(_ scene: UIScene) {
        // Called as the scene transitions from the foreground to the background.
        // Use this method to save data, release shared resources, and store enough scene-specific state information
        // to restore the scene back to its current state.
    }
}
```

#### UIWindowSceneDelegate
> Use UIWindowSceneDelegate object to manage the **life cycle** of one instance of your app's user interface

scene에서 발생하는 앱별 작업을 관리하는 추가적인 프로토콜로 scene의 life cycle을 관리한다.
`UISceneDelegate` 속성을 따르며 scene의 상태에 따라 notification을 받거나 scene의 환경 변화(사이즈 변화 등)에 응답할 수 있다.


### UISceneDelegate
> Use UISceneDelegate object to manage **life-cycle events** in one instance of your app's user interface

scene에서 발생하는 life cycle 이벤트를 관리


### Scene
[AppDelegate](https://devejs.github.io/ios/2020/10/26/ios-app-delegate.html)를 공부하면서 scene이

### Methods
메소드는 scene에 영향을 끼치는 상태 변화(scene이 foreground, active, background)에 응답하도록 정의됨.  

* `scene(_:willConnectTo:options:)`  
scene이 app에 추가함
* `sceneDidDisconnect(_:)`  
UIKit이 scene을 app에서 제거함
* `sceneDidBecomeActive(_:)`  
scene이 active되어 사용자 이벤트를 받을 수 있음
* `sceneWillResignActive(_:)`  
scene이 곧 active 상태에서 벗어나 사용자 이벤트를 받을 수 없음
* `sceneWillEnterForeground(_:)`  
scene이 곧 foreground에 올라가 사용자에게 보여짐
* `sceneDidEnterBackground(_:)`  
scene이 background로 들어감


### Reference
[Apple Docs- Scenes](https://developer.apple.com/documentation/uikit/app_and_environment/scenes)  
[Apple Docs- UIWindowSceneDelegate](https://developer.apple.com/documentation/uikit/uiwindowscenedelegate)  
[Apple Docs- UISceneDelegate](https://developer.apple.com/documentation/uikit/uiscenedelegate)  
