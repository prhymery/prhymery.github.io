---
layout: default
title: MonoBehaviour
parent: Unity
nav_order: 1
---

{: .no_toc }

---
C# 코드를 생성하면서 수도 없이 봐왔던 MonoBehaviour에 대해 정리해보았습니다.
<details><summary>참고 이미지</summary>
<div markdown="1">
![](/assets/images/MonoBehaviour/MonoBehaviour.png)
_Derive from monobehaviour_
{: .text-center }
</div></details>
---
- TOC
{:toc}
---

## 모든 Unity 스크립트가 상속받는 기본 클래스

Unity 에디터에서 C# 스크립트를 생성하면 MonoBehaviour를 자동으로 상속 받습니다.<br>
(MonoBehaviour의 상속관계는 MonoBehaviour -> Behaviour -> Component -> Object 입니다)
MonoBehaviour가 제공하는 이벤트 함수를 사용하지 않거나 게임오브젝트의 컴포넌트로 추가할 필요가 없는 클래스인 경우 MonoBehaviour를 상속받지 않고 사용할 수 있습니다.

<br>![](/assets/images/MonoBehaviour/NewBehaviourScript.png)<br>
_Unity 에디터에서 C# 스크립트 생성시 기본으로 설정되는 스크립트 이름 'NewBehaviourScript'_
{: .text-center }

## 게임 오브젝트에 스크립트를 연결할 수 있는 프레임워크를 제공

생성한 스크립트를 게임오브젝트에 컴포넌트로 추가하려면, 스크립트에 MonoBehaviour를 상속받은 클래스가 하나 이상 포함되어 있어야합니다.
MonoBehaviour를 상속받지 않는 클래스만으로 이루어진 스크립트의 경우에는 게임 오브젝트에 컴포넌트로 추가할 수 없습니다.

<br>![](/assets/images/MonoBehaviour/WithoutMonoBehaviour.png)<br>
_MonoBehaviour를 상속받은 클래스가 없는 스크립트를 게임오브젝트 컴포넌트로 추가하려고 할 때 나타나는 경고_
{: .text-center }

## 유니티 템플릿 스크립트를 제공

MonoBehaviour의 템플릿 스크립트는 개발자가 게임오브젝트에 추가할 수 있는 스크립트를 쉽게 작성할 수 있도록 기본적인 구조와 기능이 들어있는 스크립트입니다.
Unity에서 특정 시점(ex `Awake()`{: .text-green-000 }, `Update()`{: .text-green-000 })이나 이벤트가 일어날 때(ex `OnTriggerEnter()`{: .text-green-000 }) 자동으로 호출되는 합수 등을 제공합니다.

### 코루틴

코루틴은 Unity에서 사용되는 특별한 타입의 함수로 메인 스레드를 중지시키거나 게임을 중단하지 않고 여러 프레임에 걸쳐서 코드가 동작할 수 있도록 해주는 기능입니다. 네트워크 통신이나 애니메이션 등 여러 프레임에 걸쳐 실행되어야하는 작업에 사용됩니다.

### Unity 라이프사이클 함수

Unity에서 C# 스크립트를 생성하였을 때 자동으로 `Start()`{: .text-green-000 }, `Update()`{: .text-green-000 } 함수가 생성됩니다.
이 함수를 비어있는 채로 두었을 때, 그 수가 많아진다면 성능 저하를 초래할 수 있기 때문에 사용하지 않는다면 지워주는 것이 좋습니다.

## 컴포넌트 기능 제공

### Instance 생성

MonoBehaviour를 상속받은 클래스의 instance를 생성할 때 new 키워드로 생성하지 않고 새로운 게임오브젝트를 만들거나 기존에 존재하는 게임오브젝트에 컴포넌트를 추가하는 방식으로 instance를 생성합니다.
MonoBehaviour를 상속받은 클래스가 정상동작하기 위해서는 게임오브젝트에 컴포넌트로 추가되어야 하기 때문입니다.

### MonoBehaviour 체크박스

Unity Inspector 창애서 컴포넌트 이름 왼쪽에 체크박스가 있는 경우가 있습니다.<br>
컴포넌트의 클래스가 MonoBehaviour를 상속받은 클래스이고 아래의 함수 중 하나를 사용하고 있다면 체크박스가 표시됩니다.<br>
`Start()`{: .text-green-000 }, `Update()`{: .text-green-000 }, `FixedUpdate()`{: .text-green-000 }, `LateUpdate()`{: .text-green-000 }, `OnGUI()`{: .text-green-000 }, `OnDisable()`{: .text-green-000 }, `OnEnable()`{: .text-green-000 }<br>
체크박스 활성화 여부에 따라 MonoBehaviour가 활성화, 비활성화됩니다.

<br>![](/assets/images/MonoBehaviour/MonoBehaviorCheckBox.png)<br>
_MonoBehavior CheckBox_
{: .text-center }

<!-- ### null-conditional operator (**?.**) 과 the null-coalescing operator (**??**)을 지원하지 않음

C#에서 사용가능한 null-conditional operator (**?.**) 과 the null-coalescing operator (**??**)을 지원하지 않습니다.

```c#
// person.Name 에 접근하기 전에 person 이 null 일 경우 Name 에 접근하지 않고 null 을 반환
string name = person?.Name; 
// person?.Name이 null 일 경우 기본값으로 'Unknown'을 반환
string name = person?Name ?? "Unknown"; 
```

Unity의 경우  -->

