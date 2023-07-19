# 2주차

## 1️⃣ 앱이 시작할 때 main.c 에 있는 UIApplicationMain 함수에 의해서 생성되는 객체는 무엇인가?

UIApplication 객체가 생성된다.

실행중인 앱의 제어와 조정을 담당하는 중앙지점 역할을 한다. 이 객체가 생성되고 나서야 개발자가 작성한 코드대로 이벤트 처리 등 앱의 동작을 제어할 수 있게 된다.

 모든 iOS앱은 단 하나의 UIApplication 인스턴스를 가진다.

## 2️⃣ @Main에 대해서 설명하시오.

프로그램 실행 시작 시 진입점으로 타입을 지정하기 위한 스위프트 언어의 기능입니다.

@main은 AppDelegate 클래스에 선언되어져 있으며, UIApplicationDelegate 프로토콜에 작성된 main 함수를 호출하게 됨으로서 프로그램을 시작하게 됩니다.

## 3️⃣ 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?

앱이 Foreground 상태일 때는 메모리 및 기타 시스템 리소스에 높은 우선순위를 가지며 시스템은 Foreground 상태의 앱이 이러한 리소스를 사용할 수 있도록 필요에 따라 background 앱을 종료합니다.

Background 상태일 때는 가능한 적은 메모리공간을 사용하도록 해야하며 메모리 확보를 위해 앱을 종료시키기도 합니다.

**Not Running 상태**

- 앱이 실행되지 않은 상태거나 시스템에 의해 종료되어진 상태

**Foreground의 상태**

- InActive
앱이 실행중이지만 아직 아무런 이벤트를 받지 않은 상태(Foreground 상태에서 전화가 왔을때, 잠금상태, 멀티태스킹 스크린에서 InActive 상태를 가짐)
- Active
앱이 실행중이며 현재 이벤트를 받고 있는 상태

**Background 상태**

- Foreground 상태에서 HomeScreen으로 이동한 상태
- Background 상태로 전환되기 전에 호출된 Task가 끝나지 않은 경우 Background 상태에서도 실행됩니다.

**Suspend 상태**

- 앱이 Background 상태로 전환된 후 더이상 작업을 수행하지 않으면 시스템이 앱을 Suspend 상태로 전환합니다.
- App은 여전히 메모리에 존재하며 Suspend 상태가 될 당시의 상태를 저장하고 있지만, CPU나 배터리를 소모하지 않습니다.
- Suspend 상태의 App은 Foreground 상태의 App을 위해 메모리 부족 등의 이유로 시스템에 의해 언제든지 종료될 수 있습니다. 이후 App을 실행하면 이전 상태의 화면은 나오지않고 앱이 재시작됩니다.

## 4️⃣ 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.

iOS 12 이하 버전의 AppDelegate에서는 앱의 상태변화에 따른 동작에 대해 관리할 수 있었습니다.

- applicationDidBecomActive : InActive → Active
- applicationWillResignActive :  Active → InActive
- applicationDidEnterBackground : InActive → Background
- applicationWillEnterForeground : Background → Foreground
- applicationWillTerminate : 앱종료 직전 호출

iOS 13 이상부터는 SceneDelegate가 프로세스 레벨인 applicationWillTerminate를 제외하고 해당 Life Cycle을 관리할 수 있게 바뀌었습니다.

## 5️⃣ 앱이 In-Active 상태가 되는 시나리오를 설명하시오.

- 앱을 처음 시작했을 때 Not Running → InActive → Active 상태가 됩니다.
- 앱 실행 도중 홈으로 갈 때 Active → InActive → Background 상태가 됩니다.
- 다시 앱을 키면 Background → InActive → Active 상태가 됩니다.
- 앱 실행 도중 전화나 메시지 같은 특정 알림창이 화면을 가리면 앱이 이벤트를 받지 못하는 상태가 되기 때문에 InActive 상태가 됩니다.

## 6️⃣ scene delegate에 대해 설명하시오.

iOS 12 이하 버전에서는 앱델리게이트에서 프로세스의 라이프 사이클과 UI 라이프 사이클을 모두 관리하고 있었습니다.  

iOS 13 이후에서 멀티 윈도우를 지원하게 되면서 하나의 앱이 여러 화면을 가질 필요성이 생기게 되었고 앱델리게이트는 프로세스 라이프사이클을 관리하고, 씬델리게이트는 각각의 씬에 맞는 UI 라이프 사이클을 관리할 수 있도록 하게 되었습니다.

따라서 씬델리게이트를 통해 화면의 상태에 따라 라이프 사이클을 관리할 수 있는데,

- scene(_willConnectTo:options:) : 씬이 앱에 추가될 때 호출되는 메서드입니다.
- sceneDidDisconnect(_:) : 씬의 연결이 해제될 때 호출되는 메서드
- sceneWillResignActive : Active → InActive
- sceneWillEnterForegorund: InActive
- sceneDidBecomeActive : InActive → Active, willEnterForeground가 호출 된 후에 호출되는 메서드, 사용자와 상호작용이 가능한 시점
- sceneDidEnterBackground : InActive → Background
