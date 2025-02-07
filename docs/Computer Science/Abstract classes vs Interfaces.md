---
layout: default
title: Abstract classes vs Interfaces
parent: Computer Science
nav_order: 3
---

# <b>Abstract classes vs Interfaces</b>
{: .no_toc }

---
용도에 대해 자주 헷갈리는 추상클래스와 인터페이스를 정리해보았습니다.
- TOC
{:toc}
## Abstract classes

단독으로 생성될 수 없고 다른 클래스에 상속하기 위한 클래스입니다.<br>
구현되지 않은 추상 메서드와 구현된 메서드를 가질 수 있습니다.<br>
공유할 코드나 구현부를 하위 클래스에 상속해야하는 경우에 사용합니다.<br>
하위 클래스에서 상속받은 구현부를 사용하지 않을 수 있습니다.

## Interfaces

인터페이스는 상속받은 하위 클래스가 따라야 할 계약을 정의합니다.<br>
인터페이스를 상속받은 하위 클래스는 상속받은 모든 멤버를 구현해야 합니다.<br>
상속이 깔끔하게 맞아 떨어지지 않는 경우(여러 클래스의 특성을 상속 받아야 하거나, 특정 부모 클래스의 멤버, 필드 및 메서드를 일부만 사용하는 경우)에 유연하게 적용이 가능합니다.

## Abstract classes, Interfaces 비교

||Abstract classes|Interfaces|
|멤버|필드, 생성자, 구현 메서드|메서드 시그니처, 프로퍼티, 이벤트, 인덱서|
|메서드 구현|전체 혹은 일부 구현|메서드 구현 불가|
|Static 멤버|가질 수 있음|선언하거나 가질 수 없음|
|생성자|사용 가능|사용 불가|
|접근 한정자|모든 접근 한정자 사용가능|모든 멤버는 암묵적으로 public|
|상속|단일 추상상 클래스 상속만 가능|다중 인터페이스 상속 가능|

참고 자료 - [Level up your code with game programming patterns](https://resources.unity.com/games/level-up-your-code-with-game-programming-patterns)
