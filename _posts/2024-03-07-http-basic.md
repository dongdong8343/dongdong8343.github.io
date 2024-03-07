---
title: "HTTP 개념 정리(3) - HTTP 기본"
excerpt: "HTTP 특징 설명"

categories:
  - Etc
tags:
  - [HTTP 특징]
sidebar:
  nav: "counts"
---

## 모든 것이 HTTP

- HTTP 메시지에 거의 모든 형태의 데이터 전송 (HTML, TEXT, IMAGE, 음성 등등)
- 서버간에 데이터 주고 받을 때도 HTTP

### HTTP 역사

HTTP 0.9, 1.0, 1.1 , 2, 3이 있는데 1.1을 가장 많이 사용하고 2, 3도 점점 증가

TCP 기반 : HTTP/1.1, HTTP/2 (하는 작업들이 많아서 속도 떨어짐 (3way handshake 등))

UDP 기반 : HTTP/3 (애플리케이션 레벨에서 성능 개선해서 나옴)

## HTTP 특징

1. **클라이언트 서버 구조**

   클라이언트가 요청을 하면 서버가 응답할 때까지 대기하고 응답이 오면 결과 보여준다.

   사실 클라이언트와 서버가 분리되어있다는 사실이 중요하다.

   분리가 돼있어서 클라이언트는 UI, 서버는 데이터, 비즈니스 로직에 집중 가능하다.

   이 말은 각각 독립적으로 진화할 수 있다는 의미다.

2. **무상태 프로토콜(Stateless)**
   - **Stateful**
       <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/9c5c03a0-ea7c-42ea-bc87-93f03a428d3b" width="80%" height="auto" />
       </div>
       
       서버가 클라이언트의 상태를 항상 유지하고 있음. 
       
       즉 중간에 서버가 바뀌면 맥락을 이해하지 못하게 됨.
       
       ⇒ 중간에 다른 서버로 바뀌면 안됨. 바꾸려면 인수인계 하듯이 정보 알려줘야 함.
       
       ⇒ **중간에 요청, 응답을 받는 서버가 장애가 나면 하던 작업 다시 해야함…**

   - **Stateless**
       <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/880fc9db-fab3-42c4-a4df-d1950bdbf6e5" width="80%" height="auto" />
       </div>
       
       서버가 클라이언트의 상태 유지를 안하고 있다.
       
       그럼 맥락을 어떻게 유지하지?
       
       클라이언트가 서버에 데이터를 보낼 때 필요한 데이터를 전부 보낸다. 
       
       (정보 많이 보내는게 단점이 된다.)
       
       ⇒ 중간에 서버 바뀌어도 됨. → 서버 확장성이 높다.(클라이언트가 몰려도 상관 x)

   - **Stateless의 실무 한계**
     모든 것을 무상태로 설계 할 수 있는 경우도 있고 없는 경우도 있다. (케바케)
     ex) 무상태 - 로그인이 필요 없는 화면
     상태 유지 - 로그인 (일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지함.)
     최대한 무상태로 설계하고 상태 유지는 꼭 필요한 경우에만 사용
3. **비연결성**
   - **연결을 유지하는 모델**
       <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/79118fee-769d-4f8f-b7ff-1a26a72531d4" width="80%" height="auto" />
       </div>
       
       계속 연결해야해서 자원이 소모된다.

   - **연결 유지 안하는 모델 - HTTP**
       <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/6cd75fa8-8a17-4fae-b917-617f91197c87" width="80%" height="auto" />
       </div>
       
       필요한 것만 주고 받고 연결 끊는다 
       
       → 최소한의 자원 유지 (서버 자원을 매우 효율적으로 사용할 수 있다.)

   - **비연결성 한계와 극복**
     데이터 주고 받을 때마다 TCP/IP 연결 해야함. → 3 way handshake 시간 추가
     웹 브라우저에서 사이트 요청하면 수많은 자원 다운로드 함.
     초기에는 하나 다운 받을 때마다 연결하고 종료하고를 반복함 → 시간 오래 걸림
       <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/1c7336b0-3398-40d9-b0bb-22971dec5f2d" width="80%" height="auto" />
       </div>
       
       지금은 HTTP 지속 연결(Persistent Connections)로 문제 해결 → HTTP/2, 3에서 더 최적화
       
       데이터 다 받을 때까지 연결 유지함.
       
       <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/e9fcc525-93a0-4dd0-9c33-cc6e2ebc16bc" width="80%" height="auto" />
       </div>

4. **HTTP 메시지**

   <div align="center">
           <img src="https://github.com/dongdong8343/algorithm/assets/93115530/8369fc73-ed3c-4c12-b345-b811732a5a57" width="80%" height="auto" />
       </div>

   - **시작 라인(request-line) - 요청 메시지**
     request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)
     ex) GET /search?q=hello&hl=ko HTTP/1.1
     - method (HTTP 메서드)
       종류 : GET, POST, DELETE, PUT…
     - request-target (요청 대상)
       absolute-path[?query]
     - HTTP-version (HTTP 버전)
   - **시작 라인(status-line) - 응답 메시지**
     status-line = HTTP-version SP status-code SP reason-phrase CRLF
     ex) HTTP/1.1 200 OK
     - HTTP-version (HTTP 버전)
     - status-code (HTTP 상태 코드) : 요청 성공, 실패를 나타냄.
       200 : 성공
       400 : 클라이언트 요청 오류
       500 : 서버 내부 오류
     - reason-phrase (이유 문구) : 사람이 알아볼 수 있게 상태를 나타냄.
   - **HTTP 헤더**
     header-field = field-name ":" OWS field-value OWS (OWS:띄어쓰기 허용)
     ex) Host: [www.google.com](http://www.google.com/)
     ex) Content-Type: text/html;charset=UTF-8
     ex) Content-Length: 3423
     - HTTP 헤더의 용도
       HTTP 전송에 필요한 모든 부가정보 포함
       필요하면 임의의 헤더 추가 가능
   - HTTP 메시지 바디
     실제 전송할 데이터
     BYTE로 표현 가능한 모든 데이터 전송 가능하다.(HTML, 문서, 이미지, 영상, JSON 등)

5. **단순함, 확장 가능**

---

- 김영한님의 모든 개발자를 위한 HTTP 웹 기본 지식을 수강하면서 정리한 내용입니다.
