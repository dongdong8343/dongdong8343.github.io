---
title: "HTTP 개념 정리(4) - HTTP 메서드"
excerpt: "HTTP 메서드 설명"

categories:
  - Etc
tags:
  - [HTTP 메서드]
sidebar:
  nav: "counts"
---

## 회원 정보 관리 API를 만드는 상황

- 회원 목록 조회
- 회원 조회
- 회원 등록
- 회원 수정
- 회원 삭제

위 API들을 만들어야 함.

이 때 URI를 설계 해야한다. → **리소스 식별이 가장 중요하다.**

저기서 리소스는 회원이 된다.

그래서 아래와 같이 URI를 설계했다.

<div align="center">
    <img src="https://github.com/dongdong8343/algorithm/assets/93115530/dfc331d0-1dfb-4e1b-b7ed-de813a3bbd37" width="80%" height="auto" />
</div>

/members/{id}로 하면 어떤게 조회인지 등록인지 구분할 수 없다.

리소스와 행위(조회, 등록, 수정, 삭제)를 분리하는 것이 중요한데 **이 때 행위는 HTTP 메서드를 사용해서 구분 가능하다.**

## GET

```
GET /search?q=hello&hl=ko HTTP/1.1
Host: [www.google.com](http://www.google.com/)
```

- 리소스 조회
- 서버에 데이터 전달할 경우 query 통해서 전달 가능
- 메시지 바디 사용해서 데이터 전달 가능하지만 지원하지 않는 서버가 많아서 권장하지는 않는다.

### 리소스 조회 과정

1. 클라이언트가 요청 메시지를 서버에 전달

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/70cb7ea1-b2c4-4eeb-9f24-d0fb94dc09a2" width="80%" height="auto" />
</div>

2. 요청 메시지가 서버에 도착

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/fa1b60a3-ec09-4600-9895-88ddfcc2f169" width="80%" height="auto" />
</div>

3. 서버가 응답 메시지를 클라이언트한테 전달

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/02014771-7ea0-4d25-bb51-159de953d5a3" width="80%" height="auto" />
</div>

## POST

```
POST /members HTTP/1.1
Content-Type: application/json
{
    "username": "hello",
    "age": 20
}
```

- 메시지 바디를 통해 요청 데이터 전달
- 요청 메시지를 처리 → 메시지 바디를 통해 들어온 데이터를 처리하는 모든 기능을 수행
- 신규 리소스 등록, 프로세스 처리에 주로 사용
  - HTML FORM에 입력한 정보로 회원 가입, 주문 등
  - 게시판 글쓰기, 댓글 달기
  - 신규 주문 생성
  - 문서 끝에 내용 추가
  ⇒ 리소스 URI에 POST 요청이 오면 어떻게 처리할지 따로 정해야 함.
- 프로세스 처리
  - 결제 완료 → 배달 시작 → 배달 완료처럼 값 변경을 넘어 프로세스 처리하는 경우
  - POST 결과로 새로운 리소스 생성 안될 수 있다.
  - 리소스를 중심으로 URI를 설계하면 아주 이상적임
    BUT, HTTP 주요 메소드로 나타낼 수 없는 경우에도 POST 사용
    POST `/orders/{orderId}/start-delivery`

### 리소스 등록 과정

1. 요청 메시지 서버에 전달

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/ada9ebad-b9a3-4a3d-964d-b16d2299dc39" width="80%" height="auto" />
</div>

2. 서버에서 신규 리소스 생성

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/5d135d93-baae-490b-9991-2e5db21953c1" width="80%" height="auto" />
</div>

3. 리소스를 잘 생성했다고 클라이언트에게 응답 메시지 전달

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/ae4ac68e-4356-4027-8957-c8adb4a31ee9" width="80%" height="auto" />
</div>

## PUT

```
PUT /members/100 HTTP/1.1
Content-Type: application/json
{
    "username": "hello",
    "age": 20
}
```

- 리소스를 덮어버림 → 클라이언트가 리소스 위치 알고 있음.

### PUT 과정

1. 리소스가 있는 경우 → 기존에 리소스 삭제하고 대체

   <div align="center">
   <img src="https://github.com/dongdong8343/algorithm/assets/93115530/28822b90-73e7-4bf2-b8a4-52c15a82bdad" width="80%" height="auto" />
   </div>

   <div align="center">
   <img src="https://github.com/dongdong8343/algorithm/assets/93115530/61f1c208-4a66-4df2-8d1c-31467a3915c0" width="80%" height="auto" />
   </div>

   - 리소스를 완전히 대체함.
       <div align="center">
       <img src="https://github.com/dongdong8343/algorithm/assets/93115530/d7f8f55a-2683-415b-ac93-898d7dc8f287" width="80%" height="auto" />
       </div>
       
       <div align="center">
       <img src="https://github.com/dongdong8343/algorithm/assets/93115530/bb721679-b51e-4362-b205-d7be72e309b1" width="80%" height="auto" />
       </div>


2. 리소스가 없는 경우 → 리소스 생성

   <div align="center">
   <img src="https://github.com/dongdong8343/algorithm/assets/93115530/3aba4d9f-36e2-4ea2-b4c5-2d6da24f25a0" width="80%" height="auto" />
   </div>

   <div align="center">
   <img src="https://github.com/dongdong8343/algorithm/assets/93115530/bb436a57-9e0c-497f-b59a-8d3a93c45df7" width="80%" height="auto" />
   </div>

## PATCH

```
PATCH /members/100 HTTP/1.1
Content-Type: application/json
{
    "age": 50
}
```

- 기존 리소스의 일부만 수정함.

### PATCH 과정

1. 요청 메시지 서버로 전달

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/be9f0598-7040-41e7-b0ab-7e4d7dfbfbde" width="80%" height="auto" />
</div>

2. 기존 리소스 일부만 수정됨.

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/e345e48c-0d6d-44c8-904a-5c97531b3bde" width="80%" height="auto" />
</div>

## DELETE

```
DELETE /members/100 HTTP/1.1
Host: localhost:8080
```

- 리소스 삭제

### DELETE 과정

1. 요청 메시지 서버로 전달

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/a68e4878-5072-4463-81e8-9a9a885aecd8" width="80%" height="auto" />
</div>

2. 리소스 삭제

<div align="center">
<img src="https://github.com/dongdong8343/algorithm/assets/93115530/f46b964f-878b-4c23-8829-55be1e7183d3" width="80%" height="auto" />
</div>

## HTTP 메서드 속성

1. **안전**

- 계속 호출해도 리소스가 변하지 않음
- GET

1. **멱등**

- 몇 번을 호출해도 결과가 같음.
- GET, PUT, DELETE
- POST, PATCH는 특정 자원의 값을 1 증가 시키는 연산을 지시하면 리소스가 계속 변화되므로 멱등성을 안가짐.
- 활용 → 정상 응답을 못줬을 때, 같은 요청을 다시 가능한지 판단하는 근거가 됨.

1. **캐시 가능**

- 응답 결과 리소스를 캐시해서 사용해도 되는지 여부
  - 캐싱 - 리소스를 임시로 저장했다가 같은 요청이 들어오면 빠르게 응답 가능.
- GET, HEAD, POST, PATCH → 실제로 GET, HEAD 정도만 캐시로 사용
  POST, PATCH → 리소스에 변화를 주는 요청임.
  요청 바디의 데이터에 따라 리소스가 변경 되는 경우가 많음.
  → 요청 바디에 따라 리소스 응답 결과가 달라질 수 있다.
  → 요청 바디를 캐시 키의 일부로 고려해야 하는데 구현 복잡해짐.

---

- 김영한님의 모든 개발자를 위한 HTTP 웹 기본 지식을 수강하면서 정리한 내용입니다.
