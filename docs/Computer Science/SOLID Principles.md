---
layout: default
title: SOLID Principles
parent: Computer Science
nav_order: 2
---

# <b>SOLID Principle</b>
{: .no_toc }

---

- TOC
{:toc}

---

## SOLID

**객체 지향 프로그래밍 및 설계(Object-Oriented Design, OOD) 기본 원칙 다섯가지의 앞을 자를 따서 만든 용어**입니다.<br>
이해하기 쉽고 유지 관리하기 쉬운 유연하며 변화에 탄력적인 모듈 방식의 소프트웨어 디자인 가이드입니다.<br>
프로그래머는 SOLID 윈칙을 적용하여 **시간 경과에 따른 요구사항의 변화에 더 강력하고 테스트 가능하며 적응가능한 코드를 작성**할 수 있습니다.

---

## S(단일 책임 원칙, Single Responsibility Principle, SRP)

**하나의 클래스는 하나의 책임만 가져야 합니다.**<br>
클래스나 모듈이 특정한 작업 및 책임에 초점이 맞춰지기 때문에 높은 응집도를 가지게 됩니다.
클래스에 대한 이해와 테스트, 유지보수를 쉽게 해줍니다.

### SRP 적용시 고려사항
{: .no_toc }

- **Readability**<br>
적은 양의 클래스는 읽기 쉽습니다.<br>
대부분의 개발자들이 200~300자 정도의 클래스를 추천합니다.<br>
- **Extensibility**<br>
소규모 클래스로부터 상속 받는 것이 의도하지 않은 오류의 위험성을 피할 수 있습니다.<br>
- **Reusability**<br>
클래스의 규모를 작게 모듈화한다면 다른 곳에서 재사용 할 수 있습니다.

<details close><summary>예시</summary><div markdown="1">

### SRP 위반
{: .no_toc }
![img-description](/assets/images/SOLID/without SRP.png)
_플레이어 클래스 안에 여러가지 요소들이 포함되어 있다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
public class UnrefactoredPlayer : MonoBehaviour
{
    [SerializeField] private string inputAxisName;
    [SerializeField] private float positionMultiplier;
    private float yPosition;
    private AudioSource bounceSfx;
    
    private void Start()
    {
        bounceSfx = GetComponent<AudioSource>();
    }
    
    private void Update()
    {
        float delta = Input.GetAxis(inputAxisName) *Time.deltaTime;
        yPosition = Mathf.Clamp(yPosition + delta, -1, 1);
        transform.position = new Vector3(transform.position.x, yPosition* positionMultiplier, transform.position.z);
    }
    
    private void OnTriggerEnter(Collider other)
    {
        bounceSfx.Play();
    }
}
```

</div></details>

### SRP 적용
{: .no_toc }
![img-description](/assets/images/SOLID/with SRP.png)
_플레이어 클래스에서 분리된 각각의 클래스를 플레이어 클래스가 참조하고 있다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
[RequireComponent(typeof(PlayerAudio), typeof(PlayerInput), typeof(PlayerMovement))]
public class Player : MonoBehaviour
{
    [SerializeField] private PlayerAudio playerAudio;
    [SerializeField] private PlayerInput playerInput;
    [SerializeField] private PlayerMovement playerMovement;
    
    private void Start()
    {
        playerAudio = GetComponent<PlayerAudio>();
        playerInput = GetComponent<PlayerInput>();
        playerMovement = GetComponent<PlayerMovement>();
    }
}
```

```c#
public class PlayerAudio : MonoBehaviour
{
}
```

```c#
public class PlayerInput : MonoBehaviour
{
}
```

```c#
public class PlayerMovement : MonoBehaviour
{
}
```

</div></details>

</div></details>

---

## O(개방 폐쇄 원칙, Open/Closed Principle, OCP)

**소프트웨어 요소(클래스, 모둘, 함수 등)는 확장에는 열려있으나 변경에는 닫혀 있어야 합니다.**<br>
**기존에 정상 동작하고 있는 코드의 수정 없이 클래스의 기능을 확장할 수 있어야 합니다.**<br>
클래스의 기존 코드 변경 없이 새로운 기능을 추가하거나 확장시킬 수 있어야 합니다.<br>
기존 코드가 변경되지 않기 때문에 새로운 코드를 추가했을 때 오류 발생시 새로운 코드 부분만 확인하면 되므로 디버깅이 쉬워집니다.
인터페이스, 추상 클래스, 다형성을 사용하여 해당 원칙을 적용합니다.

<details close><summary>예시</summary><div markdown="1">

### OCP 위반
{: .no_toc }
![img-description](/assets/images/SOLID/without OCP.png)
_새로운 도형을 추가할 때마다 기존 코드인 AreaCalculator 에<br> Get도형Area 메소드를 추가해 주어야한다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
public class AreaCalculator
{
    public float GetRectangleArea(Rectangle rectangle)
    {
        return rectangle.width * rectangle.height;
    }
    
    public float GetCircleArea(Circle circle)
    {
        return circle.radius * circle.radius * Mathf.PI;
    }
}
```

```c#
public class Rectangle
{
    public float width;
    public float height;
}
```

```c#
public class Circle
{
    public float radius;
}
```

</div></details>

### OCP 적용
{: .no_toc }
![img-description](/assets/images/SOLID/with OCP.png)
_새로운 도형을 추가할 때마다 추가할 도형 클래스에 CalculateArea 메소드를 구현하면 된다_
{: .text-center }
<details close><summary>코드</summary><div markdown="1">

```c#
public abstract class Shape
{
    public abstract float CalculateArea();
}
```

```c#
public class Rectangle : Shape
{
    public float width;
    public float height;
    
    public override float CalculateArea()
    {
        return width * height;
    }
}
```

```c#
public class Circle : Shape
{
    public float radius;
    
    public override float CalculateArea()
    {
        return radius * radius * Mathf.PI;
    }
}
```

</div></details>

</div></details>

---

## L(리스코프 치환 원칙, Liskov Substitution Principle, LSP)

**하위 클래스는 상위 클래스를 대체할 수 있어야 합니다.**<br>
하위 클래스에서 어떠한 변경 없이도 상위 클래스의 코드가 정상 동작하여야 합니다.

### LSP 적용시 고려사항
{: .no_toc }

- **하위 클래스에서 기능을 제거하는 경우 LSP 위반일 가능성이 있습니다.**<br>
하위 클래스에서 메소드를 구현하지 않고 비워두어 오류가 발생하지 않아도 LSP 를 위반하는 것입니다.
- **추상화는 단순하게 유지되어야 합니다.**<br>
베이스 클래스에는 오직 하위 클래스가 종속받는 공통 기능만 정의되어 있어야합니다.
- **하위 클래스는 베이스 클래스의 public 멤버와 동일한 public 멤버를 가져야 합니다.**<br>
상위 클래스와 동일한 public 멤버는 하위 클래스에서 같은 시그니쳐를 가지고 동일한 동작을 수행해야합니다.
- **계층구조보다 클래스 간의 상호작용을 고려하여야 합니다.**<br>
현실세계의 계층구조와 다를지라도 클래스의 계층구조에 맞게 설계해야 됩니다.(아래의 예시 참고)
- **상속보다 인터페이스를 생각해야 합니다.**<br>
상속을 통해 넘겨받는 것보다 인터페이스로 분리된 기능을 만들어 조합하는 것이 더 다채로운 구현이 가능합니다.
<details close><summary>예시</summary><div markdown="1">

### LSP 위반
{: .no_toc }
![img-description](/assets/images/SOLID/without LSP.png)
_기차의 경우 좌우로 움직일 수 없기에 빨간색으로 표시된 메소드는 아무런 기능을 수행하지 않는다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
public class Vehicle
{
    public float speed = 100;
    public Vector3 direction;
    
    public void GoForward()
    {
    }
    
    public void Reverse()
    {
    }
    
    public void TurnRight()
    {
    }
    
    public void TurnLeft()
    {
    }
}
```

```c#
public class Navigator
{
    public void Move(Vehicle vehicle)
    {
        vehicle.GoForward();
        vehicle.TurnLeft();
        vehicle.GoForward();
        vehicle.TurnRight();
        vehicle.GoForward();
    }
}
```

</div></details>

### LSP 적용
{: .no_toc }
![img-description](/assets/images/SOLID/with LSP.png)
_부모 클래스를 세분화하고 인터페이스를 사용하여 LSP 를 적용하였다_
{: .text-center }
<details close><summary>코드</summary><div markdown="1">

```c#
public interface ITurnable
{
    public void TurnRight();
    public void TurnLeft();
}
```

```c#
public interface IMovable
{
    public void GoForward();
    public void Reverse();
}
```

```c#
public class RoadVehicle : IMovable, ITurnable
{
    public float speed = 100f;
    public float turnSpeed = 5f;
    
    public virtual void GoForward()
    {
    }
    
    public virtual void Reverse()
    {
    }
    
    public virtual void TurnLeft()
    {
    }
    
    public virtual void TurnRight()
    {
    }
}
```

```c#
public class RailVehicle : IMovable
{
    public float speed = 100;
    
    public virtual void GoForward()
    {
    }
    
    public virtual void Reverse()
    {
    }
}
```

```c#
public class Car : RoadVehicle
{
}
```

```c#
public class Train : RailVehicle
{
}
```
</div></details>

</div></details>

---

## I(인터페이스 분리 원칙, Interface Segregation Principle, ISP)

**클라이언트가 사용하지 않는 메소드에 의존하도록 강요 받으면 안됩니다.**<br>
**클라이언트가 필요한 메소드만 구현할 수 있게 인터페이스를 간결하게 유지해야 합니다.**<br>
인터페이스는 최대한 구체적으로 세분화되어 설계되어야 합니다.
즉, 클라이언트의 특정 요구 사항에 맞게 간소화된 인터페이스를 사용하는 것이 좋습니다.<br>
ISP 는 시스템을 분리하고 수정과 재배포를 용이하게 도와줍니다.

<details close><summary>예시</summary><div markdown="1">

### ISP 위반
{: .no_toc }

<details close><summary>코드</summary><div markdown="1">

```c#
public interface IUnitStats
{
    public float Health { get; set; }
    public int Defense { get; set; }
    public void Die();
    public void TakeDamage();
    public void RestoreHealth();
    public float MoveSpeed { get; set; }
    public float Acceleration { get; set; }
    public void GoForward();
    public void Reverse();
    public void TurnLeft();
    public void TurnRight();
    public int Strength { get; set; }
    public int Dexterity { get; set; }
    public int Endurance { get; set; }
}
```

</div></details>

### ISP 적용
{: .no_toc }
![img-description](/assets/images/SOLID/with ISP.png)
_인터페이스를 세분화하여 불필요한 오버헤드를 줄이고 클래스를 다양한 방식으로 구성할 수 있다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
public interface IMovable
{
    public float MoveSpeed { get; set; }
    public float Acceleration { get; set; }
    public void GoForward();
    public void Reverse();
    public void TurnLeft();
    public void TurnRight();
}
```

```c#
public interface IDamageable
{
    public float Health { get; set; }
    public int Defense { get; set; }
    public void Die();
    public void TakeDamage();
    public void RestoreHealth();
}
```

```c#
public interface IUnitStats
{
    public int Strength { get; set; }
    public int Dexterity { get; set; }
    public int Endurance { get; set; }
}
```

```c#
public interface IExplodable
{
    public float Mass { get; set; }
    public float ExplosiveForce { get; set; }
    public float FuseDelay { get; set; }
    public void Explode();
}
```

```c#
public class ExplodingBarrel : MonoBehaviour, IDamageable, IExplodable
{
}
```

```c#
public class EnemyUnit : MonoBehaviour, IDamageable, IMovable, IUnitStats
{
}
```

</div></details>

</div></details>

---

## D(의존관계 역전 원칙, Dependency Inversion Principle, DIP)

**고수준의 모듈은 저수준의 모듈에 의존하지 않아야 하고, 두 모듈 다 추상화에 의존해야 합니다.**<br>
**하나 이상의 구체적인 클래스에 의존하지 말고, 추상화에 의존해야 합니다.**<br>
종속성을 줄여 느슨한 결합도를 가지게 되므로 확장에 유리합니다.
모듈이 특정한 구현이 아닌 추상화에 의존해야 해당 모듈의 구현을 변경할 때 의존 관계에 있는 다른 모듈에게 영향을 주지 않습니다.<br>
즉, 의존 관계에 있는 다른 모듈에 영향을 주지 않기 위해 각각의 모듈은 특정한 구현이 아닌 추상화에 의존해야 합니다.

<details close><summary>예시</summary><div markdown="1">

### DIP 위반
{: .no_toc }
![img-description](/assets/images/SOLID/without DIP.png)
_Switch 클래스가 Door 클래스에 대한 의존성이 커서 다른 클래스에 스위치를 재사용하기 힘들다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
public class Switch : MonoBehaviour
{
    public Door door;
    public bool isActivated;
    
    public void Toggle()
    {
        if (isActivated)
        {
            isActivated = false;
            door.Close();
        }
        else
        {
            isActivated = true;
            door.Open();
        }
    }
}
```

```c#
public class Door : MonoBehaviour
{
    public void Open()
    {
       Debug.Log("The door is open.");
    }
    public void Close()
    {
       Debug.Log("The door is closed.");
    }
}
```

</div></details>

### DIP 적용
{: .no_toc }
![img-description](/assets/images/SOLID/with DIP.png)
_Switch 클래스의 의존성이 기존 구체적 클래스인 Door에서<br> 추상적 인터페이스인 ISwitchable 로 옮겨가게 되면서 의존성이 역전되었다_
{: .text-center }

<details close><summary>코드</summary><div markdown="1">

```c#
public interface ISwitchable
{
    public bool IsActive { get; }
    public void Activate();
    public void Deactivate();
}
```

```c#
public class Switch : MonoBehaviour
{
    public ISwitchable client;
    
    public void Toggle()
    {
        if (client.IsActive)
        {
            client.Deactivate();
        }
        else
        {
            client.Activate();
        }
    }
}
```

```c#
public class Door : MonoBehaviour, ISwitchable
{
    private bool isActive;
    public bool IsActive => isActive;
    
    public void Activate()
    {
        isActive = true;
        Debug.Log("The door is open.");
    }
    
    public void Deactivate()
    {
        isActive = false;
        Debug.Log("The door is closed.");
    }
}
```

</div></details>

![img-description](/assets/images/SOLID/with DIP2.png)
_DIP 적용으로 Switch 클래스의 재사용이 가능해졌다_
{: .text-center }

</div></details>

참고 자료 - [Level up your code with game programming patterns](https://resources.unity.com/games/level-up-your-code-with-game-programming-patterns)