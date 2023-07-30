# 1️⃣ UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?
- UIApplication 객체는 UIApplicationMain(_:_:_:_:) 함수에서 Singleton 객체로 생성됨
- UIApplication은 앱의 본체인 객체 중요한 역할을 많음
  - 앱을 처음 시작할때 무엇을 설정 할 것인가
  - 메모리에 무엇을 로드할 것인가 사용자
  - 사용자의 클릭이나 스크롤등의 이벤트가 발생 했을때 어떻게 동작되어야 하는가
  - 등등 앱의 기능이라고 생각하는 모든 것들은 UIApplication에 포함되어 있는 하위 객체

- UIApplication를 다루기 어렵고 굳이 변경할 필요도 없음. 하지만 원하는 방향이나 목적에 맞게 특별하게 처리해야 할 경우가 생길 수 있음
- 그래서 UIApplication 객체는 AppDelegate라는 대리 객체를 통해서 커스텀 코드를 처리할 수 있도록 권한을 줌
- UIApplicationMain 함수는 iOS 앱의 진입점을 정의하는 함수로 UIApplicationMain 함수를 직접 작성하는 것이 아니라 앱의 진입점으로 선택된 클래스에 어트리뷰트를 붙이는 방식으로 사용함
```swift
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
```
- 즉, UIApplication 객체는 앱이 해야 할 중요하고 핵심적인 일, 앱의 생명주기 관리나 이벤트 처리와 같은 것들을 담당하고, AppDelegate는 커스텀 코드를 처리합니다.

## 질문
### UIApplicationMain 함수가 호출되지 않으면 어떤 일이 발생하나요?
- 앱의 진입점(Entry Point)가 누락되서 앱이 실행되지 않습니다

### iOS 앱에서 UIApplication은 어떤 디자인 패턴과 연관되어 있는지 알려주세요.
- Singleton 패턴: UIApplication은 앱의 생명 주기를 관리하는 중요한 클래스로, 앱 전체에서 하나의 인스턴스만 존재해야 함. 이것을 Singleton 패턴으로 구현하여 앱 전역에서 쉽게 접근하고, 모든 객체가 같은 인스턴스를 공유하여 일관성을 유지할 수 있음. AppDelegate 클래스에서 UIApplication의 인스턴스를 얻는 것도 Singleton 패턴

- Delegate(위임) 패턴: UIApplication은 앱의 동작을 제어하고 시스템과 상호 작용하기 위해 다양한 Delegate 프로토콜을 활용. Delegate 패턴은 객체 사이의 상호 작용을 위해 사용되는 디자인 패턴으로, 한 객체가 다른 객체의 대리자 역할을 수행하여 필요한 동작을 구현

### 앱이 전체적으로 실행될 때의 과정
![문제1](https://github.com/Andrew-0411/TIL/assets/45560895/a75ae392-8fd4-4e97-9957-4d805396ea42)
![문제2](https://github.com/Andrew-0411/TIL/assets/45560895/aba1a8f0-2a4f-4792-8674-acfd28541f4d)
1. UIApplicationMain() 
2. EventLoop
3. Handle events
4. Background
5. applicationDidEnterBackground:

## Reference
- [앱의 생명주기](https://jinshine.github.io/2018/05/28/iOS/%EC%95%B1%EC%9D%98%20%EC%83%9D%EB%AA%85%EC%A3%BC%EA%B8%B0(App%20Life%20Cycle)%EC%99%80%20%EC%95%B1%EC%9D%98%20%EA%B5%AC%EC%A1%B0(App%20Structure)/)
- [iOS앱의 기본 구조 및 생명 주기](https://monsieursongsong.tistory.com/9)
