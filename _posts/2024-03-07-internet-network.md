---
title: "HTTP 개념 정리(1) - 인터넷 네트워크"
excerpt: "IP, TCP, UDP, PORT, DNS 개념 설명"

categories:
  - Etc
tags:
  - [IP, TCP, UDP, PORT, DNS]
sidebar:
  nav: "counts"
---

## IP

메시지 전달할 때 인터넷 망을 통해서 데이터 전송함.

이 인터넷 망은 굉장히 복잡하게 되어있음.

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/b985b3e8-ec80-44dd-8fc7-cd41e52393d1" width="80%" height="auto" />
</div>

이 때 IP 주소라는 것을 부여해서 출발지와 목적지를 알아내서 원하는 곳에 데이터를 보낼 수 있다.

이 때 패킷이라는 통신 단위로 데이터를 전달하게 된다.

패킷에다가 여러가지 정보를 넣어서 전송하게 된다.

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/9acb7b0b-479a-4df4-be8f-64c9d8ca02a2" width="80%" height="auto" />
</div>

전송 과정에서 여러가지 문제가 발생할 수 있다.

1. **비연결성**

   받을 대상이 존재하지 않아도 일단 무작정 패킷을 보낸다.

2. **비신뢰성**

   패킷이 가는 도중에 소실 될 위험이 존재한다.

   <div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/5220e888-b926-4c82-93df-95edb181bea4" width="80%" height="auto" />
    </div>
    
    그리고 패킷이 전달되는 순서가 꼬일 수 있다. 1번 패킷, 2번 패킷 순으로 도착해야하는데 2번 패킷, 1번 패킷 순으로 꼬여서 전달될 수 있다.

   <div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/b298219c-b5b2-44cd-8924-d5d849bf64a7" width="80%" height="auto" />
    </div>
    
    왜냐하면 인터넷 망 내에 노드들끼리 전송될 때 상황을 고려해서 다른 노드로 전송하기 때문에 1번 패킷을 보낸 곳으로 정확히 2번 패킷을 보내지 않는다.

## TCP, UDP

TCP - 전송 제어 프로토콜(Transmission Control Protocol)

UDP - 사용자 데이터그램 프로토콜(User Datagram Protocol)

## TCP/IP

IP 패킷 정보에는 위에서 보다시피 그냥 출발지 IP와 목적지 IP를 작성해서 데이터를 보낸다. 그렇기 때문에 위에서 말한 문제들이 발생할 수 있다.

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/57657a8a-9b31-4c17-8165-93b2d49dd6bf" width="80%" height="auto" />
</div>

이를 해결해주고자 있는것이 TCP이다.

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/800ab541-ac94-4b9d-9cad-577dec699477" width="80%" height="auto" />
</div>

위 그림은 TCP/IP 패킷 정보이다. 기존 IP와는 다르게 TCP 세그먼트가 감싸져있다. TCP 세그먼트를 살펴보면 출발지 PORT, 목적지 PORT, 전송 제어, 순서 등의 정보들이 들어가 있다.

### TCP의 특징

1. **연결 지향 - TCP 3way handshake**

   <div align="center">
       <img src="https://github.com/dongdong8343/algorithm/assets/93115530/96aa40de-e215-4526-a9ed-25b4fc0fca96" width="80%" height="auto" />
   </div>

   연결이 서로 된 것을 확인한 후에 데이터를 주고 받는다. 그래서 목적지에 문제가 발생하면 데이터를 애초에 보내지 않는다.

2. **데이터 전달 보증**

   데이터가 전달된 것을 확인할 수 있고 데이터를 못 받으면 파악 가능하다.

   데이터를 전송하면 받은 쪽에서 잘 받았다고 응답해주기 때문이다.

   <div align="center">
       <img src="https://github.com/dongdong8343/algorithm/assets/93115530/4f0210e8-e616-4d4c-a72e-3ba9628efdc8" width="80%" height="auto" />
   </div>

3. **순서 보장**

   순서가 이상하게 오면 파악 가능하다.

   <div align="center">
       <img src="https://github.com/dongdong8343/algorithm/assets/93115530/2eb25f0b-0fa9-446d-bd6b-d7a7199e76a2" width="80%" height="auto" />
   </div>

## UDP 특징

TCP가 가지고 있는 기능들은 없다. 하지만 TCP가 가진 기능이 없기 때문에 단순하고 빠르다.

### 굳이 믿을만한 TCP 놔두고 UDP를 쓰는 이유

TCP가 가진 기능이 많고 그렇기 때문에 거쳐야하는 작업들이 많다. 따라서 데이터를 전송할 때 많은 시간들이 걸린다. 하지만 UDP는 TCP가 가진 기능이 없기 때문에 단순하고 빠르다.

따라서 신뢰성보다는 연속성, 성능이 중요한 곳에서는 UDP를 사용한다.

### 그럼 UDP랑 IP랑 다를게 뭐지?

TCP에서 내가 더 최적화를 하고 싶은 생각이 들 수도 있다. 하지만 TCP는 이미 다 정의가 되어있기 때문에 내가 기능을 추가하지 못한다. 하지만 UDP를 통해서 내가 원하는 추가 작업을 해서 더 최적화를 할 수 있다.

## PORT

TCP와 UDP에는 PORT라는 것이 추가돼있다.

내가 만약에 게임, 노래, 영상 등의 여러 작업을 한다고 가정하자. 그럼 여러 패킷이 한 IP주소로 오게 된다. 여러 패킷이 오게 되면 뭐가 어떤 패킷인지 파악하기 어렵다.

하지만 PORT를 이용하면 여러 패킷을 각 작업에 맞게 구분할 수 있게 된다.

**같은 IP내에서 프로세스를 구분하기 위해서 PORT를 사용한다.**

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/7f715c7e-12a0-4bf6-9ef9-c4c5132a579d" width="80%" height="auto" />
</div>

게임 : 클라이언트(8090) ↔ 서버(11220)

화상통화 : 클라이언트(21000) ↔ 서버(32202)

웹 브라우저 : 클라이언트(10010) ↔ 서버(80)

위와 같이 같은 IP에서 서로 다른 PORT로 연결함으로써 패킷을 올바른 곳으로 전송할 수 있게 된다.

비유) IP = 아파트, PORT = 아파트 몇 동 몇 호

### **PORT 번호**

- 0 ~ 65535 : 할당 가능
- 0 ~ 1023 : 잘 알려진 포트라 사용하지 않는 것이 좋다.
- FTP : 20, 21 / TELNET : 23 / HTTP : 80 / HTTPS : 443

## DNS - 도메인 네임 시스템(Domain Name System)

### IP의 문제점

1. IP 기억하기 어렵다. ex) 200.200.200.2
2. IP가 바뀔 수도 있다.

### DNS??

전화번호부라고 생각하면 이해하기 쉽다.

홍길동 - 010-1111-1111

우리는 전화번호를 전부 외울 필요없이 홍길동이라는 이름만 찾아서 전화번호를 찾을 수 있다.

이렇듯 DNS를 사용해서 IP주소를 알아낼 수 있다.

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/105614bc-8781-451b-984f-e925270a2306" width="80%" height="auto" />
</div>

DNS 서버에 도메인 명 - IP 주소가 쌍으로 저장되어 있다.

그럼 우리는 도메인 명을 이용해서 IP주소로 접속할 수 있게 된다.

따라서 위에 적은 IP의 문제점들을 해결할 수 있게 된다. 도메인 명을 이용해서 IP를 기억하기 쉽고 IP가 바뀌더라도 바뀐 IP를 수정만 해주면 기존의 도메인 명을 이용해서 접속할 수 있게 된다.

---

- 김영한님의 모든 개발자를 위한 HTTP 웹 기본 지식을 수강하면서 정리한 내용입니다.
