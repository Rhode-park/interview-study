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
