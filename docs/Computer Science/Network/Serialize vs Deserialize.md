---
layout: default
title: Serialize vs Deserialize
parent: Network
grand_parent: Computer Science
nav_order: 1
---

# Serialize vs Deserialize
{: .no_toc }

---
C# 네트워크 에서 json 파일을 처리할 때 사용하던 직렬화, 역직렬화에 대해 알아보았습니다.
- TOC
{:toc}

---

## 직렬화(Serialize)

  **메모리에 저장되어 있는 추상적인 객체나 데이터 구조를 물리적으로 디스크에 저장하거나 네트워크 통신으로 전송하기 위해 스트링이나 바이너리 형식으로 변환하는 것을**말합니다.

## 역직렬화(Deserialize)

스트링이나 바이너리 형식의 파일로 **디스크에 저장된 데이터나 네트워크 통신으로 받은 데이터를 사용할 수 있도록 다시 객체나 데이터 구조로 변환하는 과정**입니다.

## 직렬화 하는 이유

- 데이터를 디스크에 저장하는 경우 참조 타입 데이터는 가능하지 않고 값 타입 데이터만 가능합니다. 그 이유는 프로세스가 정상적으로 종료될 때 프로세스 내에서 할당된 모든 메모리는 해제되고 프로그램이 새로 실행될 때마다 데이터를 할당하는 메모리 주소가 다르기 때문에 이전에 가지고 있던 주소 값으로는 기존의 데이터를 찾을 수 없습니다. 또한 다른 기기로 데이터를 전송하는 경우 각각의 기기마다 사용하고 있는 메모리 공간 주소가 전혀 다르기 때문에 데이터를 찾을 수 없습니다.

- 데이터를 네트워크 통신으로 전송하는 데에도 역시 참조 타입 데이터는 가능하지 않고 값 타입 데이터만 가능합니다. 다른 플랫폼이나 기기로 데이터를 전송하는 경우, 각각의 기기마다 사용하고 있는 메모리 공간 주소가 전혀 다르기 때문에 데이터를 찾을 수 없습니다.

- string 이 포인터로 구현되어있는 경우, 내부적으로 메모리가 연속적으로 할당 되어있지 않기 때문에 이 메모리 데이터를 직렬화(연속적으로 배치 및 값 타입으로 변조)하는 것이 필요하다.