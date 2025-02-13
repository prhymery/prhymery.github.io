---
layout: default
title: WebSocket
parent: Network
grand_parent: Computer Science
nav_order: 1
---

---
- TOC
{:toc}

---

## 정의

단일 TCP(Transmission Control Protocol) 연결을 이용하여 동시에 양방향 통신 채널을 제공하는 컴퓨터 통신 프로토콜입니다.<br>
서버와 클라이언트 간에 전이중 통신 방식, 양방향성, 연결 지속성을 제공합니다.<br>
request-response 기반인 HTTP 와는 다르게 반복적인 새로운 연결 없이 실시간 데이터 교환이 가능합니다.

<details close><summary>WebSocket diagrams</summary><div markdown="1">

![img-description](/assets/images/WebSocket/WebSocketDiagram.png)<br>
_[WebSocket diagram](<https://en.wikipedia.org/wiki/WebSocket#:~:text=WebSocket%20is%20a%20computer%20communications,as%20RFC%206455%20in%202011.>)_
{: .text-center }

![img-description](/assets/images/WebSocket/WebSockets.png)<br>
_[WebSockets](<https://blog.algomaster.io/p/websockets>)_
{: .text-center }

</div></details>


<details close><summary>HTTP vs WebSocket</summary><div markdown="1">

![img-description](/assets/images/WebSocket/HTTPvsWebSocket_01.png)<br>
_[HTTP vs WebSocket](<https://www.scaleway.com/en/blog/iot-hub-what-use-case-for-websockets/>)_
{: .text-center }

![img-description](/assets/images/WebSocket/HTTPvsWebSocket_02.png)<br>
_[HTTP vs WebSocket](<https://websocket.org/guides/road-to-websockets/>)_
{: .text-center }

![img-description](/assets/images/WebSocket/HTTPvsWebSockets.png)<br>
_[HTTP vs WebSockets](<https://www.linkedin.com/posts/kiran-s-38ba9227a_lets-talk-http-vs-websockets-http-1-activity-7094313329589948416-fOju>)_
{: .text-center }

![img-description](/assets/images/WebSocket/WebSocketvsHTTPConnection.png)<br>
_[WebSocket vs HTTP Connection](<https://apidog.com/blog/what-is-websocket-and-how-it-works/>)_
{: .text-center }

</div></details>

## 특징

### 전이중 통신 방식(Full-Duplex)
클라이언트와 서버가 동시에 데이터를 주고 받을 수 있습니다.

### 연결 지속성(Persistent connection)
하나의 연결이 유지되어 오버헤드를 줄임
- 반복적으로 새로운 연결 생성 없이 실시간으로 데이터를 교환합니다.

### 낮은 지연(Low latency)
온라인 게임, 채팅 등 실시간 데이터 업데이트에 이상적입니다.

### 이벤트 주도 방식(Event-Driven)
polling 대신 listener 를 이용해서 메세지를 받습니다.<br>
<h5><i>HTTP Polling : 정기적으로 서버에 request 를 보내어 업데이트를 확인합니다.</i></h5>

### 효과적인 데이터 전송(Efficient data transfer)
HTTP에 비해 대역폭 사용이 적습니다.<br>

## 작동 원리

### Handshake
클라이언트가 서버에 Websocket 연결 개시를 위한 HTTP request(Upgrade) 를 보냅니다.<br>
<h5><i>webSocket 이 HTTP와의 호환성을 갖도록 설계되어있어서 호환성 확보를 위해 WebSocket hanshake 에서 HTTP Upgrade header 를 사용하여 HTTP → WebSocket 프로토콜로 전환합니다.</i></h5>

### Upgrade
서버가 Websocket 을 지원하면 Websocket 으로 업그레이드 됩니다.

### Data exchange
연결이 성공하면 클라이언트와 서버는 메세지를 이용해 실시간으로 데이터를 교환할 수 있습니다.

## Protocol

### Opening handshake
HTTP request + HTTP response 로 연결을 설정합니다.<br>
클라이언트가 HTTP request 를 보내면 서버가 HTTP response 로 success 에 status code 101 (Switching Protocols) 를 보냅니다.<br>
handshake 가 HTTP 와 호환이 가능하기 때문에 WebSocket 서버가 HTTP (80), HTTPS (443) 포트를 사용할 수 있습니다.<br>
한번 연결이 설정되면 통신은 HTTP 프로토콜을 따르지 않는 binary frame-based protocol 로 전환됩니다.<br>

### Frame-based message
Opening handshake 이후 클라이언트와 서버는 언제라도 서로에게 데이터 메세지(text, binary)나 컨트롤 메세지(close, ping, pong)를 보낼 수 있습니다.<br>
하나의 메세지는 한 개 이상의 frame 으로 구성됩니다.<br>
단편화(fragmentation)를 통해 하나의 메세지를 두 개 이상의 프레임으로 나누어 전송하므로써
- 메모리 오버헤드를 줄이고<br>
(전체 메세지에 대한 버퍼 대신 해당 프레임에 대한 버퍼만 있으면 됩니다)
- 데이터 신뢰성을 높이며<br>
(프레임이 소실되었을 때 전체 프레임이 아닌 해당 프레임만 다시 보내면 됩니다)
- 메세지 다중화가 가눙합니다.<br>
(동일 연결 상에서 하나의 거대한 메세지가 다른 메세지를 막는 것을 방지합니다)

### 주요 Opcodes (Operaction codes)
- Close
    - Closing handshake 를 시작할 때 보냅니다.
    - TCP closing handshake 를 보완하여 데이터 손실을 방지할 수 있습니다.
    - Close frame 이후에는 frame 을 보낼 수 없습니다.
- Ping, Pong
    - latency 측정 및 keepalive, heartbeat 에 사용됩니다.
    - ping 을 받은 즉시 pong 을 보내야 합니다.
    - ping 을 보내지 않고 pong 을 받은 경우에 pong 은 무시됩니다.

<h5><i>Keepalive - 하나의 기기와 다른 기기가 연결되어 있는지 확인하기 위한 메세지<br>
Heartbeat - 하드웨어나 소프트웨어가 생성하는 주기적인 신호로, 정상적인 작동을 나타냄</i></h5>