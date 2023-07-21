# 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?
- UIApplication 객체가 생성됨(인스턴스가 생성됨)

<br />

## UIApplicationMain?
```swift
@main
class AppDelegate: UIResponder, UIApplicationDelegate
```
- 앱의 본체에 해당하는 객체인 UIApplication 객체를 생성하고 App의 Life Cycle 관리
- 기존 Xcode11에서는 @UIApplicationMain이 사용 되었다가 Xcode12부터 @main으로 변경

<br />

## UIApplication?
```swift
class UIApplication: UIResponder
```
- 모든 App은 단 하나의 UIApplication 인스턴스를 가지고 있음
- Singleton으로 만들어지며 shared 속성으로 접근할 수 있음
- UIApplication은 사용자로 부터 발생하는 이벤트를 AppDelegate로 전달하는 역할을 함
- Delegate를 인스턴스화하고 이를 앱의 객체에 할당

<br />

## UIApplicationDelegate?
```swift
protocol UIApplicationDelegate
```
- 앱의행위, App Life Cycle를 관리하기위해 사용되는 메서드의 집합체를 정의하는 프로토콜
- 앱의 공유된 동작을 관리하는데 사용
- 하는 일
    - 앱의 중앙 데이터(CoreData, UserDefault, FileSystem) 구조를 초기화
    - 앱의 화면(Scene)을 구성
    - 메모리 부족 경고, 다운로드 완료 알림 같은 앱 외부에서 발생한 알림((Notification)에 응답
    - 앱 자체를 타겟으로 해 앱의 scene, 뷰나 뷰 컨트롤러와 관련이 없는 이벤트에 응답

<br />

## 질문
### UIApplication과 UIApplicationDelegate의 차이점은 무엇인가요?
- UIApplication은 iOS 앱의 생명주기를 관리하고, 앱의 실행 및 종료, 상태 전환 등을 처리하는 클래스. 앱을 실행하고 관리하는 데 필요한 기능을 제공하며, UIApplication은 싱글톤 객체로 앱 전체에서 하나의 인스턴스만 존재하며, UIApplication.shared로 접근할 수 있습니다
- UIApplicationDelegate는 앱의 상태 변화에 대한 이벤트를 처리하는 메서드들을 정의. 앱이 시작되거나 종료될 때, background로 진입하거나 foreground로 복귀할 때 등의 상황에서 호출되는 메서드를 구현하여 필요한 작업을 수행할 수 있음.
- 즉 UIApplication은 앱 자체를 관리하고 동작을 제어하는 클래스이고, UIApplicationDelegate는 앱의 상태 변화에 대응하여 필요한 작업을 처리하는 메서드를 제공하는 프로토콜

### Main Run Loop에 대해서 알고 있는것을 전부 설명해 주세요
- Main Run Loop 라는 것은 유저가 이벤트를 일으키는 이벤트들을 순차적으로 처리하는 프로세스
- UIApplication은 Main Run Loop 를 View 와 관련된 이벤트나 View 의 업데이트에 활용

### 유저가 발생시키는 이벤트의 처리 과정을 순서대로 나열해 주세요
1. 유저가 이벤트를 일으킨다.(터치, 줌인 등)
2. 시스템을 통해 이벤트가 생성된다.
3. UIKit 프레임워크를 통해 생성된 port로 해당 이벤트가 앱으로 전달된다.
4. 이벤트는 앱 내부적으로 Queue의 형태로 정리되고, Main Run Loop에 하나씩 매핑된다.
5. UIApplication 객체는 이때 가장 먼저 이벤트를 받는 객체로 어떤 것이 실행되야 하는지 결정한다

<br />

### Reference
- [Apple Developer Documentation: UIApplication](https://developer.apple.com/documentation/uikit/uiapplication/)
- [Apple Developer Documentation: UIApplicationDelegate](https://developer.apple.com/documentation/uikit/uiapplicationdelegate)
- [Apple Developer Documentation: UIApplicationMain](https://developer.apple.com/documentation/uikit/1622933-uiapplicationmain)
- [Apple Developer Documentation: Run Loops](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/Multithreading/RunLoopManagement/RunLoopManagement.html)
- [Understanding iOS application entry point](https://olszanowski.blog/posts/understanding-ios-app-entrypoint/)
- [What is @main in Swift](https://medium.com/@abedalkareemomreyh/what-is-main-in-swift-bc79fbee741c)
