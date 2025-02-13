---
layout: default
title: Mono vs IL2CPP
parent: Unity
nav_order: 1
---

{: .no_toc }

---
Unity 프로젝트 설정 중 하나인 Mono와 IL2CPP에 대해 찾아보았습니다.
<details><summary>참고 이미지</summary>
<div markdown="1">
![](/assets/images/ScriptingBackend/ScriptingBackend.png)
_Unity/Project Settings/Player/Scripting Backend_
{: .text-center }
</div></details>
---
- TOC
{:toc}
---

## Scripting Backend

Unity에서 스크립팅을 지원하는 프레임워크입니다.<br>
개발자가 작성한 코드를 컴파일하고 실행하는데 사용되는 기술을 말합니다.

---

## Mono

개발자가 **Cross-platform 앱을 쉽게 만들 수 있도록 설계된 소프트웨어 플랫폼**입니다.<br>
Micorosoft가 후원하는 오픈 소스로 .NET Framework의 implementation입니다.
일반적으로는 **JIT(J**ust-**I**n-**T**ime)[^JIT] 컴파일러에서 사용되지만 **AOT(A**head-**O**f-**T**ime)[^AOT] 컴파일러도 지원합니다.

### Unity 에서의 Mono

Unity는 오픈 소스인 **Mono 프로젝트의 포크를 사용**합니다.<br>
(오픈 소스 Mono와는 다르게 게임 개발에 맞게 최적화된 부분이 있고 JIT 컴파일러만 지원하는 것 같습니다)

C#으로 작성된 스크립트가 IL(**I**ntermediate **L**anguage)코드로 컴파일된 후 Momo 런타임 환경에서 실행됩니다.
Mono 런타임은 IL코드를 실행하고 메모리 관리, 가비지 콜렉터, 스레드 같은 기능이 있는 VM(**V**irtual **M**achine)을 제공합니다.

Mono 스크립팅 백엔드는 JIT 컴파일을 사용하여 런타임 시점에 요청 시 코드를 컴파일합니다.<br>
플랫폼이 JIT과 Mono를 지원하고 AOT도 지원하는 경우 Mono가 기본값입니다.<br>
Unity Editor 에서는 빠른 실행을 위해 Mono를 사용합니다.<br>
AOT 컴파일을 지원하지 않는 플랫폼에 적합합니다.

---

## IL2CPP

Unity에서 개발한 방식으로 다양한 플랫폼에서 Unity 앱의 성능을 개선하였습니다.<br>
**IL**(**I**ntermediate **L**anguage) **2**(to) **CPP**(C++)의 약자로 MSIL(**M**icro**S**oft **IL**)을 C++ 코드로 전환하고, 타겟 플랫폼에서 직접 실행될 수 있는 적합한 네이티브 바이너리 파일로 컴파일합니다.

AOT 컴파일을 사용하며 실행 전에 전체 애플리케이션을 컴파일합니다.<br>
Mono나 JIT 컴파일을 지원하지 않는 플랫폼에 적합합니다.(일부 플랫폼은 런타임 코드 생성을 지원하지 않아 타겟 디바이스에서 JIT 컴파일에 의존하는 일부 관리 코드가 작동하지 않습니다)

### IL2CPP의 장점

- IL 코드를 사용할 수 있는(.NET Framework나 Mono 런타임 환경을 지원하는) 플랫폼보다 C++ 코드를 지원하는 플랫폼이 더 많기 때문에 다양한 플랫폼을 지원할 수 있습니다.<br>
- 타겟 플랫폼에 최적화된 C++ 코드를 생성하기 때문에 VM에서 IL 코드를 실행하는 것보다 성능이 향상됩니다.<br>
- IL 코드 대신 역설계(Reverse-engineering)하기 어려운 컴파일된 C++로 대체하여 보안성을 개선하였습니다.

---

## Mono 와 IL2CPP 비교

**Mono - JIT 컴파일을 사용**하여 **런타임 시점에 요청 시 코드를 컴파일**합니다.<br>
**IL2CPP - AOT 컴파일을 사용**하여 **실행 전에 전체 애플리케이션을 컴파일**합니다.<br>
일반적으로 **Mono가 사용하기 쉽고, 컴파일 시간이 빠르기 때문에 대부분의 프로젝트에서 권장**되고, **IL2CPP는 최대 성능이 필요한 고성능 프로젝트에 더 적합**합니다.

[^JIT]: JIT(**J**ust-**I**n-**T**ime) : 프로그램에서 코드가 실제 실행하는 시점(just before it is executed)에 기계어로 번역하는 컴파일 기법입니다. 동적 번역(Dynamic translation), 런타임 컴파일(Run-time compilations)으로도 불립니다.
[^AOT]: AOT(**A**head-**O**f-**T**ime) : 런타임 시 수행해야 할 작업량을 줄이기 위해 미리(Ahead of time) 빌드 타임에서 컴파일하는 기법입니다.

||Mono|IL2CPP|
|:-|:-|:-|
|Compiler|JIT|AOT|
|Performance|Slower|Faster|
|Security|Weaker|Better|
|Memory footprint|more|less|
|Build times|Faster|Slower|
|Build file size|less|more|

---