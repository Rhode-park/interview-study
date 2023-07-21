# Bounds와 Frame의 차이점을 설명하시오.

<br />

## Common
- 두 개념 모두 위치와 사이즈를 반환하는 CGRect 타입을 가짐
- CGRect?(CG: CoreGraphics): View의 크기(CGSize)와 좌표(CGPoint)를 담는 구조체
- iOS 좌표계 시스템의 **좌측 상단**이 원점(0,0) 이며 수평이 x축 수직이 y축

<br />

## frame
```swift
var frame: CGRect { get set }
```
- origin: 상위 뷰(Super View) 좌표계를 기준
    - 상위 뷰(Super View)는 자신의 기준으로 한단계 상위 뷰를 말함
    - 현재 View의 원점이 얼마만큼 떨어져 있는지를 나타냄
- origin 변경 시
    - 하위 뷰(Sub View)가 이동 시 상위 뷰(Super View)를 기준으로 (x,y) 만큼 이동
    - 상위 뷰(Super View)가 이동 시 하위 뷰(Sub View)도 따라서 같이 움직임
- size: Super View(상위 뷰)에서 현재 view가 차지하는 사각형 영역의 크기를 나타냄
- UIView 위치나 크기를 설정할 경우 사용

<br />

## bounds
```swift
var bounds: CGRect { get set }
```
- origin: View 자신의 좌표계를 기준
    - frame과는 다르게 상위 뷰와는 아무런 관련이 없음
    - 자신의 좌표계를 기준으로 하므로 (0, 0)으로 초기화 함
- origin 변경 시
    - 해당 View의 ViewPoint를 (x,y) 만큼 이동
    - 하위 뷰(Sub View)가 마치 (-x, -y) 만큼 이동한것처럼 보임
- size: 자신의 좌표계에서의 크기를 나타냄
- ScrollView에서 스크롤할 때, View 내부에 drawRect()로 그림을 그릴 때 사용

<br />

## 질문

<br />

### Bounds와 Frame은 각각 어떤 타입을 사용하나요?
- CGRect
### CGRect는 무엇인가요? 
- View의 크기와 좌표를 담는 구조체
### CGRact 구조체 안에는 위치를 설정하는 이것과()와 크기를 설정하는 이것()가 있습니다 각각 무엇일까요?
- CGPoint, CGSize
### CGRact, CGPoint, CGSize CG는 무엇의 약자인가요
- Core Graphics
### Frame과 Bounds는 각각 무엇을 기준으로 자신의 위치와 크기를 표현할까요?
- Frame: SuperView, bounds: 자기 자신
### 언제 Bounds를 사용하고 언제 Frame 사용할까요?
- Frame: 뷰의 위치와 크기를 설정하거나 부모 뷰 내에서 뷰의 위치를 조정할 때
- Bounds: 뷰 내에서 하위뷰의 위치와 크기를 조절할 때 / UIScrollView

<br />

## Reference
- [Apple Developer Documentation: Frame](https://developer.apple.com/documentation/uikit/uiview/1622621-frame)
- [Apple Developer Documentation: Bounds](https://developer.apple.com/documentation/uikit/uiview/1622580-bounds)
- [Apple Developer Documentation: CGRect](https://developer.apple.com/documentation/corefoundation/cgrect)
- [Apple Developer Documentation: CGPoint](https://developer.apple.com/documentation/corefoundation/cgpoint)
- [Apple Developer Documentation: CGSize](https://developer.apple.com/documentation/corefoundation/cgsize)
